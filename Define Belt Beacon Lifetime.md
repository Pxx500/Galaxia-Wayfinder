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

# Belt Beacon Lifetime

## Marker Lifetime

A Beacon registers a physical travel anchor, not an Automated Outpost or a guarantee of landing services. Physical Belt Coordinates are distinct from persistent remote asteroids.

While the physical Beacon exists, it keeps its Star Map marker alive. The marker has no manual deletion action in this state.

When the Beacon is destroyed, its coordinate marker remains on the asteroid map. Its right-click context menu then exposes a `Delete marker` action. Any member of the owning team may use that action to remove the marker for the team. The action is unavailable while the Beacon block still exists.

Retaining known coordinates does not preserve destroyed endpoint services, revive endpoint identities or guarantee a safe arrival. Existing flight and site checks still apply.

## Remaining Scope

Team-scoped marker deletion is settled. No public or cross-team sharing feature follows from it. Exact Beacon naming, limits and coordinate mapping remain separate concerns.

Source: project-lead decision, 2026-09-17.

## Gameplay Flow

A player places a Beacon to return to a physical belt coordinate. Its marker remains on the Star Map while the Beacon exists, without a manual deletion option.

If the Beacon is destroyed, the team keeps the coordinate until a member chooses `Delete marker` from its context menu. Returning there still requires the usual flight and site checks, and any destroyed endpoint services remain unavailable.
