---
type: wayfinder-ticket
ticket_type: grilling
status: open
parent: Star Map Visibility Wayfinder
areas:
  - "[[Area - Observation and Research]]"
blocked_by: []
claimed_by: local-wayfinder-reconciliation
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

## Discussion Proposal

Prefer the physically larger body, with a stable tie-break for equal sizes rather than render order. The selected-object and star exceptions still take precedence. This awaits the owner's decision. It does not choose a compression curve, fade duration or internal rendering algorithm.
