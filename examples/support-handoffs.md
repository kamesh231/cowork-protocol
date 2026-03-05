# Support Handoff Failures — When Context Gets Lost

## Domain

Customer Support

## Product

Intercom (Fin AI Agent), with similar patterns observed across Zendesk AI and Freshdesk Freddy

## What Happened

A mid-market SaaS company deployed Intercom's Fin AI agent to handle first-line customer support. Fin was configured to resolve queries autonomously using the company's knowledge base, and escalate to human agents when it couldn't resolve.

The resolution rate hovered around 50% — meaning half of all conversations required a human handoff. The handoffs are where things broke down:

**Problem 1: Lost context.** When Fin escalated, the human agent received a conversation transcript but no structured summary of what Fin had already tried, what solutions were offered and rejected, or why Fin decided to escalate. Human agents spent the first 2-3 minutes re-reading the transcript and often asked the customer to repeat information.

**Problem 2: Late escalation.** Fin sometimes continued trying to help long after it should have escalated. It would offer 3-4 irrelevant knowledge base articles while the customer grew frustrated. By the time a human received the conversation, the customer was already angry — not at the original issue, but at the AI interaction.

**Problem 3: Early escalation.** For certain query types, Fin escalated immediately because its confidence was below threshold — even for questions it had successfully resolved hundreds of times before. The confidence model was global, not contextual. Being uncertain about one topic made it cautious about everything.

**Problem 4: No feedback loop.** When human agents resolved escalated tickets, Fin didn't learn from the resolution. The same types of queries continued being escalated at the same rate week after week. Human agents noticed they were answering the same escalated questions repeatedly.

**Problem 5: Invisible attribution.** CSAT scores were reported as a single metric across all tickets. The team couldn't tell whether declining CSAT was caused by Fin's resolutions, Fin's escalation timing, or human agent performance post-escalation. The collaboration had no observability.

## Missing Primitives

| Primitive | Was it present? | What went wrong |
|-----------|----------------|-----------------|
| **Context Packet** | Partial | Transcript was transferred, but no structured summary of actions taken, solutions offered/rejected, or escalation reason. |
| **Escalation Trigger** | Basic | Binary: resolve or escalate. No graduated modes (flag but continue, pause and ask, hard stop). |
| **Trust Score** | No | Fin's confidence model was global, not per-topic. High accuracy on billing questions didn't earn trust for billing queries specifically. |
| **Trust Threshold** | Partial | Single threshold for all query types. No contextual thresholds per domain. |
| **Override Signal** | No | Human resolutions didn't feed back into Fin's learning. Same escalation patterns persisted. |
| **Confidence Signal** | No | Fin didn't communicate its uncertainty level to the customer or the human agent. Humans couldn't tell if Fin was "almost there" or "completely lost." |
| **Action Attribution** | No | CSAT wasn't segmented by actor (Fin-resolved vs. Fin-escalated-then-human-resolved). Collaboration quality was invisible. |
| **Collaboration Quality Score** | No | No meta-metric tracking how well Fin + humans were working together. Only individual metrics (resolution rate, CSAT). |

## The Fix

The team built several workarounds over 3 months:

1. **Structured escalation notes:** Custom workflow that generates a summary when Fin escalates: query type, articles offered, customer sentiment, and reason for escalation.

2. **Topic-specific confidence tuning:** Manually adjusted Fin's confidence thresholds per topic category (billing, technical, account management) instead of using a single global threshold.

3. **Escalation speed alerts:** Monitoring for conversations where Fin took more than 4 turns before escalating — flagged as "late escalation" for review.

4. **Split CSAT reporting:** Built a custom dashboard segmenting CSAT by: Fin-only resolution, Fin-escalated-quick-handoff, and Fin-escalated-delayed-handoff.

5. **Weekly "Fin learning" review:** Manual process where a support lead reviews the top 20 escalated queries and updates the knowledge base. Not automated, but creates a partial feedback loop.

## Primitives the Fix Accidentally Implemented

| Fix | COWORK Primitive |
|-----|-----------------|
| Structured escalation notes | **Context Packet** — what travels with the handoff |
| Topic-specific confidence | **Trust Score** (contextual) — per-domain trust levels |
| Escalation speed alerts | **Escalation Trigger** (graduated) — detecting late escalation |
| Split CSAT reporting | **Action Attribution** + **Collaboration Quality Score** |
| Weekly learning review | **Override Signal** (manual, batch) — human feedback reaching the system |

## Lessons for the Protocol

1. **Context Packets need to be structured, not just transcripts.** A wall of text is not context. The handoff needs: what was tried, what was rejected, customer sentiment, escalation reason, and suggested next steps — all in a parseable format.

2. **Trust must be contextual.** A support agent who's great at billing questions shouldn't be distrusted for billing queries just because it struggles with technical issues. Per-domain trust scores are essential.

3. **Escalation Trigger needs graduated modes.** Binary escalation (handle it / give up) creates both late and early escalation failures. The protocol should define: flag-but-continue, pause-and-ask, and hard-stop as distinct modes.

4. **Confidence Signal should be visible to the human.** When a human receives an escalation, they should see the agent's confidence level and reasoning — not just the conversation. "Fin was 30% confident and escalated after 2 failed article suggestions" is far more useful than a raw transcript.

5. **Collaboration Quality Score is a missing metric.** Individual metrics (resolution rate, CSAT, handle time) don't capture how well the human-agent collaboration is functioning. A meta-metric that tracks handoff quality, escalation timing, and feedback loop effectiveness is needed.

6. **The feedback loop must be automated, not manual.** A weekly review process where a human updates the knowledge base is a band-aid. Override Signals should automatically surface patterns (e.g., "these 5 query types are escalated 80% of the time — here's what human agents do differently") and feed back into agent behavior.
