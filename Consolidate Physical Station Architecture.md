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

Which parts of the construction-centric Station design and the existing physical Station implementation remain the working direction while room-optimization work is paused?

## Owner Direction

On 2026-09-16 the owner requested consolidation, pausing room optimization and leaving the existing room implementation in place for now. At that time the work was to review the existing physical-stations PR, merge it if ready, then potentially continue the separate Station work. The PR has since merged as recorded below.

## Resolution Status

Architecture consolidation completed on 2026-09-16. This resolved status records the selected responsibilities and deferred scope. The owner subsequently merged PR 373 into Galaxia master as `b1e42710`. [[Physical Station PR 373 Review]] preserves the review findings and verification history, not a current instruction to reopen the merged PR. The merge does not mark the separate construction-centric Station rework as implemented.

## Consolidated Direction

| Responsibility | Working direction | Owning decision or evidence |
| --- | --- | --- |
| Station identity and construction membership | Keep the construction-centric Station model. Controllers and internal or external functional devices belong to the connected construction rather than requiring a room-to-airlock chain | [[Resolve Physical Station Controller Succession]] |
| Device connectivity and optimization | Keep the connected path witness, batched invalidation and last confirmed service state during recalculation. Paths prove connections between registered functional points rather than discovering unknown devices | [[Define Physical Station Change Tracking]] |
| Physical room ownership | Retain the accepted requirement that multiple controllers do not duplicate a single physical room's environmental state or cost | [[Define Physical Station Room Ownership]] |
| Room discovery and validation implementation | Retain the existing bounded geometry-checking approach for this stage. Do not replace it with scanline traversal, wall-surface tracing, a new air-space index or a background validation pipeline as part of this integration | Reviewed PR code |
| Airlock mechanics and Station attachments | Preserve the existing airlock construction, door controls and GUI capabilities, and existing device/resource integrations where compatible with their actual contracts. Concrete defects still require review | [[Physical Station PR 373 Comparison and Room Separation Proposal]] |

Construction membership, room geometry and pressure connectivity remain separate responsibilities. Keeping the current room implementation temporarily does not select airlock registrations as the long-term source of Station membership.

## Deferred Room Redesign

The manual-only approval lifecycle, expanded airlock-side classification and validation-recovery questions are parked, not resolved. Their earlier decisions and proposals remain historical context in the owning notes. They are not additional acceptance criteria for Bankuz's existing PR. The current validation lifecycle remains the baseline for this stage, without declaring the earlier manual-only direction permanently rejected.

No requirement to prohibit shared walls or ceilings was accepted. Room separation through scaffolding and surface-only room detection remain unselected proposals. No new optimization or measured performance claim follows from this consolidation.

Deferred owning notes:

- [[Define Manual Physical Room Validation]]
- [[Define Airlock Space Classification]]
- [[Define Physical Room Validation Recovery]]

## Integration Boundary

The PR was reviewed for the behavior it added, not for implementing the later construction-centric redesign. Its merge does not certify that the separate local Station rework is integrated into master. These efforts retain distinct scope.

The owner authorized review and merge, subject to readiness, and subsequently reported the merge. Historical CI results alone were not merge authority. Public communication still requires approval of its exact wording under project policy.

## Provenance

[[Physical Station PR 373 Comparison and Room Separation Proposal]] was reviewed during this consolidation. Its suggestions are not independently accepted requirements. The owner direction above determines the current scope.
