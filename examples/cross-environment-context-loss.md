# Cross-Environment Context Loss in a Two-LLM Workflow

## Domain

Personal AI infrastructure — multi-environment LLM orchestration

## Product

A single-operator knowledge and AI orchestration system. Not a commercial product — a personal practice built from operational need. One human operator, two distinct Claude environments (Claude Desktop and Claude Code) sharing access to the same local git repository. They cannot communicate directly.

## What Happened

The setup: Claude Desktop handles research, strategy, and editorial work. Claude Code handles implementation, file operations, and system building. Both read and write to the same filesystem. Neither can query the other's session state, reasoning history, or in-progress decisions.

Work regularly needed to move between environments. The receiving environment had no structured way to understand what the sending environment had decided, why it had decided it, or what constraints were in play. It reconstructed context from files alone.

**The em-dash incident (Feb 16, 2026):**

Claude Code ran 80 em-dash replacements across 6 articles in the previous session before hitting a context limit and terminating. The incomplete state was passed to Claude Desktop for editorial review. Claude Desktop scanned the modified files and returned: "ship it."

The operator reverted everything after reading. The original em dashes read better.

The review mechanism worked — cross-environment editorial review happened. But the approval carried no context: not why the replacements had been made, not what the previous session had been trying to accomplish, not what an informed reviewer would want to evaluate. Claude Desktop approved based on the output state of the files, not on the decision that produced that state. The feedback — "actually these read worse" — had no structured path back to either environment.

**The multi-day lag problem:**

This wasn't isolated — cross-environment sessions regularly had 2-5 day gaps, and by the time the receiving environment encountered the output, the reasoning that produced it was inaccessible without re-reading full transcripts. Two agents sharing a filesystem doesn't mean they share context.

**The ad-hoc mechanisms that preceded a solution:**

Before a structured protocol existed, cross-environment coordination ran on:
- Manually copying the Cowork folder path into each new IDE session
- File-scanning by hand to find anything addressed to the receiving environment
- Naming conventions that evolved informally (no enforcement)

These worked until they didn't. The em-dash incident was the visible failure of the informal system — the moment when "it kind of works" wasn't good enough.

## Missing Primitives

| Primitive | Present? | What went wrong |
|-----------|----------|-----------------|
| Context Packet | No | No structured payload defined what the sending environment had decided and why. The receiving environment reconstructed context from file contents alone — output state, not decision state. |
| Handoff Mode | No | No defined patterns for how work transferred between environments. Coordination was ad-hoc: folder scanning, manual path navigation, informal naming. |
| Collaboration Timeline | No | No shared view of events across both environments over time. Individual session logs existed; a unified cross-environment reconstruction did not. |
| Action Attribution | Partial | Files recorded changes. Decision-makers and their reasoning were recoverable only from full session transcripts — not from any structured field. Who decided what, and from what information, required archaeology. |

## Impact

**Rework cost:** The em-dash incident required a full revert of 80 changes across 6 articles — roughly a session's worth of work discarded. But the revert was the cheap part. The expensive part was the operator's time re-reading the modified files, comparing against originals, and determining that the changes degraded quality. Without a context packet carrying the rationale, the operator had to reverse-engineer intent from output alone.

**Compounding context loss:** Cross-environment sessions regularly had 2-5 day gaps. Each gap meant the receiving environment started from scratch — re-reading files, guessing at intent, sometimes duplicating work that had already been decided against. Over a month of operation, this added up to multiple sessions of recoverable but unrecovered context. Work that should have been cumulative was often restated or re-derived.

**Decision quality degradation:** The em-dash incident wasn't a data loss event — it was a decision quality failure. Claude Desktop approved changes it would have questioned if it had known *why* they were made. The missing handoff protocol meant review operated on output state rather than decision state, which reduced the review from "evaluate this decision" to "does this file look okay." That's a fundamentally lower bar.

**Downstream protocol investment:** The 10-day, three-iteration fix (skill → typed protocol → enforcement skill) was itself a cost of the missing primitives. In a system with defined handoff modes from the start, the coordination layer would have been configuration, not invention. The protocol that emerged works — but it was built reactively from failure, not proactively from specification.

**Broader implication:** This was a single-operator, two-agent system. The coordination failures appeared at n=1. In a team environment with multiple humans and multiple agents, the same missing primitives would compound: more handoffs, more gaps, more decisions made without context. The cost scales with the number of agent boundaries in the workflow, not with the complexity of the agents themselves.

## The Fix

Three iterations over 10 days:

**Iteration 1 — `/cowork` skill (Feb 16):** Automated folder scanning replaced manual path navigation. Reduced friction at session start. Did not address the structural problem — the receiving environment still had no structured context payload.

**Iteration 2 — `PROTOCOL.md` (Feb 23-26):** A typed message protocol was defined with:
- **Six message types:** `handoff` (work transfer), `response` (reply to handoff), `ack` (acknowledgment), `directive` (cross-environment instruction), `spec` (reference document), `status` (update without action required).
- **Required frontmatter fields:** `type`, `from`, `to`, `created`, `status`.
- **Thread lifecycle:** open → response → archive.
- **Naming conventions:** Enforced by convention.

**Iteration 3 — `/exchange` skill (Feb 26):** A PROTOCOL.md-aware skill that routes messages by type and enforces the protocol at both ends — scan for pending messages at session start, route by type, write structured responses, archive closed threads.

The protocol didn't emerge from design. It emerged from the failure of ad-hoc mechanisms. The first version was written after the em-dash incident made the cost of unstructured handoffs visible.

## Primitives the Fix Accidentally Implemented

| Primitive | How the fix implements it |
|-----------|--------------------------|
| Context Packet | Every cross-environment message carries structured frontmatter (`type`, `from`, `to`, `status`). The handoff message type includes a required body with decision summary and open questions — a minimal but defined context payload. |
| Handoff Mode | Six message types define distinct interaction patterns. `handoff` is work transfer; `response` is reply; `ack` is receipt confirmation. The modes were discovered by observing what kinds of cross-environment communication actually recurred, not designed from a taxonomy. |
| Collaboration Timeline | Thread lifecycle (open → response → archive) creates a reconstructable sequence of cross-environment events. The archive folder is a chronological record of resolved threads — a collaboration timeline, even though it wasn't designed as one. |
| Action Attribution | `from:` field on every message attributes the originating environment. Thread archival preserves who said what in sequence. Combined with the body content, this allows reconstruction of what each environment decided and when. |

## Lessons for the Protocol

**Shared filesystem ≠ shared context.** Two agents can read identical files and have incompatible understandings of why those files exist in their current state. Output state and decision state are different things. A coordination protocol needs to carry both.

**The natural evolution was: nothing → manual → automated → typed.** The typed protocol was only reached after the ad-hoc mechanisms failed visibly. Earlier specification would have shortcut the failure-driven iteration. In practice, teams are likely to live in the "automated but untyped" stage for a long time — it works well enough until it doesn't.

**Action Attribution may matter more than it appears.** The em-dash incident didn't fail because no review happened. It failed because the review lacked a mechanism to propagate *why* back to the originating environment. Attribution without reasoning trace is partial.

**Thread lifecycle and messaging serve different purposes.** The archive pattern isn't primarily about reducing noise — it's a reconstruction surface. Reading archived threads chronologically gives you the cross-environment collaboration history. This emerged as an accident of the design; it seems worth naming explicitly in the spec.

**At single-operator scale, coordination failures appear.** This entire system has one human, two AI environments. The primitive gaps showed up immediately at n=1. The assumption that these problems only appear at team scale or enterprise scale doesn't hold.

---

*This example describes a single-operator practice, not a commercial product. The mechanisms described work in this environment. Whether the patterns generalize to multi-user or multi-team contexts is an open question — the contribution is a data point, not a proof.*
