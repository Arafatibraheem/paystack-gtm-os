# Paystack outbound GTM system

**Status: design v1, 2026-11-13. Work in progress; nothing here is live.**

Built from [context/icp/icp.md](../icp/icp.md), [personas.md](../icp/personas.md) and [signal-matrix.md](../icp/signal-matrix.md). Tool rules come from the playbooks in [knowledge-base/playbooks/](../../knowledge-base/playbooks/). **INFERRED** = a design choice the context files do not support; validate it. **OPEN** = a decision still to be made.

## Stack

| Job | Tool | Status |
|---|---|---|
| Signals, enrichment, fit check, people, emails | Clay, driven locally through `tools/rex` | In stack (CLAUDE.md) |
| Scheduling, glue, reply routing | n8n | In stack (CLAUDE.md) |
| System of record | HubSpot | In stack (CLAUDE.md) |
| Email finding | Clay waterfall: Prospeo, Icypeas, LeadMagic, Findymail | Playbook default (clay/expert.md) |
| Email validation | Bounceban | Playbook default (clay/expert.md) |
| Email sequencer | OPEN: kit supports Instantly, Smartlead, PlusVibe, Email Bison | Not chosen |
| LinkedIn automation | OPEN: playbook example is HeyReach | Not chosen |
| Deliverability test | MailReach via `/inbox-placement-test` | Skill exists |

## Flow

```
0 Context OS ──► 1 Signals ──► 2 Find companies ──► 3 Enrich ──► 4 ICP fit check
                                                                     │ fail ──► suppress / nurture
                                                                     ▼ pass
 11 Weekly loop ◄── 10 HubSpot ◄── 9 Replies ◄── 8 Sequence ◄── 7 Emails ◄── 6 People ◄── 5 Route by segment
      │
      └──► updates Context OS (step 0)
```

The workflow always starts from the signal, then applies the ICP filter (signal-matrix-framework.md guardrail).

---

## Step 0: Context OS

**What happens:** every run reads the same source of truth. Segments, personas, angles and signals live in `context/icp/`; facts live in `context/docs/research/`; copy rules live in `knowledge-base/playbooks/`. Campaign specs are written to `output/campaigns/<workflow-slug>/workflow-spec.md` by `/build-workflow-spec`, then `/campaign-copy`.

**Tool:** this repo plus Claude Code skills.

| Decision | Answer → leads to |
|---|---|
| Does the workflow have an approved spec (`STRUCTURE-APPROVED`)? | Yes → build in Clay. No → run `/build-workflow-spec` first; nothing gets built without it |
| Is every claim in the copy traceable to `context/`? | Yes → continue. No → cut it or add a sourced fact to research first (CLAUDE.md rule) |
| Has the matrix changed since the last build? | Yes → re-run affected workflows' specs. No → reuse |

---

## Step 1: Buying signals

**What happens:** each workflow watches one mother intent from signal-matrix.md on a schedule. Build order from the matrix: W1 funding, W2 new Shopify/Woo stores, W3 market-entry hiring, W4 Lagos betting licences.

**Tool:** Clay sources, triggered by n8n on the cadence below.

| Signal (matrix ID) | Source | Cadence | Segment |
|---|---|---|---|
| U1 New funding | Crunchbase via Clay "Find Organization"; Big Deal and Condia trackers via Clay HTTP | Every two weeks (workflow-anatomy.md: funding = bi-weekly) | 1, then 4, 6 |
| U2 New Shopify/Woo store, no Paystack | BuiltWith via Clay "Find Technology Stack" | Monthly (tech adoption = monthly) | 4, 5 |
| U3 Market-entry hiring + Stripe on site | Clay "Find Jobs" + BuiltWith | Weekly (job posts = weekly) | 6 |
| N1 New Lagos betting licence | lslga.org register via Clay HTTP, diffed | Monthly | 3 |
| U5, U6, U4 (later builds) | See signal-matrix.md | Weekly / monthly | 1, 2, 3, 5 |

| Decision | Answer → leads to |
|---|---|
| Is the signal newer than the last run? | Yes → new row. No → skip (dedupe on domain + signal ID) |
| Is the signal a COMPOUND-only type (U9 competitor tech)? | Yes → never starts a workflow; used only as enrichment in step 3. No → can start a workflow |
| Was the domain contacted in the suppression window? | Yes → hold until window ends, unless a new signal fires (workflow-anatomy.md: re-entry on new signal). No → continue. Window length: OPEN |

---

## Step 2: Finding companies

**What happens:** each signal row becomes a company row with a clean domain, the one key used everywhere after this.

**Tool:** Clay Companies table.

| Decision | Answer → leads to |
|---|---|
| Does the row have a resolvable domain? | Yes → normalise (lowercase, no www, no path). No → Clay company lookup by name; still none → drop and count it in the weekly loop |
| Does the domain already exist in HubSpot? | As customer → suppress. As open deal → suppress, notify owner. As closed-lost or contacted → continue only if suppression window passed. Not found → continue |
| Does BuiltWith show Paystack on the site? | Yes → suppress (existing user; signal-matrix.md U2 note). No → continue |

---

## Step 3: Enrichment

**What happens:** add the fields the fit check and the copy need, and nothing else. 2 to 4 secondary enrichments per workflow (workflow-anatomy.md).

**Tool:** Clay. Run conditions so paid columns only run on rows that passed earlier gates.

| Field | Source | Why |
|---|---|---|
| HQ country, industry, employee count | Clay "Enrich Company" | Segment and geography check |
| Funding round and date | Crunchbase | U1 and narrative |
| Payment tech on site (Paystack, Flutterwave, Stripe, Shopify, WooCommerce) | BuiltWith | Suppression, U9 compound, U3 compound |
| Licence status (CBN PSP list, LSLGA register) | Clay HTTP | Segment 1 and 3 routing, competitor screen |
| Subscription pricing on site | Claygent | U6 and narrative |

| Decision | Answer → leads to |
|---|---|
| Did a field return empty? | Yes → leave empty, never guess; copy uses the fallback route. No → use it |
| Does the row need Claygent (5 to 25 credits, clay/expert.md)? | Only if it passed the fit check's free gates first. Otherwise skip |
| Is projected spend inside budget? | Yes → run. No → stop and run `/calculate-costs` on a sample first. Budget: OPEN |

---

## Step 4: ICP fit check

**What happens:** a rules-based pass or fail, run in this order so the free checks run first.

**Tool:** Clay formula columns (free), then one Claygent column only where a rule needs judgement.

| # | Check (source) | Pass → | Fail → |
|---|---|---|---|
| 1 | HQ or launch market is Nigeria, Ghana, Kenya, South Africa or Côte d'Ivoire (icp.md) | Next check | Egypt or Rwanda only → nurture list until availability confirmed. Europe or UAE only → disqualify (icp.md non-fit) |
| 2 | Not an existing Paystack user (BuiltWith, HubSpot) | Next check | Suppress |
| 3 | Not a payment provider competing with Paystack (CBN PSP list screen, signal-matrix.md N2) | Next check | Disqualify; optionally flag as partner lead (INFERRED) |
| 4 | Does not need many African markets or 30+ currencies from one provider (icp.md non-fit) | Next check | Disqualify. How to detect this: OPEN (INFERRED proxy: operating in 8+ African countries) |
| 5 | Ghana merchant needing international cards (icp.md non-fit: Ghana international = N/A) | Disqualify | Next check |
| 6 | Matches at least one segment definition (step 5) | Route | No segment → hold; count in weekly loop as an ICP gap |

No size filter: icp.md has no size threshold (open question).

---

## Step 5: Routing by segment

**What happens:** each company gets exactly one segment, which sets the angle table, lead product and personas. Order runs from the most specific evidence to the least so a company never lands in two segments (INFERRED order).

**Tool:** Clay formula column.

| Order | Rule | Segment | Lead product (signal-matrix.md) |
|---|---|---|---|
| 1 | On LSLGA register | 3. NG betting | Transfers for payouts, Checkout |
| 2 | Nigeria HQ, lending/savings/investment app | 1. NG fintech | Direct Debit, virtual accounts, Transfers |
| 3 | HQ outside Africa, hiring or launching in a live market | 6. International entrant | Checkout across five markets |
| 4 | Nigeria HQ, corporate selling online (telecoms, insurance, consumer goods) | 2. NG enterprise | Checkout, recurring billing |
| 5 | Shopify or WooCommerce on a target-country domain | 4. Shopify / Woo | Shopify app / Woo plugin |
| 6 | Kenya HQ taking M-PESA and cards | 5. Kenyan merchant | M-PESA and cards |
| 7 | Nigerian school or university | 7. NG education | Education pricing |

| Decision | Answer → leads to |
|---|---|
| Segment 3 or 6 (no named customer, signal-matrix.md)? | Yes → copy uses no customer proof, only Paystack facts. No → may use named-customer proof once quotes are verified (personas.md warning) |
| Segment 7? | Low priority; do not build until titles are known (personas.md open question) |

---

## Step 6: Finding people

**What happens:** find up to one person per persona at each company, using the titles in personas.md.

**Tool:** Clay "Find People" (Apollo-backed) into one shared People table (`/build-clay` pattern).

| Segment | Champion | Economic buyer | Influencer |
|---|---|---|---|
| 1. NG fintech | CTO, IT Manager | Founder, co-founder | Chief Risk Officer |
| 2. NG enterprise | CTO | Chief Transformation Officer | Risk title INFERRED |
| 3. NG betting | CTO (INFERRED) | Founder / CEO (INFERRED) | Skip until titles known |
| 4. Shopify / Woo | Founder is also the buyer | Founder | None (INFERRED) |
| 5. Kenyan merchant | CTO (INFERRED) | Founder (INFERRED) | Skip |
| 6. International entrant | CTO (INFERRED) | Country manager / GM being hired, or founder (INFERRED) | Skip |

| Decision | Answer → leads to |
|---|---|
| Person found for the persona the workflow targets (signal-matrix.md Matrix 3)? | Yes → continue. No → try the next persona in the row. None → company goes to a "no contact" list, reviewed weekly |
| More than one match for a persona? | Pick most senior current title; never more than three people per company (INFERRED cap) |
| LinkedIn URL found? | Yes → eligible for LinkedIn steps. No → email only |

---

## Step 7: Finding and verifying emails

**What happens:** waterfall, then validation, then a send/no-send decision.

**Tool:** Clay waterfall Prospeo → Icypeas → LeadMagic → Findymail, then Bounceban (clay/expert.md: limit depth to 3 to 4 providers; always validate).

| Decision | Answer → leads to |
|---|---|
| Waterfall found an email? | Yes → validate. No → LinkedIn-only if URL exists; else drop and count |
| Bounceban result: valid | Send |
| Bounceban result: catch-all / risky | INFERRED: send only from a separate low-risk inbox group, or LinkedIn-only. Decide after the first week's bounce data |
| Bounceban result: invalid | Never send. LinkedIn-only if URL exists |
| Bounce rate on the last batch above 3% (copy-frameworks.md target)? | Yes → pause the workflow, check the provider order and domain hygiene before the next batch. No → continue |

Coverage of African professional emails in these providers is unknown (INFERRED risk). Measure find rate per country in week one.

---

## Step 8: The sequence (email and LinkedIn)

**What happens:** copy comes from the workflow spec, written with `/campaign-copy` under copy-iron-laws.md, copy-bans.yaml and the no-em-dash rule. Angles come from signal-matrix.md Matrix 1.

**Tool:** email sequencer (OPEN), LinkedIn tool (OPEN), n8n to keep channels in sync.

### Email (copy-frameworks.md follow-up stack)

| Step | Day | Job |
|---|---|---|
| 1 | 0 | Earn the reply: the signal as an observation, one question |
| 2 | 3 to 4 | Add new value: one Paystack fact from research |
| 3 | 7 to 10 | New angle or "right person?" |
| 4 (optional) | 14+ | Close out or referral |

### LinkedIn (linkedin-dm-frameworks.md)

| Touch | When | Rule |
|---|---|---|
| Connection request | Day 1 to 2 (after email day 0) | Empty, no note |
| DM 1 | After accept | One-sentence question about their situation |
| DM 2 | 3 to 5 days after DM 1 | Context + soft offer. No third DM |

| Decision | Answer → leads to |
|---|---|
| Before launch: does `/campaign-qa` pass and does `/inbox-placement-test` show inbox placement? | Yes → ask the user for approval to send (CLAUDE.md: ask before sending). No → fix and retest |
| Prospect has email and LinkedIn? | Both channels, staggered. Email only → email. LinkedIn only → LinkedIn |
| Reply on either channel? | Pause the other channel immediately (linkedin-dm-frameworks.md) |
| Connection not accepted after 2 weeks? | Stop LinkedIn for that person |
| Segment 4 founders (high volume, small companies)? | INFERRED: email only to start; add LinkedIn only if reply rate is low |

LinkedIn volume limit: 20 to 30 connection requests per day per account (linkedin-dm-frameworks.md). Email sends per inbox per day: OPEN.

---

## Step 9: Reply handling

**What happens:** every reply is classified and routed within one business day (INFERRED SLA).

**Tool:** sequencer webhook → n8n → classification (AI step in n8n, human check on anything not obvious) → HubSpot.

| Reply type | Leads to |
|---|---|
| Positive (wants to talk) | HubSpot deal created, owner assigned, task to book within one business day. Stop all sequences for the company |
| Referral ("talk to X") | Add X as contact, new sequence referencing the referrer. Stop the original person |
| Not now / timing | HubSpot status "Nurture", re-enter when a new signal fires |
| Objection: held funds or payouts (personas.md) | Owner replies personally; no templated answer until sales provides one (OPEN) |
| Objection: price (personas.md) | Owner replies with published pricing from research only; no invented discounts |
| Objection: needs more markets or banking and credit (personas.md) | Log reason; disqualify if it matches an icp.md non-fit, else owner replies |
| Already a Paystack user | Mark customer, fix suppression source, count as a data error |
| Not interested | Close, suppress for the window |
| Unsubscribe / stop | Suppress permanently across all channels |
| Out of office | Pause, resume after return date |
| Bounce | Mark email invalid, count against bounce rate |

Data protection: Nigeria's NDPA 2023 and GAID 2025 apply to personal data (research/market.md). Consent basis for cold outreach in each market: OPEN, needs legal review before launch.

---

## Step 10: CRM (HubSpot)

**What happens:** HubSpot is the record; Clay and the sequencer are not. Only rows that pass step 4 and have a verified contact are synced.

**Tool:** HubSpot, synced from Clay and n8n.

| Object | Key | Properties written |
|---|---|---|
| Company | Domain (dedupe key) | Segment, signal ID, signal date, workflow W#, fit result, suppression reason |
| Contact | Email, else LinkedIn URL | Persona, channel, sequence status, reply type |
| Deal | Created on positive reply only | Segment, workflow W#, lead product, source signal |

| Decision | Answer → leads to |
|---|---|
| Company exists? | Update properties; never overwrite owner or lifecycle stage set by sales |
| Contact exists in another active sequence? | Do not enrol twice; log a conflict |
| Deal closes won or lost? | Write the outcome back to the workflow W# so step 11 can score signals by revenue, not just replies |

---

## Step 11: Weekly feedback loop

**What happens:** once a week, read results and change the Context OS. Every change goes in the week's work log.

**Tool:** HubSpot and sequencer reports pulled by n8n into a weekly summary; changes made in this repo.

| Metric (copy-frameworks.md target) | Below target → change |
|---|---|
| Bounce < 3% | Fix email waterfall order or validation (step 7) |
| Open rate 60 to 80% | Fix deliverability or subject lines first; do not touch body copy |
| Reply rate 5 to 15% | Change angle in signal-matrix.md Matrix 1 or the workflow spec |
| Positive reply rate 2 to 8% | Re-score the signal in Matrix 2; consider killing it |
| Unsubscribe < 0.5% | Tighten the fit check (step 4) |

| Decision | Answer → leads to |
|---|---|
| A signal produced no positive replies after enough sends? | Mark KILLED in signal-matrix.md with the reason. "Enough": OPEN |
| A reply revealed a new pain, objection or title? | Add to personas.md with the source (reply, date) |
| A won deal names a customer or quote? | Add to research/customers.md, so it can be used as proof |
| Many companies held with no segment (step 4, check 6)? | Propose a new segment in icp.md |
| An open question got answered? | Move it from Open questions into the body of icp.md or personas.md |
| What worked or failed? | Write it in `knowledge-base/learnings/` |
| Next week's plan | Update `weekly-priorities/` |

---

## Four-pillar check

| Pillar | How the design meets it | Gaps |
|---|---|---|
| **Clean data** | Domain is the single key (step 2). Suppression of customers, open deals, competitors (steps 2, 4). Empty fields stay empty (step 3). Validation before every send, 3% bounce stop (step 7). HubSpot dedupes on domain and email (step 10) | African email coverage unknown. Catch-all handling INFERRED. CBN and LSLGA page dates unclear (signal-matrix.md) |
| **Always-on signals** | Each workflow runs on a cadence set by signal velocity (step 1). Re-entry on new signal, suppression otherwise | Only 4 signals verified for first build. Segment 2 has no strong timing signal. Volumes are INFERRED until the first Clay runs |
| **Composable workflows** | 9 of 16 signals are universal: one Clay build, keyword swaps (signal-matrix.md). Same fit check, routing, people, email and CRM steps for every workflow; only step 1 and the angle change | Sequencer and LinkedIn tool not chosen, so step 8 is not yet wired |
| **Tight feedback loops** | Weekly metric review with a named change per metric. Deal outcomes written back to the workflow. Replies feed personas, wins feed research, kills feed the matrix | No owner named for the weekly review (OPEN). Kill threshold for signals OPEN |

## Open decisions

1. Email sequencer and LinkedIn tool.
2. Suppression window length.
3. Clay credit budget per workflow.
4. Sends per inbox per day; number of sending domains.
5. Legal basis for cold outreach under NDPA and other markets' laws.
6. Owner of the weekly review and of replies.
7. Templated answers to the held-funds and price objections.
8. How many sends before a signal can be killed.
