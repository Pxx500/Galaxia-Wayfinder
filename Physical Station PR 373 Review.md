---
type: review
status: archived
tags:
  - galaxia/alpha
---

# Physical Station PR 373 Review

Historical review and completion record for [Airlock 2 electric bogaloo](https://github.com/GTNewHorizons/Galaxia/pull/373). The owner merged it as `b1e42710`, recorded in [[Consolidate Physical Station Architecture]]. Earlier conflicts, pending review and publication states are no longer active blockers.

## Accepted Airlock Behavior

- Auto-seal closes an airlock when a connected room loses its seal. Redstone and proximity cannot automatically reopen it while unsafe
- Manual opening overrides Auto-seal for that opening and warns the player that opening towards vacuum will depressurize the room. Closing clears the override
- Refresh requests a server-side airlock check and room updates, not just a reopened GUI
- Successful room checks renew airlock registrations, allowing a replacement airlock to reconnect without dismantling a valid room

These changes retained the existing room-detection and construction-ownership model. They did not implement the separate construction-centric Station rework or the deferred airlock-side classification redesign.

## Completed Corrections

The takeover implemented the previously inert Auto-seal setting, server-authoritative Refresh and removal of an unused parallel room-sync path. Follow-up corrections covered narrow-doorway proximity, inventory metadata during survival construction, resuming construction past valid panels and client controller-state synchronization.

Door broad faces retained connected textures. Thin edges reused the existing airlock casing texture, with texture matching based on the rendered face.

## Dated Evidence And Limits

The September 2026 completion record reports passing focused physical-station client scenarios, `agentVerify`, PMD and IntelliJ analysis. Behavior defects were reproduced before their fixes. This note does not certify the current checkout.

A pre-existing secondary-controller path could lack its backing Station and skip oxygen updates. It was outside the bounded PR fixes and was not reproduced in game during the original review. Check current code before treating it as an open defect.

## Related Decisions

- [[Consolidate Physical Station Architecture]]
- [[Resolve Physical Station Controller Succession]]
- [[Physical Station Rework Execution]]
- [[Physical Station PR 373 Comparison and Room Separation Proposal]] preserves the earlier source discussion
