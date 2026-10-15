---
type: wayfinder-ticket
ticket_type: task
status: resolved
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Automation and Infrastructure]]"
blocked_by: []
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/task
---

# Consolidate Physical Station Architecture


## Question

Which construction-centric Station responsibilities remain the working direction while room optimization is paused?

## Resolution

Keep the construction-centric Station model, but retain the existing room implementation and validation lifecycle for this stage. Consolidation was accepted on 2026-09-16.

| Responsibility | Direction | Owner |
| --- | --- | --- |
| Identity and construction membership | Controllers and functional devices belong through face-connected construction, not a room-to-airlock chain | [[Resolve Physical Station Controller Succession]] |
| Device connectivity | Connected path witness, batched invalidation and last confirmed service state during recalculation | [[Define Physical Station Change Tracking]] |
| Room ownership | One physical room has one environmental state and cost even with several controllers | [[Define Physical Station Room Ownership]] |
| Room discovery | Retain bounded geometry checking rather than introduce a new traversal, air-space index or background pipeline | Existing room implementation |
| Airlocks and attachments | Preserve door controls, GUI and device/resource integrations under their actual contracts | [[Physical Station PR 373 Comparison and Room Separation Proposal]] |

Construction membership, room geometry and pressure connectivity remain distinct. Keeping the room implementation does not make airlock registrations the long-term membership authority. Connectivity paths join registered functional points, not discover unknown devices.

## Deferred Scope

- [[Define Manual Physical Room Validation]]
- [[Define Airlock Space Classification]]
- [[Define Physical Room Validation Recovery]]

These retain earlier decisions and proposals without requiring the redesign now. No shared-wall or shared-ceiling prohibition, scaffolding-based room separation, surface-only detection or measured optimization claim is accepted.

Later pressure decisions in [[Define Celestial Capability Rules]] do not settle deferred geometry or recovery questions.

## Implementation Boundary

Physical Station PR 373 merged into master as `b1e42710`. Its merge does not establish integration of the separate construction-centric rework. [[Physical Station PR 373 Review]] preserves historical review evidence.

The comparison note supplies proposals and evidence, not independent authority to add requirements.
