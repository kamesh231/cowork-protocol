# COWORK Protocol

### An Open Standard for Human-Agent Collaborative Software

> MCP solved how agents connect to tools. COWORK solves how agents and humans coordinate through those tools.

---

## The Problem

Every B2B SaaS product is adding AI agents. None of them agree on how those agents should collaborate with humans.

The result: every company reinvents trust models, handoff protocols, permission systems, and feedback loops from scratch. Each implementation is incompatible. The experience is inconsistent. The industry is solving the same problems independently and poorly.

## The Bet

Within 3 years, every B2B SaaS product will need human-agent collaboration. An open protocol that defines the shared primitives — the way HTTP defined web communication or OAuth defined authorization — will become foundational infrastructure.

## The Framework: Three Interaction Zones

Traditional software design assumed one interaction model: **HCI** (Human-Computer Interaction).

Two new zones are emerging:

- **ACI** (Agent-Computer Interaction) — How AI agents navigate, act, and operate inside software
- **HAI** (Human-Agent Interaction) — How humans and agents collaborate: trust, handoffs, feedback, shared context

COWORK defines the primitives, patterns, and specifications for all three zones.

## Primitives (Draft v0.1)

We've identified six primitive categories with 18 primitives total. Each is a draft meant to be challenged and refined.

| Category | Primitives |
|----------|-----------|
| **Trust** | Trust Score, Trust Threshold, Trust Evidence |
| **Authority** | Action Scope, Delegation Contract, Escalation Trigger |
| **Handoff** | Context Packet, Handoff Mode, Continuity State |
| **Feedback** | Override Signal, Approval Signal, Collaboration Quality Score |
| **Communication** | Confidence Signal, Reasoning Trace, Intent Declaration |
| **Observability** | Action Attribution, Collaboration Timeline, Intervention Map |

📄 **[Full primitives specification →](./docs/primitives.md)**

## Why Not Just Use MCP / A2A?

COWORK is complementary, not competitive:

| Protocol | What it solves |
|----------|---------------|
| **MCP** (Anthropic) | How agents connect to tools |
| **A2A** (Google) | How agents communicate with other agents |
| **OAuth / RBAC** | How humans get permissions |
| **COWORK** | How agents and humans coordinate through shared workflows |

MCP handles plumbing. A2A handles agent-to-agent. COWORK handles the collaboration layer where humans and agents actually work together.

## Current Phase: Primitives Discovery

We're in Phase 1 — validating, challenging, and refining the primitive taxonomy through structured workshops with designers, PMs, engineers, and AI practitioners.

### How to Contribute

1. **Read the [primitives spec](./docs/primitives.md)** and open issues for what's missing, wrong, or redundant
2. **Join the discussion** in [GitHub Discussions](../../discussions)
3. **Attend a workshop** — we're running 90-min sessions on each primitive category
4. **Share real-world examples** — where have you seen human-agent collaboration break in production?

### Who We Need

- **Designers** — Can these primitives be rendered into natural experiences?
- **Product Managers** — Will real product teams actually adopt this?
- **Engineers / Architects** — Can these be implemented without unreasonable overhead?
- **AI/ML Practitioners** — Are these compatible with how agents actually work?
- **Domain Experts** — Are the primitives universal or accidentally biased toward one vertical?

## Roadmap

| Phase | Goal | Timeline |
|-------|------|----------|
| 1. Primitives Discovery | Validate primitive taxonomy | 8-10 weeks |
| 2. Pattern Definition | Reusable interaction patterns per zone | 10-12 weeks |
| 3. Specification Draft | Formal versioned spec (JSON Schema / Protobuf) | 8 weeks |
| 4. Reference Implementation | Working examples for common SaaS patterns | 12 weeks |
| 5. Adoption & Ecosystem | Real-world pilots + community growth | Ongoing |

## Background Reading

- [Traditional SaaS Is Dead. It Just Doesn't Know It Yet.](link-to-substack-part-1) — Why the architecture needs to change
- [The Designer's Role Isn't Dying. It's Splitting Into Three.](link-to-substack-part-2) — The HCI → ACI → HAI framework

## License

- Specification: Apache 2.0
- Reference implementations: MIT

---

*This protocol is a living draft. Everything in it is meant to be challenged. If you're reading this, you're invited to shape it.*

**Created by [Kamesh](link-to-linkedin)** · Contributions welcome
