# Software Delivery Skills Repo — Setup Brief

## Purpose

This document captures the full design for a personal AI skills repository structured around software delivery disciplines. It is intended as a handoff to continue building in Cowork with filesystem access.

The repo is **strictly software delivery focused** — no education, VET, or training content.

---

## Repo Name

`software-delivery-skills`

---

## Discipline Structure

Eight disciplines plus shared, each prefixed for scannability:

| Prefix | Discipline | Mindset / Focus |
|---|---|---|
| `sa-` | Solution Architect | Business-aligned, abstract, cross-system. Option papers, capability mapping, vendor evaluation, stakeholder governance. |
| `swa-` | Software Architect | Technical design, NFRs, patterns, system design, ADRs, tech stack decisions, migration paths. |
| `pm-` | Product Manager | Discovery, roadmapping, prioritisation frameworks, backlog refinement, acceptance criteria, feature outcome reviews. |
| `dl-` | Delivery Lead | Work decomposition, epic/ticket structuring, story mapping, sprint flow, WIP management, backlog health, flow metrics. |
| `em-` | Engineering Manager | People and team health. Capacity planning, roadmaps, standups, blockers, escalation, 1:1 coaching, team dynamics. |
| `tl-` | Tech Lead | Team technical standards, unblocking others, PR standards, code review culture, quality gates, technical micro-decisions. |
| `dev-` | Developer | Hands-on building. Task estimation, implementation, debugging, root cause analysis, personal post-incident learnings. |
| `qa-` | Quality Assurance | Test strategy, risk-based test prioritisation, functional/integration/unit testing, defect triage, quality metrics, escape analysis. |
| `ops-` | DevOps / Platform | Infrastructure as code, CI/CD pipelines, platform services, deployment strategy, observability, environment management, incident response in production. |
| `sec-` | Security | "How do we NOT end up on the news?" PCI compliance, PII handling, threat modelling, access control, data classification. Always adversarial — devil's advocate mindset. |
| `da-` | Data & Analytics | Data modelling, data flows between systems, event schemas, logging strategy, reporting pipelines, analytics architecture. Data as a first-class concern. |
| `shared-` | Shared | Cross-cutting skills: communication, documentation, facilitation. |

---

## Core Capabilities Per Discipline

Every discipline (except shared) has five core skill folders covering the same capabilities, interpreted through that discipline's lens:

| Capability | What It Covers |
|---|---|
| `planning` | Upfront thinking, strategy, scoping, estimation, roadmapping |
| `delivery` | Execution, standards, flow, shipping, day-to-day output |
| `problem-solving` | Diagnosis, unblocking, triage, constraint navigation |
| `retro` | Review, reflection, metrics analysis, learning, improvement |
| `conflict-resolution` | Disagreements, alignment, negotiation, difficult conversations |

---

## Full Folder Structure

```
software-delivery-skills/
├── README.md
├── SKILL-TEMPLATE.md
│
├── solution-architect/
│   ├── sa-planning/SKILL.md
│   ├── sa-delivery/SKILL.md
│   ├── sa-problem-solving/SKILL.md
│   ├── sa-retro/SKILL.md
│   ├── sa-conflict-resolution/SKILL.md
│   ├── sa-blueprint-writer/SKILL.md          # Existing skill — migrate
│   └── sa-balance-guardian/SKILL.md           # Existing skill — migrate
│
├── software-architect/
│   ├── swa-planning/SKILL.md
│   ├── swa-delivery/SKILL.md
│   ├── swa-problem-solving/SKILL.md
│   ├── swa-retro/SKILL.md
│   └── swa-conflict-resolution/SKILL.md
│
├── product-manager/
│   ├── pm-planning/SKILL.md
│   ├── pm-delivery/SKILL.md
│   ├── pm-problem-solving/SKILL.md
│   ├── pm-retro/SKILL.md
│   └── pm-conflict-resolution/SKILL.md
│
├── delivery-lead/
│   ├── dl-planning/SKILL.md
│   ├── dl-delivery/SKILL.md
│   ├── dl-problem-solving/SKILL.md
│   ├── dl-retro/SKILL.md
│   └── dl-conflict-resolution/SKILL.md
│
├── engineering-manager/
│   ├── em-planning/SKILL.md
│   ├── em-delivery/SKILL.md
│   ├── em-problem-solving/SKILL.md
│   ├── em-retro/SKILL.md
│   └── em-conflict-resolution/SKILL.md
│
├── tech-lead/
│   ├── tl-planning/SKILL.md
│   ├── tl-delivery/SKILL.md
│   ├── tl-problem-solving/SKILL.md
│   ├── tl-retro/SKILL.md
│   ├── tl-conflict-resolution/SKILL.md
│   └── tl-react-style-guide/SKILL.md         # Existing skill — migrate
│
├── developer/
│   ├── dev-planning/SKILL.md
│   ├── dev-delivery/SKILL.md
│   ├── dev-problem-solving/SKILL.md
│   ├── dev-retro/SKILL.md
│   └── dev-conflict-resolution/SKILL.md
│
├── quality-assurance/
│   ├── qa-planning/SKILL.md
│   ├── qa-delivery/SKILL.md
│   ├── qa-problem-solving/SKILL.md
│   ├── qa-retro/SKILL.md
│   └── qa-conflict-resolution/SKILL.md
│
├── devops-platform/
│   ├── ops-planning/SKILL.md
│   ├── ops-delivery/SKILL.md
│   ├── ops-problem-solving/SKILL.md
│   ├── ops-retro/SKILL.md
│   └── ops-conflict-resolution/SKILL.md
│
├── security/
│   ├── sec-planning/SKILL.md
│   ├── sec-delivery/SKILL.md
│   ├── sec-problem-solving/SKILL.md
│   ├── sec-retro/SKILL.md
│   └── sec-conflict-resolution/SKILL.md
│
├── data-analytics/
│   ├── da-planning/SKILL.md
│   ├── da-delivery/SKILL.md
│   ├── da-problem-solving/SKILL.md
│   ├── da-retro/SKILL.md
│   └── da-conflict-resolution/SKILL.md
│
└── shared/
    ├── shared-communication/SKILL.md
    ├── shared-documentation/SKILL.md
    └── shared-facilitation/SKILL.md
```

---

## Existing Skills to Migrate

Three skills already exist and should be migrated into the new structure. Their full content is included below for copy-paste.

### 1. sa-blueprint-writer (from: blueprint-writer)

Current location: `solution-architect/sa-blueprint-writer/SKILL.md`

```yaml
---
name: sa-blueprint-writer
description: >
  Produces architectural blueprints for software initiatives - the kind used by enterprise
  architecture teams to communicate a proposed solution across business, application, data,
  and technology dimensions. Use this skill whenever a user asks to write, draft, create,
  or structure an architectural blueprint, solution design, technical blueprint, or architecture
  document. Also trigger when a user describes a new system or feature initiative and wants
  it documented for stakeholder review or engineering handoff. The output is a Confluence-ready
  markdown document following the established blueprint template used at FCTG. Blueprint writing
  is an iterative process - expect multiple rounds of questions and refinement before the document
  is complete.
---
```

Full skill content: See existing `blueprint-writer/SKILL.md` — migrate as-is with the updated name prefix.

---

### 2. sa-balance-guardian (from: balance-guardian)

Current location: `solution-architect/sa-balance-guardian/SKILL.md`

```yaml
---
name: sa-balance-guardian
description: >
  Acts as a product, business and common sense representative when reviewing solutions and
  architectural decisions. Evaluates whether a solution strikes the right balance between
  tactical and strategic — surfacing when engineering excellence lacks ROI, when short-term
  wins create long-term debt, or when a solution is well-balanced and ready to proceed.
  Triggered during blueprint drafting, tech decision reviews, sign-off stages, or any ad hoc
  review of a proposed solution. The output is a conversational, thoughtful dialogue — not a report.
---
```

Full skill content: See existing `balance-guardian/SKILL.md` — migrate as-is with the updated name prefix.

---

### 3. tl-react-style-guide (from: react-component-style-guide)

Current location: `tech-lead/tl-react-style-guide/SKILL.md`

```yaml
---
name: tl-react-style-guide
description: >
  Apply React component conventions when generating, editing, or reviewing React code.
  Use when writing React components, hooks, types, data models, or file structures.
  Covers component definition, composition patterns, file naming, props, data fetching,
  styling, and code style.
---
```

Full skill content: See existing `react-component-style-guide/SKILL.md` — migrate as-is with the updated name prefix.

---

## Skill Template

Every SKILL.md should follow this structure:

```yaml
---
name: {prefix}-{capability}
description: >
  One paragraph. What this skill does, when to trigger it, what the output looks like.
---
```

```markdown
# {Skill Name}

Brief intro — what this skill is, who it serves, and what mindset it operates from.

---

## When to Use

Trigger conditions — what the user says or asks that should activate this skill.

---

## Step 1: Understand Context

What to gather before acting. Questions to ask, research to do.

---

## Step 2: Execute

The core process — what the skill actually does. May have sub-steps.

---

## Step 3: Output

What the deliverable looks like. Format, tone, structure.

---

## What Good Looks Like

Signs the skill was used well. Quality indicators.

## What Bad Looks Like

Anti-patterns. Signs the skill was misapplied or the output is weak.
```

---

## Design Principles

1. **Each skill is self-contained** — it should work without needing to read other skills
2. **Skills capture Hilary's specific approach** — not generic best practice. The value is in codifying how she thinks and operates
3. **Skills are conversational first** — they guide Claude's behaviour in dialogue, not just document generation
4. **The five core capabilities are interpreted per discipline** — an architect retro is fundamentally different from a developer retro
5. **Shared skills are genuinely cross-cutting** — if it only applies to one discipline, it belongs there
6. **Security is always adversarial** — the sec- skills should always ask "how do we not end up on the news?"
7. **No education content** — this repo is strictly software delivery

---

## Suggested Build Order

1. Scaffold the full folder structure with empty SKILL.md files
2. Create SKILL-TEMPLATE.md and README.md
3. Migrate the three existing skills (blueprint-writer, balance-guardian, react-style-guide)
4. Populate one discipline end-to-end as a reference (suggest: solution-architect, since two skills already exist)
5. Work through remaining disciplines one at a time

---

## Next Steps

Continue in Cowork where filesystem access is available to:
- Create the repo structure
- Migrate existing skills
- Begin populating skills through collaborative conversation