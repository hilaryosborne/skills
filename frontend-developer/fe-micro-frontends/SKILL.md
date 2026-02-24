---
name: fe-micro-frontends
description: >
  Guides the design, implementation, and integration of micro-frontends. Use this
  skill whenever a user is building, embedding, reviewing, or discussing a micro-frontend,
  micro-UI, or independently deployable frontend component. Also trigger when discussing
  how to compose multiple frontend applications into a single user experience, how to share
  state or communicate between micro-frontends, how to structure a micro-frontend with its
  BFF and SDK, or when evaluating whether something should be a micro-frontend at all.
  Covers composition patterns, cross-app communication, shared dependencies, the
  micro-frontend/BFF/SDK triad, embedding strategies, and real-world lessons learned
  from adopting micro-frontend architecture at scale.
---

# Micro-Frontend Patterns

Micro-frontends extend the principles of microservice architecture to the frontend. Each
micro-frontend is an independently built, tested, and deployed frontend application that
is composed into a larger user experience by a parent (or "macro") application. The user
sees a single application. In reality, they interact with several independent applications
published by different teams.

Micro-frontends enable autonomous teams to own vertical slices of the product - from the
UI through to the BFF that serves it. The pattern delivers real benefits in team autonomy
and deployment independence, but it also teaches hard lessons about granularity, coupling,
and developer experience that this skill captures.

---

## The Micro-Frontend Triad

A micro-frontend is not just the UI component. It is a triad:

**Micro-Frontend (MFE)** - the UI layer. A self-contained frontend application that
renders a specific capability. It is embedded into a parent application at runtime.

**Backend for Frontend (BFF)** - the data layer. A backend service owned by the same
team, designed exclusively to serve the MFE. It orchestrates calls to shared backend
services and returns responses shaped for the MFE's components. See the fe-bff-patterns
skill for detailed BFF guidance.

**SDK / Platform** - the integration layer. A published package (typically an npm library)
that the parent application uses to embed and communicate with the MFE. It exposes hooks,
event handlers, and configuration to the consuming application.

This triad is owned by one team. The team builds the UI, builds the backend that serves
it, and publishes the SDK that lets other applications embed it. This full-stack ownership
is what gives teams genuine autonomy.

---

## Composition Patterns

### Runtime integration via JavaScript (preferred)

Each micro-frontend is included on the page using a `<script>` tag and exposes a global
function or web component as its entry point. The parent application determines which
MFE to mount and calls the relevant function, telling it where and when to render.

This is the most flexible approach. It allows independent deployment (updating the script
URL updates the MFE), technology flexibility (each MFE can use its own framework version),
and clean runtime isolation.

### Integration via SDK hooks

The consuming application imports the MFE's SDK and uses a hook (like `useMicroPlatform`)
to interact with it. The SDK handles mounting, event communication, and lifecycle
management. This pattern creates a clean programmatic interface between the parent and
child applications.

### Embedding patterns

The parent application embeds MFEs using a combination of:

- Script-based loading for the MFE bundle
- SDK hooks for programmatic interaction
- Event bus for cross-MFE communication
- Window object conventions (e.g. `window.app.{platform}`) for shared state access

---

## Cross-Application Communication

Micro-frontends should communicate as little as possible. Every communication channel
between MFEs is a coupling point. The goal is independent operation, not a distributed
monolith.

When communication is needed:

### Events (preferred)

Custom events allow MFEs to communicate indirectly. An MFE emits an event when something
happens (user selected a flight, cart updated). Other MFEs or the parent application
listen for events they care about. This keeps coupling implicit and allows MFEs to be
added or removed without breaking others.

An event bus pattern works well for cross-cutting concerns like authentication - MFEs
subscribe to events like "sign in" or "ready" and react accordingly.

### Callbacks via parent (for explicit contracts)

The parent application passes callbacks and data down to MFEs, similar to React's
props-down pattern. This makes the contract between parent and MFE explicit and
type-safe, but it creates a dependency on the parent for coordination.

### What to avoid

- **Shared global state** - sharing Redux stores, global variables, or mutable state
  between MFEs creates the same coupling problems as a monolith. Each MFE should have
  its own state management.
- **Direct MFE-to-MFE calls** - if one MFE needs to directly call another's API or
  access its internals, the boundary is wrong. Either they should be one MFE, or they
  should communicate through events or the parent.
- **Shared domain models** - the moment two MFEs share a data model, they are coupled.
  Each MFE should own its own types, even if they look similar.

---

## Shared Dependencies and Components

### Shared UI components

Share "dumb" visual primitives: icons, buttons, labels, design system components. These
contain only UI logic and no business or domain logic. A shared design system provides
this layer well.

Do not share components that contain business logic. A `ProductTable` that knows what a
"product" is and how it behaves belongs in a specific MFE, not in a shared library. Domain
logic in shared libraries creates coupling that defeats the purpose of micro-frontends.

### Dependency duplication

Independent builds mean each MFE bundles its own dependencies. This can lead to React
being downloaded multiple times. This is a real trade-off:

- Building independently enables autonomous deployment
- Sharing dependencies creates build-time coupling and lockstep releases

The pragmatic approach is to externalise the heaviest shared dependencies (React,
React-DOM) as externals that the parent application provides, while accepting some
duplication for smaller libraries. This balances bundle size against deployment independence.

### Published typings

MFE SDKs should publish TypeScript types so consuming applications get type safety at
integration points. This is a lightweight form of contract that catches breaking changes
at compile time rather than runtime.

---

## Common Pitfalls

Real-world micro-frontend adoption surfaces recurring problems that this skill should
help avoid:

### Granularity matters

Micro-frontends that are too small introduce large amounts of code duplication and DX
overhead. Each MFE has its own repo, build pipeline, deployment, and runtime overhead.
A micro-frontend should represent a meaningful business capability, not a single UI
widget. If an MFE is too small to justify its own team, BFF, and deployment pipeline,
it's probably too small to be a micro-frontend.

### Implicit coupling is dangerous

Interdependency between MFEs and platforms can cause cascading failures when APIs change
and impacts aren't caught in testing. Types should flow through published SDKs, not
through assumptions. When an MFE's interface changes, consuming applications should
know at compile time, not at runtime.

### Developer experience compounds

Every MFE adds DX friction: more repos to clone, more local servers to run, more
deployment pipelines to understand. When the number of MFEs grows, release management
of features that span multiple MFEs requires complex coordination. This isn't a reason
to avoid micro-frontends, but it's a reason to be deliberate about granularity and to
invest in tooling and automation.

### The macro app bottleneck

The parent application can become a bottleneck when every MFE needs review, testing, and
release coordination through it. This is especially painful when the macro app has its own
release cadence that doesn't align with MFE team timelines.

---

## When to Use a Micro-Frontend

A micro-frontend makes sense when:

- A distinct team owns a business capability end-to-end (UI + BFF + data)
- The capability needs independent deployment - shipping changes without coordinating
  releases with other teams
- The capability has its own lifecycle - it evolves at a different pace than the rest
  of the application
- Multiple applications need to embed the same capability (e.g., a booking management
  MFE used across multiple host applications)

A micro-frontend may not be the right choice when:

- The feature is tightly coupled to the parent application's routing, state, or layout
- The team building it is the same team that owns the parent application
- The feature is small enough that the overhead of a separate build, deploy, and runtime
  is not justified
- The feature shares so much state with the parent that the integration boundary would
  be artificial

---

## Testing

Each micro-frontend should have its own comprehensive test suite covering unit and
integration tests. The MFE should be testable in isolation - without the parent
application running.

Integration testing between the MFE and the parent application should focus on the
integration boundary: does the MFE mount correctly, does event communication work,
do callbacks fire as expected. Don't re-test the MFE's internal business logic at the
integration level - that's already covered by the MFE's own tests.

For user journeys that span multiple MFEs, use functional/end-to-end tests focused on
validating the integration, not the internal logic of each MFE.

---

## What Good Looks Like

Each MFE team operates autonomously - they can build, test, and deploy without waiting
for other teams.

The boundary between MFEs is clean - they communicate through events or explicit
contracts, not shared state.

The parent application composes MFEs without knowing their internals.

Published SDKs with TypeScript types make the integration contract explicit and
type-safe.

Each MFE has its own BFF, giving the team full-stack ownership.

## What Bad Looks Like

MFEs that are too granular - every small widget is its own micro-frontend with its own
repo, pipeline, and runtime overhead.

MFEs that share Redux stores, domain models, or mutable global state.

A parent application that is tightly coupled to MFE internals and breaks when any MFE
changes.

Release coordination that requires multiple teams to deploy in lockstep - the opposite
of what micro-frontends should enable.

MFEs without their own BFF, depending on a shared backend API that serves multiple
frontends with compromise responses.
