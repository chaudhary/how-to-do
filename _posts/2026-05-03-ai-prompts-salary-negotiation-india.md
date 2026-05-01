---
layout: post
title: "AI Prompts to Negotiate Your Salary in India (with the CTC math)"
date: 2026-05-03
category: Personal Finance
description: "Indian salary negotiation isn't just about the headline number. Here's how to use Claude or ChatGPT to model CTC trade-offs, draft counter-offers, and avoid the variable-pay traps that eat 20% of your apparent raise."
reading_time: 9
related_tool: /tools/salary-calculator
related_tool_name: Salary Calculator
---

You got an offer letter. The headline reads ₹38 LPA. The HR manager wants you to sign by Friday. Your current CTC is ₹28 LPA, so it's a 35% jump.

Then you read the structure: ₹3 LPA RSU vesting over 4 years. ₹4 LPA performance bonus, "subject to company and individual performance." ₹2 LPA joining bonus, clawback if you leave within 18 months. Suddenly the certain part of your offer is ₹29 LPA, which is barely a 4% raise after inflation.

Indian salary negotiation has a specific shape — a wide gap between headline CTC and certain in-hand, with multiple components that mean different things at different employers. A good LLM prompt can model this in seconds. Here's the playbook.

## The first prompt: decompose any offer

Paste this into Claude or ChatGPT, replacing the structure with your offer:

```
I have a job offer in India. Help me decompose this into "certain" 
income, "high-probability" income, and "lottery ticket" income.

Offer details:
- Total CTC: ₹[AMOUNT] per annum
- Fixed CTC: ₹[FIXED]
- Variable / Performance bonus: ₹[VARIABLE], paid quarterly/annually
  based on company + individual rating
- Joining bonus: ₹[JOINING] (clawback if I leave within [MONTHS])
- ESOP / RSU value: ₹[ESOP] over [YEARS] vest, [CLIFF]-month cliff
- Retention bonus: ₹[RETENTION] payable after [MONTHS]
- Notice period: [DAYS] days
- Other components: [Gratuity, employer PF contribution, insurance]

Walk me through:
1. The certain income vs the contingent income
2. What "average rating" historically means at this company 
   (if you know — otherwise ask me what I've heard from people inside)
3. The risk-adjusted CTC (e.g. variable at 80%, RSU at 60% probability)
4. Comparison with my current ₹[CURRENT_CTC] CTC at [CURRENT_COMPANY]
5. Three specific things I should ask the recruiter before accepting
```

Claude does a good job of categorising. It'll flag that "27% bonus" sounds great but historical average payouts are often 70–85% of target, so plan for ~22%. It'll model RSU at the post-tax post-vesting reality, not the headline.

The output usually looks like:

> **Certain income (₹26 L)**: Fixed CTC + employer PF + standard insurance.
> 
> **High-probability income (₹4 L)**: Performance bonus assuming average rating. Most companies pay out 70-90% of target.
> 
> **Lottery ticket (₹6 L)**: RSU/ESOP, joining bonus with clawback, retention bonus payable in 24 months. These have meaningful probability of zero — RSU only if stock doesn't crash, joining bonus only if you stay 18+ months, retention only if you stay 24+ months.

That's the framing you actually need. Most candidates evaluate offers on the headline. A good LLM forces you to evaluate on certain + risk-weighted contingent.

## The second prompt: in-hand math

Once you know the components, ask:

```
For a CTC of ₹[FIXED] in India (excluding variable):
- I'm in [Bangalore / Mumbai / Delhi / Pune / Hyderabad]
- Single, no dependents, age 32
- I plan to file under the New tax regime (or Old, with these deductions: …)

Compute:
1. Monthly in-hand take-home after tax, PF, professional tax
2. Annual tax liability (with cess)
3. The monthly cash I can actually plan around
4. How much my employer's PF contribution adds to my retirement corpus
5. If I do voluntary PF (VPF) at an additional 12%, what's the post-tax 
   yield given Rule 9D's ₹2.5L cap?
```

The in-hand math is where most online "salary calculators" fail — they don't differentiate between fixed and variable, they ignore Rule 9D for high earners, and they don't handle Bangalore's professional tax versus Maharashtra's. Claude or ChatGPT, with the right prompt, gets it right because you're forcing it to think component-by-component.

For a sanity check, plug your fixed CTC into our [Salary Calculator]({{ "/tools/salary-calculator" | relative_url }}). It does the same math but visualises monthly bands.

## The negotiation prompt

This is where AI saves you the most time. Drafting a counter-offer is hard because tone matters: too aggressive and you lose the offer; too passive and you leave money on the table.

```
I want to counter-offer this Indian job offer. Help me draft an email.

Offer breakdown:
- Total CTC: ₹38 LPA
- Fixed: ₹26 LPA
- Variable: ₹4 LPA at target
- RSU: ₹6 LPA over 4 years
- Joining bonus: ₹2 LPA
- Notice: 60 days

What I'm asking for:
- Fixed CTC: ₹30 LPA (rationale: peer at [SIMILAR COMPANY] offered me 
  ₹29 LPA fixed; I have a competing offer at ₹28 fixed)
- RSU: ₹8 LPA over 4 years (rationale: equivalent to peers at L5)
- Joining bonus: ₹3 LPA, clawback reduced to 12 months from 18
- Variable: keep at ₹4 LPA target

Tone: professional, not aggressive. I want this offer; I'm asking for 
adjustments to make it competitive with my current alternatives.

Please draft:
1. The email itself (3-4 paragraphs)
2. Counter-arguments I should be ready to give if they push back 
   on any of these asks
```

The output is usually 80% sendable. You'll edit a few lines for voice, but the structure — leading with enthusiasm, anchoring asks with specifics, providing rationale grounded in market data — is what most candidates struggle to write themselves at 11 PM the night before the deadline.

## Indian salary negotiation traps

There are a few specifically Indian quirks that LLMs sometimes miss. Add these to your prompts.

### Trap 1: Variable pay percentages

Top tier IT firms (Infosys, TCS, Wipro): variable is typically 0–3% of CTC. Negligible.

Mid-tier (HCL, LTI, Mindtree): 5–10%.

Product companies (Flipkart, Razorpay, PhonePe): 10–20%, usually paid out 70–90% of target.

Big tech India offices (Google, Microsoft, Amazon): 15–25% variable, but historical payouts are very close to 100% of target unless you have a Below Average rating.

Startups: variable can be 0–10%, but often "stretch goals" with payout ratio of 60–70% in tough years.

Make sure your AI prompt knows the company tier — otherwise it'll average across these and produce numbers that don't reflect your situation.

### Trap 2: ESOP/RSU valuations

For listed Indian companies (Infosys, TCS), RSU value is straightforward — multiply units × current stock price.

For private startups, the ESOP "value" in your offer letter is usually based on the **last preferred-share funding round price**, multiplied by your option count. This is **not** the price at which you can sell. Common stock (employee ESOPs) is typically 30–60% of the preferred-share price during a liquidity event. So a ₹50L ESOP grant at the last 409A might be ₹20L when actually liquidating.

A good prompt:

```
This is an Indian startup ESOP grant. Last funding round was Series 
[B/C/D] at $[VALUATION] in [YEAR]. The grant is ₹[AMOUNT] over 
4 years with a 1-year cliff. 

What's a realistic post-tax value if:
1. The company exits via IPO in 4 years at 1.5x last round
2. The company exits via acquisition at last-round valuation
3. The company stays private and I leave after 4 years

Account for: common-stock haircut vs preferred (typical 30-50%), 
Indian capital gains tax on ESOPs, and the fact that vested options 
expire 90 days after I leave (typical Indian startup terms).
```

This is the math no offer letter shows you, and most candidates don't run.

### Trap 3: Joining bonus clawback structure

A ₹3 LPA joining bonus with "100% clawback if you leave within 24 months" is more like ₹1.5 LPA in expected value if you have a 30% chance of leaving early.

Better structures:
- "Pro-rata clawback" — you owe back the unvested portion only.
- "Cliff clawback" — full clawback for 12 months, then nothing.
- "Tax adjustment" — clawback amount is gross-of-tax (usually pushes back; ask for net-of-tax).

Always ask for the clawback term in writing before accepting.

### Trap 4: Notice period buyout

If your current notice is 60 days and your new employer says "we'll pay your notice buyout," confirm:

- Will they pay it as a one-time bonus (taxable in the year received)?
- Will they pay it directly to your old company (cleaner, but hits your old employer's books)?
- Or just give you the cash to handle it (gets messy with FNF reconciliation)?

Use our [Notice Period & FNF Calculator]({{ "/tools/notice-period-fnf-calculator" | relative_url }}) to know the exact buyout amount before you accept.

## The "BATNA" prompt

Before any negotiation, AI is genuinely useful for steeling yourself with alternatives:

```
My offer at hand: ₹38 LPA at [COMPANY A].
My current job: ₹28 LPA at [COMPANY B].
My competing offers in flight: ₹35 LPA at [COMPANY C], 
  ₹40 LPA at [COMPANY D] (early-stage startup, mostly ESOP).

My BATNA (best alternative to a negotiated agreement) if I walk:
- Stay at current job for 6 months and reapply later
- Take Company C
- Take Company D and accept ESOP risk

Help me:
1. Rank these on certain CTC + 5-year expected value
2. Identify the leverage I have at Company A
3. Suggest what to ask for and how much I can push without 
   risking the offer being withdrawn
```

The "leverage" question is key. Most candidates negotiate from a place of fear — "what if they pull the offer." A clear BATNA framing reframes the conversation: you're not begging, you're choosing among options.

## When to skip AI entirely

Don't use AI for:

- **Verbal phone negotiations.** AI suggestions sound robotic when read aloud. Use it to prepare bullet points; ad-lib the actual call.
- **Sensitive personal context.** Reasons for asking more (medical, family, ageing parents) — those should come from you, not a model.
- **Competitor company names.** Do not feed your AI tool the names of confidential offers. Some teams use shared workspaces; your data could leak.
- **The actual signing.** AI can review contracts but read every word yourself. Especially the non-compete and IP-assignment clauses.

## A workflow that actually saves time

1. Get the offer.
2. Run the **decompose prompt**. Identify certain vs contingent.
3. Run the **in-hand prompt**. Get the monthly cash number.
4. Cross-check with our [Salary Calculator]({{ "/tools/salary-calculator" | relative_url }}) and [Income Tax Calculator]({{ "/tools/income-tax-calculator" | relative_url }}).
5. Run the **BATNA prompt**. Know your walk-away.
6. Run the **negotiation prompt** to draft the counter.
7. Edit the draft for voice. Send.
8. Use the [Notice Period & FNF Calculator]({{ "/tools/notice-period-fnf-calculator" | relative_url }}) to plan your transition.

Total time: 30 minutes versus the 4 hours most people spend Googling, posting on r/india, and asking friends.

The AI doesn't make the decision for you. It just speeds up the prep so you can spend your energy on the actual conversation.
