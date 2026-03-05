# COWORK Protocol

### An Open Standard for Human-Agent Collaborative Software

> MCP solved how agents connect to tools. COWORK solves how agents and humans coordinate through those tools.

---

## The Problem

Every B2B SaaS product is adding AI agents. None of them agree on how those agents should collaborate with humans.

The result: every company reinvents trust models, handoff protocols, permission systems, and feedback loops from scratch. Each implementation is incompatible. The experience is inconsistent. The industry is solving the same problems independently and poorly.

## The Bet

Within 3 years, every B2B SaaS product will need human-agent collaboration. An open protocol that defines the shared primitives — the way OAuth defined authorization or HTTP defined web communication — will become foundational infrastructure.

## The Framework: Three Interaction Zones

Traditional software design assumed one interaction model: **HCI** (Human-Computer Interaction).

Two new zones are emerging:

| Zone | What it covers | Example |
|------|---------------|---------|
| **HCI** | Human-Computer Interaction | How a human uses a CRM dashboard |
| **ACI** | Agent-Computer Interaction | How an AI agent navigates APIs, schemas, and tool interfaces |
| **HAI** | Human-Agent Interaction | How a human and an AI agent collaborate — trust, handoffs, feedback |

COWORK defines the primitives, patterns, and specifications for all three zones.

## Primitives (Draft v0.1)

We've identified **18 primitives across 6 categories**. Each is a draft meant to be challenged and refined.

| Category | Primitives | Core Question |
|----------|-----------|---------------|
| **Trust** | Trust Score, Trust Threshold, Trust Evidence | How does an agent earn and lose autonomy? |
| **Authority** | Action Scope, Delegation Contract, Escalation Trigger | What can an agent do, and under what conditions? |
| **Handoff** | Context Packet, Handoff Mode, Continuity State | How do humans and agents transfer work seamlessly? |
| **Feedback** | Override Signal, Approval Signal, Collaboration Quality Score | How does the system learn from human corrections? |
| **Communication** | Confidence Signal, Reasoning Trace, Intent Declaration | How does an agent express uncertainty and intent? |
| **Observability** | Action Attribution, Collaboration Timeline, Intervention Map | How do you see what happened and who did what? |

📄 **[Full primitives specification →](./docs/primitives.md)**

## How This Fits the Ecosystem

COWORK is complementary, not competitive:

```
┌─────────────────────────────────────────────┐
│           Human-Agent Collaboration          │
│                  COWORK                       │  ← Trust, handoffs, feedback,
│                                               │     authority, communication
├─────────────────────────────────────────────┤
│           Agent-Agent Communication          │
│                   A2A                         │  ← Agent discovery, negotiation,
│                                               │     message passing
├─────────────────────────────────────────────┤
│            Agent-Tool Connectivity           │
│                   MCP                         │  ← Tool schemas, data access,
│                                               │     action execution
├─────────────────────────────────────────────┤
│           Human Authorization                │
│                OAuth / RBAC                   │  ← User roles, permissions,
│                                               │     access control
└─────────────────────────────────────────────┘
```

MCP handles plumbing. A2A handles agent-to-agent. OAuth handles human auth. **COWORK handles the collaboration layer where humans and agents actually work together.**

## Real-World Evidence

These aren't theoretical problems. They're happening in production right now:

- 📄 **[CRM Data Integrity](./examples/crm-data-integrity.md)** — How missing COWORK primitives led to weeks of silent data corruption in HubSpot
- 📄 **[Support Handoff Failures](./examples/support-handoffs.md)** — Why Intercom's Fin achieves ~50% resolution when handoff context is lost
- 📄 **[More examples →](./examples/)**

## Current Phase: Primitives Discovery

We're in **Phase 1** — validating the primitive taxonomy through structured workshops.

| Phase | Goal | Timeline | Status |
|-------|------|----------|--------|
| **1. Primitives Discovery** | Validate primitive taxonomy | 8-10 weeks | 🟢 Active |
| 2. Pattern Definition | Reusable interaction patterns per zone | 10-12 weeks | ⬜ Next |
| 3. Specification Draft | Formal versioned spec | 8 weeks | ⬜ Planned |
| 4. Reference Implementation | Working examples | 12 weeks | ⬜ Planned |
| 5. Adoption & Ecosystem | Real-world pilots | Ongoing | ⬜ Future |

## Contributing

### Quick Start

1. **Read** the [primitives spec](./docs/primitives.md)
2. **Challenge** — open an issue for what's missing, wrong, or redundant
3. **Share** — add your real-world examples to the [examples folder](./examples/)
4. **Join** — attend a workshop ([sign up here](link))

### Who We Need

| Role | What you'd do |
|------|--------------|
| **Designers** | Validate that primitives can be rendered into natural experiences |
| **Product Managers** | Validate that real product teams would adopt this |
| **Engineers** | Validate that primitives are implementable without unreasonable overhead |
| **AI/ML Practitioners** | Validate compatibility with how agents actually work |
| **Domain Experts** | Validate that primitives are universal, not biased to one vertical |

### How to Contribute

See [CONTRIBUTING.md](./CONTRIBUTING.md) for guidelines.

## Background Reading

- [Part 1: Traditional SaaS Is Dead. It Just Doesn't Know It Yet.](link) — Why the architecture needs to change
- [Part 2: The Designer's Role Isn't Dying. It's Splitting Into Three.](link) — The HCI → ACI → HAI evolution
- [Part 3: Your AI Agent Is Silently Destroying Your CRM.](link) — A real-world case study in missing primitives

## License

- Specification: [Apache 2.0](./LICENSE)
- Reference implementations: MIT

---

*This protocol is a living draft. Everything in it is meant to be challenged.*
*If you're reading this, you're invited to shape it.*

**Created by [Kamesh](link-to-linkedin)** · [Twitter](link) · [Substack](link)
