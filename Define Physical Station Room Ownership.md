---
type: wayfinder-ticket
ticket_type: grilling
status: resolved
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Automation and Infrastructure]]"
secondary_areas:
  - Area - Travel and Logistics
blocked_by:
  - "[[Resolve Physical Station Controller Succession]]"
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Physical Station Room Ownership


## Room Ownership

A Room is one physical enclosed space, not one copy per controller. Multiple controllers must not duplicate its environmental effects, volume or energy demand. Station membership and Room ownership are separate.

Station membership propagates through face-connected construction independently of airlocks. Several controllers can join one Station before airlocks exist. Airlocks affect sealing, and the main controller selects the active Station fragment.

This resolves ownership only. Manual validation, boundary invalidation, airlock-side classification and startup recovery remain in their deferred owning notes.

## Implementation Boundary

The initial rework's first integration scenario failed before split or takeover checks, while joining two enclosed rooms into one active Station. The pre-rework boundary flood used diagonal neighbors and accepted only the current controller position in `ArbitraryShapeDefinition`. Those historical findings explain why accepting more controllers as boundaries alone cannot prove unique ownership.

They do not establish the current branch's behavior or implementation of later room-lifecycle decisions.

## Provenance

Accepted on 2026-09-13.

## Related Topics

- [[Resolve Physical Station Controller Succession]]
- [[Define First Physical Station Contract]]
- [[Define Manual Physical Room Validation]]
- [[Define Airlock Space Classification]]
- [[Define Physical Room Validation Recovery]]

## Gameplay Flow

The player can connect several controllers to one Station. When they serve the same enclosed Room, it remains one physical space with one environmental state, volume and energy demand rather than a separate copy for each controller.
