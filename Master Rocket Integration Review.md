---
type: source
status: unreviewed
tags:
  - galaxia/alpha
  - wayfinder/source
---

# Master Rocket Integration Review

Source: Owner-requested read-only comparison of rocket-missions ea604929 against origin/master c6acaf0b, including https://github.com/GTNewHorizons/Galaxia/pull/387, https://github.com/GTNewHorizons/Galaxia/pull/389 and https://github.com/GTNewHorizons/Galaxia/pull/390
Imported: 2026-10-20

## Source Snapshot

The owner asked whether the newly merged rocket features overlap or conflict with the vehicle schedule and repair work. This intake records observed code differences and recommendations. It does not accept a new design decision or authorize changing existing Wayfinder decisions.

- PR 387 adds source-silo requested-item fulfillment, a separate global flight registry, fuel/staging/loadout calculations, assembler stock/recipes/UI, GT machine I/O and gantry/rendering changes
- Master automation targets one destination and tracks requested item delivery. It is not an ordered vehicle schedule with per-visit actions
- Returning master modules requires cargo to be empty and adds their definitions to assembler type-count stock. This differs from concrete identity, contents, wear and selective material-aware repair on the owner's branch
- Master and the owner's branch have different persistence, definition-key and entity handoff contracts. A merge-tree simulation reported 52 conflicted files, with additional semantic differences outside textual conflicts
- PR 389 adds useful orbit/station infrastructure, plus elevator motor-tier-3 travel to all registered Galaxia destinations. The universal teleport path bypasses rocket mission planning and needs explicit transport-policy consideration
- PR 390 adds shared GUI styling and improved Star Map windows. Most shared style API already matches the owner's branch
- The review recommends one persistent vehicle-owned schedule executor, with master rail/visual/I/O improvements integrated below it. A silo fulfillment feature could produce jobs through that same executor. This remains a recommendation, not an accepted decision
- An additional reload-during-crewed-ascent risk was identified by comparing serialization paths, but has not been reproduced in-game
- No production files were changed, no game/build was run, and no public GitHub communication was posted

The detailed local review is at ~/.agents/docs/Galaxia/worktrees/review-rocket-integration/docs/reviews/2026-10-20-master-rocket-overlap.md.

[[Sources]]
