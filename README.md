# Software Delivery Skills

A personal AI skills repository structured around software delivery disciplines. Strictly software delivery focused - no education, VET, or training content.

## Design Principles

1. **Each skill is self-contained** - it should work without needing to read other skills
2. **Skills capture Hilary's specific approach** - not generic best practice. The value is in codifying how she thinks and operates
3. **Skills are conversational first** - they guide Claude's behaviour in dialogue, not just document generation
4. **The five core capabilities are interpreted per discipline** - an architect retro is fundamentally different from a developer retro
5. **Shared skills are genuinely cross-cutting** - if it only applies to one discipline, it belongs there
6. **Security is always adversarial** - the sec- skills should always ask "how do we not end up on the news?"
7. **No education content** - this repo is strictly software delivery

## Disciplines

| Prefix | Discipline | Mindset / Focus |
|---|---|---|
| `sa-` | Solution Architect | Business-aligned, abstract, cross-system |
| `swa-` | Software Architect | Technical design, NFRs, patterns, system design |
| `pm-` | Product Manager | Discovery, roadmapping, prioritisation, backlog |
| `dl-` | Delivery Lead | Work decomposition, sprint flow, WIP management |
| `em-` | Engineering Manager | People, team health, capacity, coaching |
| `tl-` | Tech Lead | Team technical standards, PR culture, quality gates |
| `dev-` | Developer | Hands-on building, estimation, debugging |
| `qa-` | Quality Assurance | Test strategy, defect triage, quality metrics |
| `ops-` | DevOps / Platform | CI/CD, infrastructure, observability, incident response |
| `sec-` | Security | PCI compliance, PII handling, threat modelling, access control |
| `da-` | Data & Analytics | Data modelling, event schemas, reporting pipelines |
| `shared-` | Shared | Communication, documentation, facilitation |

## Core Capabilities

Every discipline (except shared) has five core skill folders covering the same capabilities, interpreted through that discipline's lens:

| Capability | What It Covers |
|---|---|
| `planning` | Upfront thinking, strategy, scoping, estimation, roadmapping |
| `delivery` | Execution, standards, flow, shipping, day-to-day output |
| `problem-solving` | Diagnosis, unblocking, triage, constraint navigation |
| `retro` | Review, reflection, metrics analysis, learning, improvement |
| `conflict-resolution` | Disagreements, alignment, negotiation, difficult conversations |

## Writing New Skills

Use `SKILL-TEMPLATE.md` as the starting point for any new skill. Every SKILL.md follows the same structure: YAML frontmatter, intro, trigger conditions, steps, and quality indicators.
