# SOAP Template Structure

This is the established SOAP (Solution on a Page) template. SOAPs follow this structure as
a backbone but adapt sections based on what the document is actually about. Sections that
don't apply can be noted as N/A or omitted if the SOAP is clearly better without them.

---

## Header Table

| Field | Content |
|---|---|
| **Initiatives** | Initiative name with issue tracker link |
| **Business Owner/Sponsor** | Owner or sponsor from business |
| **Project Manager** | PM if applicable |
| **Epics/Goals** | List of epics with issue tracker links |
| **Feature(s)** | Description of the initiative and related epics |
| **Document status** | DRAFT / PEER REVIEWED / ENDORSED with dates |
| **Document owner** | Solution Architect or Head of Engineering |
| **Architect** | Solution Architect or Software Architect |
| **Impacted Platforms/Products** | Systems, platforms, products impacted |
| **Contributors** | People contributing to this artefact |

---

## Executive Summary

High-level overview so the reader can decide whether the document is relevant to them.
Keep it to one or two paragraphs.

---

## Description (Problem Statement)

Business context for why the solution is required:

- What is the context of the problem
- Why does the problem need to be fixed
- What is the urgency of the solution

---

## Scope

What the solution covers:

- Global or regional
- Which brands or business units
- Solution context and relevant information

---

## Out of Scope

What is explicitly excluded:

- Constraints that currently affect scope
- Any system or process flow not documented here

---

## Requirements

### Functional

Reference or present the functional requirements that guide the solution design.
Link back to business requirements in the parent blueprint where possible.

### Non-Functional

Reference or present the non-functional requirements that guide the solution design.

### Scenarios

| # | Title | Detailed Scenario | How should it be handled | Comments |
|---|---|---|---|---|
| 001 | | | | |

---

## Options Analysis (optional)

Where multiple solutions exist, provide a high-level overview with pros/cons and
justification for the recommended solution. Key factors that led to the decision
should be explicitly mentioned.

---

## Risks/Dependencies

Risks and dependencies that may prevent implementation, with mitigating factors.

---

## Solution Design

The core of the SOAP. The method of defining the solution will be specific to each
solution. Recommended tools:

- Data models
- System context diagrams
- Sequence diagrams
- Application diagrams
- Deployment/infrastructure diagrams

### Deployment Diagrams

Diagrams that communicate:

- What endpoints are exposed
- Where each service is deployed (Kubernetes cluster, serverless, VPC, etc.)
- Lines of communication between services including:
  - Authentication method for each line
  - Encryption on each line
  - Networks traversed (public, internal, etc.)

Include links to diagramming tools (Miro, Lucidchart, etc.).

---

## Considerations

### Data Privacy / Data Security

How the solution manages, processes, and stores sensitive data:

- Alignment with relevant data protection regulations (GDPR, CCPA, etc.)
- Access control for business-sensitive data

### Security

How data is protected:

- Data at rest
- Data in transit
- Access management
- Access monitoring
- Service protection
- Authentication flow diagrams

### Code Management

| System/Service | Repo | Location | Contains | Repo Managed by | Package Managed by |
|---|---|---|---|---|---|
| | | GitHub/GitLab link | | | |

### Architecture Alignment

How the solution aligns with the organisation's architectural principles.

| Architecture Principle | Alignment | Notes |
|---|---|---|
| | | |

### Policies & Standards

Applicable security and privacy standards.
Reference the organisation's policy documentation for current versions.

---

## Supporting Documents

| Document | Location | Description |
|---|---|---|
| | URL | |

---

## Related SOAPs

| SOAP | Description | Action |
|---|---|---|
| Link | | |

---

## Questions

| ID | Name | Description | Status | Owner | Date Required | Response/Decision | Response by? | Source |
|---|---|---|---|---|---|---|---|---|
| QQ-001 | | | Open/Closed | | | | | |

---

## Solution Design Review

Review checklists that the solution should be assessed against:

### Security Checklist
- API authentication and authorisation
- Access restriction (IP allow-listing, etc.)
- No unnecessary information exposure
- Encryption (TLS 1.2+)
- Data minimisation
- Throttling and breach containment
- No client-side credentials
- Data classification
- Configuration change alerting
- PCI scope review (if payment-related)
- WAF protection for public APIs
- SIEM logging
- Deployment diagram with security annotations
- Sensitive data masking in logs

### Data Privacy Checklist
- Deletion mechanism for personal information
- Retention period defined
- Automated alerting for exceeded retention
- Data sovereignty compliance
- Data processing clauses in vendor contracts

### Performance Checklist
- Availability requirements considered
- Operational support agreed
- Graceful degradation for unavailable systems
- Load handling (minimum, average, peak)
- End-to-end performance within limits

### Architecture Checklist
- Non-functional requirements addressed
- Functional requirements addressed
- Architecture principles considered
