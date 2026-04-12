---
layout: post
title: "Time Zone Math for Remote Teams: A Practical Guide"
date: 2026-04-12
category: Productivity
description: "Handle time zones without confusion: overlap calculations, meeting scheduling, and practical tips for distributed teams."
reading_time: 4
related_tool: /tools/timezone-converter
related_tool_name: Time Zone Converter
---

Working across time zones is the tax of remote work. Here's how to pay it efficiently.

## The UTC Anchor

Stop thinking in local times. Think in UTC offsets.

- IST (India) = UTC+5:30
- ET (US East) = UTC-5 (or UTC-4 during daylight saving)
- PT (US West) = UTC-8 (or UTC-7 during DST)
- GMT (UK) = UTC+0 (or UTC+1 during BST)
- JST (Japan) = UTC+9
- AEST (Australia) = UTC+10 (or UTC+11 during DST)

When someone says "Let's meet at 2pm," the first question is: whose 2pm?

## Finding Overlap

The overlap window between two time zones is where real-time collaboration happens. Everything else should be async.

**India (IST) and US East (ET)**: 10.5 hour difference.
- If both work 9am-6pm:
- IST 9am = ET 10:30pm (previous day)
- IST 6pm = ET 7:30am
- ET 9am = IST 7:30pm
- Overlap: IST 7:30pm-9pm / ET 9am-10:30am (about 1.5 hours)

**India and US West (PT)**: 13.5 hour difference.
- Overlap is painful. IST 9:30pm = PT 9am.
- Realistic overlap: maybe 30 minutes if someone stretches.

**India and UK (GMT)**: 5.5 hour difference.
- Good overlap: IST 1:30pm-6pm / UK 9am-12:30pm (3.5 hours)

## Scheduling Meetings

### Rule 1: Rotate the pain
If the meeting is always at a bad time for the same team, resentment builds. Alternate between time slots that inconvenience different groups.

### Rule 2: Anchor to the smallest overlap
If your overlap is 1.5 hours, protect it. Don't waste it on status updates that could be async. Use synchronous time for decisions, brainstorming, and relationship-building.

### Rule 3: Always include the time zone
"Meeting at 3pm" is ambiguous. "Meeting at 3pm ET / 12:30am IST" is not. Even better: share a link that converts to local time (Google Calendar does this automatically).

### Rule 4: Account for daylight saving
The US, Europe, and Australia change clocks on different dates. For 2-3 weeks per year, your carefully calculated offsets are wrong by an hour. Set calendar reminders around DST transitions.

## The Async-First Approach

Time zone overlap is precious and limited. Maximize it by making everything possible async:

- **Decisions**: Write proposals in documents. Collect feedback async. Use meetings only to resolve disagreements.
- **Updates**: Record 3-minute Loom videos instead of calling meetings.
- **Code reviews**: Written comments, not live walkthroughs.
- **Questions**: Post in Slack/Teams with context. Don't expect instant replies.

## Quick Conversion Tricks

### IST to ET
Subtract 10.5 hours (subtract 11, add 30 min). IST 3pm = ET 4:30am.

### IST to PT
Subtract 13.5 hours. IST 3pm = PT 1:30am.

### IST to GMT
Subtract 5.5 hours. IST 3pm = GMT 9:30am.

### The "noon trick"
12:00 noon IST = 6:30am GMT = 1:30am ET = 10:30pm PT (previous day).

Memorize one anchor conversion for each zone pair you deal with regularly. Derive everything else from that.

## Tools That Help

- Share a time zone converter link when scheduling
- Use Google Calendar (auto-converts time zones)
- Set a secondary clock on your phone for your team's zone
- World clock widgets on your desktop

The goal isn't to make time zones disappear. It's to make them a solved problem that doesn't consume mental energy every day.
