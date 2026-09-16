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

# Define Physical Station Room Ownership

## Question

When Station construction connects several controllers, what defines a physical Room and owns its volume, environmental state, devices and energy consumption without counting one space more than once?

## Accepted Constraints

- Station membership propagates through face-connected construction independently of airlocks.
- Multiple controllers can belong to one Station and can be built before airlocks.
- Airlocks still affect physical sealing independently of Station identity.
- The main controller selects the active Station fragment.

## Historical Implementation Evidence

The first real-world integration scenario for the rework failed while waiting for two connected enclosed rooms to become one active Station. The failure occurred before the split or manual takeover steps.

The pre-rework `compat/structure/ArbitraryShapeDefinition.java` flooded connected boundary blocks, including diagonal neighbors, at line 466 in that baseline. Its `addControllerBlock` builder at line 746 accepted only the current controller's coordinates. This was not the same model as the newly accepted Station-wide face connectivity. These are historical findings, not claims about the current branch.

Simply accepting all controllers as boundary blocks would not by itself establish unique ownership of room volume, environmental devices or energy consumption. That behavior must not be inferred from the Station identity decision.

## Resolution

Accepted on 2026-09-13. A Room is a physical enclosed space, not one copy per controller. Multiple controllers must not duplicate the same Room's environmental effects or energy demand. Station membership and Room ownership remain distinct concepts. The owner confirmed this as an obvious consequence of the intended physical model and authorized continued implementation.

This resolves shared room ownership only. Manual validation, boundary invalidation, airlock-side classification and startup recovery were discussed later and remain separate decisions. The implementation evidence for the initial rework does not certify those later features as implemented.

## Related Topics

- [[Resolve Physical Station Controller Succession]]
- [[Define First Physical Station Contract]]
