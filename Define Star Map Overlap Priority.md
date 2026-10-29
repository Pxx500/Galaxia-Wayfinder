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

# Star Map Overlap Priority

## Overlap Rules

For ordinary overlaps between non-parent bodies, show the physically larger body and cull the smaller one. The selected object and the system's star remain visible, as required by [[Star Map Visibility Wayfinder]]. Culling uses final screen-space bounds, not orbital perigee.

Equal-size cases must be deterministic without relying on render order. The compression curve, fade duration and internal rendering algorithm remain open.

## Gameplay Flow

When bodies overlap on the Star Map, the player sees the larger body while the smaller one is hidden. The selected object and the system's star remain visible even when they overlap other bodies.
