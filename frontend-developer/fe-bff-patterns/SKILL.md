---
name: fe-bff-patterns
description: >
  Guides the design and implementation of Backend for Frontend (BFF) layers. Use this skill
  whenever a user is designing, building, reviewing, or discussing a BFF service, a frontend
  API layer, or any backend component that exists solely to serve a specific frontend. Also
  trigger when a user is deciding what data a frontend component needs from the backend, how
  to orchestrate multiple service calls for a UI, or how to structure API responses for
  frontend consumption. Covers BFF philosophy, response shape design, orchestration patterns,
  error handling, caching, and the relationship between BFF and micro-frontend architecture.
  The BFF is a frontend concern - it is owned by the frontend team and designed to serve the
  frontend's needs, not the backend's structure.
---

# BFF Patterns

The Backend for Frontend (BFF) is a component-aware orchestration layer. It exists for one
reason: to give the frontend exactly the data it needs, in the shape it needs it, without
the frontend having to know anything about how that data is assembled from backend services.

The BFF is a frontend concern. It is owned by the frontend team, deployed alongside the
frontend, and designed entirely around what the UI needs to render. This is a deliberate
architectural choice. When the backend team designs a service, they think about domains,
entities, and business rules. When the frontend team designs a BFF, they think about
components, screens, and user interactions. These are fundamentally different perspectives,
and the BFF is where the translation happens.

The guiding principle is tight coupling between BFF and frontend, loose coupling between
BFF and backend services. The BFF response should read like a JSON representation of the
UI components it supports. If you looked at the response payload and the component tree
side by side, the structure should be recognisable.

---

## Core Philosophy

### The BFF mirrors the component tree

The most important design principle: BFF responses should be shaped around the frontend
components that consume them, not around the backend services that provide the data.

A page that renders a `ProductCard` with a `ProductCardHeader`, `ProductCardPrice`, and
`ProductCardActions` should receive a response that maps naturally to those components.
The BFF calls whatever backend services it needs - pricing, inventory, reference data -
and assembles a response that the frontend can pass straight into its component hierarchy
without transformation.

This means:

- The frontend never reshapes API responses. The BFF does that work.
- If a component needs data from three different services, the BFF orchestrates those
  three calls and returns a single, component-ready response.
- If the UI changes (a component is added, removed, or restructured), the BFF response
  changes to match. The backend services don't need to know.

### One BFF per micro-frontend

Each micro-frontend should have its own BFF. This follows the same team ownership model
as the micro-frontend pattern itself - the team that builds the UI also builds the backend
that serves it. This gives the team full autonomy over their data fetching, caching, and
error handling without depending on other teams.

When a micro-frontend needs data, it talks to its own BFF. The BFF talks to shared backend
services. This creates a clean boundary: the contract between micro-frontend and BFF is
owned by one team, while the contract between BFF and backend services is a cross-team
concern managed through API versioning and contracts.

### The BFF is not a general-purpose API

A BFF is not an API gateway. It does not try to serve multiple consumers. It does not
expose generic CRUD operations. It serves one frontend, and it serves it well. If a second
frontend needs similar data, it gets its own BFF that shapes the data for its own needs -
a mobile BFF returns different payloads than a web BFF, even when they call the same
backend services.

---

## Response Shape Design

### Match the component hierarchy

Structure the response to reflect how the frontend will consume it. If a component uses
context providers and compound composition, the BFF response should mirror that nesting.

```
// Component tree:
// <ProductCard>
//   <ProductCardHeader>
//     <ProductCardBrand />
//     <ProductCardTitle />
//   </ProductCardHeader>
//   <ProductCardPrice />
//   <ProductCardActions />
// </ProductCard>

// BFF response mirrors this:
{
  "brand": {
    "name": "Acme",
    "code": "ACM",
    "logo": "https://..."
  },
  "title": {
    "text": "Premium Widget",
    "subtitle": "Professional grade"
  },
  "price": {
    "amount": 299,
    "currency": "AUD",
    "display": "$299.00"
  },
  "actions": {
    "canSelect": true,
    "canCompare": true
  }
}
```

The frontend component tree can consume this directly. `ProductCardBrand` reads from
`brand`, `ProductCardPrice` reads from `price`. No transformation needed.

### Pre-compute display values

If the frontend needs a formatted string, the BFF should provide it. The frontend should
not be doing currency formatting, date formatting, or string concatenation from raw data.
Include both the raw value (for logic) and the display value (for rendering) where both
are needed.

### Nest objects over flat structures

Prefer nested objects with single-word property names over flat structures with compound
names. This keeps the response aligned with how context providers and leaf components will
access the data.

### Include only what the UI needs

The BFF response should contain exactly what the frontend components need to render -
nothing more. Don't pass through fields from backend services that no component will use.
This reduces payload size, simplifies the frontend, and avoids leaking backend
implementation details.

---

## Orchestration Patterns

### Parallel calls where possible

When a BFF needs data from multiple backend services, make those calls in parallel. A
search results page that needs pricing, availability, and reference data should fire all
three requests concurrently, not sequentially.

### Graceful degradation

Not all backend calls are equal. If an enrichment service is down, the core content
should still render - just without the enrichment. Design BFF responses so that optional
data can fail without breaking the core response. Use nullable fields or omit sections
rather than failing the entire request.

### Error translation

Backend services return errors that make sense in their domain. The BFF translates these
into errors that make sense for the UI. A 404 from a pricing service might mean "this
item is no longer available" to the user. The BFF should return an error shape that the
frontend can display directly, not a raw backend error that the frontend has to interpret.

```
// Don't pass through backend errors:
{ "error": "PRICING_SERVICE_ENTITY_NOT_FOUND", "code": 40004 }

// Translate to something the UI can use:
{
  "error": {
    "type": "item_unavailable",
    "message": "This item is no longer available. Please search again.",
    "recoverable": true,
    "action": { "type": "redirect", "path": "/search" }
  }
}
```

### Caching strategy

The BFF is the right place to cache responses that are expensive to assemble. Cache at
the BFF level (not per-backend-service) because the cache key should be based on what
the frontend asked for, not how the backend services are structured internally.

Consider cache-tag-based invalidation when the BFF serves content that changes based on
upstream data updates.

---

## Relationship to Backend Services

The BFF consumes backend services but does not own them. The backend team designs
services around business domains - booking, pricing, inventory, customer. The BFF
team consumes those services and reshapes the data for the UI.

This means:

- Backend services should have clean, well-documented APIs. The BFF depends on them.
- When a backend API changes, the BFF absorbs the change. The frontend doesn't need
  to know.
- The BFF should not contain business logic. It orchestrates, transforms, and shapes.
  Business rules belong in the backend services.
- The BFF should not write to backend services directly for complex operations.
  Commands (writes) should go through proper backend APIs with their own validation
  and business logic. The BFF is primarily a read-side concern.

---

## When to Build a BFF

A BFF earns its place when:

- A frontend needs data from multiple backend services combined into a single response
- The shape of the data the frontend needs is significantly different from what any
  single backend service returns
- The frontend team wants autonomy over their data layer without depending on backend
  team priorities
- Different frontends (web, mobile, micro-frontends) need the same data in different
  shapes

A BFF may not be needed when:

- The frontend talks to exactly one backend service and the response shape already
  matches what the UI needs
- The backend service is already designed as a BFF for this specific frontend
- The data transformation is trivial (a single field rename or filter)

---

## What Good Looks Like

The BFF response is immediately recognisable as the data structure behind a specific
UI component or page.

The frontend has zero data transformation logic - it passes API responses straight
into components.

Backend service changes don't ripple through to the frontend. The BFF absorbs the
change.

Each micro-frontend team owns their BFF and can iterate on their data layer
independently.

Error messages in the UI are meaningful to the user, not raw service errors.

## What Bad Looks Like

The BFF returns generic, kitchen-sink responses that contain every field from every
backend service.

The frontend is full of deep-access patterns like
`response.data.order.items[0].details.pricing.amount` because the BFF just proxied the
backend response through.

Multiple frontends share a single BFF, leading to competing requirements and
compromise responses that serve nobody well.

The BFF contains business logic - validation rules, pricing calculations, eligibility
checks - that belongs in backend services.

The BFF response shape is driven by the backend service structure rather than the
frontend component structure.
