---
layout: post
title: "Draft an Indian Rent Agreement with ChatGPT (with the actual prompt)"
date: 2026-05-01
category: Personal Finance
description: "Stop paying ₹2,000 to a lawyer for a standard 11-month rent agreement. Here's the exact ChatGPT prompt that produces a clean Indian rent agreement, plus the clauses you must check before signing."
reading_time: 8
related_tool: /tools/rent-receipt-generator
related_tool_name: Rent Receipt Generator
---

If you've rented a flat in Bangalore, Mumbai, Delhi, or any Indian city in the last few years, you know the pattern. The broker hands you a ₹100 stamp paper, a Word document downloaded from somewhere, and asks you to sign in three places. Most tenants never read past the first page. Most landlords have never read it at all.

This post fixes that, with one prompt and a checklist.

## Why bother drafting your own?

Three reasons:

1. **The "standard agreement" your broker hands you has clauses written by someone else's lawyer.** Often the landlord's. Things like "the tenant agrees to repaint the entire flat at exit" or "the tenant is liable for any structural damage discovered during their tenancy" sneak through. You'll catch these when you draft from scratch.
2. **₹2,000–5,000 saved.** Lawyers charge that much for a 4-page document any LLM can produce in 30 seconds.
3. **You actually understand what you're signing.** This matters when you want to break the lease early or when the landlord refuses to refund the deposit.

That said: I'm not a lawyer. For high-value commercial leases or properties above ₹2 crore, get a real lawyer. For a routine residential 11-month rental? ChatGPT, Claude, or any decent LLM will do it.

## The prompt

Copy this verbatim into ChatGPT or Claude. Replace the bracketed placeholders with your details:

```
Draft a residential rent agreement for an 11-month lease in India.

Parties:
- Landlord: [NAME], aged [AGE], residing at [ADDRESS], PAN [PAN_NUMBER]
- Tenant: [NAME], aged [AGE], currently residing at [ADDRESS], 
  Aadhaar masked: [LAST_4_DIGITS]

Property:
- Address: [FULL_PROPERTY_ADDRESS]
- Type: [1BHK / 2BHK / etc]
- Furnishing: [unfurnished / semi-furnished / fully furnished]
- Inventory: [list any furniture / appliances landlord is leaving behind]

Financial terms:
- Monthly rent: ₹[AMOUNT], payable by [DAY] of each month
- Security deposit: ₹[AMOUNT], refundable within 30 days of vacating
- Maintenance: [borne by tenant / included in rent]
- Annual rent escalation: [PERCENTAGE]% on renewal
- Mode of payment: [bank transfer to account]

Lease terms:
- Start date: [DATE]
- Duration: 11 months
- Lock-in period: [USUALLY 6 MONTHS, NEGOTIABLE]
- Notice period for termination: [USUALLY 1-2 MONTHS]
- Renewal: by mutual consent in writing

Required clauses:
1. Tenant's right to peaceful enjoyment of the property
2. Landlord's right to inspect with 24-hour notice
3. Allocation of utilities (electricity, water, gas, internet)
4. Penalty for late rent payment ([NEGOTIATED]% per month)
5. Restriction on subletting without written consent
6. Use of the property strictly for residential purposes
7. Maintenance responsibilities (minor repairs by tenant; structural by landlord)
8. Treatment of normal wear and tear (not deductible from deposit)
9. Force majeure (pandemic, natural disaster) clause
10. Jurisdiction: courts of [CITY]

Format the output as a formal agreement with numbered clauses, 
witness signature spaces, and standard "IN WITNESS WHEREOF" closing.
Keep it under 4 pages.
```

That's it. Hit enter. You get a clean, professional draft in 30 seconds.

## What to check before signing

The output will be 95% correct. The 5% you must verify:

### Lock-in vs notice period

A lock-in period means you can't leave during that time without paying. A notice period means you must give the landlord that much heads-up before vacating. They are different things. Make sure your agreement is explicit:

- **Lock-in: 6 months.** If you leave before 6 months, you forfeit the security deposit (negotiate this — sometimes it's just the remaining months' rent).
- **Notice period: 1 month.** After lock-in, you can leave with 1 month's written notice.

If the document says "lock-in of 11 months" — that's the entire lease. Push back. Standard is 6 months for residential, sometimes 3.

### Security deposit

In Bangalore, landlords ask for 6–10 months' deposit. In Mumbai/Delhi, 2–3 months. Karnataka tried to cap it at 10 months in 2024 but most landlords still negotiate. Check that:

- The deposit amount is clearly stated.
- Refund timeline is **30 days** maximum — push back if they say "after the next tenant is found."
- Deductions are itemised: only damage beyond normal wear, not repainting and deep-cleaning by default.

### Maintenance

Two flavours:

- **Society maintenance** (₹2K–10K/month, usually paid to the apartment association) — almost always tenant pays.
- **Building / structural maintenance** — landlord. Get this in writing.

If your apartment has BWSSB water charges or a corpus fund, name it explicitly. Disputes here are the second-most-common deposit-refund fight after damages.

### Annual escalation

Most agreements have a 5–10% rent escalation clause "on renewal." This kicks in when you renew for another 11 months. If your landlord says "next year ka rent Diwali ke baad decide karenge" without writing the percentage, get it in writing now.

### Utilities

The agreement should explicitly say who pays:

- Electricity (BESCOM, Adani, Tata Power) — almost always tenant
- Water — usually included in society maintenance, occasionally separate
- Gas pipeline (where applicable) — tenant
- Internet — tenant
- Property tax / municipal tax — landlord (always)

### Maintenance: minor vs structural

Standard split:

- **Tenant**: anything below ₹1,000–5,000 per incident (changing a fused lightbulb, replacing a tap washer, fixing a switch)
- **Landlord**: anything structural (water seepage, plumbing replacement, electrical rewiring, painting before tenant moves in)

If the agreement says "tenant is liable for all repairs" — that's a red flag. Push back.

## The clauses ChatGPT will probably miss (add them yourself)

Three clauses worth adding to the prompt or pasting at the end:

1. **Pet clause.** "Tenant may keep one [dog/cat] as a pet, subject to society rules." Add this if you have or might get a pet — retrofitting later is hard.

2. **Permission to install fixtures.** "Tenant may install fixed-line equipment (RO, AC, geyser) at their cost; these revert to the landlord at exit at the landlord's option, OR the tenant may remove them." Without this, you're forfeiting that ₹15K AC at exit.

3. **WFH / business use clause.** Since 2020, many tenants run businesses from home or do client calls. Some agreements still say "strictly residential, no commercial use." If you run a side hustle or work for a foreign employer, soften this to "use as a residence; tenant may carry on lawful work-from-home activities."

## Stamp paper, registration, notarization

Once the draft is final, the formalities:

- **Stamp duty.** Buy a non-judicial stamp paper. The amount varies by state — Karnataka is 0.5% of (annual rent + 10% of deposit) for sub-1-year leases. Mumbai is similar. Check your state's rates on the relevant Sub-Registrar website.
- **Registration.** Mandatory in some states for leases above 11 months. The reason most agreements are 11-month is to avoid registration. Ask your landlord for registration only if your lease will run beyond 11 months continuously.
- **Notarization.** Optional. Adds a layer of authenticity but doesn't make the document legally stronger than a properly stamped agreement.

For HRA tax purposes, your employer will accept a notarised or properly stamped agreement. If you're claiming HRA above ₹1L/year, you also need the landlord's PAN — make sure it's on the document.

## What to do with the signed agreement

1. Scan a clear PDF copy. Email it to yourself.
2. Generate rent receipts monthly using our [Rent Receipt Generator]({{ "/tools/rent-receipt-generator" | relative_url }}). You'll need them for HRA exemption when filing ITR.
3. Compute your HRA tax saving via the [HRA Calculator]({{ "/tools/hra-calculator" | relative_url }}).
4. If the rent crosses ₹50,000/month, deduct 5% TDS under section 194-IB and deposit it on the IT portal — most tenants forget this.

## When to actually call a lawyer

ChatGPT-drafted agreements are fine for:

- Standard residential leases up to ₹1L/month
- Furnished or unfurnished
- Bangalore / Pune / Hyderabad / Mumbai / Delhi metros

Get a real lawyer if:

- You're leasing for **2+ years** (different stamp duty regime, registration mandatory)
- The property is **commercial** (shops, offices, warehouses)
- The landlord is a **non-resident Indian** (TDS 31.2% under section 195, FEMA implications)
- The deposit exceeds **₹10 lakh** (some states require additional registration for high-value rentals)
- The property has **disputed ownership** or is part of an undivided HUF

## A note on AI-drafted legal documents

LLMs hallucinate. They will sometimes invent clause numbers, cite non-existent sections of the Transfer of Property Act, or use US-style legal phrasing. Always read the output before signing. Cross-check against any existing rent agreement you've signed in the past, ask the landlord to also review it (or get their lawyer to), and don't sign anything you don't understand.

The prompt above produces clean output 90%+ of the time. The remaining 10% — the clauses you push back on, the deposit-refund timeline, the lock-in vs notice — that's where your reading actually matters. AI gets you the boilerplate. You handle the negotiation.

Generate the receipts each month with the [Rent Receipt Generator]({{ "/tools/rent-receipt-generator" | relative_url }}), and when ITR season comes, plug your numbers into the [HRA Calculator]({{ "/tools/hra-calculator" | relative_url }}) to see exactly how much you save.
