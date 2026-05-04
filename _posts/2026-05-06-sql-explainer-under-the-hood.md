---
layout: post
title: "What Our SQL Query Explainer Is Checking Under the Hood"
date: 2026-05-06
category: Tech / Dev
description: "AI SQL explainers are everywhere. Most just paraphrase the query. Here's what ours actually checks: index coverage, join order, subquery flattening, and the 6 anti-patterns it explicitly looks for."
reading_time: 6
related_tool: /tools/sql-explainer
related_tool_name: SQL Query Explainer
---

If you paste a SQL query into a generic chatbot and ask "explain this", you get a paraphrase. "This query selects users where signup is before 2024 and joins with orders." That's the same as reading the SQL.

What you actually want from a SQL explainer is the second-order analysis: will this query be slow on production data, what indexes does it need, and is there a hidden full-table scan you should worry about. That's what our [SQL Query Explainer]({{ "/tools/sql-explainer" | relative_url }}) tries to do. Here's what's happening under the button.

## What the prompt structure actually checks

When you click "Explain", the tool runs the query through a multi-pass prompt:

```
You are a database performance engineer. Analyse this SQL query.

Query:
[USER QUERY]

Database (if specified): [POSTGRES / MYSQL / SQLITE / SQL SERVER / 
ORACLE / GENERIC]

Output structure:
1. Plain English: what does this query do, in 2 sentences?
2. Tables and approximate row counts (if user provided): 
   what data flows where?
3. Index analysis: which columns should have indexes for this 
   query to be fast? Flag any predicate that won't use an index.
4. Join analysis: in what order should these tables be joined? 
   Is the current order optimal?
5. Anti-patterns: check explicitly for these 6 issues:
   a. SELECT *
   b. Function on indexed column in WHERE 
      (e.g. WHERE LOWER(email) = 'x')
   c. OR predicates that prevent index use
   d. NOT IN with subquery (often slow + has NULL gotcha)
   e. Correlated subquery in SELECT clause 
      (N+1 in disguise)
   f. LEFT JOIN where INNER would work
6. Index recommendations: suggest 1-3 specific CREATE INDEX 
   statements with column order, including covering indexes 
   where useful.
7. Rewrite suggestion: if the query has a more idiomatic form, 
   show it.

Be specific. Don't say "this might be slow"; say "the WHERE clause 
on column X will scan all N rows because there's no index on X."
```

That's the difference. Most explainers stop at step 1. Ours uses the LLM as a senior database engineer reviewing a junior's PR.

## What the 6 anti-patterns actually look like

A short tour, in case you've seen these in your own code.

### 1. SELECT *

```sql
SELECT * FROM users WHERE created_at > '2024-01-01';
```

Why it's bad: forces the database to fetch every column, even ones you don't need. Network bandwidth scales with selected columns. Worse: if there's a covering index on (created_at, id, name), `SELECT *` won't use it because it has to also fetch the missing columns.

Fix: name the columns you want. Always.

### 2. Function on indexed column in WHERE

```sql
SELECT * FROM users WHERE LOWER(email) = 'amit@example.com';
```

Why it's bad: the index on `email` is on the original-case values. `LOWER(email)` makes it a different expression that won't use the index. Database does a full table scan.

Fix options:
- Store emails normalised (lowercase) at insert time.
- Use a functional index: `CREATE INDEX users_email_lower ON users (LOWER(email));`
- Use citext column type in Postgres.

### 3. OR predicates blocking index use

```sql
SELECT * FROM orders WHERE customer_id = 123 OR order_status = 'PENDING';
```

Why it's bad: even if you have indexes on both columns, the optimiser typically can't use them efficiently for OR — it has to scan both. Sometimes it falls back to a full table scan.

Fix: rewrite as UNION:

```sql
SELECT * FROM orders WHERE customer_id = 123
UNION
SELECT * FROM orders WHERE order_status = 'PENDING';
```

### 4. NOT IN with subquery

```sql
SELECT * FROM users WHERE id NOT IN (SELECT user_id FROM banned_users);
```

Two problems: it's typically slow because the subquery runs for every outer row (depending on optimiser), and it has a NULL gotcha — if the subquery returns any NULL, the entire NOT IN returns no rows.

Fix: use NOT EXISTS, which is both faster and NULL-safe:

```sql
SELECT * FROM users u 
WHERE NOT EXISTS (SELECT 1 FROM banned_users b WHERE b.user_id = u.id);
```

### 5. Correlated subquery in SELECT

```sql
SELECT u.name, 
       (SELECT COUNT(*) FROM orders o WHERE o.user_id = u.id) AS order_count
FROM users u;
```

Why it's bad: the subquery runs once per row of `users`. For 10K users, that's 10K subquery executions. This is the SQL equivalent of N+1.

Fix: rewrite as JOIN:

```sql
SELECT u.name, COUNT(o.id) AS order_count
FROM users u
LEFT JOIN orders o ON o.user_id = u.id
GROUP BY u.id, u.name;
```

### 6. LEFT JOIN where INNER would work

```sql
SELECT u.name, o.order_total
FROM users u
LEFT JOIN orders o ON o.user_id = u.id
WHERE o.status = 'completed';
```

Notice the WHERE clause filters on `o.status`. That makes the LEFT JOIN behave as INNER JOIN — rows where `o` is NULL get filtered out anyway. Many optimisers spot this; some don't. Either way, it's misleading.

Fix: use INNER JOIN explicitly. Tells future readers (and the optimiser) what you mean.

## Index recommendation logic

The trickiest part of the prompt is index recommendations. Generic explainers either don't suggest indexes or suggest one per WHERE column without thinking about composite ordering.

Our prompt enforces a specific structure:

```
For each query, recommend at most 2-3 indexes.
For each index:
1. Specify the columns IN ORDER (this matters for composite indexes).
2. Order columns by selectivity: equality predicates first 
   (e.g. user_id = 123), then range predicates (e.g. created_at > X).
3. If possible, include covering columns for the SELECT list 
   to enable index-only scans.
4. State estimated impact: "this index turns a full scan into 
   an index seek, expected 10-100x speedup on a 1M-row table."
```

That's "leftmost prefix" matching, which is how composite indexes work. Most LLMs don't volunteer this without being asked. The prompt forces it.

## What the explainer doesn't do

A few honest limitations:

1. **Can't see your actual query plan.** Without an EXPLAIN ANALYZE output, the recommendations are based on schema reasoning, not runtime stats. For production tuning, always run EXPLAIN ANALYZE locally and paste the result alongside the query.

2. **Doesn't know your data distribution.** "Index on `status` column" is great if status has 1000 distinct values. Useless if 99% of rows have status='ACTIVE' — the optimiser may ignore the index. The explainer guesses; you verify.

3. **Database-specific quirks.** PostgreSQL, MySQL, SQLite, SQL Server, and Oracle each handle joins, subqueries, and indexes differently. The explainer asks for the database type up front but won't catch every dialect-specific gotcha. Postgres-only features (partial indexes, BRIN indexes, JSONB operators) get less coverage than vanilla SQL.

4. **Can be wrong.** LLMs hallucinate. If the explainer suggests an index, run EXPLAIN ANALYZE before and after to confirm the recommendation actually helps. Don't deploy on faith.

## How to use it for the most signal

1. **Paste the actual production query**, not a simplified version. Anti-patterns hide in real-world clutter.
2. **Include the database type** in the input — Postgres-specific advice differs from MySQL's.
3. **Provide schema hints** ("table has 10M rows, this column has high cardinality") if you have them. The LLM uses these to prioritise recommendations.
4. **Cross-check with EXPLAIN ANALYZE.** Treat the explainer as a senior reviewer, not the source of truth. Run the recommended indexes locally first.
5. **Re-run the explainer after your fix.** Sometimes one optimisation reveals the next.

The goal isn't to replace SQL expertise. It's to compress 4 hours of "wait, why is this query slow" into 4 minutes — same as how a code reviewer doesn't replace your engineering judgment, just speeds up the catch.

Try it on a slow query you've been meaning to investigate. Use the [SQL Query Explainer]({{ "/tools/sql-explainer" | relative_url }}) and see what it flags. If it says "no obvious issues" — that's also useful information.
