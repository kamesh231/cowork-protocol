# RFC-001: Trust Primitives

**Status:** Discussion
**Author:** Kamesh
**Created:** March 2026
**Discussion:** [GitHub Discussions](link)

---

## Summary

This RFC proposes that Trust be treated as the foundational primitive category in the COWORK Protocol. Trust Score, Trust Threshold, and Trust Evidence form the base layer on which Authority, Handoff, and Feedback primitives depend. Without a resolved trust model, no other primitive can function correctly.

## Motivation

Every team that deploys AI agents in production discovers the trust problem independently:

- **Day 1:** Agent gets full access. Team is excited.
- **Week 2:** Agent makes a subtle error nobody catches.
- **Week 4:** Errors compound. Data quality degrades.
- **Week 6:** Team discovers the damage. Pulls agent access entirely.
- **Week 8:** Team manually rebuilds trust by adding staging fields and approval workflows.

This cycle repeats across every domain — CRM, support, project management, content. The pattern is universal. The solutions are always ad-hoc.

The core issue: there's no standard model for how an agent earns trust, how trust is measured, how it degrades after failures, or how it's communicated to the human.

## Proposal

### Trust Score

A multi-dimensional, contextual measure of agent reliability. Not a single number.

**Structure (proposed):**

```
trust_score: {
  agent_id: string,
  domain: string,           // e.g., "crm.deal_stage", "support.billing"
  overall: float,           // 0.0 - 1.0
  dimensions: {
    accuracy: float,        // How often the agent's actions are correct
    consistency: float,     // How predictable the agent's behavior is
    judgment: float,        // How well the agent handles edge cases
  },
  sample_size: int,         // Number of actions this score is based on
  last_updated: timestamp,
  decay_rate: float,        // How fast trust degrades without new evidence
}
```

**Key design decisions to resolve:**
1. Should trust be per-agent, per-agent-per-domain, or per-agent-per-task-type?
2. What's the minimum sample size before a trust score is meaningful?
3. Should trust scores be visible to end users or only to admins?

### Trust Threshold

A configurable boundary that determines what level of trust is required for autonomous action.

**Structure (proposed):**

```
trust_threshold: {
  action_type: string,      // e.g., "write.crm.deal_stage"
  required_trust: float,    // Minimum trust score required
  mode_below_threshold: enum, // "suggest" | "review" | "block"
  mode_above_threshold: enum, // "act" | "act_and_log" | "act_and_notify"
  override: {
    allowed: boolean,
    requires_reason: boolean,
  }
}
```

**Key design decisions to resolve:**
1. Should thresholds auto-adjust based on override patterns?
2. Can individual users set their own thresholds, or is this team/admin level?
3. How do you prevent threshold inflation (everything requiring high trust)?

### Trust Evidence

The artifacts that justify a trust score. Humans need to see why the system trusts (or doesn't trust) the agent at a given level.

**Structure (proposed):**

```
trust_evidence: {
  agent_id: string,
  domain: string,
  evidence_items: [
    {
      type: enum,           // "action" | "override" | "approval" | "escalation"
      timestamp: timestamp,
      description: string,
      outcome: enum,        // "correct" | "incorrect" | "ambiguous"
      human_feedback: string | null,
    }
  ],
  summary: {
    total_actions: int,
    correct_rate: float,
    override_rate: float,
    avg_confidence_when_correct: float,
    avg_confidence_when_incorrect: float,
  }
}
```

## Impact on Existing Primitives

Trust is upstream of everything:

- **Authority** primitives (Action Scope, Delegation Contract) should reference trust scores when determining what an agent can do
- **Handoff** primitives (Escalation Trigger) should use trust thresholds to determine when to escalate
- **Feedback** primitives (Override Signal, Approval Signal) are the primary inputs that update trust scores
- **Communication** primitives (Confidence Signal) should be calibrated against trust evidence

This creates a feedback loop: actions generate evidence → evidence updates trust → trust determines authority → authority scopes actions.

## Open Questions

1. **Cold start problem:** How do you handle trust for a new agent with no history? Default to zero trust (suggest only)? Or inherit trust from a similar agent?
2. **Trust portability:** If an agent earns trust in one organization, does any of that transfer to another? (Probably not, but worth discussing.)
3. **Trust gaming:** Can an agent artificially inflate its trust score by performing many low-risk actions? How do you weight action difficulty?
4. **Cross-domain trust:** If an agent is highly trusted for billing questions, does that give it any trust for technical questions? Should domains be fully independent?

## Alternatives Considered

**Binary trust (on/off):** Rejected because it doesn't match how human trust works. We don't fully trust or fully distrust a new colleague — we calibrate over time.

**Single-score trust:** Rejected because a single number hides too much. An agent might be great at one task type and terrible at another. Multi-dimensional trust surfaces this.

**No trust primitive (just permissions):** Rejected because permissions are static and trust is dynamic. RBAC doesn't capture "this agent used to be reliable but has been getting worse lately."

## Real-World Validation

Test this against:
1. **CRM write access** — Agent updating deal stages in HubSpot/Salesforce
2. **Support ticket resolution** — Agent resolving customer queries in Intercom/Zendesk
3. **Content moderation** — Agent flagging or removing content
4. **Code review** — Agent suggesting code changes in PRs

If the trust primitives work across all four domains without domain-specific modifications, the abstraction is correct.
