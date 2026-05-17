---
layout: post
title: "Read Your Form 16 with Claude in 2 Minutes (FY 2025-26)"
date: 2026-05-02
category: Personal Finance
description: "Your Form 16 just landed. Don't squint at the PDF for an hour — paste it into Claude or ChatGPT, get a plain-English breakdown of every section, and know exactly what to put where in your ITR."
reading_time: 6
related_tool: /tools/form16-itr1-helper
related_tool_name: Form 16 → ITR-1 Helper
---

Your employer just emailed you a 4-page PDF titled `Form_16_PartA_PartB_FY2025-26_AmitChaudhary.pdf`. Inside: tables full of TAN numbers, sections labelled "Section 17(1)" and "Section 16(ia)", quarterly TDS deductions in Roman numerals.

The traditional advice is "consult a CA" or "watch a 30-minute YouTube video." Better idea: paste it into Claude (or ChatGPT) and ask it to explain. Done in 2 minutes.

Here's the workflow.

## Step 1: Make sure you actually have both Parts

Form 16 has two parts and you need both:

- **Part A** — generated from the TRACES portal by your employer. Contains your PAN, employer's TAN, the company name, and quarterly TDS amounts.
- **Part B** — prepared manually by your employer's payroll team. Has your salary breakdown, exemptions claimed, deductions allowed, and the final tax computed.

If your email has only one PDF, check it carefully. Some employers concatenate Part A + Part B; others send two files. Reading them separately works fine. If you're missing one, ping payroll — it's their job to issue both by 15 June of the assessment year.

## Step 2: The prompt

Paste this into Claude or ChatGPT, then attach the PDF (Claude handles attachments natively; ChatGPT free tier may need you to copy text):

```
I have a Form 16 for FY 2025-26 (AY 2026-27) from an Indian employer.
Here it is. Help me with three things:

1. Walk me through every section in plain English. What does each row mean?
2. Tell me which fields go into ITR-1 boxes and which fields go into 
   ITR-2 boxes. I'm a salaried employee with no capital gains and no 
   business income.
3. Compute my final tax liability under both the Old and New regime, 
   including 4% cess and 87A rebate. Show your math step by step. 
   Tell me which regime saves more tax for me.

If anything looks wrong or missing (e.g. HRA claimed but no rent declared, 
80C exceeding ₹1.5L), flag it.
```

Claude or ChatGPT will produce a structured breakdown like this:

> **Gross salary (₹15,00,000)**: This is your total CTC minus employer PF/gratuity contributions. It includes basic, HRA, special allowance, bonuses received during the year.
>
> **Exemption under section 10 (₹1,80,000)**: Your HRA exemption. Your employer computed this based on the rent declarations you submitted. If you didn't submit rent receipts, this would be ₹0.
>
> **Standard deduction (₹75,000)**: Automatic for salaried employees under the New regime (₹50,000 under Old regime). You don't need receipts for this.
>
> **Taxable salary**: ₹12,45,000.

…and so on, line by line. With the math.

## Step 3: Cross-check against AIS

Now the part most people skip.

Form 16 only shows the income your **employer** reported. It doesn't include:

- Bank interest (savings, FD, RD)
- Dividend income from shares or mutual funds
- Capital gains from selling shares, MF units, property, or crypto
- Rental income from a property you own (not where you live)
- Freelance / consulting income
- Income from outside India

For all of those, you must check your **AIS (Annual Information Statement)** on the income tax portal at incometax.gov.in. Login → Services → Annual Information Statement.

AIS has every reportable financial transaction the government knows about: every share sold, every FD interest payment, every dividend received, every TDS deducted by anyone. Cross-check your Form 16 numbers against AIS — they should match exactly. If AIS shows ₹50,000 in dividend that's not on your Form 16, that's because dividend isn't paid by your employer. Add it to your ITR as "Income from Other Sources."

A second prompt for Claude after pasting both Form 16 and AIS:

```
Reconcile this Form 16 (employer income) with this AIS (everything 
the government knows about my financials). 

What's only in AIS, not in Form 16? Tell me which ITR section 
that income should be reported under, and whether I owe additional 
tax on it.
```

## Common Form 16 fields, decoded

If you don't want to use the prompt, here's the vocabulary:

### Part A

| Field | Means |
|---|---|
| TAN | Employer's Tax Deduction Account Number — used by IT department to track TDS by employer |
| Period | Financial year covered (e.g., 01-Apr-2025 to 31-Mar-2026) |
| Quarter | TDS deducted per quarter (Q1: Apr-Jun, Q2: Jul-Sep, Q3: Oct-Dec, Q4: Jan-Mar) |
| Total TDS | Sum across all 4 quarters — this is your tax credit |

### Part B

| Field | Means |
|---|---|
| Salary as per section 17(1) | Basic + DA + bonuses + variable pay — anything paid in cash or accrued |
| Section 17(2) — perquisites | Non-cash benefits: company car, accommodation, ESOPs (vested portion), interest-subsidised loans |
| Section 17(3) — profit in lieu | Compensation in lieu of salary: severance, ex-gratia, voluntary retirement benefits |
| Less: Sec 10 exemptions | HRA, LTA, conveyance — only allowed under Old regime |
| Standard deduction (Sec 16(ia)) | ₹50,000 (Old) / ₹75,000 (New). Automatic |
| Professional tax (Sec 16(iii)) | State-levied tax (₹200/month for ₹15K+ in Karnataka, ₹2,500/yr in Maharashtra). Old regime only |
| Income from house property | Negative if home loan interest > rental income; capped at ₹2L deduction |
| Chapter VI-A deductions | 80C (₹1.5L cap), 80D, 80CCD(1B), 80E, 80G… all only under Old regime |
| Total taxable income | What gets fed into the slab calculator |
| Tax on total income | Slab tax + surcharge if applicable |
| Less: 87A rebate | Tax becomes nil if income ≤ ₹12L (New) or ≤ ₹5L (Old). Up to ₹60K for New, ₹12.5K for Old |
| Health and Education cess | 4% on the tax-after-rebate |
| Total tax payable | Final number |
| Total TDS already deducted | Tax credit from Part A |
| Refund / balance | (TDS – Total tax). Positive = refund. Negative = pay before filing |

## Things AI tools typically miss

A few caveats:

1. **Multiple Form 16s.** If you switched jobs mid-year, you'll get one Form 16 from each employer. Claude won't automatically combine them — you have to paste both and explicitly say "treat these as two parts of my annual income, sum the gross salary, take the higher standard deduction one-time, sum 80C across both (capped at ₹1.5L)".

2. **Old vs New regime mismatch.** Your employer used the regime you declared at the start of the year. You can switch when filing ITR. If your Form 16 is computed under Old but New saves you more, file under New — TDS already deducted gets adjusted via refund.

3. **Hallucinated section numbers.** LLMs sometimes invent specific sub-sections that don't exist (e.g. "Section 17(1)(viii)") or use the wrong rebate amount. If a number looks weird, cross-check against the [income tax slab tables for FY 2025-26]({{ "/blog/" | relative_url }}) or use our [Income Tax Calculator]({{ "/tools/income-tax-calculator" | relative_url }}).

4. **Surcharge on income above ₹50L.** AI sometimes forgets to add this. Surcharge rates: 10% on ₹50L-1Cr, 15% on ₹1-2Cr, 25% on ₹2-5Cr, 37% above ₹5Cr (capped at 25% under New regime).

## When to skip AI and use the official portal

The IT portal at incometax.gov.in has an excellent **pre-fill** feature. You enter your PAN, your Form 16 + AIS data is auto-imported, and you tweak. For most salaried filers (ITR-1, ITR-2), the portal pre-fill is faster than asking AI.

Use AI when:

- You have **multiple Form 16s** (job change) and want to manually combine before filing
- You want to **understand why** a particular number is what it is
- You want to **compare regimes** without filing twice
- Your Form 16 has unusual entries (RSU vesting, sign-on bonus, relocation reimbursement) that the portal pre-fill mis-classifies

Use the portal when:

- Single Form 16, simple ITR-1
- You trust the auto-import
- You want to file in 15 minutes

## After Claude's done, what to do

1. Plug your final numbers into the [Form 16 → ITR-1 Helper]({{ "/tools/form16-itr1-helper" | relative_url }}). It maps every Form 16 field to the corresponding ITR-1 box, so you know exactly where each value goes when you sit down at incometax.gov.in.
2. Compare regimes one more time using the [Income Tax Calculator]({{ "/tools/income-tax-calculator" | relative_url }}) — confirm Claude's recommendation.
3. If you have capital gains or crypto, also use the [Capital Gains Calculator]({{ "/tools/capital-gains-calculator" | relative_url }}) and [Crypto Tax Calculator]({{ "/tools/crypto-tax-calculator" | relative_url }}). Form 16 doesn't cover those.
4. File. Pay any balance via Challan 280 (self-assessment tax) before submitting your ITR.

The 2-minute Claude pass isn't a replacement for actually understanding your taxes — it's a way to make the documents human-readable. Once you've done it twice, you'll start spotting weird entries on your own.
