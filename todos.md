# how-to-do.online — Roadmap

Priority-ordered backlog for new tools, blog posts, and SEO infrastructure. Pulled from a May 2026 Google Trends + Indian regulatory-calendar review.

Each item is sized small enough to ship in a day or two. Mark `[x]` when done.

---

## Tier 1 — Build now, peak traffic May–July 2026

These ride the ITR-filing cycle (deadline 31 Jul 2026), the post-rate-cut refinance wave, and the 1-Apr-2026 UPI 2FA mandate.

- [ ] **Crypto Tax Calculator (India, 30% + 1% TDS, Schedule VDA)**
  - Inputs: txn list (buy date, sell date, INR cost, INR proceeds, exchange fees) and wallet/exchange transfers
  - Output: 30% tax on gain, 1% TDS on transfer (≥ ₹10K threshold under section 194S), no loss carry-forward, Schedule VDA values to drop into ITR-2/3
  - Flag the ₹200/day non-disclosure penalty (Feb 2026 budget)
  - Cross-link to Income Tax Calculator and Capital Gains Calculator
- [ ] **ITR Form Picker (ITR-1 vs ITR-2 vs ITR-3 vs ITR-4)**
  - Yes/no quiz: salary only? capital gains? business income? foreign income? agricultural income > ₹5K? director or unlisted shareholder?
  - Output: recommended form + filing deadline + 234F penalty if late
  - Add note that FY 2025-26 still uses Income Tax Act 1961 (Act 2025 applies from 1 Apr 2026 onwards)
  - Companion blog: "ITR-1 vs ITR-2 explained for FY 2025-26"
- [ ] **Home Loan Refinance / Balance Transfer Calculator**
  - Inputs: outstanding principal, current rate, current EMI, tenure left, new rate offer, transfer fee + processing charges
  - Output: new EMI, monthly savings, lifetime interest savings, break-even months
  - Recommend transfer only if break-even < 50% of remaining tenure
  - Cross-link to existing EMI Calculator and Loan Comparison
- [ ] **UPI Limit & 2FA Compliance Checker**
  - Use case dropdown: P2P / merchant / tax / education / healthcare / new account first 24h
  - Output: applicable daily limit (₹1L general, ₹10L for tax/edu/health, ₹5K first-24h), required 2FA factors per "Authentication Mechanisms 2025" rules from 1 Apr 2026, balance-check 50/day cap warning
  - Blog: "RBI's new UPI rules from April 2026 — what changes for you"

---

## Tier 2 — High evergreen volume, build within 4 weeks

- [ ] **EPF Calculator with Rule 9D split (taxable vs non-taxable interest)**
  - 8.25% interest for FY 2025-26
  - Show how much interest is taxable when own contribution exceeds ₹2.5L (₹5L for govt employees)
  - Project corpus year-by-year with employer + employee contribution
  - Companion blog: "How EPF interest gets taxed under Rule 9D"
- [ ] **PM Vishwakarma / PM Mudra Eligibility Checker**
  - Trade dropdown (18 listed trades for Vishwakarma) + business stage for Mudra Shishu/Kishore/Tarun categorisation
  - Output: scheme eligibility, loan amount range, interest, documents needed, application portal link
  - Blog: "Mudra Shishu vs Kishore vs Tarun — which slab fits you"
- [ ] **CUET / NEET / JEE Percentile-to-Rank Estimator**
  - Inputs: marks or percentile, exam, year
  - Output: estimated all-India rank, branch/college fitment using last year's cutoffs
  - Time-bound traffic peak: results land June–July 2026
  - Skip if cutoff data licensing is messy

---

## Tier 3 — Easy wins, long-tail volume

- [ ] **Resignation Letter Generator (India-aware)**
  - Inputs: company, role, notice period, last working day, reason (career growth / personal / relocation), tone (formal / startup / brief)
  - Output: 3 variants with FNF, PF transfer, and relieving letter mentions
  - Print/PDF support
- [ ] **Form 16 Reader / ITR-1 Pre-fill Assistant**
  - Manual-entry first (PDF parsing client-side is fragile)
  - Inputs: Form 16 Part A + Part B fields
  - Output: which fields go into which ITR-1 boxes, with explanations
- [ ] **Notice Period Buyout / FNF Calculator**
  - Inputs: monthly basic, notice period (days), days unserved, gratuity eligibility, leave balance
  - Output: buyout amount, notice pay tax treatment, gratuity, leave encashment
  - Pairs with Resignation Letter Generator

---

## Glossary / blog content (low effort, ranks forever)

One-pager per term: definition + example + companion calculator link.

- [ ] What is XIRR (vs CAGR vs absolute)
- [ ] What is NAV (mutual fund net asset value)
- [ ] What is repo rate / reverse repo rate
- [ ] What is CRR / SLR
- [ ] What is the difference between FY and AY
- [ ] What is TDS, TCS, advance tax
- [ ] What is Form 26AS / AIS / TIS
- [ ] What is PE / PB / ROE / ROCE (cross-link to Stock Fundamentals)

---

## Comparison ("X vs Y") posts — biggest current SEO miss

Each is a calculator + comparison table + verdict. Convert decisions into pages:

- [ ] SIP vs PPF
- [ ] ELSS vs PPF
- [ ] FD vs Debt MF
- [ ] NPS vs PPF
- [ ] Term insurance vs ULIP
- [ ] CTC vs in-hand salary
- [ ] RD vs FD
- [ ] S&P 500 vs Nifty 50 returns
- [ ] HRA vs home loan interest deduction (when can you claim both)

---

## Internal architecture wins (no new content)

- [ ] Category hub pages: `/finance/`, `/dev/`, `/health/` — descriptions + curated tool list (more than the flat tools index)
- [ ] Schema.org markup on each tool page: `HowTo`, `FAQPage`, `SoftwareApplication`
- [ ] FAQ section on every existing tool page (5–7 Q&As) — directly feeds Google "People also ask"
- [ ] Shareable result URLs for calculators (e.g. `/emi-calculator?p=5000000&r=8.5&t=20`) — people share, search engines crawl
- [ ] Pair every existing calculator with a companion `_post` and cross-link both ways

---

## Dev cheatsheets (parallel evergreen track)

- [ ] Git command cheatsheet
- [ ] Linux commands cheatsheet
- [ ] HTTP status codes reference
- [ ] Cron syntax visual reference
- [ ] SQL JOIN visualizer
- [ ] Regex by example

---

## AI tools blog posts

The "AI tools" niche is saturated by generic listicles. The angle for ranking: specific problem → specific tool, India-context, opinionated first-person reviews, and companion posts for our existing AI-powered tools.

### Tier A — high intent, low competition, India angle

- [ ] **How to draft an Indian rent agreement using ChatGPT (with the actual prompt)** — pair with Rent Receipt Generator
- [ ] **Reading your Form 16 with Claude in 2 minutes** — pair with Form 16 → ITR-1 Helper
- [ ] **AI prompts to negotiate your salary in India (with CTC math)** — pair with Salary Calculator
- [ ] **Compare term insurance with ChatGPT (without the salesman)** — high-CPM finance, India

### Tier B — companion blogs for existing AI tools

- [ ] **How our LinkedIn post generator picks engagement-friendly hooks** — prompt logic + before/after
- [ ] **What our SQL Query Explainer is checking under the hood** — explainer + documentation
- [ ] **Debugging a stack trace with AI: the workflow our Log Analyzer uses**

### Tier C — opinionated comparisons

- [ ] **Why I stopped using ChatGPT for emails and switched to Claude** — first-person, workflow
- [ ] **Claude Code vs Cursor for a non-engineer: which one to start with**

### Tier D — prompt library (long evergreen)

- [ ] **The 12 ChatGPT prompts every freelancer in India needs** — pair with Resignation Letter + Invoice Generator

### Skip outright in this category

- "Top 10 AI tools 2026" listicles — saturated to the point of unrankable
- Generic "ChatGPT vs Claude vs Gemini" comparisons
- "Best AI prompts" listicles without specific India use cases
- "Will AI replace [job]?" hot-takes

---

## Skip / monitor (don't build)

- AI coding tool comparison (Claude Code vs Copilot vs Cursor) — saturated, only worth a long-form post, not a tool
- Stock screener — saturated by Screener.in, Groww, Tickertape
- Generic "how to make money online" — saturated, low quality

---

## Source notes (May 2026 research)

- ITR filing 2026 deadlines, IT Act 1961 vs 2025 rules — BusinessToday, Share India, TaxCorp
- Crypto tax 30% + 1% TDS, Schedule VDA, ₹200/day penalty — CoinDCX, ClearTax, MEXC
- RBI repo rate at 5.25%, 125 bps cut in 2025 — SMC Insurance, Upstox
- UPI rules 2026 (2FA from 1 Apr 2026, daily limits, 50/day balance check cap) — Pine Labs, Trade Brains
- EPF interest 8.25% FY 2025-26, Rule 9D taxable interest — Bajaj Finserv
- PM Vishwakarma (₹3L loan, ₹15K toolkit, 30L+ registered) and PM Mudra (Shishu/Kishore/Tarun) — Bank of India, DMI Finance
- CUET UG May 11–31, 2026; NEET admit cards live; JEE Session 2 done — NTA, PW Live
- AI dev tooling adoption — JetBrains research, Pragmatic Engineer

---

_Last updated: 2026-05-01_ (AI blog section added)
