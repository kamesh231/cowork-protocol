# Workshop Facilitation Guide

## Overview

COWORK Protocol workshops are 90-minute structured sessions where cross-functional collaborators validate, challenge, and refine primitive categories. Each workshop focuses on one category.

## Workshop Schedule

| # | Category | Focus | Status |
|---|----------|-------|--------|
| 1 | Trust | Trust Score, Trust Threshold, Trust Evidence | Upcoming |
| 2 | Authority | Action Scope, Delegation Contract, Escalation Trigger | Planned |
| 3 | Handoff | Context Packet, Handoff Mode, Continuity State | Planned |
| 4 | Feedback | Override Signal, Approval Signal, Collaboration Quality Score | Planned |
| 5 | Communication | Confidence Signal, Reasoning Trace, Intent Declaration | Planned |
| 6 | Observability | Action Attribution, Collaboration Timeline, Intervention Map | Planned |

## Format (90 minutes)

### 1. Context Setting (10 min)
- The three interaction zones (HCI, ACI, HAI)
- Why primitives matter — the OAuth analogy
- Where we are in the roadmap

### 2. Present Proposed Primitives (15 min)
- Walk through each primitive in today's category
- Definition, why it matters, real-world signal
- Present the open questions — these are what we're here to resolve

### 3. Structured Critique (30 min)
- Each participant writes 3 reactions (silent, on sticky notes or shared doc):
  - One thing that's **missing**
  - One thing that's **wrong or needs refinement**
  - One thing that's **correct and should be locked**
- Round-robin sharing and discussion
- Facilitator captures themes

### 4. Real-World Stress Test (20 min)
- Each participant applies the primitives to **their actual product**
- Prompt: "If your product implemented these 3 primitives tomorrow, what would change? What would break? What's missing for your domain?"
- Small group discussion (2-3 people per group)
- Groups report back key findings

### 5. Synthesis and Action Items (15 min)
- Facilitator summarizes:
  - Primitives validated (no changes needed)
  - Primitives revised (with specific changes)
  - New primitives proposed
  - Open questions resolved
  - Open questions still unresolved
- Assign owners for follow-up (RFC drafts, example documentation)
- Set date for next workshop

## Participant Mix

Ideal: 8-10 people per workshop

| Role | Count | Why |
|------|-------|-----|
| Designers (UX/Product) | 2-3 | Can primitives be rendered into natural experiences? |
| Product Managers | 2-3 | Will real product teams adopt this? |
| Engineers / Architects | 1-2 | Can primitives be implemented without unreasonable overhead? |
| Domain Experts | 1-2 | Are primitives universal or domain-biased? |

Cross-functional mix is mandatory. A workshop with only PMs or only engineers will produce skewed output.

## Output Template

After each workshop, the facilitator publishes a summary:

```markdown
# Workshop [#] — [Category] Primitives

**Date:** [date]
**Participants:** [count] ([role breakdown])

## Primitives Validated
- [Primitive name]: Confirmed as-is. No changes.

## Primitives Revised
- [Primitive name]: [What changed and why]

## New Primitives Proposed
- [Name]: [Brief definition and rationale]

## Open Questions Resolved
- [Question]: [Resolution and reasoning]

## Open Questions Still Open
- [Question]: [Why it's still open, what's needed to resolve]

## Real-World Examples Captured
- [Domain]: [Brief description of example shared by participant]

## Action Items
- [ ] [Person]: [Action] by [date]
```

## Remote Workshop Setup

- **Tool:** Zoom/Google Meet + shared Miro board or Google Doc
- **Pre-work:** Participants read the relevant primitives section (15 min) before the workshop
- **Recording:** Workshops are recorded but not published. Summaries are published.
- **Time zones:** Rotate workshop times to accommodate global participants

## Ground Rules

1. **No spectators.** Everyone participates. If you're in the room, you have a perspective we need.
2. **Real products over theory.** "In our product, this would..." beats "In theory, this could..."
3. **Disagree with reasons.** "I don't think this works because [experience]" is useful. "I don't like it" is not.
4. **One conversation at a time.** No side channels during discussion.
5. **Output-oriented.** Every workshop produces a published summary. We don't meet to talk — we meet to decide.
