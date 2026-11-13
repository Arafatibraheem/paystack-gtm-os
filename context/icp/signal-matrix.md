# Paystack signal matrix

**Status: work in progress (v1, 2026-11-13).** For validation with sales before any build. Method: [signal-matrix-framework.md](../../knowledge-base/playbooks/signal-matrix-framework.md) and [workflow-anatomy.md](../../knowledge-base/playbooks/workflow-anatomy.md).

Inputs: [icp.md](icp.md), [personas.md](personas.md), [research/](../docs/research/). Source codes: CO company, CU customers, CP competitors, MK market, SG signals, VO voice (all in `context/docs/research/`). **INFERRED** = not supported by research. Data sources marked "checked 2026-11-13" were confirmed to exist by web search for this matrix; they are not in the research files.

---

## Matrix 1: Segments x personas

Rows are the seven ICP priority segments (icp.md). Columns are the three personas (personas.md). Angles describe the buyer's situation, not a diagnosed problem.

### Segment definitions

| # | Segment | Target definition (filterable) | Lookalike seeds (named customers, CU) | Lead product / upsell (hypothesis) | Priority |
|---|---|---|---|---|---|
| 1 | Nigerian fintechs | Nigeria-HQ lending, savings or investment apps collecting from consumers | PiggyVest, Renmoney | Direct Debit, Dedicated Virtual Accounts, Transfers (CO) / Paystack MFB, products unknown (INFERRED) | High: ICP 4/4 |
| 2 | Nigerian enterprises | Nigeria-HQ corporates selling to consumers online (telecoms, insurance, consumer goods) | MTN, Reliance HMO, Mouka | Checkout, recurring billing (CO) / Terminal (INFERRED) | High: ICP 4/4, weak timing signals (see Matrix 2) |
| 3 | Nigerian betting operators | Holders of a Lagos (LSLGA) online sports betting licence | Not found | Transfers for payouts, Checkout (CO) | Medium: no named customer |
| 4 | Shopify / WooCommerce merchants and creators | Stores on Shopify or WooCommerce with a .ng, .com.gh, .co.ke, .co.za or .ci domain | Granadilla Swim, Shutabug | Shopify app / WooCommerce plugin (CO) / Storefront, Payment Links, Terminal (INFERRED) | Medium: high volume, no dated trigger |
| 5 | Kenyan merchants | Kenya-based businesses taking M-PESA and card payments | Not found | M-PESA 1.5%, cards 2.9% (CO) / Pesalink at checkout (unverified, CO) | Low: no named customer, no Paystack Kenya page found |
| 6 | International companies entering the seven markets | Non-African HQ companies hiring or launching in NG, GH, KE, ZA, CI | Not found | Checkout across five live markets (CO) | Medium: Paystack has a page for it (VO), no named customer |
| 7 | Nigerian educational institutions | Nigerian schools and universities collecting fees online | Not found | Education pricing: cards 0.7% capped N1,500 (CO) | Low: 1/4, no persona titles in research |

### Angles

| Segment | Champion (CTO, IT Manager) | Economic buyer (Founder, Chief Transformation Officer) | Influencer (Chief Risk Officer) |
|---|---|---|---|
| 1. NG fintechs | Collect deposits and repayments by Direct Debit, virtual accounts and transfers through one API (CO) | Fees stay capped as deposit sizes grow: local fees capped at NGN 2,000, virtual accounts capped at NGN 300 (CO). PiggyVest's co-founder raised card cost at 1.5% of each deposit (CU, unverified verbatim) | Loan collections and onboarding speed, as Renmoney credited (CU, paraphrase). Tie to the CBN AML roadmap is INFERRED |
| 2. NG enterprises | Checkout speed and reliability ("80% increase in payment processing speed since we switched to Paystack Checkout", CU story title) | Fewer payment failures and more payment options, as MTN credited (CU, paraphrase) | Reporting "for accounting, reconciliation, and audits" (VO) ahead of e-invoicing enforcement Jan to Mar 2027 (MK). Link INFERRED; risk title for enterprises INFERRED |
| 3. NG betting | Bulk payouts through the Transfers API (CO) | INFERRED: a new or renewed Lagos licence (₦50m first year, MK) means scaling collections and payouts | INFERRED: payouts under the Lagos 5% withholding tax on winnings (MK) |
| 4. Shopify / Woo | Free Shopify app, WooCommerce preferred partner (CO, VO); "Automatic payouts settled directly to your account" (VO) | "Paystack only makes money when you do" (VO); selling abroad, as Granadilla Swim did "to take Cape Town swimwear global" (CU) | No separate influencer expected at this size (INFERRED) |
| 5. Kenyan merchants | M-PESA, cards, Apple Pay and Amex through one integration (CO) | Published rates: M-PESA 1.5%, local cards 2.9% (CO) | INFERRED: payment records for eTIMS "No Invoice, No Deduction" (MK) |
| 6. International entrants | One integration across five live markets, with Egypt and Rwanda approved (CO) | Paystack says its markets cover about 46% of Africa's GDP (CO). Stripe is a shareholder (CO); the angle that this suits Stripe users is INFERRED | Paystack holds local licences, e.g. CBE and National Bank of Rwanda (CO). Buyer concern about licensing is INFERRED |
| 7. NG education | Open question: no IT title in research | Education pricing: cards 0.7% capped at N1,500, flat NGN 300 otherwise (CO) | Open question: no finance or bursary title in research |

---

## Matrix 2: Signals

Four tests from workflow-anatomy.md, scored 1 (weak) to 3 (strong). `*` = score is INFERRED. Status follows the framework: VERIFIED, VERIFIED (COMPOUND), PARTIAL, KILLED.

| ID | Type | Signal | Segments | Mother intent | Data source | Detection tool | Reason | Volume | Data | Story | Total /12 | Status |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| U1 | Universal | New funding round in the last 90 days | 1, 4, 6 | Companies fundraising | Crunchbase; Africa: The Big Deal (thebigdeal.substack.com); The Condia funding tracker (thecondia.com/category/funding-tracker) (SG, MK) | Clay "Find Organization" (Crunchbase), filter country + round date; Clay HTTP for trackers | 2* | 2: 110 deals over $100k in NG, EG, KE, ZA in H1 2026 (MK) | 3 | 3 | 10 | VERIFIED |
| U2 | Universal | New Shopify or WooCommerce store on a target-country domain, no Paystack detected | 4, 5 | Companies using specific software | BuiltWith (Shopify, WooCommerce, Paystack, Flutterwave are all tracked; checked 2026-11-13: trends.builtwith.com/payment/Paystack) | Clay "Find Technology Stack" (BuiltWith), filter TLD + first-detected date; suppress sites already showing Paystack | 2: Shopify app and Woo partner exist (CO) | 3* | 3 | 2* | 10 | VERIFIED |
| U3 | Universal | Hiring a country manager, GM or launch role in NG, GH, KE, ZA or CI, at a company HQ'd outside Africa | 6 (also 2) | Hiring specific roles | LinkedIn Jobs via Clay; Stripe on site via BuiltWith as compound | Clay "Find Jobs", location filter; Clay "Find Technology Stack" for Stripe | 3: Paystack runs a "Global Brands" page (VO, SG) | 1* | 2* | 3 | 9 | VERIFIED (COMPOUND with Stripe tech) |
| U4 | Universal | Opened new physical locations in the last 90 days | 2, 5 | Niche-specific play (physical world) | Google Places API | Clay HTTP, monthly location-count delta | 2: Virtual Terminal rollout in five markets (SG) | 2* | 2* | 3 | 9 | PARTIAL (INFERRED fit; test on 20 accounts first) |
| U5 | Universal | Hiring payments or integration engineers | 1, 2, 3 | Hiring specific roles | LinkedIn Jobs via Clay; local boards (MyJobMag, BrighterMonday) via Apify, coverage INFERRED | Clay "Find Jobs", keywords "payments", "payment integration", "fintech backend" | 2* | 2* | 2* | 2 | 8 | PARTIAL |
| U6 | Universal | Launched subscription or recurring plans | 1, 2, 4 | New product launches / Website content mentions | Company pricing pages; Product Hunt | Claygent scrape for "per month", "subscribe", "plan" | 2: Reliance HMO credits recurring billing (CU, paraphrase) | 2* | 2* | 2 | 8 | PARTIAL |
| U7 | Universal | Lookalike of named customers | 1, 2 | Lookalike of customers | Seeds: PiggyVest, Renmoney, MTN, Reliance HMO, Mouka (CU) | Clay lookalike / "Find Companies" by industry + country | 1: static, no timing | 2* | 3 | 2: testimonials unverified (CU) | 8 | VERIFIED (use as base list, not trigger) |
| U8 | Universal | Public complaints about failed payments (app store reviews) | 1, 3 | Niche-specific play | Google Play / App Store reviews | Apify review scraper into Clay, keywords "payment failed", "debited" | 3: MTN credits fewer failures (CU, paraphrase) | 2* | 1* | 1: guardrail, do not diagnose | 7 | PARTIAL (enrichment only) |
| U9 | Universal | Competitor customer (Flutterwave or Rave on site) | 1, 4, 6 | Competitor customers | BuiltWith: about 1,275 live Flutterwave sites (snapshot undated; checked 2026-11-13: trends.builtwith.com/payment/Flutterwave) | Clay "Find Technology Stack" | 1 | 2 | 3 | 1*: price comparisons conflict (CP) | 7 | VERIFIED (COMPOUND only) |
| N1 | Niche (3) | Newly listed on the Lagos (LSLGA) licensed operators register | 3 | Niche-specific play (licensing event) | lslga.org licensed operators register: 70+ entities as of Sep 2025 (checked 2026-11-13 via focusgn.com report) | Clay HTTP scrape, monthly diff | 2* | 1 | 2 | 3 | 8 | VERIFIED |
| N2 | Niche (1) | Licensed by the CBN as a payment service provider | 1 | Niche-specific play (licensing event) | cbn.gov.ng/PaymentSystem/PSPs.asp: about 75 PSSP holders per TechCabal (checked 2026-11-13) | Clay HTTP scrape, monthly diff | 1*: many licensees compete with Paystack | 1 | 2: page dates unclear | 2 | 6 | PARTIAL (screen out competitors) |
| N3 | Niche (2) | Medium taxpayer in Nigerian e-invoicing scope (turnover ₦1bn to ₦5bn) | 2 | Regulatory changes | No public taxpayer list found; turnover not observable | Proxy: employee count via Clay "Enrich Company" (INFERRED) | 1*: link INFERRED | 2* | 1 | 2 | 6 | PARTIAL (narrative enrichment only) |
| N4 | Niche (1) | CBN AML directive window | 1 | Regulatory changes | MK (applies to all fintechs; no per-company timing) | None: static | 1* | 1 | 1 | 1 | 4 | KILLED as trigger: no timing, Paystack's AML help not in research. Keep as context |
| N5 | Niche (3) | Lagos 5% withholding tax on winnings | 3 | Regulatory changes | MK (in force since early 2026) | None: static | 1* | 1 | 1 | 2 | 5 | KILLED as trigger: already in force, no per-company timing |
| N6 | Niche (5) | Kenya eTIMS "No Invoice, No Deduction" | 5 | Regulatory changes | MK (applies to all businesses since 1 Jan 2026) | None: static | 1* | 1 | 1 | 1 | 4 | KILLED as trigger: no timing, link INFERRED |
| N7 | Niche (5) | New entries in the CBK directory of authorised PSPs | 5 | Niche-specific play | centralbank.go.ke directory PDFs, updated May, Jun, Aug 2026 (checked 2026-11-13) | Clay HTTP, diff PDFs | 1: entrants are payment providers, not merchants | 1 | 2 | 1 | 5 | KILLED: wrong buyer (possible partner list) |
| X1 | Universal | New CTO, CFO or Head of Payments (90 days) | All | New leadership | Clay "Find People" | Clay | - | - | - | - | - | KILLED for now: no research evidence (removed from icp.md). Retest with sales |
| X2 | Niche (7) | School fee season / new academic session | 7 | Niche-specific play | Not found | None | - | - | - | - | - | KILLED: no data source |

**Compounding:** 9 of 16 scored signals are universal (one Clay build, keyword swaps per segment). Niche builds are only needed for Lagos betting (N1) and CBN licensees (N2). Kenya and education have no live niche signal.

**Gap:** Segment 2 (NG enterprises) ranks top in the ICP but has no strong timing signal. Best available: U7 lookalike as the base list, with U3, U4 and U6 as triggers.

---

## Build first

| Rank | Signal | Segment | Why |
|---|---|---|---|
| 1 | U1 New funding | 1. NG fintechs (then 4, 6) | Highest score (10). Data is cheap and verified (Crunchbase, Big Deal, Condia). Feeds the top ICP segment. Volume is real: 110 deals over $100k in the four largest markets in H1 2026 (MK) |
| 2 | U2 New Shopify / WooCommerce store, no Paystack | 4. Shopify / Woo merchants (then 5) | Score 10, highest volume. Integration is verified (CO). BuiltWith also gives a suppression list of existing Paystack sites, so the same build cleans every other list |
| 3 | U3 Market-entry hiring + Stripe on site | 6. International entrants | Score 9. Paystack built a page for this buyer (VO). Stripe shareholder link gives a natural story; whether Stripe users prefer Paystack is INFERRED |
| 4 | N1 New Lagos betting licence | 3. NG betting | Score 8. Cheap monthly scrape, clear event, natural opener. Risk: no named betting customer in research, so validate with sales before copy |

Not first: U4 (physical locations) scores 9 but the fit is INFERRED; test it on 20 accounts before building.

---

## Matrix 3: Workflow tracker

Other tracker columns (campaigns, launch date, Clay URL, metrics) are added when each workflow launches.

| W # | Status | Workflow name | Mother intent | Segment | Persona |
|---|---|---|---|---|---|
| W1 | Planned | Recently funded NG fintechs | Companies fundraising | 1 | Economic buyer |
| W2 | Planned | New African Shopify / Woo stores without Paystack | Companies using specific software | 4 | Economic buyer (founder) |
| W3 | Planned | Global brands hiring for African launch | Hiring specific roles | 6 | Economic buyer |
| W4 | Planned | New Lagos betting licensees | Niche-specific play | 3 | Champion |
| W5 | Planned | New physical locations (test) | Niche-specific play | 2, 5 | Economic buyer |
| W6 | Planned | Payments engineering hires | Hiring specific roles | 1, 2, 3 | Champion |
| W7 | Planned | Subscription launches | New product launches | 1, 2, 4 | Champion |
| W8 | Planned | Named-customer lookalikes | Lookalike of customers | 1, 2 | Economic buyer |
| W9 | Planned | New CBN payment licensees (screened) | Niche-specific play | 1 | Champion |

---

## To validate with sales

- Segment ranking and lead products per segment.
- Whether betting (no named customer) belongs in the first four builds.
- Volume scores marked `*`: run each Clay search once and replace with real counts.
- Whether Paystack MFB has merchant products to use as an upsell.
- Real names per segment: run Clay with the target definitions above; no examples were added beyond named customers in research.
