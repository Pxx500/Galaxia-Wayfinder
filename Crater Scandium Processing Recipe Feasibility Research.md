---
type: source
status: unreviewed
tags:
  - galaxia/alpha
  - wayfinder/source
---

# Crater Scandium Processing Recipe Feasibility Research

Source: Primary GT5-Unofficial and NewHorizonsCoreMod source, plus the owner's accepted conceptual process
Imported: 2026-10-11

## Source Snapshot

Read-only evidence for recipe authoring, not approval of quantities, machines or costs. Agent Briefing and the relevant machinery/ownership sections were read. Both repositories were fully reindexed. Local GT was `2259bc64244f9f7fc58e039d8e89ca40dd17c929`. Checked immutable upstream GT source is `2856a652b29ecf17dd5529880d589bea92a83b9f`. CoreMod was clean at `38b12ce3d59f8061742e47a63c6f1f29b7959313`. Cited raw files returned HTTP 200. [GT revision][gt-revision] [CoreMod revision][core-revision]
The new Context Mode current-head request to GitHub's GT `/commits/master` API failed with `403: rate limit exceeded`. It was reported immediately and not repeated. CoreMod's request was not reached. These are checked revisions, not a fresh latest-head claim. No production edits, builds, tests, commits or publication occurred.

### Accepted Shape And Recovery Contract

Accepted functions: enriched fluid to normal Bauxite, item Sc concentrate and spent carrier, then dilute nitric leaching to Sc solution and mineral residue, then NaOH precipitation to canonical Sc oxide and spent solution, then optional calcium reduction to Sc dust and Quicklime. Two fluid outputs are not required at separation. The same oxide from atmospheric EBF processing must retain shared Electrolyzer recovery. Calcium cannot be forced through provenance. Numerical recipes and material registration remain proposals.

### Recipe Map Capacities

| Map | Item In | Item Out | Fluid In | Fluid Out | Consequence |
| --- | ---: | ---: | ---: | ---: | --- |
| Centrifuge | 2 | 6 | 1 | 1 | One enriched fluid to two item products plus one spent fluid fits |
| Chemical Reactor | 2 | 2 | 1 | 1 | Concentrate plus one prepared acid fluid, or NaOH plus Sc solution, fits the simple shapes |
| Large Chemical Reactor | 6 | 6 | 6 | 6 | Can take NitricAcid and Water as separate free fluids |
| Electric Blast Furnace | 6 | 6 | 1 | 1 | Two solid recovery inputs and Sc plus Quicklime outputs fit |
| Electrolyzer | 2 | 6 | 1 | 1 | Solid oxide to Sc dust plus Oxygen fluid fits |

[Centrifuge and Electrolyzer maps][separation-maps] [CR and LCR maps][chemical-maps] [EBF map][ebf-map]

Two free separator fluid outputs would exceed the ordinary Centrifuge declaration, but the accepted item-concentrate shape fits. Cells are a separate shape with container bookkeeping. Direct LCR-map registration adds there only. UniversalChemical is the shared CR/LCR owner. Map capacity is not certification of every specialized controller. [Registration distinction][chemical-maps]

### Existing Identities And Forms

| Identity | Verified forms and composition | Reuse boundary |
| --- | --- | --- |
| Calcium | Existing elemental dust, with plasma registration and required blast temperature 1115 K | Dust is an existing reagent. The builder does not add the normal metal-item family, so do not casually require a new calcium ingot form |
| Quicklime | Existing dust, composition Ca:1 and O:1, electrolyzer generation enabled | Ordinary CaO material, not a new spent-calcium identity |
| Sodium Hydroxide | Existing dust identity `SodiumHydroxide_GT5U`, composition Na:1, O:1, H:1 | Use dust. No fluid is declared in this builder |
| Nitric Acid | Existing cell and fluid identity `NitricAcid`, H:1, N:1, O:3 | Existing free acid and packaged-cell forms, not proof of a separate dilute reagent |
| Scandium Oxide | Proposed Sc2O3 compound | No existing GT/CoreMod identity was established in the preceding compound audit. This task does not register one |

[Calcium][calcium] [Quicklime][quicklime] [NaOH][naoh] [Nitric acid][nitric]

A diluted/dilute-nitric literal search over local GT/CoreMod Java found no match. Existing NitricAcid plus Water in LCR avoids a new reagent identity. A dedicated diluted fluid permits a one-fluid CR shape but adds preparation and concentration semantics. Representation is unselected. Nitric cells exist, but a returned-container leach was not verified. Missing identities are scoped findings, not worldwide absence proof. Concentrate, solution and spent intermediates remain proposed content.

### Material Unit And Atomic Accounting

Ordinary dust is one material unit. Small dust is one quarter and tiny dust is one ninth. GT's base material constant is `M = 3628800`. MaterialBuilder defaults its density multiplier and divider to 1:1, and Materials computes density as `M * multiplier / divider`. Compound composition is a list of constituent amounts, not a statement that one full dust represents one whole formula unit. [Dust prefixes][dust-units] [Builder defaults and density API][builder-defaults] [Material density calculation][density]

Under the standard default density, one formula batch of Sc2O3 is **five full oxide dust**, carrying **two Sc material units and three O units**. Therefore:

| Operation | Balanced ordinary GT batch | Status |
| --- | --- | --- |
| Electrolysis | 5 Sc oxide dust to 2 Sc dust plus 3000 mB existing Oxygen gas | Conditional generator prediction for the proposed material |
| Calcium reduction | 5 Sc oxide dust plus 3 Ca dust to 2 Sc dust plus 6 Quicklime dust | Element-balanced proposed batch, not an existing Sc recipe |
| Quicklime recycling | 2 Quicklime dust to 1 Ca dust plus 1000 mB Oxygen gas | Predicted existing material generation |

Quicklime is CaO, so three formula units are six full dust, not three. Those six can recycle into three Ca. Calcium is not necessarily a permanent sink. Oxygen quantities follow GT conventions, not real-world gas volumes. Custom solutions need an explicit Sc-content ledger, not an assumption based on mB. The atmospheric example of five Sc units becoming three hot-metal units plus oxide carrying two Sc units uses five oxide dust and recovers two Sc dust. Changing oxide density invalidates this default-density accounting.

### Exact Conditional Oxide Generator Behavior

Decomposition defaults to zero flags. `addElectrolyzerRecipe()` enables bit 1 and `addCentrifugeRecipe()` bit 2. Composition/formula alone does not enable decomposition. ProcessingDust totals constituents using density, converts one eligible cell output to fluid, sets duration to `max(1, abs(getProtons() * 2 * inputDustAmount))` ticks and power to `min(4, remainingItemOutputTypes) * 30` EU/t. [Flags][builder-flags] [Generator][decomposition] [Proton average][protons] [Elements][elements]
For default-density Sc2O3, integer `(2*21 + 3*8)/5 = 13` protons. With Oxygen converted to fluid, one item-output type remains. Standard generation predicts **5 oxide dust to 2 Sc dust plus 3000 mB Oxygen at 30 EU/t for 130 ticks, or 6.5 seconds, without heat**. This is conditional new-material generation, not an existing registered or tested Sc recipe. Authored shared recovery may select different costs without changing conservation.
Quicklime actually enables electrolysis. Integer `(20+8)/2 = 14` predicts **2 dust to 1 Ca plus 1000 mB Oxygen at 30 EU/t for 56 ticks, or 2.8 seconds**. Both figures are base generator calculations, not measured throughput.

### Existing Recipe Comparators

| Checked recipe | Inputs and outputs | Existing base settings | What it establishes |
| --- | --- | --- | --- |
| Nitric mineral treatment | 1 Pyrope dust plus 10 mB Nitric Acid to six chanced mineral outputs plus 10 mB Sluice Juice | Centrifuge, 120 EU/t, 45 ticks or 2.25 s | A real acid-assisted solid separation with one spent fluid |
| Sodium-aluminate hydrolysis | 4 Sodium Aluminate dust plus 2000 mB Water to 4 Aluminium Hydroxide dust and 3 NaOH dust, selector 1 | UniversalChemical, 120 EU/t, 50 ticks or 2.5 s | Existing chemical precipitation/hydrolysis-style unit accounting |
| Salt-water NaOH preparation | 1000 mB SaltWater plus one empty cell, selector 1, to 3 NaOH dust, hydrogen cell and 1000 mB Chlorine | Electrolyzer, 30 EU/t, 36 s | An ordinary existing upstream dust reagent source |
| Calcium chloride reduction of platinum powder | 4 raw Pt chloride powder plus 1 Ca dust to 2 Pt dust plus 3 calcium-chloride dust | UniversalChemical, 30 EU/t, 30 ticks or 1.5 s | A verified calcium reduction comparator, but not an oxide reduction |
| Quicklime carbon processing | 2 Quicklime dust plus 3 carbon dust to 3 Calcium Carbide dust plus 1000 mB Carbon Monoxide | EBF, 480 EU/t, 30 s, 2573 K | A real oxide-processing EBF shape. It is not metal reduction by calcium |
| Bone-meal calcium | 3 bone meal to 1 Calcium dust | Electrolyzer, 26 EU/t, 98 ticks or 4.9 s | An existing non-Sc calcium feedstock example |

[Nitric mineral treatment][leach-comparator] [Hydrolysis][hydrolysis] [NaOH supply][naoh-supply] [Calcium reduction comparator][calcium-comparator] [Quicklime EBF comparator][quicklime-ebf] [Calcium supply][calcium-supply]

No existing calcium-plus-metal-oxide to metal-plus-Quicklime comparator was established. Checked examples led to chloride/fluoride reduction and other uses. Do not relabel platinum chloride as oxide reduction or infer Sc costs from it. These comparisons are not tuning recommendations or a scientific audit of direct oxide precipitation.

### LCR Access Check

GT's controller uses HV circuits, motor and hull, stainless rotor and large PTFE pipes. CoreMod's Assembler alternative uses those families at 480 EU/t for 10 seconds. No explicit post-HV circuit/motor appears. Structure needs inert casings, PTFE pipe casing, any-tier heating coil and ordinary hatches/buses. Full component acquisition was not traced, so complete earliest tier is unproven. [GT controller][lcr-controller] [Core controller][core-lcr] [Structure][lcr-structure]

### Generated Route And Bypass Constraints

Shared oxide electrolysis is intended, not a bypass to suppress. If authored recovery replaces generator costs, avoid a duplicate cheap generated recipe. Concentrate/solution decomposition or oxide smelt-into behavior could instead bypass accepted stages. These are conditional authoring risks, not observed Sc oxide recipes. Quicklime recycling means calcium is not necessarily a permanent sink. Preserve normal Bauxite, aluminium and titanium processing, without a new origin-specific raw ore. [Decomposition][decomposition] [Smelting owner][dust-smelting]
The four-stage route fits ordinary map shapes. Remaining content decisions are intermediate Sc ledgers, acid representation, Bauxite form, recovery costs and final machines. No measured advantage for either recovery option is established.

### Verification Limits

Checked material definitions/units, generator formulas, map capacity, named comparators and the LCR boundary. No full-modpack, all-conversion, earliest-tier or throughput audit. No material/recipe implementation or game test. Latest-head checking remains limited by the reported 403. Both recovery alternatives are retained.

[[Sources]]

[gt-revision]: https://github.com/GTNewHorizons/GT5-Unofficial/commit/2856a652b29ecf17dd5529880d589bea92a83b9f
[core-revision]: https://github.com/GTNewHorizons/NewHorizonsCoreMod/commit/38b12ce3d59f8061742e47a63c6f1f29b7959313
[separation-maps]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/api/recipe/RecipeMaps.java#L789-L850
[chemical-maps]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/api/recipe/RecipeMaps.java#L1127-L1175
[ebf-map]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/api/recipe/RecipeMaps.java#L851-L858
[calcium]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/loaders/materials/MaterialsInit.java#L354-L369
[quicklime]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/loaders/materials/MaterialsInit.java#L7236-L7246
[naoh]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/loaders/materials/MaterialsInit.java#L8754-L8764
[nitric]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/loaders/materials/MaterialsInit.java#L8524-L8536
[dust-units]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/api/enums/OrePrefixes.java#L743-L808
[builder-defaults]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/api/enums/MaterialBuilder.java#L70-L82
[density]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/api/enums/Materials.java#L1385-L1388
[builder-flags]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/api/enums/MaterialBuilder.java#L439-L446
[decomposition]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/loaders/oreprocessing/ProcessingDust.java#L165-L267
[protons]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/api/enums/Materials.java#L1831-L1839
[elements]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/api/enums/Element.java#L25-L38
[leach-comparator]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/loaders/postload/chains/BauxiteRefineChain.java#L230-L244
[hydrolysis]: https://github.com/GTNewHorizons/NewHorizonsCoreMod/blob/38b12ce3d59f8061742e47a63c6f1f29b7959313/src/main/java/com/dreammaster/gthandler/recipes/ChemicalReactorRecipes.java#L62-L67
[naoh-supply]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/loaders/postload/recipes/ElectrolyzerRecipes.java#L737-L756
[calcium-comparator]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/bartworks/system/material/gtenhancement/PlatinumSludgeRecipes.java#L386-L392
[quicklime-ebf]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/loaders/postload/recipes/BlastFurnaceRecipes.java#L506-L515
[calcium-supply]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/loaders/postload/recipes/ElectrolyzerRecipes.java#L78-L83
[lcr-controller]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/loaders/load/MTERecipeLoader.java#L3827-L3833
[core-lcr]: https://github.com/GTNewHorizons/NewHorizonsCoreMod/blob/38b12ce3d59f8061742e47a63c6f1f29b7959313/src/main/java/com/dreammaster/gthandler/recipes/AssemblerRecipes.java#L1771-L1780
[lcr-structure]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/common/tileentities/machines/multi/MTELargeChemicalReactor.java#L65-L125
[dust-smelting]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/loaders/oreprocessing/ProcessingDust.java#L87-L122
