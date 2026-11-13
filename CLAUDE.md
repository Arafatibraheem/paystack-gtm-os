# Paystack GTM Context OS

## Company
Paystack (paystack.com): a payment service provider for online and in-person payments for African businesses. Part of The Stack Group (with Paystack Microfinance Bank, Zap and TSG Labs), with Stripe as a shareholder. Live in Nigeria, Ghana, Kenya, South Africa and Côte d'Ivoire, with approvals in Egypt and Rwanda. Source: `context/docs/research/company.md`.

## How this folder works
- `.claude/skills/`: reusable Claude skills for GTM tasks (listed below). Read when a task matches a skill.
- `context/icp/`: ideal customer profiles and segments. Read before any targeting, prospecting or campaign work.
  - `icp.md`: five-layer ICP (firmographic, technographic, intent signals, persona, engagement readiness), non-fits and open questions.
  - `personas.md`: champion, economic buyer and influencer personas.
- `context/positioning/`: positioning, category and competitive differentiation. Read before writing anything that compares or pitches.
- `context/messaging/`: approved messaging, value props and proof points. Read before writing any copy.
- `context/brand-kit/`: voice, tone, visual and naming guidelines. Read before producing any customer-facing asset.
- `context/docs/research/`: raw research and sourced company facts. Read when you need a fact and its source.
- `knowledge-base/playbooks/`: repeatable GTM processes, copy rules and Clay know-how. Read before running a known motion or writing copy.
- `knowledge-base/learnings/`: what worked and what did not. Read before planning a new campaign.
- `meetings/`: meeting notes and decisions. Read when you need recent context or decisions.
- `output/campaigns/`: finished campaign deliverables. Write here; read to reuse past work.
- `tools/`: local tools (Rex for Clay, crawl4ai, agent-browser). Read a tool's README before running it.
- `weekly-priorities/`: one file per ISO week (YYYY-Www.md). Read at the start of every session.
- `work-log/`: one log per ISO week, same name as the priorities file. Append to it after every change.

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
