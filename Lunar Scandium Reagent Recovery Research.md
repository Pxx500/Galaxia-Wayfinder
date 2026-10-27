---
type: source
status: unreviewed
tags:
  - galaxia/alpha
  - wayfinder/source
---

# Lunar Scandium Reagent Recovery Research

Source: Primary GT5-Unofficial and NewHorizonsCoreMod source
Imported: 2026-10-11

## Source Snapshot

> Current-use note, 2026-10-23: Design Lunar Crater Processing Recipe Chain owns the selected reagent-recovery direction and initial recipe balance. This earlier audit remains source evidence, not a competing set of current quantities.

Bounded read-only reagent audit. No recipes, ratios, machines or costs were selected, and no production files, dependencies, builds, tests, commits or public text were changed. Both repositories were fully reindexed for graph discovery. Evidence uses already checked immutable GT `2856a652b29ecf17dd5529880d589bea92a83b9f` and CoreMod `38b12ce3d59f8061742e47a63c6f1f29b7959313`. New cited GT raw excerpts returned HTTP 200. These are inspected revisions, not a fresh latest-head claim.
The known GitHub current-head API 403 was not retried. Context Mode's first ChemicalRecipes raw read timed out after 15 seconds. One longer bounded retry succeeded. A snippet request for the wrong `PowderLoader.run` symbol returned symbol-not-found, then graph-discovered `DustLoader` was read successfully. Both failures were reported immediately.
The owner supplies lunar SaltWater availability and wants partial reagent recovery. This audit does not verify celestial resource placement, practical power demand or an exact loss ratio. The accepted chemical function remains nitric leaching and NaOH precipitation.

### Existing Reagent And Intermediate Identities

| Identity | Verified definition | Consequence |
| --- | --- | --- |
| Nitric Acid | Existing GT cell/fluid, H:1 N:1 O:3 | Existing acid, not a new lunar copy |
| Sodium Hydroxide | Existing GT dust `SodiumHydroxide_GT5U`, Na:1 O:1 H:1 | Three full dust per NaOH formula batch |
| BartWorks SodiumNitrate | Dust-only `WerkstoffLoader.SodiumNitrate`, NaNO3, Na:1 N:1 O:3, no explicitly enabled electrolysis | Five full dust per formula batch. Used by the verified acid-exchange recipe |
| GT++ SODIUM_NITRATE | Separate existing solid material definition with NaNO3 and the same elemental ratios | Do not assume its item is directly interchangeable with BartWorks nitrate without checking unification |
| BartWorks Sodiumsulfate | Dust-only Na:2 S:1 O:4, electrolysis enabled | Seven full dust per formula batch, with an existing chemical sodium-recovery recipe |

[Nitric][nitric] [NaOH][naoh] [BartWorks nitrate][nitrate] [GT++ nitrate][gpp-nitrate] [Sulfate][sulfate]
Bounded graph and Java literal searches found no named sodium-nitrate-solution or spent-nitric-acid identity or direct recovery recipe in GT/CoreMod. Ammonium Nitrate Solution is a different existing identity. CoreMod's named NitricAcid hits were remapping or consumption, not a named producer. This is not all-modpack absence proof.

### Verified Nitric Acid Supply Recipes

Free-fluid equivalents of UniversalChemical entries are available in LCR through its existing cell conversion. Cells/returns below are the exact authored singleblock forms where shown. Selector circuits are reusable. Times are base times.

| Route | Exact inputs | Exact outputs | Map, EU/t, time |
| --- | --- | --- | --- |
| Direct ammonia oxidation | 1000 mB Ammonia + 4000 mB Oxygen, selector 24 | 1000 mB Nitric Acid + 1000 mB Water | LCR, 30, 16 s |
| Direct no-separate-ammonia route | 3000 mB Hydrogen + 1000 mB Nitrogen + 4000 mB Oxygen, selector 21 | 1000 mB Nitric Acid + 1000 mB Water | LCR, 480, 16 s |
| NO2 oxidation/absorption | 2000 mB Nitrogen Dioxide + 1000 mB Oxygen + 1000 mB Water, selector 24 | 2000 mB Nitric Acid | LCR, 30, 16 s |
| Absorption with NO return | 3000 mB Nitrogen Dioxide + 1 Water cell, selector 1 | 2000 mB Nitric Acid + 1 Nitric Oxide cell | UniversalChemical, 30, 12 s |
| Ammonia-to-NO preparation | 4 Ammonia cells + 2 empty cells + 10000 mB Oxygen | 4000 mB Nitric Oxide + 6 Water cells | CR, 30, 16 s |
| NO-to-NO2 preparation | 1 Nitric Oxide cell + 1000 mB Oxygen, selector 1 | 1000 mB Nitrogen Dioxide + 1 empty cell | UniversalChemical, 30, 8 s |

[Direct LCR routes][direct-acid] [NO-return absorption][absorption] [Ammonia preparation][ammonia-no] [NO oxidation][no-no2]
An ordinary source alternative therefore avoids producing ammonia as an intermediate, but it still consumes nitrogen, hydrogen and oxygen. NO2 absorption can return NO for oxidation/reuse. These recipes do not establish a free lunar nitrogen source or a requirement to have atmospheric air around the machine. Vacuum is not equivalent to having no supplied Oxygen fluid.
Nitric Acid is not universally a high-EU/t recipe. The direct ammonia LCR operation is LV, while its no-separate-ammonia alternative is HV. Whole-chain expense includes making/importing reactants, not merely the acid reactor's tier. No full lunar feedstock or energy comparison was performed.

### NaOH Supply And Existing Nitrate Recovery

| Operation | Exact inputs | Exact outputs | Map, EU/t, time |
| --- | --- | --- | --- |
| SaltWater electrolysis | 1000 mB SaltWater + 1 empty cell, selector 1 | 3 NaOH dust + 1 Hydrogen cell + 1000 mB Chlorine | Electrolyzer, 30, 36 s |
| Alternate SaltWater output packaging | Same inputs, selector 11 | 3 NaOH dust + 1 Chlorine cell + 1000 mB Hydrogen | Electrolyzer, 30, 36 s |
| Existing nitrate formation | 3 NaOH dust + 1000 mB Nitric Acid, selector 7 | 5 BartWorks SodiumNitrate dust + 1000 mB Water | UniversalChemical, 120, 1 s |
| Existing acid exchange | 10 BartWorks SodiumNitrate dust + 1000 mB Sulfuric Acid, selector 1 | 2000 mB Nitric Acid + 7 BartWorks Sodiumsulfate dust | UniversalChemical, 480, 10 s |
| Existing sulfate sodium recovery | 7 Sodiumsulfate dust + 2 Hydrogen cells | 2 Sodium dust + 1000 mB Sulfuric Acid + 2 empty cells | UniversalChemical, 30, 1.5 s |
| Existing sodium-to-base | 1 Sodium dust + 1000 mB Water, selector 1 | 3 NaOH dust + 1000 mB Hydrogen | UniversalChemical, 30, 10 s |

[SaltWater recipe][saltwater] [Nitrate formation][neutralization] [Acid exchange][exchange] [Sulfate recovery][sulfate-recovery] [Sodium hydration][sodium-water]
Sulfate also enables generated electrolysis. DustLoader uses its seven-unit constituent batch to emit 2 Sodium dust, 1 Sulfur dust and 4000 mB Oxygen. That is element decomposition, not simultaneous NaOH/acid recovery. Its BartWorks cost helper was not resolved, so no invented exact generated EU/t or duration is supplied. The explicit chemical recovery above already establishes the useful existing route. [Generator output construction][sulfate-generator]

### Balanced Recovery And Its Limits

The existing acid exchange, sulfate recovery and two sodium-hydration operations combine to the bookkeeping net **10 nitrate dust + 2000 mB Water to 2000 mB Nitric Acid + 6 NaOH dust**. Sulfuric acid and hydrogen are circulating seed stocks, not net products or guaranteed zero-bootstrap inputs. Cell packaging and buffers still matter. Every inspected recipe has deterministic full outputs for pure inputs. This is source algebra, not a measured practical closed loop.
The exact CR sulfate recipe consumes two FILLED Hydrogen cells and returns two empties. Sodium hydration returns hydrogen as gas, not already refilled cells. That gas must be routed through ordinary filling/container handling, or supplied to the standard LCR free-fluid equivalent of UniversalChemical. Empty cells do not create free hydrogen. Initial hydrogen and sulfuric acid stock must exist before this cycle starts.
Formula balance is `NaNO3 + H2O -> NaOH + HNO3`. A new compressed version of that net would be NEW authored content, not an existing direct recipe. The coordinator's unselected sulfate alternative, **7 Na2SO4 dust + 2000 mB Water to 6 NaOH dust + 1000 mB Sulfuric Acid**, is also NEW as one operation. Existing sulfate-to-sodium and sodium-to-NaOH steps already produce that net while cycling hydrogen. No new operation is required merely to make the atomic equation balance.
Existing CR has one free-fluid output, while LCR has six. A one-fluid spent-mixture input producing NaOH dust plus one Nitric Acid fluid fits either map's capacity. Producing recovered acid plus a separate waste fluid requires LCR or explicit container/item waste handling. Capacity is not a machine selection. [Map capacities][maps]
The formula-defined and mixture cases must stay distinct. BartWorks calls SodiumNitrate a `MIXTURE`, but its formula and constituents are explicit. That enum label does not make it chemically undefined. Pure NaNO3 bounds acid and base to one formula unit each per nitrate unit. Separate lower yields require the remaining Na/N to be allocated to waste, retained solution or other outputs, not silently deleted in a claimed balanced reaction.
An undefined contaminated spent solution can have an authored recoverable fraction. Its fluid volume alone does not establish nitrate, Na or N content. It needs a ledger based on consumed acid/base and retained impurities. Fractional recovery from that mixture can preserve losses and reagent makeup without redefining pure canonical nitrate.
Important constraint: if the lunar chain outputs ordinary pure BartWorks nitrate, the existing deterministic recovery loop remains available. A lower-yield new compressed recipe does not impose a universal recovery ceiling. To support partial recovery, account for limited extractable nitrate/base or explicitly discarded residue at the contaminated-spent stage. Do not invent provenance restrictions on ordinary nitrate or assume perfect recovery from a dirty mixture. No recovery percentages were selected here.

### Bounded Crystallization Follow-Up

Distillery declares **1 item input, 1 item output, 1 fluid input and 1 fluid output**. Distillation Tower declares **2, 1, 1 and 11** respectively. The ordinary Distillery can therefore support one spent-solution fluid becoming nitrate dust plus recovered water. No Tower is required merely to allow a solid salt output. Existing Distillery precedent is **1000 mB SaltWater plus selector 1 to 2 Salt dust and 1000 mB DistilledWater at 30 EU/t for 80 seconds**. Exact chosen batch volumes still need the selected machine's tank-capacity check. [Distillery map][distill-maps] [Tower map][tower-map] [Salt crystallization][salt-distill]
The parent's NEW candidate is **9000 mB SpentScLeach to 27 BartWorks nitrate dust plus 6000 mB Water**. It is not an existing recipe or a selected cost. If the prior chain's ledger supplies a theoretical 30 nitrate dust from 6000 mB acid and 18 NaOH dust, 27 recovered dust gives 90% aggregate recovery of both reagents through the existing pure-salt loop. The missing three nitrate dust-equivalents must be explicitly unrecoverable or discarded material in the spent-mixture contract. Fluid volume alone cannot prove that ledger.
Each existing acid-exchange operation takes ten nitrate dust. Twenty-seven per new batch leaves buffered salt between operations. Across ten candidate batches, 270 nitrate dust run 27 existing exchanges, giving 54000 mB acid and 162 NaOH dust versus the stated original 60000 mB acid and 180 NaOH dust. This is aggregate batch arithmetic, not permission for fractional machine runs. No artificial lower NaOH cap is implied, and no new sulfate recovery recipe is needed for this direction.

### Scope And Outcome

There is an existing sodium-nitrate acid-regeneration route and an existing complete sodium/base continuation. Reusing those operations is a credible alternative to new recovery chemistry. A shorter partial-recovery operation remains proposed content whose ledger and balance must be authored explicitly. This audit covered named GT/CoreMod reagent hits, the owning recipes and relevant map shapes, not all mods, every nitrogen source, practical throughput or full earliest-tier availability. Only this unreviewed source note was created.

[[Sources]]

[nitric]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/loaders/materials/MaterialsInit.java#L8524-L8536
[naoh]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/loaders/materials/MaterialsInit.java#L8754-L8764
[nitrate]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/bartworks/system/material/WerkstoffLoader.java#L1246-L1258
[gpp-nitrate]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gtPlusPlus/core/material/MaterialMisc.java#L43-L58
[sulfate]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/bartworks/system/material/WerkstoffLoader.java#L936-L948
[direct-acid]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/loaders/postload/recipes/ChemicalRecipes.java#L5453-L5481
[absorption]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/loaders/postload/recipes/ChemicalRecipes.java#L2781-L2811
[ammonia-no]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/loaders/postload/recipes/ChemicalRecipes.java#L4396-L4403
[no-no2]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/loaders/postload/recipes/ChemicalRecipes.java#L2741-L2751
[saltwater]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/loaders/postload/recipes/ElectrolyzerRecipes.java#L737-L756
[neutralization]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/bartworks/system/material/gtenhancement/PlatinumSludgeRecipes.java#L642-L651
[exchange]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/goodgenerator/loader/RecipeLoader.java#L330-L339
[sulfate-recovery]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/bartworks/system/material/gtenhancement/PlatinumSludgeRecipes.java#L465-L473
[sodium-water]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/loaders/postload/recipes/ChemicalRecipes.java#L1654-L1664
[sulfate-generator]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/bartworks/system/material/werkstoff_loaders/recipe/DustLoader.java#L84-L220
[maps]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/api/recipe/RecipeMaps.java#L1127-L1175
[distill-maps]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/api/recipe/RecipeMaps.java#L650-L652
[tower-map]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/api/recipe/RecipeMaps.java#L1176-L1178
[salt-distill]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/loaders/postload/recipes/DistilleryRecipes.java#L162-L171
