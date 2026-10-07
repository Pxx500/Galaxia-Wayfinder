---
type: source
status: unreviewed
tags:
  - galaxia/alpha
  - wayfinder/source
---

# SiGe Engraving Recipe Research

Source: Pinned GT5/CoreMod source audit
Imported: 2026-10-07

## Source Snapshot

This intake records a bounded source investigation prompted by the owner's requirement that SiGe chips follow mandatory Laser Engraver processing, with an optional hydrochloric-acid wash afterward. It does not accept recipe balance or replace the owning decision.

### Verified Facts

The pinned GTNH pattern is blank wafer → engraved/patterned wafer → cut chips. Engraving does not ordinarily produce finished chips directly.

GT5-Unofficial revision: `000a4d9b24d77f40a79da7a105bb79ac7efca817`.

| Existing Recipe | Inputs and Output | Base Settings |
| --- | --- | --- |
| Early ILC engraving | Ordinary silicon wafer + reusable red lens → 1 ILC wafer | MV 120 EU/t, 60 s, no cleanroom requirement |
| HV ILC engraving | Phosphorus-doped silicon wafer + reusable red lens → 4 ILC wafers | HV 480 EU/t, 45 s, cleanroom required |
| Early CPU engraving | Ordinary silicon wafer + reusable white lens → 1 CPU wafer | MV 120 EU/t, 60 s, cleanroom required |
| HV CPU engraving | Phosphorus-doped silicon wafer + reusable white lens → 4 CPU wafers | HV 480 EU/t, 45 s, cleanroom required |

Primary sources: [ProcessingCrafting.java, ILC wafer recipes, lines 277–290](https://github.com/GTNewHorizons/GT5-Unofficial/blob/000a4d9b24d77f40a79da7a105bb79ac7efca817/src/main/java/gregtech/loaders/oreprocessing/ProcessingCrafting.java#L277-L290) and [CPU engraving, lines 423–437](https://github.com/GTNewHorizons/GT5-Unofficial/blob/000a4d9b24d77f40a79da7a105bb79ac7efca817/src/main/java/gregtech/loaders/oreprocessing/ProcessingCrafting.java#L423-L437).

Lens inputs use `GTUtility.copyAmount(0, aStack)`. The lens must be present but is not consumed. [GTRecipe.java, lines 520–545](https://github.com/GTNewHorizons/GT5-Unofficial/blob/000a4d9b24d77f40a79da7a105bb79ac7efca817/src/main/java/gregtech/api/util/GTRecipe.java#L520-L545) consumes items according to their recipe input amount, so zero-cost tool inputs are not deducted.

The `WaferEngravingRecipes` adapter adds early wafer recipes to the regular Laser Engraver map. Its special water handling identifies later Naquadah, Europium and Americium wafers or beamline masks. It does not impose that handling on every wafer. Source: [GTRecipeConstants.java, lines 351–409](https://github.com/GTNewHorizons/GT5-Unofficial/blob/000a4d9b24d77f40a79da7a105bb79ac7efca817/src/main/java/gregtech/api/util/GTRecipeConstants.java#L351-L409).

NewHorizonsCoreMod revision: `fe1a49ae577fee5ec4c1cf53d2545b475fb6b5af`.

- One ILC wafer cuts into eight ILC chips at 64 EU/t for 45 s, with no listed fluid or cleanroom requirement. Source: [CuttingMachineRecipes.java, lines 31–32](https://github.com/GTNewHorizons/NewHorizonsCoreMod/blob/fe1a49ae577fee5ec4c1cf53d2545b475fb6b5af/src/main/java/com/dreammaster/gthandler/recipes/CuttingMachineRecipes.java#L31-L32).
- One CPU wafer cuts into eight CPU chips at MV 120 EU/t for 45 s, requiring a cleanroom. Source: [CuttingMachineRecipes.java, lines 45–47](https://github.com/GTNewHorizons/NewHorizonsCoreMod/blob/fe1a49ae577fee5ec4c1cf53d2545b475fb6b5af/src/main/java/com/dreammaster/gthandler/recipes/CuttingMachineRecipes.java#L45-L47).
- HV NAND engraving uses a phosphorus-doped wafer and a reusable Ender Pearl lens, requiring a cleanroom for 45 s. This is another existing pattern, not a required SiGe ingredient. Source: [LaserEngraverRecipes.java, lines 102–108](https://github.com/GTNewHorizons/NewHorizonsCoreMod/blob/fe1a49ae577fee5ec4c1cf53d2545b475fb6b5af/src/main/java/com/dreammaster/gthandler/recipes/LaserEngraverRecipes.java#L102-L108).

### Reachable Lens Precedent

Ruby is defined with plate generation and red dye classification in [MaterialsInit1.java, line 578](https://github.com/GTNewHorizons/GT5-Unofficial/blob/000a4d9b24d77f40a79da7a105bb79ac7efca817/src/main/java/gregtech/loaders/materials/MaterialsInit1.java#L578).

The ordinary lens-generation branch takes one material plate and produces one lens, with small dust when that form exists, in an MV Lathe at 120 EU/t for 60 s. This supplies the Ruby plate-to-lens route without a later special lens. Source: [ProcessingLens.java, lines 67–81](https://github.com/GTNewHorizons/GT5-Unofficial/blob/000a4d9b24d77f40a79da7a105bb79ac7efca817/src/main/java/gregtech/loaders/oreprocessing/ProcessingLens.java#L67-L81).

The exquisite-gem route is an alternative, not a prerequisite for the proposed plate route. Ordinary Laser Engraver processing does not introduce an EBF coil-heat gate.

### Proposal, Not Accepted Recipe Balance

Use a reusable Ruby lens and keep the standard stage distinction:

1. Existing monocrystal cutting produces blank SiGe wafers.
2. Mandatory Laser Engraver processing changes a blank SiGe wafer into an engraved SiGe wafer.
3. An optional HCl wash follows engraving.
4. A Cutting Machine produces SiGe chips from the engraved wafer.
5. Existing proposed module packaging consumes those chips.

A candidate engraving setting is one blank SiGe wafer plus a non-consumed Ruby lens → one engraved SiGe wafer at HV 480 EU/t for 45 s. These settings are proposed, not accepted. Chip counts and wash benefits remain with the owner's balance decision.

A no-cleanroom SiGe recipe could follow the early ILC precedent, but that is an explicit content choice. The sources show that cleanroom requirements depend on the recipe. Neither HV voltage nor the phrase standard GTNH settles that choice alone.

The inspected standard wafer recipes do not establish the optional HCl wash. It needs a stated benefit and a viable unwashed path. It must not replace mandatory engraving.

This engraving investigation does not fix Ge yield, blend ratios, seed chance or PolySiGe yield. In particular, it does not carry forward earlier powder-return or eight-dust bootstrap proposals.

### Verification Scope

The investigation read exact pinned revisions using local `git show` and `git grep`, not current checkout line ranges. A graph lookup returned no `ProcessingCrafting` node, so pinned source reads supplied the evidence. No builds or production edits ran. The links above identify those same immutable revisions.

[[Sources]]
