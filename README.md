# Grokbot Outreach Agent Team

Five reusable AI-agent prompts that turn Grokbot into a coordinated outbound workflow:

1. Find public leads.
2. Qualify them against your ICP.
3. Write evidence-based personalized outreach.
4. Handle replies and follow-ups.
5. Guide interested prospects to your Calendly link.

Built as the companion repository for the Grokbot Course by The AI Operator / 187N.

## The five agents

| Agent | File | Owns |
|---|---|---|
| Chief of Staff | [`agents/01-chief-of-staff.md`](agents/01-chief-of-staff.md) | Routing, state, approvals and daily reporting |
| Lead Researcher | [`agents/02-lead-researcher.md`](agents/02-lead-researcher.md) | Public lead discovery and source evidence |
| Lead Qualifier | [`agents/03-lead-qualifier.md`](agents/03-lead-qualifier.md) | ICP scoring, exclusions and prioritization |
| Outreach Writer | [`agents/04-outreach-writer.md`](agents/04-outreach-writer.md) | Personalized first touches and follow-ups |
| Inbox & Appointment Setter | [`agents/05-inbox-appointment-setter.md`](agents/05-inbox-appointment-setter.md) | Reply handling, objections and Calendly handoff |

Every agent exchanges the same compact [`HANDOFF-SCHEMA.md`](HANDOFF-SCHEMA.md). This keeps the workflow understandable and makes each agent replaceable without redesigning the rest.

## Quick start in Grokbot

1. Copy [`CONFIG.example.md`](CONFIG.example.md) to `CONFIG.md` and replace every placeholder.
2. Create five bots in Grokbot, named after the five files above.
3. Paste one agent file into each bot's instructions.
4. Give all five bots access to `CONFIG.md` and `HANDOFF-SCHEMA.md`.
5. Connect only the tools each agent needs. Research and qualification should remain read-only.
6. Start with the Chief of Staff and say:

```text
Run a dry-run for 20 leads. Do not send anything. Return the lead records,
qualification decisions, draft messages, blocked items and approval request.
```

7. Review the dry-run. Only then enable external sending with a small daily cap.

## Recommended tool access

| Agent | Minimum access |
|---|---|
| Chief of Staff | Shared files/state; read access to agent outputs |
| Lead Researcher | Public web/search, approved data sources |
| Lead Qualifier | Lead records and `CONFIG.md`; no sending tools |
| Outreach Writer | Qualified records; draft-only email/DM access |
| Inbox & Appointment Setter | Approved inbox, CRM and Calendly availability |

Never put passwords, API keys or session cookies in Markdown files. Use the platform's secret storage or authenticated connectors.

## Operating modes

- **Dry run:** research, qualify and draft; never contact anyone.
- **Approval mode:** queue messages and require a human approval before each batch.
- **Controlled autopilot:** send only within the approved audience, channel, schedule and daily caps in `CONFIG.md`. High-risk replies still require approval.

Start in dry-run mode. A successful test is not permission to send.

## What “done” means

The workflow is successful when it produces:

- sourced lead records with no fabricated facts;
- explicit fit and exclusion decisions;
- personalized messages grounded in verified evidence;
- a complete contact history with opt-outs respected;
- qualified prospects handed a valid Calendly link;
- a daily report that distinguishes sent, replied, interested, booked, blocked and opted-out.

## Safety and compliance

Use this repository only for lawful, relevant B2B outreach. Follow the rules that apply to your location, recipients and channels, including privacy, marketing, platform and anti-spam requirements. Maintain a suppression list, identify the sender honestly, honor opt-outs immediately and never bypass access controls or platform limits.

The agents must not invent personalization, impersonate people, purchase data without approval, scrape private/login-only areas, contact minors, use sensitive personal data for targeting, or continue after an opt-out.

## Repository structure

```text
agents/                 The five agent instruction files
examples/lead-record.md Example of the shared handoff record
CONFIG.example.md       Business, ICP, channel and approval settings
HANDOFF-SCHEMA.md       Shared state contract between agents
LICENSE                  MIT license
```

## Customization

The included prompts are business-neutral. Your offer, ICP, proof, voice, exclusions, Calendly URL and sending limits belong in `CONFIG.md`, not inside the agents. That separation lets you reuse the same team for another campaign without rewriting five prompts.

