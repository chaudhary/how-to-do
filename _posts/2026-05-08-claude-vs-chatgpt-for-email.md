---
layout: post
title: "Why I Stopped Using ChatGPT for Emails and Switched to Claude"
date: 2026-05-08
category: Tech / Dev
description: "I write 30-40 work emails a day. I tried ChatGPT, Gemini, and Claude on the same drafting tasks for 3 months. Here's why Claude won, what ChatGPT does better, and the workflow I landed on."
reading_time: 6
related_tool: /tools/email-writer
related_tool_name: Email Writer
---

This post is a first-person take, not a benchmark. I've been writing 30–40 work emails a day for 8 months now (mix of internal team comms, client-facing escalations, and the occasional "no, we're not extending the deadline" pushback). I tried ChatGPT, Gemini, and Claude on the same emails for 3 months. Eventually I stopped reaching for the others.

Here's the comparison, what each one is actually good at, and why "best AI" is the wrong question.

## The trial setup

For 12 weeks, every time I had a non-trivial email to write, I'd:

1. Draft a bullet list of points to make.
2. Send the same prompt to ChatGPT (4o), Gemini (2.5 Pro), and Claude (Sonnet 4.5).
3. Pick the best output.
4. Track which one I picked.

By week 8, the count was: Claude 64%, ChatGPT 26%, Gemini 10%.

By week 12, I'd stopped using Gemini entirely. ChatGPT was still in the rotation for one specific use case (more on this). For everything else, Claude.

## What Claude does better

**Specifics.** Claude handles ambiguous requests by inferring the most likely scenario and writing for it. Example prompt I used multiple times:

> "Write a polite escalation email to the client account manager about the stuck contract review. We've been waiting 3 weeks. Don't sound annoyed, but make it clear we need a date."

**Claude's draft** felt close to how I'd write it: opened with context, named the specific blocker ("legal review of clause 4.2"), proposed a date ("can you commit to Friday this week?"), closed warmly without being saccharine.

**ChatGPT's draft** was generic. "I wanted to follow up on our pending discussion." "Looking forward to your prompt response." Useful as a structure, but I had to rewrite every paragraph for voice.

**Gemini's draft** was passable but had this corporate-newsletter feel — overly formal, with phrases like "I trust this email finds you well" that haven't been used by a human in 30 years.

**Tone control.** When I asked for "polite but firm" or "direct but not aggressive," Claude understood the gradient. ChatGPT often went too soft ("I just wanted to gently mention…"); Gemini stayed in the corporate-template register regardless.

**Editing existing drafts.** This is where Claude is most ahead. If I write a rough email and ask "tighten this, remove the parts that sound defensive," Claude actually does it. ChatGPT sometimes rewrites the whole thing, which I have to undo. Gemini occasionally misreads "tighten" as "expand."

**Following meta-instructions.** "Don't use em dashes." "Avoid the word 'leverage'." "Sign off with 'Thanks' not 'Best regards'." Claude remembers these across the conversation. ChatGPT forgets after 3-4 exchanges. Gemini occasionally ignores them entirely.

## What ChatGPT does better

Two things, genuinely:

**1. Tabular and bulleted formatting.** When I need an email with a comparison table or a structured list (for example, summarising 5 vendor quotes), ChatGPT's markdown rendering is better. Claude defaults to prose; ChatGPT defaults to tables. For "show me the data" emails, ChatGPT wins.

**2. Multilingual edge cases.** I occasionally write emails in Hindi, Hinglish, or Marathi for vendor coordination. ChatGPT's multilingual handling is more natural — Claude does it well in English-Hindi mix, but a pure-Hindi email from Claude sometimes reads like translated English. ChatGPT (especially 4o and later) writes Hindi that feels like Hindi.

For these two cases, I still keep ChatGPT around.

## Where Gemini falls short

Gemini was the easiest decision. Two recurring problems:

1. **Tone dial doesn't go warm.** Gemini's professional emails always feel like they were written by HR Compliance. The default voice is reserved, formal, and slightly defensive.
2. **Awkward "I" usage.** Gemini frequently writes "I will be sending the report tomorrow" instead of "I'll send the report tomorrow." Small thing; adds up across 40 emails.

These are voice issues, not capability issues. Gemini knows the right facts; the writing just doesn't sound human enough.

## My actual email workflow now

Here's the loop I run for every non-trivial email:

1. **Bullet the points** in a Notion page or a quick text file. 30 seconds of thinking — the actual content of what to say.
2. **Send to Claude** with the bullets, target tone, and any meta-rules ("no em dashes, sign-off as 'Thanks'").
3. **Read the draft.** 60% of the time, it's sendable as-is. 30% of the time, I edit one or two sentences. 10% of the time, I rewrite from scratch (usually because I missed a key bullet).
4. **Final pass for voice.** Replace anything that sounds AI-written. Common fixes:
   - "I hope this email finds you well" → delete entirely
   - "I would like to" → "I'd like to" (or just delete)
   - "Please feel free to" → "Let me know if"
   - "I appreciate your understanding" → "Thanks for the heads up" (or just delete)

The whole loop takes 2–3 minutes for an email I'd have spent 8 minutes writing from scratch.

## Things AI still doesn't do well for emails

**Reading the room.** If a colleague is in a tense thread with a client, the AI doesn't know that. It writes the "ideal" email; you have to inject the relational context.

**Internal politics.** The email to your boss who has explicitly told you not to escalate things to the VP — the AI will happily draft an email that copies the VP because it doesn't know your political situation.

**Speed for trivial replies.** "OK", "Thanks", "Got it, will do by EOD" — for these, typing is faster than prompting. Use AI for emails over 100 words. Below that, it's overhead.

**Multi-thread context.** If a thread has 12 messages, you'd be feeding all of them to the AI for context. Claude handles this fine but it's annoying. Gmail's "smart compose" is better for in-thread replies because it's already inside Gmail.

## Companion tool

Our [Email Writer]({{ "/tools/email-writer" | relative_url }}) packages this workflow — bullet-point input, tone selection, output you can copy. Behind the scenes, the tool uses Claude with a system prompt that bans the same set of cliches I avoid manually ("hope this email finds you well", "kindly", "feel free to", "looking forward").

If you're testing tools yourself, run the same prompt through ChatGPT, Claude, and Gemini for a week. Pick what wins for *your* writing voice. The "best" AI isn't a fixed answer — Claude wins for me because I write in a particular register; someone who writes corporate-formal emails might prefer ChatGPT. The trial run takes 30 minutes a day for a week and saves you months of suboptimal tool choice.

## TL;DR

- **Claude** for everything that needs voice, tone, or editing.
- **ChatGPT** for emails with tables, charts, or non-English content.
- **Gemini** for nothing in this category, in my testing.

Try our [Email Writer]({{ "/tools/email-writer" | relative_url }}) on your next sticky email and see how it lands.
