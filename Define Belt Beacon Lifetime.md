---
type: wayfinder-ticket
ticket_type: grilling
status: resolved
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Destinations]]"
blocked_by:
  - "[[Define Asteroid Belt Physical Travel and Beacons]]"
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Define Belt Beacon Lifetime

## Question

When a Belt Beacon is destroyed, does its known coordinate remain a navigable map point, or does the registered point disappear with the block?

## Established Input

The resolved belt contract distinguishes physical Belt Coordinates from persistent remote asteroids. A Beacon registers a physical travel anchor, not an Automated Outpost or a guarantee of landing services. Its lifetime was left as fog.

## Resolution

Accepted on 2026-09-17: while the physical Beacon exists, it keeps its Star Map marker alive. The marker has no manual deletion action in this state.

When the Beacon is destroyed, its coordinate marker remains on the asteroid map. Its right-click context menu then exposes a `Delete marker` action. Any member of the owning team may use that action to remove the marker for the team. The action is unavailable while the Beacon block still exists.

Retaining known coordinates does not preserve destroyed endpoint services, revive endpoint identities or guarantee a safe arrival. Existing flight and site checks still apply.

## Remaining Scope

Team-scoped marker deletion is settled. No public or cross-team sharing feature follows from it. Exact Beacon naming, limits and coordinate mapping remain separate concerns.
