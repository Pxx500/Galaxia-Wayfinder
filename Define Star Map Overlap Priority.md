---
type: wayfinder-ticket
ticket_type: grilling
status: resolved
parent: Star Map Visibility Wayfinder
areas:
  - "[[Area - Observation and Research]]"
blocked_by: []
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Define Star Map Overlap Priority

## Question

Which non-selected body remains visible when two non-parent bodies overlap on the Star Map?

## Established Input

[[Star Map Visibility Wayfinder]] already protects the selected object and the system's star. Culling uses final screen-space bounds, not orbital perigee. Those rules are not reopened.

## Resolution

On 2026-09-17 the owner selected the physically larger body as visible and the smaller body as culled for ordinary non-parent overlaps. The already accepted selected-object and star exceptions still take precedence. Equal-size cases must remain deterministic under the owning visibility model, without relying on render order. This does not choose a compression curve, fade duration or internal rendering algorithm.
