# Real-World Examples

These are documented cases where human-agent collaboration broke (or worked) in production. Each example maps the experience to specific COWORK primitives.

## Why Examples Matter

The COWORK Protocol isn't built from theory. It's built from production pain. Every primitive in the spec should be traceable to a real-world failure that it would have prevented.

## Current Examples

| Example | Domain | Key Missing Primitives |
|---------|--------|----------------------|
| [CRM Data Integrity](./crm-data-integrity.md) | CRM / RevOps | Intent Declaration, Action Scope, Action Attribution, Trust Threshold |
| [Support Handoff Failures](./support-handoffs.md) | Customer Support | Context Packet, Escalation Trigger, Trust Score, Confidence Signal |

## Contributing an Example

We need examples from every domain. If you've experienced human-agent collaboration breaking in production, your story helps build a better protocol.

1. Copy the [TEMPLATE.md](./TEMPLATE.md)
2. Fill in your experience (anonymous examples are fine)
3. Map the failure to COWORK primitives
4. Submit a PR

### Domains We Need Most

- [ ] Project management (Linear, Jira, Asana)
- [ ] Sales automation (Salesforce, HubSpot, Outreach)
- [ ] Content management (Notion, Contentful, WordPress)
- [ ] IT operations (ServiceNow, PagerDuty)
- [ ] Financial operations (billing, forecasting, compliance)
- [ ] HR / recruiting (Greenhouse, Lever, Workday)
- [ ] Code review / DevOps (GitHub Copilot, CI/CD agents)

Your example doesn't need to be polished. Messy, honest production stories are more valuable than clean write-ups.
