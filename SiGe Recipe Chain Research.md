---
type: source
status: unreviewed
tags:
  - galaxia/alpha
  - wayfinder/source
---

# SiGe Recipe Chain Research

Source: Owner-approved scope and local GT5-Unofficial / NewHorizonsCoreMod source audit at pinned revisions
Imported: 2026-10-07

## Source Snapshot

This is a concrete proposal to react to, not accepted recipes or an implementation plan. First space is HV. Rocket automation remains optional before Luna. SiGe crystal growth requires microgravity. The resulting electronics serve both Rocket upgrades and satellites. Final electronics assembly need not happen in space.

### Provenance and Limits

GT5 baseline: `000a4d9b24d77f40a79da7a105bb79ac7efca817`. CoreMod baseline: `fe1a49ae577fee5ec4c1cf53d2545b475fb6b5af`. Local HEADs differ, so the audit used `git show` and `git grep` against those exact commits. Graph and Context Mode tools were unavailable in this subagent session. No builds ran. Recipe presence and recipe-map fit are source-verified, not a tested playable pack.

`Materials.SiliconSG` means **Silicon Solar Grade (Poly SI)**. It does not mean silicon-germanium or semiconductor-grade silicon. GT++ already registers Germanium as a generated solid material and exposes its molten fluid and dust forms. Reuse that material.

### Existing Feedstock Recipes

The following are existing recipes, not proposed additions. Durations below are base recipe times before machine overclocking. Cells and integrated circuits are containers/selectors, not unexplained consumed reagents.

| Process | Inputs → outputs | Machine, power, duration |
| --- | --- | --- |
| Silica | 8 sand → 3 silicon-dioxide dust | Electrolyzer, 25 EU/t, 25 s |
| Silicon | 3 silicon-dioxide dust + 2 carbon dust → 1 silicon ingot + 2,000 mB carbon monoxide, 11.11% ash | EBF, 120 EU/t, 4 s, 1,200 K |
| Chlorination | 1 silicon dust + 4,000 mB chlorine, selector 2 → 1,000 mB silicon tetrachloride | Chemical Reactor, 30 EU/t, 20 s |
| Solar-grade purification | 4 sodium dust + 1,000 mB silicon tetrachloride, selector 1 → 1 solar-grade silicon dust + 8 salt dust | Chemical Reactor, 30 EU/t, 5 s |
| Salt separation | 2 salt dust → 1 sodium dust + 1,000 mB chlorine | Electrolyzer, 30 EU/t, 16 s |
| Carbon | 1 graphite dust → 4 carbon dust | Electrolyzer, 64 EU/t, 5 s |
| Washing | 1 crushed sphalerite + 1,000 mB water → 1 purified crushed sphalerite + stone dust and chance byproduct | Ore Washer, 16 EU/t, 25 s |
| Water separation | 1,000 mB water → 2,000 mB hydrogen + oxygen cell | Electrolyzer, 30 EU/t, 100 s |
| Sulfur oxidation | 1 sulfur dust + 2,000 mB oxygen, selector 3 → 1,000 mB sulfur dioxide | Chemical Reactor, 8 EU/t, 3 s |
| Further oxidation | 1,000 mB sulfur dioxide + oxygen cell, selector 1 → 1,000 mB sulfur trioxide + empty cell | Chemical Reactor, 30 EU/t, 10 s |
| Acid | 1,000 mB sulfur trioxide + water cell, selector 1 → 1,000 mB sulfuric acid + empty cell | Chemical Reactor, 8 EU/t, 16 s |

Macerate silicon ingots into dust for chlorination. Salt, sulfur, graphite, sphalerite, sand, copper and tin are starting-world feedstocks, not space materials. Copper plates and fine wire use ordinary metal-working recipes. Tin has molten form and no blast-furnace requirement. No argon, helium, hydrogen, gallium-arsenide seed, purified-water tier, SMD component or later circuit is needed by the proposed new chain.

The existing germanium route remains unchanged: purified crushed sphalerite ×1 + carbon dust ×4 + sulfuric acid 250 mB + selector 15 → molten germanium 36 mB, **Alloy Blast Smelter, 4,000 EU/t, 37.5 s**, IV. Do not lower it to HV.

### Proposed Complete New Subchain

Every row below is invented gameplay content. Quantities model progression and batching, not exact industrial chemistry. Only growth has the environmental requirement.

| Step | Inputs → outputs | Machine, power, duration |
| --- | --- | --- |
| Low-yield Ge bootstrap | 1 purified crushed sphalerite + 4 carbon dust + 250 mB sulfuric acid → 4 mB existing molten germanium | HV Chemical Reactor, 480 EU/t, 30 s |
| Blend | 7 solar-grade silicon dust + 144 mB molten germanium → 8 SiGe blend dust | MV Mixer, 120 EU/t, 20 s |
| Grow | 8 SiGe blend dust → 1 SiGe crystal boule | HV-powered EBF, 480 EU/t, 120 s, 1,784 K, **microgravity required** |
| Cut | 1 SiGe crystal boule + 100 mB ordinary water → 16 SiGe wafers | MV Cutting Machine, 120 EU/t, 40 s |
| Process wafers | 1 SiGe wafer + 250 mB hydrochloric acid → 4 SiGe chips | HV Chemical Bath, 480 EU/t, 30 s |
| Package | 4 SiGe chips + 2 copper plates + 8 fine copper wires + 144 mB molten tin → 1 SiGe control module | HV Assembler, 480 EU/t, 30 s |

The Ge bootstrap deliberately has no selector circuit. The single-block Chemical Reactor has two item input slots, already occupied by sphalerite and carbon. Copying the ABS selector would create a reachable machine-capacity blocker.

Hydrochloric acid already has an 8 EU/t, 3 s Chemical Reactor recipe from 1,000 mB hydrogen and a chlorine cell, producing 1,000 mB acid and the empty cell. Hydrogen comes from ordinary water electrolysis. This avoids inventing another etchant chain.

Five new item forms carry distinct player-visible operations: blend, boule, wafer, chip, module. No new chemical fluids or Ge intermediates. Wafer processing is deliberately an abstract combined chip-fabrication operation. It must not be described as physically accurate etching, lithography or industrial semiconductor manufacture.

The module is a **Galaxia-specific reusable recipe ingredient**, not an ore-dictionary circuit-tier replacement. Proposed allocation: one module for the first Rocket control upgrade and one per upgraded satellite's electronics package. The cheaper opening satellite remains on its existing starting-world contract and doesn't require this module. Specialty fluoride optical fibers belong to satellite production, not the first Rocket upgrade.

### Yield, Bottlenecks and Reachable Blockers

One growth batch needs 144 mB Ge. The new route needs **36 purified sphalerite**, 144 carbon dust and 9,000 mB sulfuric acid. It occupies a single HV reactor for 18 minutes before overclocking. The IV ABS needs **4 purified sphalerite**, 16 carbon dust and 1,000 mB acid, taking 150 seconds. Its Ge yield per ore and reagent is nine times better, and its base throughput is 7.2 times better. Energy is approximately 10.37 million EU early versus 12 million EU ABS per batch, so the proposal rewards upgrading through throughput and resource efficiency, not energy efficiency.

A batch gives 16 wafers, 64 chips and **16 modules**. Each module amortizes 2.25 purified sphalerite, 9 carbon dust, 562.5 mB sulfuric acid and 7/16 solar-grade silicon dust. Wafer acid and packaging materials add their listed costs. A first upgrade therefore doesn't require an entire boule to be consumed, and surplus modules encourage satellites without forcing automation before Luna.

The concrete technology floor is working HV plus an ordinary EBF meeting 1,784 K. The existing MV silicon-boule recipe already uses that heat, so the proposal doesn't secretly demand higher-grade coils. It does not use the ordinary GaAs-seeded silicon boule as input, and SiGe chips never become ordinary GT chips.

The real unmet capability is enforcing **microgravity on the EBF growth recipe**. Existing recipe-map compatibility doesn't prove environmental enforcement. A registered recipe with an inert metadata flag is insufficient. This needs the shared Galaxia capability rule, not a copied orbital-location gate or another processing machine by default. Other steps may run on the starting world.

Early Ge doesn't remove gates on existing Ge consumers. Abyssal Alloy and Arceus Alloy retain their other inputs and high-tier processing. No recipes, generated alloy tiers or circuit substitutions are changed. Their full progression audit belongs with the broader Ge-consumer audit, not an assertion that mere early Ge access is harmless.

### Primary Source Anchors

- GT5 `gregtech/loaders/postload/recipes/{ElectrolyzerRecipes,BlastFurnaceRecipes,ChemicalRecipes,CuttingRecipes}.java` at the pinned commit, especially EBF lines 223–232 and 385–395, electrolyzer lines 26–35, 94–100, 107–114 and 227–234, chemical recipes around 680–746 and 2,900–3,085
- GT5 `gregtech/loaders/materials/MaterialsInit1.java:696` identifies SiliconSG, and `gregtech/loaders/oreprocessing/ProcessingDirty.java:64–80` supplies ore washing
- GT5 `gtPlusPlus/core/recipe/RecipesGregTech.java:860–870` supplies the unchanged IV Ge route, `gtPlusPlus/core/item/ModItems.java:257` registers Germanium generation, and `gtPlusPlus/core/material/MaterialsElements.java:57` defines the material
- GT5 `gregtech/api/recipe/RecipeMaps.java` declares the Mixer, Chemical Bath and Chemical Reactor input/output capacities used here. Existing cutter water variants and assembler molten-solder recipes provide precedent, not existing SiGe recipes
- CoreMod pinned `BlastFurnaceRecipes.java:659` and `ChemicalBathRecipes.java:87` concern solar-grade silicon ingots. Neither is necessary here. CoreMod `VacuumFurnaceRecipes.java:44–45` contains later Ge recovery, not the opening route

[[Sources]]
