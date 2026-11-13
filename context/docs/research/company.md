# Paystack: company

Raw research, not conclusions. All facts checked 2026-11-13 unless stated otherwise.

**Method note (applies to all research files):** paystack.com returns HTTP 403 to automated fetches, so Paystack's own pages could not be read directly. Sources used instead: support.paystack.com (fetched), Paystack's Shopify App Store listing (fetched), the Stripe newsroom (fetched), press coverage (fetched), and search-index results for paystack.com pages. Where a fact comes only from a search-index result, it is marked **[search index, not fetched]**. Page *titles* from the search index are reliable; body wording from the search index may be paraphrased.

## What they sell

- Self-description: "Paystack is a payment service provider that facilitates easy, fast and secure online and in-person payments" for African businesses. Offers "no-code, low-code, and pro-code tools" plus add-ons: recurring payments, invoicing, subscription billing, split payments. Source: https://support.paystack.com/en/articles/2130562 (checked 2026-11-13)
- Homepage page title: "Paystack - Modern online and offline payments for Africa". Source: https://paystack.com/ **[search index, not fetched]** (checked 2026-11-13)

### Products

| Product | What it is | Source |
|---|---|---|
| Checkout / Payments API | Hosted payment page and APIs for online payments | https://paystack.com/docs/payments/ [search index, not fetched] |
| Payment Links, Storefront, Product Links | No-code selling: links, a digital shop with themes, product variants and inventory | https://paystack-changelog.netlify.app/ [search index, not fetched] |
| Subscriptions, Recurring Charges | Recurring billing | https://paystack.com/docs/payments/ [search index, not fetched] |
| Split Payments | Divides a transaction's payout across several accounts | https://paystack.com/docs/payments/ [search index, not fetched] |
| Direct Debit (Nigeria) | Charge customers' bank accounts directly; built with NIBSS | https://paystack.com/docs/payments/ [search index, not fetched] |
| Transfers | Single and bulk payouts via API | https://paystack.com/docs/payments/ [search index, not fetched] |
| Dedicated Virtual Accounts (Nigeria) | Priced at "1% per transaction (capped at NGN 300)" | https://support.paystack.com/hc/en-us/articles/360009881920 |
| Paystack Terminal (physical) and Virtual Terminal | In-person payments. Virtual Terminal launched in Nigeria in 2023 with no hardware, later expanded to Côte d'Ivoire, Ghana, Kenya, South Africa | https://dabafinance.com/en/news/stripeowned-paystack-launches-new-product-for-offline-payments ; https://paystack.com/ci [search index, not fetched] |
| Zap | Consumer app for fast bank transfers in Nigeria, launched March 2025; Paystack's first consumer product | https://www.semafor.com/article/01/20/2026/paystack-eyes-growth-beyond-payments-with-restructuring ; https://techpoint.africa/news/paystack-launches-zap/ |
| Paystack Microfinance Bank (MFB) | Formed by acquiring Ladder Microfinance Bank in Nigeria; acquisition completed January 2026 | https://techpoint.africa/news/paystack-creates-holding-company/ ; https://www.semafor.com/article/01/20/2026/paystack-eyes-growth-beyond-payments-with-restructuring |
| TSG Labs | Venture studio building products with emerging tech including AI, kept separate from regulated entities | https://techpoint.africa/news/paystack-creates-holding-company/ |

- Integrations: Shopify (since 2016), WooCommerce preferred payment partner (2021), Apple Pay (2021), Xero (2022). Source: https://en.wikipedia.org/wiki/Paystack (citing Disrupt Africa, WordPress.org, TechCrunch, Africa Fintech Network)
- Zap was later added to Paystack Checkout so merchants can accept payment from customers' bank accounts. One report says a CBN regulatory fine pushed Zap into a rebuild phase. Source: https://thecondia.com/paystack-revives-zap-eight-months-after/ [search index, not fetched]. Not verified against a primary source.
- Reported 2026 launches not verified: a rebuilt Dashboard (May 2026), "Paystack Index" AI checkout tool (June 2026), Pesalink at checkout in Kenya (July 2026), rebuilt merchant app (24 Sep 2026), Small Business Bundle. Source: search summary citing Owler and the Paystack blog, https://www.owler.com/company/paystack and https://paystack.com/blog. **Not verified.**

## Pricing model

Pay per transaction, no setup fee. Paystack's words on its Shopify listing: "Paystack only makes money when you do." Source: https://apps.shopify.com/paystack (checked 2026-11-13)

Transaction pricing, quoted from https://support.paystack.com/hc/en-us/articles/360009881920 (checked 2026-11-13; the article shows no last-updated date):

| Country | Local | International |
|---|---|---|
| Nigeria (NGN) | "1.5% + NGN 100 (all local channels, including Direct Debit)". "All local transaction fees are capped at NGN 2,000". "the NGN 100 fee is waived for transactions under NGN 2,500" | "3.9% + NGN 100 (via Mastercard, Visa, Verve cards)"; Amex "4.5%". USD cards "3.9%" |
| Ghana (GHS) | "1.95% (cards, mobile money, bank transfer)" | N/A |
| Kenya (KES) | "2.9% (cards)"; "1.5% (M-PESA)" | "3.8%" (Mastercard, Visa, Apple Pay, Amex) |
| South Africa (ZAR) | "2.9% + R1.00 (VAT exclusive)"; "2% (via EFT)" | "3.1% + R1.00 (VAT exclusive)" |
| Côte d'Ivoire (XOF) | "3.2% VAT excl (cards)"; "1.95% VAT excl." mobile money (Wave, MTN, Orange Money) | "3.8% VAT excl." |
| Egypt (EGP) | "2.7% + EGP 2.5" Visa/Mastercard; "2.0% + EGP 2.5" Meeza | "3.5% + EGP 2.5" |

- Nigerian educational institutions: local cards "0.7% capped at N1,500"; other methods "a flat NGN300 fee". Same source.
- Rwanda pricing: Not found.
- Transfer (payout) pricing: Not found (lives in a separate support article not retrieved).
- Terminal pricing: exists at https://support.paystack.com/en/articles/2131842, not retrieved.
- Enterprise or negotiated pricing: Not found.

## Markets

- Licensed and operational: Côte d'Ivoire, Ghana, Kenya, Nigeria, South Africa. Regulatory approvals in Egypt and Rwanda. Paystack says these markets are about 46% of Africa's GDP. Source: https://techpoint.africa/news/paystack-creates-holding-company/ (published 2026-01-20)
- Licences: Payment Service Provider authorisation from the National Bank of Rwanda; Payment Facilitator and Payment Service Provider from the Central Bank of Egypt. Source: search summary of Paystack's Jan 2026 announcement, https://paystack.com/blog/company-news/10-years-of-paystack-and-the-beginning-of-the-stack-group [search index, not fetched]
- Egypt and Rwanda general availability: Not confirmed. Support article still describes a "private beta" in Côte d'Ivoire and Egypt. Source: https://support.paystack.com/en/articles/2130562
- Timeline: launched Lagos January 2016, Nigeria only; South Africa May 2021; Côte d'Ivoire, Egypt, Rwanda early access November 2023. Sources: https://www.semafor.com/article/01/20/2026/paystack-eyes-growth-beyond-payments-with-restructuring ; https://en.wikipedia.org/wiki/Paystack ; https://techpoint.africa/2023/11/02/paystack-expands-to-egypt-rwanda-and-cote-divoire/
- Exited Europe and UAE operations in November 2023 (33 layoffs). Source: https://techcabal.com/2023/11/16/paystack-layoffs/

## Scale

- "300,000 merchants" (Semafor, Jan 2026). Source: https://www.semafor.com/article/01/20/2026/paystack-eyes-growth-beyond-payments-with-restructuring
- "Over 200,000 businesses use Paystack" (support article). Source: https://support.paystack.com/en/articles/2130562
- Payment volume grew "more than twelvefold" since the 2020 acquisition. Absolute TPV: Not found. Source: https://techpoint.africa/news/paystack-creates-holding-company/
- Profitable across all markets for the first time in February 2025; seven profitable months in 2025, per Akinlade. Revenue and profit figures: Not found. Source: https://www.semafor.com/article/01/20/2026/paystack-eyes-growth-beyond-payments-with-restructuring
- At acquisition (Oct 2020): "more than half of all online transactions in Nigeria"; "More than 60,000 businesses in Nigeria and Ghana". Source: https://stripe.com/newsroom/news/paystack-joining-stripe

## Funding and ownership

| Date | Event | Amount | Investors | Source |
|---|---|---|---|---|
| 2016 | Y Combinator W16 | Not confirmed | Y Combinator | https://en.wikipedia.org/wiki/Paystack |
| Dec 2016 | Seed | $1.3M | Incl. Tencent, Comcast Ventures | https://www.forbes.com/sites/mfonobongnsehe/2016/12/19/nigerian-fintech-startup-paystack-raises-1-3-million/ (via Wikipedia) |
| Aug 2018 | Series A | $8M | Led by Stripe; Visa, Tencent | https://ventureburn.com/2018/08/paystack-8-series-a/ (via Wikipedia) |
| Oct 2020 | Acquired by Stripe | "over $200 million" (terms undisclosed) | Stripe | https://techcrunch.com/2020/10/15/stripe-acquires-nigerias-paystack-for-200m-to-expand-into-the-african-continent |
| Oct 2025 / Jan 2026 | The Stack Group (TSG) holding company formed; agreements signed Oct 2025, pending regulatory approval | Not disclosed | Founding shareholders: Stripe, Shola Akinlade, Paystack employees | https://techpoint.africa/news/paystack-creates-holding-company/ |

- Stripe's percentage stake in TSG: Not found.
- Total raised before acquisition: reported as about $10M to $11.7M; TechCabal says $11.5M. Sources conflict. https://techcabal.com/2020/10/15/stripe-acquires-paystack/

## Team size

- "Paystack's 209 employees" are founding TSG shareholders (Semafor, Jan 2026). Source: https://www.semafor.com/article/01/20/2026/paystack-eyes-growth-beyond-payments-with-restructuring
- Current (Nov 2026) headcount: Not found.
- Open roles seen in 2026 (aggregators, not verified live): Security GRC Officer, Senior DevOps Engineer, Senior Data Engineer, Product Marketer (Lagos), Project Management role at Paystack MFB. Source: https://job-boards.greenhouse.io/paystack and aggregators listed at https://jobera.com/job/paystack-security-grc-officer-1aede52f/ [search index, not fetched]

## Leadership

- Shola Akinlade: co-founder and CEO. Source: https://techpoint.africa/news/paystack-creates-holding-company/
- Ezra Olubi: co-founder and former CTO. Suspended then fired November 2025 over misconduct allegations; Paystack cited "significant negative reputational damage". Will not hold a stake in TSG. Sources: https://weetracker.com/2025/11/14/paystack-ezra-olubi-suspended-sexual-misconduct-allegations/ ; https://www.semafor.com/article/01/20/2026/paystack-eyes-growth-beyond-payments-with-restructuring
- Other executives (CTO, CFO, COO, country leads, Paystack MFB MD): **Not found.** Third-party org charts are out of date (some still list Olubi as CTO).

## Key quotes from leadership

- Shola Akinlade: "There are significant opportunities to support businesses beyond payments" and "TSG enables us to address the challenges African companies face over the next decade". Source: https://techpoint.africa/news/paystack-creates-holding-company/
- Shola Akinlade: "We're betting on African entrepreneurs." Source: https://www.semafor.com/article/01/20/2026/paystack-eyes-growth-beyond-payments-with-restructuring
- Shola Akinlade (2020): "We believe deeply that with the right tools, African creators, developers, and entrepreneurs can do incredible things." Source: https://stripe.com/newsroom/news/paystack-joining-stripe
