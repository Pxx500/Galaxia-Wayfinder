---
type: wayfinder-ticket
ticket_type: grilling
status: deferred
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Automation and Infrastructure]]"
blocked_by:
  - "[[Define Physical Station Room Ownership]]"
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Define Airlock Space Classification


## Scope

Deferred under [[Consolidate Physical Station Architecture]]. The existing room lifecycle remains the baseline. Side classification, geometry redesign and automatic leak detection are not selected for implementation.

[[Define Celestial Capability Rules]] owns the later accepted pressure rules. Those rules settle equalization and proven vacuum breaches, not the unresolved classification cases below.

## Question

How do airlock sides distinguish validated rooms, confirmed exterior and unresolved space, and what pressure behavior applies when an open side is unresolved?

## Constraints

- A structurally valid airlock is a geometric room boundary whether open or closed. Door state affects pressure, including when validation finishes, not geometry approval.
- Missing room membership is not proof of exterior. The far side may be an enclosed but unvalidated space.
- A search stopped at an airlock has not explored its far side.
- Distinct room counts cannot substitute for face coverage. A pillar can touch one room on several faces.
- Boundary-to-room dependencies identify affected approvals, not demonstrated leaks. Removing a shared wall differs from opening a room to exterior vacuum.

## Unaccepted Design Candidates

Side-aware relations could distinguish a validated room reference, confirmed exterior and unresolved space. Validation could establish room-side relations, while exterior classification would require reachability evidence. Dependent results would need invalidation when their supporting geometry changes. Neither this storage model nor a Station-wide geometry revision is selected.

A damage-origin six-face leak search could test the opening created by boundary damage using current airlock openness. Reaching a confirmed exterior margin would prove a leak. Finding a controller would not prove enclosure, and missing data or a work limit would be inconclusive. Events could be batched, but the search might still traverse all connected air space. Automatic leak detection would be an exception to the earlier manual-check direction and remains unapproved.

## Open Decisions

1. What happens to pressure when an open side is unresolved, including a closed unvalidated enclosure or temporarily missing data? An unresolved warning is proposed, but neither retention nor removal is selected.
2. Which player action recognizes an unassigned side? Does Validate inspect both sides?
3. What invalidates confirmed exterior classification after remote construction closes the space?
4. What happens to stored atmosphere when approval is invalidated without a proven route to exterior?

Immediate equalization between sealed joined rooms and immediate emptying through a proven vacuum breach are accepted. These do not settle unknown geometry or make missing room data proof of a leak.

## Provenance

Owner discussion on 2026-09-13, deferred on 2026-09-16. Later pressure decisions are in [[Define Celestial Capability Rules]]. [[Voxel Game Room Validation Research]] supplies comparison evidence, not adopted policy.
