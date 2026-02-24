---
name: tl-planning
description: >
  TODO - Skill description to be written.
---

# Planning

TODO - Skill content to be written following SKILL-TEMPLATE.md.

## Notes for when this skill is built

### Establish principles and decision criteria per initiative

Every initiative should start by defining the principles and goals that future
technical decisions will be measured against. Without these, disagreements during
delivery become opinion vs opinion with no shared yardstick.

The principles must be scoped to the initiative's ambition:

- **Strategic initiative** (e.g. building a universal data model to represent a
  user across all systems): principles should reflect that — flexibility,
  extensibility, designed for the next consumer, not just the current one.
- **Tactical initiative** (e.g. adding an email field to an existing user model):
  principles should match — ship it, keep it simple, don't over-engineer for a
  future that isn't in scope.

If the principles don't match the ambition of the work, they'll either
over-constrain simple changes or under-protect important ones.

These principles feed directly into tl-conflict-resolution — when technical
disagreements arise, the first question that skill asks is "does the team have
established principles to measure this decision against?" If planning did its
job, the answer is yes and the conflict is half-resolved already.
