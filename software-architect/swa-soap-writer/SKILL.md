---
name: swa-soap-writer
description: >
  Produces SOAP (Solution on a Page) documents for software architecture. SOAPs are the
  technical design layer beneath blueprints - they describe how a specific component,
  service, or capability will be built. Use this skill whenever a user asks to write, draft,
  create, or structure a SOAP, solution on a page, technical design document, or service
  design. Also trigger when a user describes a specific technical component they want documented
  for peer review, architecture board endorsement, or engineering handoff. SOAPs are iterative -
  expect multiple rounds of questions and refinement before the document is complete. The output
  is a Confluence-ready markdown document following established SOAP conventions.
---

# SOAP Writer

SOAPs (Solution on a Page) are the primary artefact used by software architects to
communicate how a specific component, service, or capability will be built. They sit
one level below architectural blueprints - where a blueprint describes the initiative-level
solution across business, application, data, and technology dimensions, a SOAP zooms into
a single piece of that architecture and designs it in enough detail for a delivery team to
build from.

SOAPs are written for engineers and technical reviewers. The reader should be able to
understand the problem, the design, the trade-offs, and the open questions without needing
to talk to the architect.

The SOAP template provides a backbone structure, but real SOAPs adapt significantly based
on what the document is about. An infrastructure SOAP covering CDN caching patterns looks
nothing like a data architecture SOAP defining schemas, which looks nothing like a frontend
integration SOAP describing SDK embedding patterns. The skill of writing a good SOAP is
knowing which sections to expand, which to condense, and what domain-specific content to
add that the template doesn't anticipate.

SOAP writing is collaborative and iterative. The first draft gets everything known onto
the page and makes the gaps visible. Subsequent sessions fill gaps as discoveries are made,
spikes are completed, and stakeholder feedback comes in.

---

## Step 1: Research

Before asking the author anything, search for relevant context in the team's documentation.
The goal is to arrive at the conversation already informed, so the author can focus on
decisions and design rather than explaining background.

Search for:

- The parent blueprint this SOAP sits under (most SOAPs are referenced from a blueprint)
- Related SOAPs in the same domain - understand what's already been designed nearby
- Options papers or prior analysis that explored alternatives
- The systems and services mentioned - look for existing architecture documentation
- Any epics or initiatives linked to this work

Read what you find. Use it to pre-fill answers where possible and to form sharper questions.
Keep a list of every document you reference - these go into the Supporting Documents and
Related SOAPs tables at the end.

---

## Step 2: Ask the Author

After researching, present a focused set of questions in a single pass. Group them clearly.
The author may not be able to answer everything - that's expected and normal. Unanswered
questions get recorded in the Questions table at the end of the document.

Adapt these based on what you already know from research. Skip questions you can already
answer and flag what you found.

**About the component:**
- What is this SOAP designing? (service, data model, integration, infrastructure component)
- Which blueprint does it sit under?
- Who is the architect and document owner?
- What problem does this specific component solve within the broader initiative?
- What systems and teams are involved?

**About scope:**
- What is explicitly included in this SOAP?
- What is explicitly excluded?
- What regions, brands, or business units does this cover?
- Are there related SOAPs that handle adjacent concerns?

**About the current state:**
- How does this work today, if at all?
- What are the pain points or limitations with the current approach?
- What existing systems does the new design need to integrate with?

**About the proposed solution:**
- What options have been considered?
- Which option is preferred, and why were others ruled out?
- Walk me through the solution design - how does it work end to end?
- What are the key technical decisions already made?
- What are the major unknowns that need spikes or further discovery?

**About non-functional concerns:**
- Does this handle PII? What data, and where is it stored?
- What are the authentication and authorisation requirements?
- What monitoring and observability is expected?
- What are the performance requirements (response time, throughput, availability)?
- Are there data retention requirements?
- Is there PCI scope?

**About delivery:**
- What spikes or discovery work is needed before building?
- What epics are planned, and which teams own them?
- Are there dependencies on other teams or SOAPs?

---

## Step 3: Draft the SOAP

With research and author answers in hand, produce the full SOAP. Read the template structure
from `references/soap-template.md` for the formal section layout, then adapt it to fit
the content.

### Adaptation is expected

The template is a backbone, not a straitjacket. Here's how SOAPs typically adapt by domain:

**Infrastructure SOAPs** (CDN caching, deployment pipelines, platform services) tend to
expand the Solution Design section with detailed infrastructure diagrams, options analysis
per component, endpoint specifications, failure scenarios, and monitoring metrics. The
Requirements section may be replaced by a Goals section with measurable outcomes.

**Data architecture SOAPs** (schemas, data models, data flows) tend to expand with entity
relationship descriptions, code samples showing the proposed schema, database options
analysis, data ownership and lifecycle, and detailed data privacy/retention tables.

**Frontend integration SOAPs** (SDK embedding, platform integration, micro-frontend
composition) tend to expand with integration patterns, event bus / messaging contracts,
window object conventions, sequence diagrams showing the integration flow, and practical
code samples showing how consuming applications will use the API.

**Service design SOAPs** (new services, API design, service decomposition) tend to expand
with endpoint specifications, authentication flows, deployment topology, and
service-to-service communication patterns.

In all cases, the Solution Design section is where the SOAP earns its value. This is where
you invest the most effort. Everything else supports it.

### Writing the sections

**Header table** - Fill in everything known. Mark unknowns as TBD rather than guessing.

**Executive Summary** - One to two paragraphs of plain language. What is this component,
what does it do, and why does it matter? Write it so someone can decide in 30 seconds
whether this document is relevant to them.

**Description** - The problem statement. Be concrete - include data or metrics where known.
Connect to the parent blueprint's problem statement but focus on the specific technical
problem this SOAP solves.

**Scope and Out of Scope** - Be explicit. Scope prevents creep. Out of scope prevents
assumptions. If something is "future work," say so and say why.

**Requirements** - Link back to the parent blueprint's requirements where possible. Add
technical requirements specific to this component. The scenarios table is valuable for
integration SOAPs where the reader needs to understand how different situations are handled.

**Options Analysis** - Document every option considered, including those ruled out. This
creates a decision record. For each option, explain the approach and why it was or wasn't
chosen. Use a consistent format - pros/cons tables work well for comparing multiple options
on the same dimensions.

**Solution Design** - The heart of the document. Start with an overview, then break down
by sub-component or concern. Use diagrams - system context, sequence, deployment - placed
where they support the text. Include code samples where they communicate the design better
than prose (especially for data models, API contracts, and integration patterns).

**Considerations** - Data privacy, security, code management, architecture alignment,
policies. These sections exist to ensure the design has been thought through from
compliance and governance perspectives. Don't skip them even if the answers are simple -
"this service handles no PII" is a useful statement.

**Solution Design Review** - Review checklists covering security, data privacy, performance,
and architecture alignment. These are typically completed during peer review rather than
initial drafting - leave them in the document with empty "how addressed" columns if
drafting early.

**Questions** - Every question the author could not answer goes here. This table is a
first-class part of the document. It makes gaps visible and gives reviewers something
concrete to respond to. Use the format: QQ-001, QQ-002, etc.

### Key Decisions section

Some SOAPs benefit from a dedicated Key Decisions section near the end that pulls together
the important technical decisions made throughout the document into a scannable list. This
is especially useful when the solution design is long and decisions are scattered across
sub-sections. Each decision should be a single clear statement.

---

## Step 4: Communicate Gaps and Next Steps

After producing the draft, tell the author explicitly:

- What sections are complete
- What is missing or thin
- Which questions in the Questions table are blocking progress
- What you need from them to advance the document

SOAPs improve through iteration. The first draft's job is to make the shape of the solution
visible and the gaps obvious.

---

## Iterating on the SOAP

After each session with the author, update the document and communicate:

- What was added or changed
- Which questions moved from the Questions table into the document body as answered content
- What you need next

As the SOAP matures through peer review, expect the review checklists to be filled in and
the Questions table to shrink.

---

## Tone and Writing Style

- Write as an engineer for engineers. Clear, direct, specific.
- Use prose for flows and reasoning. Use bullet points for capabilities and requirements.
- Use tables for structured comparisons (options analysis, risks, scenarios).
- Use code samples when they communicate better than prose - especially for data models,
  API contracts, and integration patterns.
- Flag unknowns explicitly with bold labels: **Further Discovery:** or **Open Question:**
- Include diagram placeholders where visuals would help, using:
  `[Diagram: <type> - <description> - to be added]`
- Never use em dashes. Use a hyphen or restructure the sentence.
- Don't pad. A tight SOAP is better than a fluffy one.
- Explain the *why* behind design decisions, not just the *what*.

---

## What Good Looks Like

A reader can understand the component's purpose, current state, proposed design, and
open questions without talking to the architect.

Design decisions are explicit and their rationale is captured - including options that
were considered and rejected.

The solution design section has enough detail for a delivery team to start writing epics.

Open questions are in the document, not in someone's head.

The SOAP adapts its structure to suit its content - an infrastructure SOAP and a data
architecture SOAP should look different because they are different.

## What Bad Looks Like

A SOAP that follows the template rigidly without adapting to its domain - every section
filled in but none expanded where the real complexity lives.

A solution design section that describes *what* without explaining *why*.

Missing options analysis - the reader has no idea what alternatives were considered.

Vague scope that doesn't clearly separate what's in from what's out.

Empty sections left in rather than being marked N/A with a reason or removed.

A document that reads like a checklist exercise rather than a technical design.
