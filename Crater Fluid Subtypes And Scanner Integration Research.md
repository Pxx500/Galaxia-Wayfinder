---
type: source
status: unreviewed
tags:
  - galaxia/alpha
  - wayfinder/source
---

# Crater Fluid Subtypes And Scanner Integration Research

Source: Local source inspection of GT5-Unofficial, NotEnoughItems, and VisualProspecting for the Galaxia crater discussion
Imported: 2026-09-16

## Source Snapshot

### Question And Scope

The user prefers one enriched-fluid family with subtypes. NBT is a possible representation, not a chosen one. This does not settle whether there is one universal input-fluid recipe. Processing should use ordinary GregTech machines and recipe maps. Craters should be discoverable with existing scanners only while the player is within the crater footprint. Discovery record refresh belongs to the scanner and map integration, not a new Galaxia refresh policy.

This is a bounded source check, not a design decision, implementation plan, or runtime verification. No builds or tests were run. No repository files were changed.

Inspected local checkout HEADs:

| Repository | HEAD |
| --- | --- |
| GT5-Unofficial | `200352fef4bf48893e1d7c06bd66381e5cf56d70` |
| NotEnoughItems | `f55dc716e3879f8877b79a0dd9a221907ada33dc` |
| VisualProspecting | `0221c742f545bf9778c6b78b147e7c5e71ef7a24` |

All three checkouts had empty `git status --short` output when checked. These are local source revisions. Galaxia's resolved dependency versions and the user's installed runtime versions were not checked and must not be assumed to match them.

### NEI Fluid Lookup

1. The default GT recipe-map NEI handler searches outputs in `loadCraftingRecipes` and inputs in `loadUsageRecipes`. Both expand a clicked fluid/container through `addFluidStacks`, then use `recipe.contains` over cached displayed stacks. Recipe fluid inputs and outputs are converted into GT fluid display items. See [GTNEIDefaultHandler.java](C:/Users/Pxx500/Documents/GitHub/GT5-Unofficial/src/main/java/gregtech/nei/GTNEIDefaultHandler.java:282), lines 282–303, 349–353, 815–862, and 898–921.

2. The display conversion does not retain arbitrary `FluidStack.tag`. `getFluidDisplayStack` uses the fluid registry ID as item damage and writes amount, heat, gas state, visibility, and an optional material name into a new tag. The reverse conversion reconstructs a `FluidStack` from the fluid ID and amount only. See [GTUtility.java](C:/Users/Pxx500/Documents/GitHub/GT5-Unofficial/src/main/java/gregtech/api/util/GTUtility.java:1227), lines 1227–1265.

3. Default NEI membership matching ignores NBT. `CachedRecipe.contains` delegates to `PositionedStack.contains`, which uses `areStacksSameTypeCrafting`. That comparator checks item identity and damage, with wildcard/damageable exceptions, not tags. See [TemplateRecipeHandler.java](C:/Users/Pxx500/Documents/GitHub/NotEnoughItems/src/main/java/codechicken/nei/recipe/TemplateRecipeHandler.java:212), lines 212–225, [PositionedStack.java](C:/Users/Pxx500/Documents/GitHub/NotEnoughItems/src/main/java/codechicken/nei/PositionedStack.java:170), lines 170–182, and [NEIServerUtils.java](C:/Users/Pxx500/Documents/GitHub/NotEnoughItems/src/main/java/codechicken/nei/NEIServerUtils.java:198), lines 198–205.

Source-backed consequence: if several recipes differ only by NBT on the same registered fluid, the inspected default GT NEI path does not distinguish those subtypes for either recipe or usage lookup. Clicking one can collect recipes for the other same-fluid variants. This supports the user's concern, but does not establish a particular recipe count.

NEI has explicit `containsWithNBT` methods, but the inspected GT default handler does not use them. Using those methods alone would not restore fluid tags already discarded by the display conversion. This is an existing mechanism, not proof of ready-made GT fluid-subtype support.

### Runtime Recipe Matching Is A Separate Limitation

The runtime fluid lookup key stores only a `Fluid` reference and compares that reference by identity. See [GTFluidLookupIngredient.java](C:/Users/Pxx500/Documents/GitHub/GT5-Unofficial/src/main/java/gregtech/api/recipe/lookup/GTFluidLookupIngredient.java:11), lines 11–35.

The default recipe backend validates candidates with `isRecipeInputEqual`. That delegates to `maxParallelCalculatedByInputs`, whose fluid calculation aggregates supplied quantities by `Fluid` reference and compares alternatives by `alt.getFluid()`. Arbitrary fluid tags are not part of that calculation. See [RecipeMapBackend.java](C:/Users/Pxx500/Documents/GitHub/GT5-Unofficial/src/main/java/gregtech/api/recipe/RecipeMapBackend.java:562), lines 562–570, and [GTRecipe.java](C:/Users/Pxx500/Documents/GitHub/GT5-Unofficial/src/main/java/gregtech/api/util/GTRecipe.java:531), lines 531–543 and 667–716.

Consumption separately calls `FluidStack.isFluidEqual` at lines 568 and 600. This is a different path from candidate acceptance. The check did not run a tagged-fluid recipe or prove the resulting machine behavior. The safe conclusion is that transparent NBT-only subtype support for ordinary GT recipe maps is not established by the current code, independently of the NEI limitation.

GT's `nbtSensitive()` setting is consumed by item input matching in `RecipeItemInput`. The inspected fluid quantity calculation does not use it. See [GTRecipeBuilder.java](C:/Users/Pxx500/Documents/GitHub/GT5-Unofficial/src/main/java/gregtech/api/util/GTRecipeBuilder.java:671), lines 671–674, and [GTRecipe.java](C:/Users/Pxx500/Documents/GitHub/GT5-Unofficial/src/main/java/gregtech/api/util/GTRecipe.java:994), lines 994–1011. `SubstituteFluidStack` supports alternative fluids with individual quantities, not a demonstrated NBT-subtype identity contract. See [SubstituteFluidStack.java](C:/Users/Pxx500/Documents/GitHub/GT5-Unofficial/src/main/java/gregtech/api/objects/SubstituteFluidStack.java:20), lines 20–49. No representation is selected by this research.

### Scanner, Discovery Cache, And Depletion Ownership

Detrav in GT5 owns handheld scan activation and its scan result. Its electric scanner sends its own packet, then asks VisualProspecting for ore-vein records within the scanner radius and asks VisualProspecting to deliver them to the player. That VP handoff is not a crater-footprint query or an ore-depletion update. See [BehaviourDetravToolElectricProspector.java](C:/Users/Pxx500/Documents/GitHub/GT5-Unofficial/src/main/java/detrav/items/behaviours/BehaviourDetravToolElectricProspector.java:144), lines 144–169.

VisualProspecting owns the inspected record/cache pipeline:

- `ServerCache.prospectOreChunks` enumerates cached ore-vein records. The radius method converts the query into chunk bounds. See [ServerCache.java](C:/Users/Pxx500/Documents/GitHub/VisualProspecting/src/main/java/com/sinthoras/visualprospecting/database/ServerCache.java:85), lines 85–121.
- `DimensionCache.putOreVein` decides whether a record is new, may overwrite an existing source, replaces a changed vein type, and retains depletion state during replacement. Identical type/source records return `AlreadyKnown`. See [DimensionCache.java](C:/Users/Pxx500/Documents/GitHub/VisualProspecting/src/main/java/com/sinthoras/visualprospecting/database/DimensionCache.java:400), lines 400–431.
- `ClientCache.putOreVeins` writes incoming discoveries and posts prospecting events for changed records. The client depletion toggle updates the record and sends `VeinDepletionMessage`. See [ClientCache.java](C:/Users/Pxx500/Documents/GitHub/VisualProspecting/src/main/java/com/sinthoras/visualprospecting/database/ClientCache.java:75), lines 75–100.
- `TeamProspectionDispatcher` delivers discoveries, records newly discovered entries, and shares them with online teammates when enabled. Its separate depletion handler accepts toggles only for discovered team veins and broadcasts changed depletion state. See [TeamProspectionDispatcher.java](C:/Users/Pxx500/Documents/GitHub/VisualProspecting/src/main/java/com/sinthoras/visualprospecting/teams/TeamProspectionDispatcher.java:36), lines 36–107.

Thus existing source places scanner activation in GT5/Detrav and discovery-record update, notification, persistence-dirty marking, and depletion sharing in VisualProspecting. This is an observed division, not a new Galaxia freshness rule. Rescanning through the inspected VP ore path returns cached ore records, so it should not be described as an automatic physical ore-depletion resurvey.

### Custom Crater Integration Boundary

The inspected VP API offers `notifyOreGeneration` for a named vein type and `sendProspectionResultsToClient` for existing ore/fluid result types. `VeinTypeCaching` builds the known vein types from GregTech `OreMixes`. Unknown names resolve to `NO_VEIN`. `OreVeinPosition` stores dimension, normalized center ore-chunk coordinates, vein type, depletion, and source, not crater footprint or arbitrary crater data. See [VisualProspecting_API.java](C:/Users/Pxx500/Documents/GitHub/VisualProspecting/src/main/java/com/sinthoras/visualprospecting/VisualProspecting_API.java:89), lines 89–106, [VeinTypeCaching.java](C:/Users/Pxx500/Documents/GitHub/VisualProspecting/src/main/java/com/sinthoras/visualprospecting/database/veintypes/VeinTypeCaching.java:34), lines 34–50 and 68–70, and [OreVeinPosition.java](C:/Users/Pxx500/Documents/GitHub/VisualProspecting/src/main/java/com/sinthoras/visualprospecting/database/OreVeinPosition.java:21), lines 21–36.

Galaxia-specific crater data and the only-inside-footprint scan condition still require integration work. This research does not select a hook, result format, refresh policy, or repository allocation for that work. It does not claim that every possible extension API was audited.

### Evidence Limits

Graph-first discovery was used. Coverage metadata reported changed files and, for GT5, unavailable per-file coverage, so relevant matching and cache methods were checked directly in the local source. The findings apply to the default paths described above, not every custom handler or machine. Runtime behavior, rendering, version compatibility, and the exact Galaxia dependency graph remain unverified.

[[Sources]]
