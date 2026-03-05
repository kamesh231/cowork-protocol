# Contributing to COWORK Protocol

Thank you for your interest in shaping the future of human-agent collaboration. This protocol is built by the community, and every perspective matters.

## How You Can Contribute

### 1. Challenge the Primitives

The most valuable contribution right now is **critical feedback** on the [primitives spec](./docs/Primitives.md). We'd rather hear "this is wrong" than "this looks good."

- Open an issue with the label `primitive-feedback`
- Tell us which primitive you're challenging and why
- Share real-world examples from your own product experience

### 2. Share Real-World Examples

Have you experienced human-agent collaboration breaking in production? Those stories are gold.

- Add your example to the `examples/` folder via a PR
- Follow the template in [examples/TEMPLATE.md](./examples/TEMPLATE.md)
- The messier and more honest, the better — we learn from failures, not polish

### 3. Propose New Primitives

Think we're missing something? Propose it.

- Open an issue with the label `new-primitive`
- Include: definition, why it matters, what breaks without it, and at least one real-world signal
- The community will discuss and decide whether to include it

### 4. Join a Workshop

We run 90-minute structured workshops on each primitive category. These are where the real refinement happens.

- Check [GitHub Discussions](../../discussions) for upcoming workshop dates
- Workshops are cross-functional: we need designers, PMs, engineers, and domain experts in every session

### 5. Write an RFC

For substantial changes or additions, write a formal RFC.

- Copy the template from `rfcs/000-template.md`
- Submit as a PR
- RFCs are discussed for at least 2 weeks before any decision

## Contribution Guidelines

### Issues

- **One issue per topic.** Don't combine multiple primitive challenges into one issue.
- **Be specific.** "Trust Score feels wrong" is less useful than "Trust Score should be contextual per task type because [real example]."
- **Reference real products** where possible. Abstract feedback is harder to act on.

### Pull Requests

- Keep PRs focused. One change per PR.
- For spec changes: explain what you're changing and why in the PR description.
- For examples: follow the template in `examples/TEMPLATE.md`.

### Discussion Etiquette

- Assume good intent. People come from different domains and will use different vocabulary.
- Disagree with ideas, not people.
- "I've seen this break in production at [company/domain]" carries more weight than "I think this should be different."

## Decision Making

We use a **rough consensus model**:

- Minor changes (typos, clarifications): Merged by maintainers
- Moderate changes (primitive refinements): Require discussion + at least 2 approvals from different roles (designer + PM, or PM + engineer, etc.)
- Major changes (new primitives, structural changes): Require RFC + workshop discussion + 3 approvals from 3 different role types

No single company or individual has veto power.

## Labels

| Label | Use for |
|-------|---------|
| `primitive-feedback` | Challenging or refining an existing primitive |
| `new-primitive` | Proposing a new primitive |
| `real-world-example` | Sharing a production experience |
| `question` | Asking for clarification |
| `workshop` | Related to workshop planning or output |
| `rfc` | Formal proposal for substantial changes |
| `good-first-issue` | Good for newcomers to the project |

## Code of Conduct

We follow the [Contributor Covenant](./CODE_OF_CONDUCT.md). Be respectful, be constructive, be specific.

---

*Questions? Open a discussion or reach out to [@kamesh231](https://github.com/kamesh231).*
