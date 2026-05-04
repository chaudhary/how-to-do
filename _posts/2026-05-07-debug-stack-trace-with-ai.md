---
layout: post
title: "Debugging a Stack Trace with AI: The Workflow Our Log Analyzer Uses"
date: 2026-05-07
category: Tech / Dev
description: "Stack traces are noisy. AI is good at finding the real failure line — but only if you ask correctly. Here's the prompt structure our Log Analyzer uses and why it skips the cargo-cult 'paste your error here' approach."
reading_time: 6
related_tool: /tools/log-analyzer
related_tool_name: Log Root Cause Analyzer
---

You're 90 minutes into a production incident. Datadog is exploding with errors. You've got 200 lines of stack trace, half of it is framework code, and the actual application failure is buried in the middle. Your team Slack is full of "any updates?"

Pasting that mess into ChatGPT and asking "what's wrong?" usually returns a paraphrase of the top of the trace. Useful 30% of the time. Not enough.

Our [Log Root Cause Analyzer]({{ "/tools/log-analyzer" | relative_url }}) tries to do better with structured prompts. Here's the workflow.

## The problem with naive log analysis

When you paste a stack trace into a generic chatbot, this is what most LLMs do:

1. Read the top exception class.
2. Pattern-match against known errors in their training data.
3. Suggest the most-common cause for that exception.

That's why you get "NullPointerException usually means a variable wasn't initialised" — true, but unhelpful when you have 200 lines and need to know *which* variable, in *which* file, in *which* code path.

What you actually want is: which line is most likely the root cause, given the chain of calls, the framework noise to ignore, and the surrounding context.

## What our prompt asks

```
You are an SRE analysing a production log or stack trace. 
The user is debugging a real incident, not learning. 
Be specific and actionable.

Input:
[USER PASTES LOGS / STACK TRACE]

Optional context:
- Language / framework: [DETECT FROM INPUT IF NOT GIVEN]
- Time of incident: [USER PROVIDED]
- What the user was doing: [USER PROVIDED]

Walk through this in order:

1. SEVERITY: P0 (production down), P1 (feature broken, has workaround), 
   P2 (degraded), P3 (logged but no impact). Justify with one line.

2. ROOT CAUSE LINE: identify the SPECIFIC line in the trace 
   that is most likely the actual cause, not just the topmost 
   exception. Skip framework noise (Spring proxy classes, 
   reactor schedulers, Tomcat NIO, etc.). State the file, 
   line number, and method.

3. FAILURE MODE: classify into one of:
   - Null reference / undefined variable
   - Resource exhaustion (DB connection, memory, file descriptors)
   - Network timeout (DB, HTTP client, internal RPC)
   - Race condition / concurrency
   - Configuration error
   - External service failure
   - Data corruption / unexpected payload
   - Auth / permissions
   - Code bug (logic error in the application code itself)

4. POSSIBLE FIXES: suggest 2-3 fixes ranked by:
   a. Quickest mitigation (rollback, restart, disable feature flag)
   b. Short-term fix (deploy in next 24h)
   c. Long-term fix (architecture / process change)

5. WHAT TO CHECK NEXT: 3 specific things to look at to confirm 
   the diagnosis (e.g. "check connection pool metrics in 
   Datadog dashboard X for the same time window", 
   "grep for WARN-level logs from kafka-producer 
   in the 5 min before this trace").

6. POSTMORTEM TAGS: suggest 2-3 tags for the postmortem 
   (e.g. "downstream-dependency-failure", "missing-circuit-breaker", 
   "stale-cache-miss").

Be specific. Don't say "check your database connection"; 
say "the trace shows HikariCP connection-acquisition timeout 
after 30 seconds; check pool exhaustion in connection metrics".
```

The structured 6-step output is the difference between "this is probably a DB issue" and "your HikariCP pool is exhausted, likely because line 145 of OrderService isn't releasing the connection after a transaction rollback."

## Skipping the framework noise

The hardest part of stack-trace analysis is figuring out what to ignore. A typical Java stack trace has 50–80% noise:

```
at org.springframework.aop.framework.JdkDynamicAopProxy.invoke(...)
at com.sun.proxy.$Proxy145.findById(Unknown Source)
at org.springframework.data.repository.CrudRepository...
at org.springframework.transaction.interceptor.TransactionInterceptor...
at reactor.core.publisher.Mono.subscribe(...)
[... 30 more lines of framework ...]
at com.yourcompany.order.OrderService.processOrder(OrderService.java:145)
^^^^ THIS IS THE LINE THAT MATTERS
at org.springframework.web.servlet.DispatcherServlet...
[... more framework noise ...]
```

The prompt explicitly tells the LLM to skip framework noise. We list the most common offenders by ecosystem:

- **Java/Kotlin**: Spring proxies, AOP interceptors, reactor schedulers, Tomcat NIO
- **Node.js**: async hooks, Express middleware chains, native promises
- **Python**: asyncio internals, Django middleware, gunicorn workers
- **Go**: runtime, goroutine scheduler, net/http internals
- **Ruby**: ActiveRecord query method missing, Rack middleware

These don't tell you what's wrong; they tell you the path the request took. The actual bug is almost always in your application code, somewhere in the middle.

## The "what to check next" question

Most LLM outputs stop at "here's the likely cause." Our prompt forces it to suggest concrete next steps. Examples it produces in practice:

> "Check Datadog dashboard for `db.connection_pool.active` in the 10 minutes before this trace. If it's at the pool max, the pool is exhausted. If it's normal, look at the per-tenant query patterns."

> "Run `kubectl logs -p` on pods restarted in this window. The pod restart suggests OOM."

> "Grep for `KafkaProducerException` in the same time window. The retry-exhaustion message in this trace suggests a downstream Kafka issue, not a bug in your service."

The prompt is doing what a senior SRE would do: pointing at the next action, not just the diagnosis.

## What it can't do

A few honest limitations:

1. **No access to your monitoring or codebase.** It can suggest "check the connection pool metrics", but it can't actually pull the metrics. You still have to switch tools.

2. **Doesn't know your service architecture.** "Check the upstream service" is correct advice but useless if it doesn't know which upstream service. You can give it context, but a generic LLM can't infer your topology.

3. **Sometimes wrong about the root cause line.** If your stack trace is unusual (custom AOP, generated code, a JIT-inlined frame), the LLM may pick the wrong line. Treat its suggestion as a starting hypothesis, not a verdict.

4. **Sensitive data risk.** Stack traces sometimes contain PII (email, user IDs, query parameters). Sanitise before pasting if your data sensitivity is high. Our [Log Analyzer]({{ "/tools/log-analyzer" | relative_url }}) processes data client-side, but you're still sending the trace to an LLM API.

## A workflow for production incidents

What a senior on-call engineer actually does, with our tool plugged in:

1. **0-2 min**: Confirm the incident is real (page is firing, customer impact). Set incident severity in your incident tool.
2. **2-5 min**: Pull the most representative stack trace from your error tracker (Sentry, Datadog, etc.). Paste into the [Log Analyzer]({{ "/tools/log-analyzer" | relative_url }}).
3. **5-7 min**: Read the analyzer's output. Use the "what to check next" suggestions to guide your dashboard hunt.
4. **7-15 min**: Verify or refute the hypothesis using monitoring. Iterate (refine the trace input or add context, re-run).
5. **15-25 min**: Apply the quickest mitigation (feature-flag rollback, traffic shed, restart pods). Communicate in incident channel.
6. **Post-incident**: Use the "postmortem tags" output to seed the writeup.

The 5–7 minute step is where AI saves the most. A senior SRE skips this because they've seen the pattern; a junior loses 30 minutes pattern-matching against the wrong cause. The analyzer compresses the gap.

## What it's NOT for

- Replacing observability tooling. Datadog, New Relic, Sentry, Honeycomb — these aren't going anywhere. The Log Analyzer reads what they already capture.
- Replacing institutional knowledge. The reason your last incident was tricky is probably specific to your stack. AI starts from scratch every time.
- Postmortem writing. The output is good for tags and timeline; the actual "what we learned" section needs human reflection.

## Try it on a real incident

If you have a recent stack trace lying around (Slack, Sentry, your terminal history), paste it into the [Log Root Cause Analyzer]({{ "/tools/log-analyzer" | relative_url }}). See if its diagnosis matches what you eventually figured out. If it doesn't, that's a useful calibration for next time you reach for it.

Cross-check with our [SQL Query Explainer]({{ "/tools/sql-explainer" | relative_url }}) when the issue turns out to be a slow query — the two pair well during prod incidents.
