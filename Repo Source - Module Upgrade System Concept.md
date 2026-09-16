---
type: source
status: unreviewed
origin: "Repository docs/generic-module-upgrade-system-proposal.md"
imported: 2026-08-01
tags:
  - galaxia/alpha
  - wayfinder/source
  - galaxia/automation
---

# Repo Source - Module Upgrade System Concept

Source: repository proposal `docs/generic-module-upgrade-system-proposal.md`
Imported: 2026-08-01

All proposed Java APIs, builder syntax, migration stages, network encoding choices, and implementation sequencing were intentionally discarded. This snapshot preserves the product and domain contract proposed for module upgrades.

## Source Snapshot

### Concept

Module definitions should describe their available upgrade paths in a uniform way so modules with different semantics can share one player-facing upgrade workflow. Domain-specific behavior remains with the module, while generic presentation and operation planning consume the declared path.

### Requirements

- An upgrade path has a stable identity and one or more typed axes.
- Each axis exposes allowed levels and the module's current and selected target values.
- One confirmation may change multiple related axes as one operation.
- The path supplies material cost, build duration, refunds, labels, and effect summaries.
- Dependencies between axes can disable invalid combinations without hard-coding one module type into the generic workflow.
- Opening the interface selects the current state, not an implicit next upgrade.
- Confirmation is available only when the target differs from the current state and satisfies all rules.
- A module may eventually expose multiple paths, even if the first usable version presents only one.
- Generic infrastructure does not replace module-specific rules for applying an upgrade or explaining specialized effects.

### Open Decisions

- Whether Alpha needs this generic contract or only specific module upgrades.
- Whether multiple paths must be selectable in the first player-facing version.
- Whether costs belong to individual axis levels, complete target selections, or both.
- How dependent axes should be presented to the player.
- Which upgrade effects and constraints are stable product rules rather than implementation choices.


## Intake

- [[Sources]]
