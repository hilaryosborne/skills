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

# Blueprint Writer

Architectural blueprints are the primary artefact used by solution architects to communicate
a proposed design across business, application, data, and technology dimensions. They are
written for a mixed audience: senior engineering leads, product owners, and business sponsors.
The reading time should be kept to 20 minutes or under.

Blueprints are not exhaustive technical specs. They communicate intent, scope, options
considered, and the rationale behind decisions. Detailed implementation design goes into
SOAPs (Solution Architecture Proposals), which blueprints reference but don't replace.

Blueprint writing is an ongoing, collaborative process. Expect to produce a first draft based
on available information, then iterate with the author over multiple sessions as more detail
emerges. Unanswered questions belong in the document itself - not just in the conversation.

---

## Step 1: Research

Before asking the author anything, search Confluence for relevant existing documentation.
Look for: related blueprints, options papers, SOAPs, PMD entries, architecture decisions,
and any documents that describe the systems involved.

Search for the initiative name, any system names mentioned, and related capability areas.
Read anything that looks relevant. Use what you find to pre-fill answers where possible and
to form more informed questions.

Keep a list of every Confluence document you read and use - these become references at the
end of the blueprint.

---

## Step 2: Ask the Author

After researching, present a comprehensive set of questions to the author in a single pass.
Group them clearly so the conversation is efficient. The author may not be able to answer
everything - that is fine and expected. Unanswered questions get recorded in the Questions
table at the end of the document.

Ask all of the following. Adapt wording to what you already know from research.

**About the initiative:**
- What is the initiative name and Jira/PMD link?
- Who is the business owner/sponsor?
- Who is the document owner and architect?
- What problem is this solving, and why now? Are there any metrics or data that quantify the problem?
- Is there an existing options paper or prior analysis we should reference?

**About scope:**
- What is explicitly in scope?
- What is explicitly out of scope?
- Which brands and regions does this cover?
- What are the future phases or follow-on initiatives expected after this one?

**About the current state:**
- How does this capability work today? Walk me through the current flow or process.
- What systems are involved today, and what are their roles?
- What are the known pain points, limitations, or risks with the current approach?

**About the proposed solution:**
- What options are being considered? List each one, even if some are already ruled out.
- For each option: what is the approach, and what is the reason it was included or excluded?
- Which option is preferred, and why?
- What are the key design decisions already made?
- What are the major open questions or unknowns that still need resolution?
- What systems and teams will be involved in delivering this?

**About non-functional concerns:**
- Does this solution handle or store PII? If so, what data and in which systems?
- Are there authentication or authorisation requirements?
- What are the observability expectations - New Relic, Splunk, Launch Darkly, other?
- Are there data retention requirements?
- Is a pen test required?

**About delivery:**
- What spikes or discovery work is already planned or needed?
- What epics are expected, and which teams own them?
- Are there workshops or stakeholder reviews planned?
- What are the known dependencies on other teams or systems?

---

## Step 3: Draft the Blueprint

With research complete and author answers in hand, produce the full blueprint. Follow the
document structure below exactly. For every question the author could not answer, add a row
to the Questions table at the end of the document rather than leaving the section blank or
making something up.

After producing the draft, tell the author what is missing and what you need from them next.
Blueprints improve through iteration - the goal of the first draft is to get everything known
onto the page and make the gaps visible.

---

## Document Structure

Always produce the blueprint using this exact structure. Sections that genuinely don't apply
can be noted as "N/A" with a brief reason, but don't omit them silently.

### Header Table

```
| Initiatives        | [Jira/PMD link or initiative name]   |
| Business Owner     | [Name]                               |
| Document Status    | DRAFT                                |
| Document Owner     | [Name]                               |
| Architect          | [Name]                               |
| Diagrams           | [Miro board link or "TBD"]           |
```

---

### 1. Overview

One to three paragraphs of plain-language context. What is this initiative? Why does it exist?
Who does it serve? Write it so a non-technical sponsor can understand the value of the work.

#### 1.1. Problem Statement

Describe the specific problems being solved. Use numbered points for multiple distinct problems.
Be concrete - include data or metrics where known. Reference the PMD or initiative ticket.

#### 1.2. Scope

Bullet list of what IS included. Each bullet is a short noun phrase followed by a dash and a
one-sentence description:

```
* **Flight Disruption Notification** - uplift the supply system to send email notifications
  for major disruptions with a link for self-service acceptance.
```

#### 1.3. Out of Scope

Bullet list of what is explicitly excluded, with a brief reason for each. Prevents scope creep.

#### 1.4. Future Considerations

Items not in scope now but expected to follow. Gives the reader a sense of the larger direction.

---

### 2. Current State

Describe how things work today. Organise into sub-sections per system or flow. Write in present
tense. Focus on what is relevant to the proposed change.

Use bullet points to describe system capabilities, and prose to describe flows and pain points.
Call out current limitations, workarounds, or risks that motivate the solution.

**Diagram placement:** Open the Current State section with a level 1 systems diagram placeholder
before any sub-sections. Add further diagram placeholders before sub-sections where a specific
flow or system benefits from visual support. Use this format:

```
[Diagram: Level 1 systems - <short description of what the diagram shows> - to be added in Miro]
```

---

### 3. Proposed Solution

This is the core of the blueprint. Start with a level 1 systems diagram placeholder showing the
proposed architecture, then an overview paragraph, then break down the solution into numbered
sub-sections - one per major capability, system, or decision area.

**Diagram placement:** Place a top-level diagram placeholder at the start of section 3. Add
further diagram placeholders within sub-sections where a specific flow or integration warrants
visual support. Use this format:

```
[Diagram: Level 1 systems - <short description of what the diagram shows> - to be added in Miro]
```

#### Options Analysis

Document every option that was considered, including those already ruled out. This creates a
record of the decision-making process and prevents revisiting rejected approaches. Format:

```
### 3.1. Solution Options

#### 3.1.1. Option 1 - [Name]
[One paragraph describing the approach and its implications]
**Not Preferred:** [One sentence on why this was ruled out, or "Under consideration" if still live]

#### 3.1.2. Option 2 - [Name]
...

### 3.2. Preferred Option - [Name]
[Explain why this was chosen over the alternatives. If no preferred option has been selected
yet, state that explicitly and list what criteria will determine the decision.]
```

If no options have been considered yet, note this and flag it as a gap to resolve.

#### Per-Capability Sub-sections

Each sub-section covers a distinct capability or system concern. Use bold inline labels for:

- `**Decision:**` - a specific technical or architectural decision made
- `**Further Discovery:**` - an open question or unknown that needs resolution before delivery
- `**Risk:**` - a specific risk introduced by this design choice
- `**Not Preferred:**` - used within options to explain why an approach was ruled out

Write in flowing prose, not bullet points. Include the *why* behind design choices, not just
the *what*.

---

### 4. Security

#### 4.1. Data Security

For each data entity created, stored, or transmitted by the proposed solution:

```
| High-level item    | [Entity name]                    |
| Included details   | [Fields or data types]           |
| Contains PII       | Yes / No                         |
| System             | [System that owns or stores it]  |
| Data Retention     | [Retention period / policy]      |
```

#### 4.2. Security Considerations

Authentication approach, API security, pen test recommendations, access controls. Reference
decisions made in section 3 where relevant.

---

### 5. Observability, Alerting & Reporting

How will the system be monitored in production? Reference existing tooling (New Relic, Splunk,
Launch Darkly, Datadog) and note any new dashboards, alerts, or reporting requirements.
If no changes are expected, say so briefly.

---

### 6. Assumptions

```
| Assumption | Description                                             |
| ABA-01     | [A statement of what is assumed to be true]             |
| ABA-02     | ...                                                     |
```

Assumptions are things believed to be true but not yet confirmed. They are risks if wrong.

---

### 7. Risks

```
| Risk   | Description                                               |
| ABR-01 | [What could go wrong and what the impact would be]        |
| ABR-02 | ...                                                       |
```

---

### 8. Dependencies

```
| Dependency | Description                                              |
| ABD-01     | [System or team] - [what this solution depends on them for] |
| ABD-02     | ...                                                      |
```

---

### 9. Next Steps

```
#### SOAPs
[Detailed Solution Architecture Proposals to be created]

#### Spikes
[Time-boxed discovery work needed to resolve unknowns]

#### Epics
[Recommended epics, owning teams, and epic links where known]

#### Collaboration
[Workshops, review sessions, or key stakeholders to engage]
```

---

### 10. Open Questions

Every question the author could not answer during the intake process goes here. This table
is a first-class part of the document - it makes gaps visible and gives stakeholders something
concrete to respond to.

```
| ID   | Question                                              | Owner | Status |
| OQ-01 | [The unanswered question]                            | TBD   | Open   |
| OQ-02 | ...                                                  |       |        |
```

Update this table as questions are answered across sessions. Mark answered questions with
their answer and the date resolved, and move confirmed answers into the relevant section of
the document body.

---

### 11. References

List every Confluence document, options paper, PMD entry, SOAP, or external source that
informed this blueprint. Include the document title and link.

```
| Title | Link | Notes |
| [Document name] | [Confluence or Jira URL] | [Why it is relevant] |
```

If no references were found during research, note that and describe what was searched for.

---

## Tone and Writing Style

- Write as a practitioner writing for peers, clear, direct, and specific.
- Avoid vague generalisations. Flag unknowns with **Further Discovery:** rather than guessing.
- Use **bold** for key terms on first use, decision labels, and section labels within prose.
- Diagrams are important. Where none exist, add a placeholder:
  `[Diagram: Level 1 systems - {description} - to be added in Miro]`
- Avoid passive voice where possible.
- Don't pad. A tight document is better than a fluffy one.
- **Never use em dashes (-).** Use a hyphen (-) or restructure the sentence instead.

---

## What Makes a Good Blueprint

A reader can understand the problem, current state, and proposed solution without needing
to ask the architect questions.

Decisions are explicit and their rationale is captured.

Open questions are in the document, not just in someone's head.

Every option considered is recorded, including those ruled out.

Scope is unambiguous - what is in, what is out, and what comes later.

It could be handed to a delivery team to begin writing epics.

---

## Iterating on the Blueprint

After each session with the author, update the document and clearly communicate:

- What was added or changed
- What questions remain open (point to the Questions table)
- What you need from the author to progress the next section

Blueprints are living documents during the design phase. Each iteration should move more
questions from section 10 into the body of the document as answered content.
