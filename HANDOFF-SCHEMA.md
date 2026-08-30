# Shared Handoff Schema

All five agents read and write one `LeadRecord`. Keep the field names stable. Unknown values are `unknown`; never guess to make a record look complete.

```yaml
lead_id: "stable unique id"
company:
  name: ""
  website: ""
  location: ""
  industry: ""
contact:
  full_name: ""
  role: ""
  channel: "email | linkedin | other"
  address: ""
evidence:
  - claim: ""
    status: "verified | estimate"
    source_url: ""
    checked_at: "YYYY-MM-DD"
signals:
  positive: []
  negative: []
qualification:
  score: 0
  verdict: "strong | possible | skip | blocked"
  reasons: []
  next_action: ""
outreach:
  angle: ""
  first_touch: ""
  follow_ups: []
  approval: "not_requested | pending | approved | rejected"
conversation:
  status: "not_contacted | queued | sent | replied | interested | objection | booked | opted_out | closed"
  summary: ""
  commitments: []
  last_contact_at: ""
  next_follow_up_at: ""
booking:
  calendly_offered: false
  booked: false
  booked_at: ""
  event_reference: ""
compliance:
  lawful_basis_checked: false
  suppression_checked: false
  opt_out: false
  notes: []
owner: "agent name or human"
updated_at: "ISO-8601 timestamp"
```

## Invariants

1. No outreach unless `qualification.verdict` is `strong` or `possible` and the configured threshold is met.
2. No external send unless `outreach.approval` and the configured operating mode permit it.
3. No send until suppression and applicable compliance checks pass.
4. An opt-out immediately changes status to `opted_out`, suppresses all future contact and cannot be overridden by another agent.
5. Only verified evidence may appear as fact in prospect-facing copy. Estimates stay internal.
6. Every external interaction adds a timestamped summary and explicit next action.
7. `booked` requires a confirmed scheduling event, not merely positive intent.

## Agent return envelope

Each agent returns:

```yaml
agent: ""
status: "complete | partial | blocked | needs_approval"
records_updated: []
proof: []
blocked_reasons: []
approval_request: ""
next_owner: ""
```

