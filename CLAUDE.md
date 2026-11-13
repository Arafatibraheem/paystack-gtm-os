# Paystack GTM Context OS

## Company
Paystack (paystack.com): a payment service provider for online and in-person payments for African businesses. Part of The Stack Group (with Paystack Microfinance Bank, Zap and TSG Labs), with Stripe as a shareholder. Live in Nigeria, Ghana, Kenya, South Africa and Côte d'Ivoire, with approvals in Egypt and Rwanda. Source: `context/docs/research/company.md`.

## How this folder works
- Root files:
  - `CLAUDE.md`: this file. Project instructions, read first.
  - `README.md`: what this repo is and how it is laid out.
  - `.gitignore`: keeps `.env`, data exports and local settings out of Git.
  - `.env`: local secrets, never committed (ignored).
- `.claude/skills/`: reusable Claude skills for GTM tasks (listed under Skills below; each skill's own files live in its folder). Read when a task matches a skill.
- `context/icp/`: ideal customer profiles and segments. Read before any targeting, prospecting or campaign work.
  - `icp.md`: five-layer ICP (firmographic, technographic, intent signals, persona, engagement readiness), seven ranked segments, non-fits and open questions.
  - `personas.md`: champion, economic buyer and influencer personas.
  - `signal-matrix.md`: segments x personas angles, scored buying signals, build-first list and workflow tracker (v1, work in progress).
- `context/positioning/`: positioning, category and competitive differentiation. Read before writing anything that compares or pitches. (Empty.)
- `context/messaging/`: approved messaging, value props and proof points. Read before writing any copy. (Empty; `facts.md` still to be created.)
- `context/brand-kit/`: voice, tone, visual and naming guidelines. Read before producing any customer-facing asset. (Empty.)
- `context/docs/`: system and research documents.
  - `gtm-system.md`: end-to-end outbound GTM system design (v1), with tools, decisions and open items.
  - `research/`: raw research and sourced company facts. Read when you need a fact and its source.
    - `company.md`: products, pricing, markets, funding, team, leadership.
    - `customers.md`: named customers, industries, case studies, testimonials.
    - `competitors.md`: competitors and how each positions itself.
    - `market.md`: regulation and market changes by country.
    - `signals.md`: public evidence of buying triggers.
    - `voice.md`: how Paystack describes itself, in its own words.
- `knowledge-base/playbooks/`: repeatable GTM processes, copy rules and Clay know-how. Read before running a known motion or writing copy.
  - `signal-matrix-framework.md`: method for building signal matrices.
  - `workflow-anatomy.md`: workflow layers and the Mother Intent Catalog.
  - `copy-frameworks.md`: copy structure, follow-up stack, metrics targets.
  - `copy-iron-laws.md`: non-negotiable copy rules.
  - `copy-bans.yaml`: banned words and phrases.
  - `linkedin-dm-frameworks.md`: LinkedIn connection requests and DMs.
  - `templates/facts-template.md`: template for `context/messaging/facts.md`.
  - `clay/expert.md`: Clay reference (providers, waterfalls, credits).
  - `clay/actions-data-credits.md`: Clay actions and their credit costs.
  - `clay/formulas.md`: Clay formula patterns.
  - `clay/iron-laws.md`: Clay build rules.
  - `clay/prompts.md`: Clay AI column prompt patterns.
- `knowledge-base/learnings/`: what worked and what did not. Read before planning a new campaign. (Empty.)
- `meetings/`: meeting notes and decisions. Read when you need recent context or decisions. (Empty.)
- `output/campaigns/`: finished campaign deliverables, one folder per workflow (`<slug>/workflow-spec.md`). Write here; read to reuse past work. (Empty; W1 spec in progress.)
- `tools/`: local tools, each with a README. Read a tool's README before running it.
  - `rex/`: drives Clay locally.
  - `crawl4ai/`: crawls web pages into Markdown.
  - `agent-browser/`: browser automation.
- `weekly-priorities/`: one file per ISO week (YYYY-Www.md). Read at the start of every session.
  - `2026-W46.md`: current week.
- `work-log/`: one log per ISO week, same name as the priorities file. Append to it after every change.
  - `2026-W46.md`: current week.

### Skills
- Research to copy, in order: `/campaign-strategy`, `/signal-matrix`, `/build-workflow-spec`, `/campaign-copy`.
- Clay builds: `/build-clay`, `/prompt-builder`, `/campaign-contract`, `/design-clay-table-json`, `/import-clay-table`, `/save-clay-schema`.
- Clay costs and data: `/calculate-costs`, `/workspace-cost-audit`, `/export-tables`.
- QA and deliverability: `/campaign-qa`, `/inbox-placement-test`.
- Research and visuals: `/crawl4ai`, `/agent-browser`, `/miro-gtm-flowchart`.

## Rules
- Cite a source (URL or file path) for every company fact.
- Never invent numbers. If a figure is unknown, say so and flag it.
- No em dashes in any copy. This overrides any skill or playbook.
- Ask before sending or publishing anything.
- Log every change in this week's work log (`work-log/YYYY-Www.md`) with a timestamp.

## Tools
- Clay: list building, enrichment and AI research columns. Driven locally through `tools/rex`.
- HubSpot: CRM, the system of record for contacts, companies and deals.
- n8n: workflow automation connecting the GTM stack.
