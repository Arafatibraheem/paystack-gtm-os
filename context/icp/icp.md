# Paystack ICP

Built only from [context/docs/research/](../docs/research/) (checked 2026-11-13). Each row names its research file. "INFERRED" carries over from the research. Anything the research does not support is listed under Open questions.

Sources key: CO = [company.md](../docs/research/company.md), CU = [customers.md](../docs/research/customers.md), CP = [competitors.md](../docs/research/competitors.md), MK = [market.md](../docs/research/market.md), SG = [signals.md](../docs/research/signals.md), VO = [voice.md](../docs/research/voice.md)

## 1. Firmographic

| Attribute | Fit | Source |
|---|---|---|
| Geography (live) | Nigeria, Ghana, Kenya, South Africa, Côte d'Ivoire | CO |
| Geography (approved, availability unconfirmed) | Egypt, Rwanda | CO |
| Geography (inbound expansion) | International companies entering those markets ("Paystack for Global Brands") | SG, VO |
| Industries with named customers | Fintech: savings (PiggyVest), lending (Renmoney); telecoms (MTN); health insurance (Reliance HMO); mobility (Moove); food delivery (Chowdeck); e-commerce (Granadilla Swim); manufacturing/retail (Mouka, INFERRED); creators (Shutabug) | CU |
| Industries with a dedicated Paystack page | Corporates, Fintechs, Global Brands, Entrepreneurs, Betting, Developers | CU, VO |
| Industries with special pricing | Nigerian educational institutions | CO |
| Funding context | Startups in Nigeria, Egypt, Kenya, South Africa (the four largest funding markets in H1 2026) | MK, SG |

Size is deliberately not a filter: the research shows customers from individual creators to MTN and gives no size threshold (see Open questions). Prioritise by segment instead, below.

### Priority segments, ranked by evidence

Scored on four checks the research can answer. ✓ = supported, ✗ = not found. Ranking method is INFERRED; each check is sourced.

| # | Segment | Named customers (CU) | Paystack segment page (VO) | Product fit (CO) | Dated trigger (MK) | Score |
|---|---|---|---|---|---|---|
| 1 | Nigerian fintechs (lending, savings) | ✓ PiggyVest, Renmoney | ✓ "Paystack for Fintechs" | ✓ Direct Debit, Dedicated Virtual Accounts, Subscriptions, Transfers | ✓ CBN AML directive: roadmap within 3 months, fintech compliance 24 months from Mar 2026 | 4/4 |
| 2 | Nigerian enterprises and corporates | ✓ MTN, Reliance HMO, Mouka | ✓ "Paystack for Corporates" | ✓ Checkout, recurring billing | ✓ E-invoicing: medium taxpayers enforced Jan to Mar 2027 (link to Paystack INFERRED) | 4/4 |
| 3 | Nigerian betting operators | ✗ Not found | ✓ "Paystack for Betting" (headline not found) | ✓ Transfers for payouts | ✓ Lagos 5% withholding tax on winnings (2026) | 3/4 |
| 4 | Shopify / WooCommerce merchants and creators | ✓ Granadilla Swim, Shutabug | ✓ Shopify listing, "Paystack for Entrepreneurs" | ✓ Storefront, Payment Links, plugins | ✗ None | 3/4 |
| 5 | Kenyan merchants | ✗ Not found | ✗ Not found | ✓ M-PESA at 1.5%, cards | ✓ eTIMS "No Invoice, No Deduction" since 1 Jan 2026 (link INFERRED) | 2/4 |
| 6 | International companies entering the seven markets | ✗ Not found | ✓ "Paystack for Global Brands" | ✓ Stripe is a shareholder (CO); Semafor says Stripe integration positions it for cross-border growth (CP) | ✗ None | 2/4 |
| 7 | Nigerian educational institutions | ✗ Not found | ✗ Not found | ✓ Special pricing: cards 0.7% capped at N1,500 | ✗ None | 1/4 |

Competitive pressure per segment (CP): fintechs face Monnify (virtual accounts); enterprises face Interswitch; betting faces Peach Payments (lists betting and gaming); SA Shopify merchants face Yoco and Peach; Kenya faces Pesapal and M-PESA direct; international entrants face Flutterwave (more markets, 30+ currencies).

## 2. Technographic

| Attribute | Fit | Source |
|---|---|---|
| E-commerce platform | Shopify, WooCommerce | CO, SG |
| Accounting | Xero | CO, SG |
| Build approach | In-house dev team using APIs and webhooks (no-code, low-code and pro-code all supported) | CO, CU |
| Payment methods needed | Cards, bank transfer, Direct Debit (NG), mobile money (GH, KE, CI), M-PESA (KE), EFT (ZA), Apple Pay | CO |
| Billing model | Subscriptions, recurring charges, split payments | CO, SG |
| Payouts | Bulk transfers via API | CO, SG |
| In-person | Physical or Virtual Terminal | CO, SG |
| Current provider (displacement) | Flutterwave, Moniepoint/Monnify, Interswitch, Kora, Peach, Yoco, Hubtel, Pesapal, M-PESA direct | CP |

## 3. Intent signals

| Signal | Evidence strength | Source |
|---|---|---|
| Launching in, or entering, one of the seven markets | Paystack page for international companies; multi-country customer story (Chowdeck) | SG |
| New funding round | INFERRED (no Paystack data linking funding to purchase) | SG |
| Compliance deadline: NG e-invoicing (medium taxpayers enforced Jan to Mar 2027; emerging go-live 1 Jul 2027) | INFERRED link to reconciliation need | MK, SG |
| Compliance deadline: CBN AML directive (fintechs, 24 months from Mar 2026) | INFERRED | MK, SG |
| Compliance: Kenya eTIMS "No Invoice, No Deduction" (since 1 Jan 2026) | INFERRED | MK, SG |
| Lagos betting 5% withholding tax on winnings (2026) | INFERRED | MK, SG |
| Launching subscriptions, insurance, or loan repayments | Reliance HMO and Renmoney testimonials (paraphrased) | CU, SG |
| Public evidence of failed payments or slow processing | Customer story titles (80% speed, 93% time reclaimed); MTN testimonial (paraphrased) | CU, SG |
| Adding in-store or offline sales | Virtual Terminal rollout across five markets | SG |
| Paying out to many users (marketplace, gig, lender, betting) | INFERRED | SG |

## 4. Persona

Three buying roles, detailed in [personas.md](personas.md):

| Role | Titles found in research | Source |
|---|---|---|
| Champion | CTO / Chief Technical Officer, IT Manager | CU |
| Economic buyer | Founder / co-founder; Chief Transformation Officer (enterprise) | CU |
| Influencer | Chief Risk Officer | CU |

## 5. Engagement readiness

Dated windows per segment, as of 2026-11-13. Treat an account as ready when it is in a priority segment AND inside its window. Whether these deadlines actually drive payment purchases is INFERRED; the dates come from press, not regulator circulars (MK).

| Segment | Window | What is due | Source |
|---|---|---|---|
| 1. Nigerian fintechs | Now to Mar 2028 | CBN AML directive: roadmap was due within 3 months of Mar 2026; full fintech compliance 24 months from Mar 2026 | MK |
| 2. Nigerian enterprises | Now to Mar 2027 | E-invoicing enforcement for medium taxpayers (turnover ₦1bn to ₦5bn) Jan to Mar 2027 | MK |
| 2. Nigerian enterprises (smaller) | Before 1 Jul 2027 | E-invoicing go-live for emerging taxpayers | MK |
| 3. Nigerian betting | Now (in force) | Lagos 5% withholding tax on winnings since early 2026 | MK |
| 5. Kenyan merchants | Now (in force) | eTIMS "No Invoice, No Deduction" since 1 Jan 2026 | MK |
| 4, 6, 7 | No dated window | Use event triggers from section 3 (market entry, funding, subscription launch, payment-failure complaints) | SG |

Not ready: Egypt- or Rwanda-only businesses until general availability is confirmed (CO).

## Who is not a fit, and why

| Profile | Why | Source |
|---|---|---|
| Businesses selling only in Europe or the UAE | Paystack cut those operations in November 2023 | CO |
| Businesses needing many African markets or 30+ currencies from one provider | Paystack covers seven markets; Flutterwave claims 30+ currencies and more African markets | CO, CP |
| Merchants needing general availability in Egypt or Rwanda today | Only approvals and a private beta confirmed | CO |
| Ghana merchants needing international cards | Ghana international pricing listed as N/A | CO |

## Open questions (not answered by research)

- Employee count, revenue or transaction volume thresholds for a good fit.
- Which segment (SMB, mid-market, enterprise) drives most Paystack revenue.
- Whether Paystack restricts any industries (e.g. crypto, adult, high-risk).
- Fit for POS agent networks under CBN geo-fencing (Moniepoint's core).
- What Paystack MFB offers merchants, and whether credit is available.
- Rwanda pricing; transfer and terminal pricing.
- Which triggers actually convert (no Paystack data found).
- Whether the segment ranking matches Paystack's actual pipeline and win rates. Sales should validate before building lists.
- Named customers for betting, Kenya, international entrants and education.
