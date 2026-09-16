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

## Current Scope

Deferred on 2026-09-16 under [[Consolidate Physical Station Architecture]]. Do not add a new side-classification or pressure model to the current PR integration. Preserve this discussion without treating its unanswered questions as resolved or its proposed representation as implemented. Existing-code defects are reviewed separately from this deferred redesign.

## Question

How do airlock sides identify validated rooms, confirmed exterior space and unresolved space, and what pressure behavior applies when an open side is unresolved?

## Accepted Constraints

- Opening or closing a structurally valid airlock does not invalidate room geometry. Pressure behavior uses the current door state, including when a geometry validation finishes.
- A missing room assignment is not proof of exterior space. The far side may be an unvalidated but enclosed space.
- A room search stopped by a geometric airlock boundary has not automatically explored the space beyond that boundary.
- A pillar can touch the same room on several faces. Room-count and adjacent-air-count equality is not a reliable classification rule.

## Proposed Representation

Awaiting final confirmation of the behavior, not a settled storage format:

- Identify each airlock's two physical sides and relate them to known room boundaries.
- Represent a side as a validated room reference, confirmed exterior or unresolved space. Keep a closed but unvalidated enclosure unresolved unless a distinct gameplay status is selected.
- Known room-side relations come from validation reaching the airlock from that side. Exterior classification needs a separate reachability result, not an absent room ID.
- Invalidation removes or invalidates relations that depended on the affected approval. Stale results must not remain authoritative indefinitely.

## Open Decisions

1. What happens to pressure when an open airlock leads to unresolved space? This includes a closed but unvalidated neighboring room and temporarily missing data.
2. What player action requests recognition of an unassigned airlock side? Does room Validate include checking the other side, or is there a separate explicit action?
3. What invalidates a previously confirmed exterior result when remote construction closes that space? A Station-wide geometry revision was proposed as a conservative mechanism, not accepted as a final policy.
4. What happens to stored atmosphere when a room approval is invalidated without a proven route to exterior? Geometry invalidation and physically demonstrated venting must not be silently equated.

## Recommendation Awaiting Owner Approval

An open unresolved side should prevent claiming that the connected space can maintain pressure and should display a clear unresolved-space warning. It must not be falsely labelled confirmed exterior. Whether atmosphere is immediately removed, retained or evolves while unresolved needs a separate explicit rule.

## Latest Exploratory Proposal: Damage-Origin Leak Search

Status: not accepted. The owner suggested searching from a destroyed boundary position toward a controller or the exterior box. The assistant proposed refining this into a separate automatic leak check. The owner remained unsure and requested recording the discussion, not implementation.

- Start a six-face air-space search at the opening created by boundary damage.
- Reaching a confirmed exterior margin establishes an escape route. Finding a controller does not establish enclosure because the controller's space may itself have another opening.
- Exhausting the reachable space without exterior access establishes no escape route only for complete, current geometry data. Missing data or a search limit is inconclusive.
- Unlike geometric room validation, a leak search would use current airlock openness. An open airlock permits airflow, while a closed airtight airlock blocks it.
- Group related destruction events rather than starting one search per destroyed block. Such a search can still cover the entire connected air space. It is not guaranteed to be cheap or local.
- This proposal would make leak detection automatic while room creation and reapproval remain manual. That is an exception to the earlier manual-check direction and needs explicit owner approval.

No pressure update rate, atmosphere-loss rule, unresolved-result behavior or automatic leak-search requirement has been accepted. Do not implement this candidate or treat it as the chosen solution on the strength of this note.

## Concrete Cases To Resolve

- Removing a wall between two otherwise enclosed rooms invalidates the old boundary description but does not alone prove an escape route to exterior.
- Removing a wall from a room to confirmed exterior changes both geometry and exterior reachability.
- Removing a wall to an unvalidated space cannot be classified by absent room IDs alone.
- The boundary-to-room index identifies affected approvals. It is not, by itself, a proof of depressurization.

## Provenance

Owner discussion on 2026-09-13. The last assistant proposal described side relations and a geometry revision, but the owner requested consolidation before accepting the outstanding behavior. Do not turn those proposals into approved gameplay by recording them here.

Research comparison: [[Voxel Game Room Validation Research]]. Its archived and 2D implementations are evidence, not adopted behavior.
