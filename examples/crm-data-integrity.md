# CRM Data Integrity — Silent Corruption at Scale

## Domain

CRM / Revenue Operations

## Product

HubSpot (reported by multiple teams; pattern observed across Salesforce and Pipedrive as well)

## What Happened

A revenue operations team gave their AI agent write access to HubSpot CRM. The agent was tasked with enriching contact records, updating deal stages based on activity signals, and cleaning duplicate entries.

For the first few weeks, everything appeared to work. The team saw faster data updates and fewer manual tasks.

Then the problems surfaced — all at once:

- **Conversion rates dropped** in reports, but pipeline activity hadn't changed
- **Marketing attribution broke** — UTM parameters had been silently overwritten during "enrichment"
- **Duplicate records appeared** — the agent's dedup logic had edge cases that created new duplicates instead of merging
- **Deal stages were incorrect** — the agent moved deals based on activity signals that didn't account for context (e.g., a support email was interpreted as sales engagement)
- **Commission calculations were wrong** — because deal stages feed commission logic, multiple reps were over/underpaid

The damage had been compounding for approximately 3 weeks before anyone noticed. Root cause analysis took longer than the actual cleanup because nobody could tell which changes were made by the agent versus humans.

## Missing Primitives

| Primitive | Was it present? | What went wrong |
|-----------|----------------|-----------------|
| **Intent Declaration** | No | Agent wrote directly to production fields. No staging or proposal layer. |
| **Action Scope** | No | Agent could modify any field on any object. No field-level restrictions or volume caps. |
| **Action Attribution** | No | CRM audit log didn't distinguish human vs. agent changes. Investigation required manual forensics. |
| **Trust Threshold** | No | Agent had full write access from day one. No graduated trust, no earning autonomy through demonstrated accuracy. |
| **Override Signal** | No | When humans manually corrected agent errors, the agent received no feedback. It continued making the same types of mistakes. |
| **Collaboration Timeline** | No | No chronological view of human + agent actions per record. Impossible to reconstruct the sequence of corruption. |

## The Fix

The team built the following workarounds:

1. **Staging properties:** Created `ai_suggested_stage`, `ai_suggested_owner`, and similar fields. Agent writes to staging fields only. Human reviews and promotes to canonical fields.

2. **Batch approval workflow:** A daily workflow surfaces 10-20 agent suggestions for human review. Human approves, modifies, or rejects each one.

3. **Volume alerts:** Slack notification triggers if the agent modifies more than 50 records in an hour.

4. **Field-level restrictions:** Agent blocked from modifying UTM fields, commission-relevant fields, and primary contact identifiers.

5. **Attribution tagging:** Custom property `last_modified_by_agent: true/false` added to track which changes came from the AI.

## Primitives the Fix Accidentally Implemented

| Fix | COWORK Primitive |
|-----|-----------------|
| Staging properties | **Intent Declaration** — agent proposes before acting |
| Batch approval workflow | **Handoff Mode: Review** — agent acts, human validates before commit |
| Human reviewing 10-20 records | **Trust Threshold** — requires human approval below trust level |
| Gradually reviewing fewer records | **Trust Calibration** — trust earned through demonstrated accuracy |
| Volume alerts | **Action Scope** — velocity constraints on agent actions |
| Attribution tagging | **Action Attribution** — tracking who made which change |

## Lessons for the Protocol

1. **Intent Declaration should be the default mode**, not direct action. Agents should propose changes to a staging layer by default. Direct writes should require earned trust.

2. **Action Scope needs volume/velocity constraints**, not just field-level permissions. An agent that can modify one record should not automatically be able to modify 500 without a pause.

3. **Action Attribution must be a first-class system feature**, not a custom workaround. Every system that allows agent writes should natively distinguish human vs. agent vs. collaborative changes.

4. **Trust Thresholds should be contextual per field sensitivity.** Updating a phone number is not the same risk as updating a deal stage. The threshold model needs to account for downstream impact, not just field type.

5. **The feedback loop is critical.** Without Override Signals flowing back to the agent, the system never improves. The team's agent kept making the same mistakes because it never learned from corrections.

6. **Silent failure is the most dangerous failure mode.** The protocol should include observability primitives that surface agent activity patterns proactively — not just when humans go looking.
