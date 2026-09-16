---
type: review
status: in-progress
tags:
  - galaxia/alpha
---

# Physical Station PR 373 Review

## Active Takeover

The owner authorized taking over and finishing the PR after its author stepped away. The owner explicitly selected completing Auto-seal on 2026-09-16: loss of sealing closes the airlock and suppresses automatic reopening by redstone or proximity while the danger remains. The previous review draft will not be published as a message to the former author.

The owner clarified that manual opening overrides Auto-seal and must warn the player that opening towards vacuum will depressurize the room. Automatic controls remain blocked until the connected rooms are safe. The manual override lasts for that opening and resets when the door closes.

This execution keeps room detection and construction ownership unchanged. Door safety belongs to TileEntityAirlock, room sealing remains with TileStationBase, and Refresh uses the existing server-authoritative GUI interaction path. No new persistent service or room architecture is required.

Active execution checklist:

- [x] Integrate current master, preserve both branches' changes and replace the removed asset-deletion API. Conflict resolutions are staged and integrated compileJava succeeded. The merge is not committed yet
- [ ] Prove and implement Auto-seal through observable door behavior, including suppression of automatic reopening and recovery
- [ ] Make Refresh perform its server-side rescan and remove the unused parallel room-sync path
- [ ] Verify focused gameplay and GUI scenarios, the full GUI suite, agentVerify and Java analysis
- [ ] Record completed scope and remaining merge or publication requirements

Tests must protect player-visible door state or server acceptance of GUI actions through production interfaces. Do not expose private state or test source text. Existing master defects outside this scope remain separate unless they prevent the accepted behavior from working.

The review below is the pre-fix baseline, not the final state of the takeover.

## Scope and Verdict

Reviewed on 2026-09-16. Local verdict: changes needed before merge. No GitHub review, approval, comment, push or merge has been submitted.

- PR: [Airlock 2 electric bogaloo](https://github.com/GTNewHorizons/Galaxia/pull/373), authored by sbancuz
- PR head: `ecdba756e3f19705ca890b903d8a1c42afbf9151`
- Review merge base: `41711fe11934f8bcfdfb2530761c2cf61680e35b`
- Current target master: `7f66da49bb56775d00e5bf4ccfa49c0aacb30f1e`
- Diff: `git diff 41711fe1...ecdba756`, 26 files, 1694 additions and 127 deletions
- Review checkout: `C:/Users/Pxx500/Documents/GitHub/Galaxia/worktrees/review-physical-stations-373`

## Architectural Scope

The selected direction is owned by [[Consolidate Physical Station Architecture]]. This PR is the airlock and existing-room baseline, not the implementation of the later construction-centric Station design. Room-optimization proposals, manual-only validation and the new pressure-classification model are not merge requirements.

The PR keeps controller-owned room state and airlock-based StationGraph discovery. Controllers discover their geometry and register with airlocks. The graph aggregates connected controllers and attachments. Door changes mark room seal calculations dirty. The new GUI reads controller data and changes door settings through synchronized values. This description is evidence of current behavior, not endorsement of every ownership choice.

Keep the existing airlock construction, orientation, door controls and UI capabilities where correct. Do not replace them with the separate Station rework merely to resolve conflicts. No save migration or compatibility shim is proposed. Detailed future implementation plans and diagrams are omitted because this is a bounded review of an unchanged PR, not authorization for that redesign.

## Standards

### S1. Unused parallel airlock synchronization path

Non-blocking maintainability finding. `StationGraphSyncHandler` adds an airlock reference, room snapshots, collection and serialization, but the new `AirlockGUI` uses its own per-value room synchronization. No caller sets the handler's airlock reference or consumes `getRoomSnapshots()` in the reviewed source. The extra path expands the protocol and maintenance surface without serving the current UI.

Evidence: `core/network/StationGraphSyncHandler.java:110`, `:152`, `:216` and `registry/celestial/station/gui/AirlockGUI.java:144`. Graph discovery and repository text search both checked consumers, including Lombok-generated setter names. Recommend removing the unused branch, not adding another abstraction. Broader analyzer warnings are not automatically review defects.

## Behavior and Specification

No standalone originating specification or linked prerequisite was found in the PR body, comments or commit messages. Formal specification traceability is therefore unavailable. The findings below use the new controls' explicit user-facing promises and concrete code paths, not later Wayfinder requirements.

### R1. Auto-Seal On Leak Has No Runtime Behavior

Priority: P2. Merge-blocking recommendation.

The UI exposes an enabled-by-default setting whose tooltip promises automatic closing when either room loses its seal. The setting is synchronized and persisted, but no runtime path consumes it to close the airlock. `updateEntity()` handles redstone and proximity only. A player can enable the advertised protection without receiving it.

Evidence: `registry/celestial/station/gui/AirlockGUI.java:66`, `registry/celestial/station/TileEntityAirlock.java:65`, `:187`, `:225`, `:447`, `:470` and `assets/galaxia/lang/en_US.lang`.

The bounded remedy is either to remove the unavailable control or implement its promised behavior with an explicit precedence relative to redstone and proximity. This review does not choose that gameplay behavior on the owner's behalf.

### R2. Refresh Does Not Perform the Advertised Rescan

Priority: P2. Functional correction recommended before merge.

The tooltip promises to rescan for newly linked rooms. `StationButtonWidget.refreshButton()` only calls `GuiFactories.tileEntity().openClient(...)`. Reopening builds `AirlockGUI` again, but `TileEntityAirlock.buildUI()` does not request a structure check or rebuild room registrations. Existing synchronization may refresh the display, but this button does not cause the promised scan.

Evidence: `registry/celestial/station/gui/StationButtonWidget.java:58`, `registry/celestial/station/TileEntityAirlock.java:432`, and `assets/galaxia/lang/en_US.lang:695`.

Correct the server-side action or accurately scope the control to refreshing the display. This is independent of the deferred manual room-validation redesign.

### Existing Baseline Issue: Secondary Room Oxygen Updates

A newly joining secondary takes another controller's graph without receiving a backingStation reference. Its `tick()` returns before oxygen advancement when `getBackingStation()` is null. The PR replaces a potential null dereference with this return, but current master independently contains the same guard and missing lookup. This is not a new regression relative to the current merge target and is not used as an additional scope-expanding PR blocker.

Evidence: `registry/celestial/station/TileStation.java:218`, `:328`, `:417`, `:628` and comparison with `git diff 41711fe1..7f66da49 -- .../TileStation.java`. The eventual Station ownership integration must account for it. No in-game reproduction was performed in this review.

## Merge Readiness

GitHub reports `CONFLICTING`, `DIRTY` and `REVIEW_REQUIRED`. There are no submitted reviews or review threads. A read-only merge-tree check against current master confirms conflicts in:

- `.gitignore`
- `core/network/StationGraphSyncHandler.java`
- `registry/celestial/station/TileStation.java`
- `assets/galaxia/lang/en_US.lang`

There is also a semantic integration defect in a file that merges without a textual conflict. The PR adds `CelestialAssetStore.destroyAsset(assetId)` in `registry/celestial/station/Station.java:163`. Current master removed that API and routes synchronized deletion through `AssetStateSync.SERVER.destroyAsset`. The simulated merge tree retains the removed call. This must be reconciled and the integrated result built before merge. This is source-level evidence, not a claim that an integrated build was run.

The PR checklist says another PR is required before merge, but neither the body nor its only issue comment identifies it. That dependency is unresolved, not presumed fulfilled. GitHub permits squash merge, while a required independent review is still absent. Do not bypass either condition or submit public text without the owner's approval of its wording.

## Verification and Limits

- Reused the completed CI run for the exact unchanged PR head: [build and test](https://github.com/GTNewHorizons/Galaxia/actions/runs/34690030769), success
- Reused the completed PMD and IntelliJ audit for the unchanged review checkout. Both analyzers completed, PMD reported zero processing errors. Report: `C:/Users/Pxx500/AppData/Local/java-pmd-audit/reports/b108ca29-5868-4201-ad67-6a40d2663b70/audit.json`
- Rechecked the functional findings against current source and inspected the merge target differences
- The PR adds or changes no test files. Existing CI is not proof that these interactions work in game
- No client run, new test harness, source edit, conflict resolution, integrated build or new commit was performed
- Main, review and Station rework working trees were clean at the verification checkpoint

Review totals: one non-blocking Standards finding and two PR Behavior findings. The separate pre-existing oxygen issue is recorded as baseline debt. Merge conflicts, a removed API call, missing review approval and an unidentified declared dependency prevent claiming merge readiness.

## Review Disposition

Architecture consolidation is complete. The requested merge remains blocked. Production fixes and the choice of whether to implement or remove the unavailable auto-seal control require owner direction. Review publication requires approval of exact text. No deferred implementation specification is created here.
