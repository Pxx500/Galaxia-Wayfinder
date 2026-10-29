---
type: wayfinder-ticket
ticket_type: grilling
status: resolved
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Travel and Logistics]]"
secondary_areas:
  - Area - Automation and Infrastructure
blocked_by: []
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Define Authoritative Orbital Time and Hammer Status

## Question

Which server-owned clock and synchronized status representation ensure that Hammer dispatch execution and every GUI view describe the same orbital route state without rerunning the full planner in multiple client widgets?

## Established Input

- Server dispatch is authoritative.
- Client world time must not become a second authority for route eligibility or dispatch timing.
- The original problem was duplicate status calculations in the Hammer configuration window and Station side panel.
- The target should remove duplicate planner work and make status consistent, not merely move the same client calculation into another helper.
- The product contract is server-owned status and consistent client presentation, not a required packet shape or revision scheme.

## Resolution

Hammer dispatch status is transient server-derived presentation based on the authoritative team assets and server orbital time. GUI readers consume that authoritative result instead of independently deciding route feasibility.

Both GUI readers only look up the synchronized status by asset ID and module ID. They do not run the route planner or combine independent client mirrors.

Status inspection does not consume the route-probe cooldown. Actual dispatch planning owns that effect. Status is refreshed with authoritative publication, removed with its asset or client state, and is not durable gameplay state.

## Current Implementation Evidence

Inspection on 2026-09-12 found per-asset status publication for Automated Facilities in `core/network/AssetStateSync.java:223`, with inspection caches scoped by team and system. Client state is updated and removed per asset at lines 387, 409, and 431. Paths are under `src/main/java/com/gtnewhorizons/galaxia/`. Physical Hammer status parity was not established by that inspection.

## Related Topics

- [[Define Space Transport Dispatch Model]]
- [[Simplify Module Execution Lifecycle]]
- [[Area - Travel and Logistics]]
