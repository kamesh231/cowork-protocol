# Example Template

Use this template when adding a new real-world example to the `examples/` folder.

---

## Title

<!-- Short, descriptive title -->

## Domain

<!-- e.g., CRM, Customer Support, Project Management, Content, IT Operations, Sales -->

## Product

<!-- Name the product if possible. "Anonymous B2B SaaS" is fine if you can't. -->

## What Happened

<!-- Tell the story. What was the agent doing? What went wrong? How did humans discover the problem? What was the impact? -->

## Missing Primitives

<!-- Map the failure to specific COWORK primitives. Use this format: -->

| Primitive | Was it present? | What went wrong |
|-----------|----------------|-----------------|
| Intent Declaration | No | Agent wrote to production fields directly |
| Action Scope | Partial | No volume caps existed |
| ... | ... | ... |

## The Fix

<!-- What did the team build to solve it? Staging fields? Approval workflows? Custom dashboards? -->

## Primitives the Fix Accidentally Implemented

<!-- Map the fix back to COWORK primitives. Often teams build primitives without naming them. -->

## Lessons for the Protocol

<!-- What should the COWORK spec learn from this example? Any new primitives needed? Any existing primitives that should be refined? -->
