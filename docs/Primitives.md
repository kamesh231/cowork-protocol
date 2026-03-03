# **COWORK Protocol**

### **An Open Standard for Human-Agent Collaborative Software**

**Status:** Primitives Discovery Phase   
**Author:** Kamesh (initiator)   
**Version:** 0.1 — Draft for collaborator review

---

## **1\. Why This Exists**

Every SaaS product today was designed for a single interaction model: humans operating software. As AI agents become active participants in workflows — not just tools, but co-workers — the software layer needs a new foundational design language.

MCP (Model Context Protocol) solved the connectivity problem: how agents talk to tools. What's missing is the **collaboration problem**: how agents and humans coordinate, build trust, hand off work, and learn from each other inside a shared system.

COWORK Protocol aims to define the primitives, patterns, and specifications that any product team can adopt to make their software agent-native — whether they're retrofitting existing products or building from scratch.

This isn't a product. It's infrastructure for a new design paradigm.

---

## **2\. The Three Interaction Zones**

The protocol addresses three distinct but interconnected zones:

**HCI (Human-Computer Interaction)** — How humans interact with software in the presence of agents. Existing zone, but requires evolution: situational awareness, agent state visibility, intervention surfaces.

**ACI (Agent-Computer Interaction)** — How agents interact with software systems. The "UX for agents": tool schemas, permission boundaries, error handling, action scoping.

**HAI (Human-Agent Interaction)** — How humans and agents collaborate directly. Trust calibration, handoff protocols, communication bridging, feedback loops.

The protocol defines primitives for each zone and the connective tissue between them.

---

## **3\. Identifying the Primitives**

Before building anything, we need to agree on the atomic building blocks. These are the irreducible concepts that every human-agent collaborative system needs — regardless of domain, product, or tech stack.

Below is a proposed starting taxonomy. This is explicitly a draft meant to be challenged, expanded, and refined by the collaborator community.

---

### **3.1 — Trust Primitives**

Trust is the foundational layer. Without it, no collaboration model works.

**Trust Score** A dynamic, contextual measure of how much authority an agent has earned in a specific domain. Not a single number — a multi-dimensional profile.

Key questions for collaborators:

* Should trust be global (agent-level) or contextual (per task type, per domain)?  
* How does trust degrade? Time decay? Failure events? Human overrides?  
* Is trust visible to the human, the agent, or both?

**Trust Threshold** The minimum trust level required for an agent to act autonomously vs. requiring human approval. Different actions have different thresholds.

Key questions:

* Who sets thresholds — the product, the team, or the individual user?  
* Should thresholds be static (configured) or adaptive (learned)?  
* How do you prevent threshold fatigue (everything requiring approval)?

**Trust Evidence** The artifacts that justify an agent's trust score — past actions, success rates, override history, human feedback signals.

Key questions:

* What counts as positive vs. negative evidence?  
* How is evidence surfaced without overwhelming the human?  
* Can agents present their own evidence ("here's why I'm confident")?

---

### **3.2 — Authority Primitives**

Authority defines what an agent is allowed to do and under what conditions.

**Action Scope** The bounded set of actions an agent can take within a given context. Not a flat permission list — a contextual, conditional authority model.

Key questions:

* How do scopes compose? (Agent can send emails AND access CRM, but can it use CRM data in emails?)  
* Are scopes granted by role, by task, or by trust level?  
* How are scope violations handled — silent failure, escalation, or logging?

**Delegation Contract** An explicit agreement between a human and an agent about what's delegated, under what constraints, and for how long. The "job description" for the agent.

Key questions:

* Should contracts be formal (configured) or emergent (learned from behavior)?  
* Can contracts be renegotiated mid-task?  
* How are conflicting contracts resolved (two humans delegate contradictory instructions)?

**Escalation Trigger** The conditions under which an agent must stop acting and involve a human. The "I need help" signal.

Key questions:

* Who defines escalation conditions — the agent, the human, or the system?  
* Is escalation binary (stop/continue) or graduated (flag but continue, pause and wait, hard stop)?  
* How do you prevent over-escalation (agent becomes useless) vs. under-escalation (agent acts beyond its competence)?

---

### **3.3 — Handoff Primitives**

Handoffs are the transitions between human and agent action. The most fragile point in any collaboration.

**Context Packet** The structured bundle of information transferred during a handoff. When an agent escalates to a human (or vice versa), what travels with the handoff?

Key questions:

* What's the minimum viable context for a handoff?  
* How do you prevent context overload (agent dumps everything it knows)?  
* Should context packets be standardized across tools or domain-specific?

**Handoff Mode** The type of transition occurring. Not all handoffs are the same.

Proposed modes:

* **Escalate** — Agent can't proceed, human takes over  
* **Delegate** — Human assigns task to agent  
* **Collaborate** — Both working simultaneously, need coordination  
* **Review** — Agent completed work, human validates before commit  
* **Takeover** — Human overrides agent mid-action

Key questions:

* Are these modes sufficient? What's missing?  
* Should the mode be declared explicitly or inferred from behavior?  
* How does the receiving party (human or agent) acknowledge the handoff?

**Continuity State** The mechanism that ensures no work is lost or duplicated during a handoff. The "save point" of collaboration.

Key questions:

* How granular should state capture be?  
* Can both parties see the continuity state?  
* What happens when a handoff fails (human doesn't respond, agent times out)?

---

### **3.4 — Feedback Primitives**

Feedback is how the collaboration gets smarter over time. Without it, the system is static.

**Override Signal** When a human changes an agent's decision, that's a learning signal. But it needs structure to be useful.

Key questions:

* Should overrides include a reason (structured or freeform)?  
* How do you distinguish "agent was wrong" from "human has different preference"?  
* Does the agent see the override in real time or in batch?

**Approval Signal** The inverse of override — human confirms the agent's action was correct. Equally important for learning.

Key questions:

* Should approval be explicit (human clicks approve) or implicit (human doesn't intervene)?  
* How do you avoid approval fatigue?  
* Does implicit approval carry the same weight as explicit?

**Collaboration Quality Score** A meta-metric that tracks how well the human-agent collaboration is functioning over time. Not agent performance — collaboration performance.

Key questions:

* What inputs feed this score? Override rate? Resolution speed? Human satisfaction?  
* Who sees this metric — the human, the agent, the admin?  
* Can this score trigger system-level changes (auto-adjust trust thresholds)?

---

### **3.5 — Communication Primitives**

How humans and agents exchange information within the collaboration.

**Confidence Signal** How an agent communicates its certainty level about a decision or action. The agent equivalent of "I'm pretty sure, but you might want to check."

Key questions:

* Numeric score vs. categorical (high/medium/low) vs. natural language?  
* Should confidence be shown proactively or only when asked?  
* How do you calibrate confidence so it's actually meaningful (not always "high")?

**Reasoning Trace** A human-readable explanation of why the agent made a specific decision. Not a debug log — a narrative.

Key questions:

* How detailed should traces be by default?  
* Should traces be layered (summary → detail → full chain)?  
* Are traces generated in real time or reconstructed after the fact?

**Intent Declaration** Before acting, the agent states what it intends to do and why. The "I'm about to..." signal.

Key questions:

* When is intent declaration required vs. optional?  
* Should the human be able to modify intent before execution?  
* How does intent declaration differ from asking for permission?

---

### **3.6 — Observability Primitives**

How the system makes human-agent collaboration visible and debuggable.

**Action Attribution** Every action in the system is tagged with who did it — human, agent, or collaborative (both involved).

Key questions:

* How do you attribute actions that were agent-drafted and human-approved?  
* Should attribution be visible in the UI or only in audit logs?  
* How does attribution interact with accountability (who's responsible when things go wrong)?

**Collaboration Timeline** A chronological view of all human and agent actions within a shared workflow. The "story" of the collaboration.

Key questions:

* How granular should the timeline be?  
* Should it show agent "thinking" or only final actions?  
* Can timelines be replayed for training or debugging?

**Intervention Map** A visual or structured representation of where humans typically intervene in agent workflows. The pattern recognition layer.

Key questions:

* How is this data collected without being invasive?  
* Can intervention maps drive automatic trust adjustments?  
* Should agents have access to their own intervention maps?

---

## **4\. What's Explicitly Not in Scope (Yet)**

The protocol focuses on collaboration primitives. The following are adjacent but intentionally excluded from the initial scope to keep the effort focused:

* **Agent intelligence / capability** — How smart the agent is. That's an AI/ML problem, not a protocol problem.  
* **Agent-to-agent coordination** — Multi-agent orchestration is a valid future scope but adds massive complexity.  
* **Domain-specific workflows** — The protocol should be domain-agnostic. Vertical implementations come from adopters.  
* **Specific UI implementations** — The protocol defines what needs to exist, not what it looks like. Reference implementations come later.

---

## **5\. Collaboration Model: How We Build This Together**

This protocol cannot be designed by one person or one company. It needs perspectives from across the product, design, and engineering landscape. Here's the proposed collaboration structure.

---

### **5.1 — Who We Need at the Table**

**Designers (UX/Product)** They understand interaction patterns, mental models, and the human side of collaboration. They'll pressure-test whether the primitives are designable — can they actually be rendered into experiences that feel natural?

**Product Managers** They understand customer workflows, business constraints, and adoption friction. They'll pressure-test whether the primitives are adoptable — will real product teams actually use this?

**Engineering Leaders / Architects** They understand systems design, protocol specifications, and integration complexity. They'll pressure-test whether the primitives are implementable — can they be built without unreasonable overhead?

**AI/ML Practitioners** They understand agent capabilities, limitations, and learning dynamics. They'll pressure-test whether the primitives are compatible with how agents actually work today and where they're heading.

**Domain Experts (vertical SaaS leaders)** They understand specific workflows in healthcare, fintech, support, sales, etc. They'll pressure-test whether the primitives are universal or accidentally biased toward one domain.

---

### **5.2 — Collaboration Phases**

**Phase 1: Primitives Discovery (Current Phase)** Goal: Validate, challenge, and refine the primitive taxonomy above.

Activities:

* Publish this document as an open RFC (Request for Comments)  
* Host 4-6 structured workshops with cross-functional collaborators  
* Each workshop focuses on one primitive category (Trust, Authority, Handoff, Feedback, Communication, Observability)  
* Output: Finalized primitive taxonomy with definitions, relationships, and open questions resolved

Timeline: 8-10 weeks

**Phase 2: Pattern Definition** Goal: Define reusable interaction patterns built on the validated primitives.

Activities:

* Working groups per zone (HCI patterns, ACI patterns, HAI patterns)  
* Each group documents 5-10 canonical patterns with examples  
* Cross-group review to ensure patterns compose well across zones  
* Output: Pattern library with visual references and protocol specifications

Timeline: 10-12 weeks

**Phase 3: Specification Draft** Goal: Formalize the protocol into a versioned specification.

Activities:

* Technical writing sprint to convert patterns into spec language  
* Schema definitions for each primitive (JSON Schema / Protocol Buffers)  
* Compatibility mapping with existing standards (MCP, OpenAPI, OAuth scopes)  
* Output: COWORK Protocol v0.1 specification document

Timeline: 8 weeks

**Phase 4: Reference Implementation** Goal: Build a working reference implementation that demonstrates the protocol.

Activities:

* Pick 2-3 common SaaS patterns (support ticket routing, CRM update, content approval)  
* Build reference implementations using the protocol primitives  
* Open-source the reference code with documentation  
* Output: GitHub repo with working examples, SDK scaffolding, and contributor guide

Timeline: 12 weeks

**Phase 5: Adoption and Ecosystem** Goal: Drive real-world adoption and community growth.

Activities:

* Launch at a relevant conference or through major tech publications  
* Partner with 3-5 SaaS companies for pilot adoption  
* Establish governance model for protocol evolution  
* Output: Live production implementations and growing contributor base

Timeline: Ongoing

---

### **5.3 — Workshop Structure for Phase 1**

Each workshop follows the same format to keep output consistent:

**Duration:** 90 minutes

**Format:**

* 10 min — Context setting (the three zones, why primitives matter)  
* 15 min — Present proposed primitives for this category  
* 30 min — Structured critique (what's missing, what's wrong, what's redundant)  
* 20 min — Real-world stress testing (apply primitives to participants' actual products)  
* 15 min — Synthesis and action items

**Output per workshop:**

* Validated / revised primitive definitions  
* New primitives identified  
* Open questions documented  
* Real-world examples captured

**Participant mix per workshop:** 2-3 designers, 2-3 PMs, 1-2 engineers, 1-2 domain experts (8-10 people max for productive discussion)

---

### **5.4 — Governance and Contribution Model**

**Open RFC model:** All primitives and patterns are published as RFCs. Anyone can comment, propose changes, or submit new primitives.

**Working groups:** Self-organized groups around each zone (HCI, ACI, HAI) and each primitive category. Working groups meet bi-weekly and report monthly.

**Decision making:** Rough consensus model. Major changes require input from at least 3 different role types (designer \+ PM \+ engineer minimum). No single company or individual has veto power.

**Licensing:** Apache 2.0 for the specification, MIT for reference implementations. Maximum adoption, minimum friction.

---

## **6\. How This Connects to the Broader Ecosystem**

The protocol is designed to complement, not compete with, existing standards:

**MCP (Model Context Protocol)** — Defines how agents connect to tools. COWORK defines how agents and humans collaborate through those tools. MCP handles the plumbing. COWORK handles the coordination.

**OAuth / RBAC** — Existing permission models for humans. COWORK extends these concepts to agent authority with trust-based, contextual scoping.

**OpenAPI / Tool Schemas** — Existing standards for API descriptions. COWORK adds a collaboration layer on top: intent declaration, confidence signals, and escalation triggers embedded in tool interactions.

**A2A (Agent-to-Agent Protocol by Google)** — Defines how agents communicate with other agents. COWORK focuses on the human-agent boundary. The two protocols could compose: A2A for multi-agent coordination, COWORK for the human collaboration layer.

---

## **7\. Immediate Next Steps**

1. **Circulate this document** to 15-20 people across design, product, engineering, and AI who are thinking about this space. Not as a finished proposal — as a conversation starter.

2. **Recruit 3-5 co-authors** who want to actively shape the primitives. Ideal profile: people who have built products where humans and AI interact and have felt the pain of there being no standard.

3. **Schedule the first workshop** focused on Trust Primitives. Trust is foundational — if we get this right, everything else builds on it. If we get it wrong, nothing else matters.

4. **Set up the open infrastructure:** GitHub repo for the spec, a Discord or Slack for async collaboration, and a lightweight website explaining the vision.

5. **Write a public launch post** (LinkedIn \+ Substack) announcing the initiative and inviting collaborators. Position it as: "We're not building a product. We're defining a language for how humans and agents work together."

---

## **8\. The Bet We're Making**

The bet is this: within 3 years, every B2B SaaS product will need to support human-agent collaboration. Most will try to figure it out independently and poorly. An open protocol that defines the shared primitives — the way HTTP defined web communication or OAuth defined authorization — will become foundational infrastructure.

We're not early because the technology isn't ready. We're early because the vocabulary doesn't exist yet.

This is a language problem before it's a technology problem. Define the primitives. Build the language. The protocol follows.

---

*This document is a living draft. Everything in it is meant to be challenged. If you're reading this, you're invited to shape it.*

