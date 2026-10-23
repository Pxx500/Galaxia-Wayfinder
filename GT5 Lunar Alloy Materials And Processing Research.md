---
type: source
status: unreviewed
tags:
  - galaxia/alpha
  - wayfinder/source
---

# GT5 Lunar Alloy Materials And Processing Research

Source: Primary GTNewHorizons/GT5-Unofficial source, inspected upstream commit `bc7a940f5e6583b5c79d049635d1586c8f4ad764`
Imported: 2026-10-10

[[Sources]]

## Source Snapshot

> Current-use note, 2026-10-23: the Al-Sc route and crater Scandium direction are now selected in Design Lunar Crater Processing Recipe Chain. Unresolved labels below describe the earlier research context. Keep the original recipe/source evidence separate from subsequent gameplay decisions.

### Scope And Provenance

This is factual intake for a proposed low, medium and advanced Space-Grade Alloy production family. The owner selected normal existing materials and deposits around iron, platinum, gold, cobalt and aluminium, not origin-specific replacement raw ores. Iron is the working low route, gold-cobalt is the working medium route, and aluminium-scandium remains unresolved. One canonical alloy, atmosphere-free production, ordinary GT downstream machines and preservation of titanium processing remain accepted context. New functional intermediates are proposals, not existing code facts.

Context read: the accepted crater decision, Design Lunar Crater Processing Recipe Chain, the earlier Discord crater proposal and the accepted early orbital content note. The Discord source's asteroidal materials, scandium-rich bauxite, separate alloy identities and recovery assumptions were not adopted. This note does not duplicate the separate real-world scandium research or classify Wayfinder notes.

The local GT checkout was clean at `2259bc64244f9f7fc58e039d8e89ca40dd17c929`. The parent had just rebuilt and verified its graph, so it was reused rather than reindexed again. Graph discovery and caller traces were followed by HTTP 200 reads of the relevant immutable upstream files at `bc7a940f5e6583b5c79d049635d1586c8f4ad764`, current upstream master during this research round. This SHA records an inspected snapshot, not a permanent target version. No production, dependency, server, game or test state was changed. [Inspected commit][commit]

This is not a complete pack-script, external-mod, world-generation or runtime recipe audit. Material declarations and recipe generators establish code support, not in-game availability under every configuration.

### Existing Identities And Feedstock Forms

All six normal GT identities exist. Their material builders declare dust, metal and ore forms. Ordinary ore processing then works through ore-prefix identities such as crushed ore, purified crushed ore, centrifuged crushed ore and dust. Raw extraction form and finished metal are not interchangeable progression stages. [Material declarations][material-init] [Crushed processing][crushed] [Dirty processing][dirty]

| Material identity | Existing normal source/feedstock example | Verified processing constraint |
| --- | --- | --- |
| `Materials.Iron` | Iron, magnetite, brown/yellow limonite and banded-iron mix definitions | No required EBF flag on the iron metal definition. Ordinary non-EBF ore/dust smelting is generated, subject to direct-smelting and yield rules |
| `Materials.Gold` | Gold occurs in the magnetite/vanadium-magnetite mix named Gold | No required EBF flag on gold. Normal ingot/block/nugget identity reuses Minecraft forms |
| `Materials.Cobalt` | Cobaltite in the Nickel mix. Cobaltite and cobalt oxide are existing separate materials | Cobalt metal requires blast processing and disables generic EBF generation. Explicit cobalt reduction recipes are MV and 1200 K, not automatically the metal definition's 1700 K |
| `Materials.Platinum` | Cooperite/platinum group ores and ordinary platinum ore forms | Ordinary ore and byproduct outputs are redirected to Platinum Metallic Powder. Existing poor-yield EBF and chemical-refining routes differ |
| `Materials.Aluminium` | Bauxite mix includes normal aluminium and ilmenite. Bauxite, alumina and hydroxide are existing materials | Aluminium and alumina disable generic EBF recipes. The checked efficient bauxite refining branch includes HV processing and an LCR |
| `Materials.Scandium` | Ore forms are declared, but no Sc placement in the checked default OreMixes or SmallOres | Requires 1814 K blast processing. No explicit acquisition chain was established by this bounded source pass |

[Iron and gold][iron-gold] [Cobalt definition][cobalt] [Platinum definition][platinum] [Aluminium definition][aluminium] [Scandium definition][scandium] [Ore mix defaults][ore-mixes]

The draft's spelling Hematite needs a separate caution. `Materials.Hematite` exists with dust/metal/ore declarations, but its current builder defines neither iron composition nor direct smelting to Iron. `Materials.BandedIron` instead declares 2 Iron plus 3 Oxygen and direct smelting to Iron. A scientific mineral name is not proof that the similarly named GT material follows the desired iron recipe. [Hematite declaration][hematite] [Banded iron declaration][banded-iron]

### Ordinary Ore Processing Is Already A Reusable Owner

`ProcessingDirty.registerOre` generates low-power maceration and washing routes. Water washing consumes 1000 units and produces a purified form, a chance byproduct and stone. Its distilled-water variant consumes 200 units and has a shorter base duration. Thermal centrifuging uses 48 EU/t and another byproduct selection. `ProcessingCrushedOre.registerOre` processes purified and centrifuged forms. These generic owners call output-conversion helpers rather than treating every material as freely smeltable pure metal. [Dirty processing][dirty] [Crushed processing][crushed]

`ProcessingOreSmelting.registerOre` removes old furnace recipes and checks the input and direct-smelting material's required-blast flags. High-temperature or explicitly non-autogenerated materials do not get a generic ore-to-ingot EBF shortcut. Non-blast materials receive smelting with prefix-dependent yields. A mixed-ore config can change yield. Therefore a proposed crater using normal ore or crushed forms should retain these existing rules rather than assign generic metal yields solely from the metal's name. [Ore smelting owner][ore-smelting]

### Platinum Refining And A Real Existing Shortcut

The graph identifies `PlatinumSludgeOutputs.convertSmelting` consumers in ProcessingDust, ProcessingOreSmelting, ProcessingRawOre and ProcessingOre. The helper changes smelting outputs associated with platinum into `WerkstoffLoader.PTMetallicPowder`, except the deliberate finished platinum dust/tiny-dust case. Its dust-output conversion also replaces platinum dust-family outputs with that powder. These are active ordinary processing boundaries, not merely a recipe-description convention. [Conversion owner][pt-conversion]

| Existing platinum route | Inputs and output | Machine and requirements |
| --- | --- | --- |
| Poor-yield direct powder route | 3 Platinum Metallic Powder dust to 2 platinum nuggets | EBF, circuit 1, MV, 30 s, 2041 K from platinum melting point |
| Powder to concentrate | Platinum Metallic Powder plus aqua regia to Platinum Concentrate and residue | Universal Chemical, LV. Normal purified cooperite and other specified ore feeds also have concentrate recipes |
| Concentrate separation | Platinum Concentrate plus ammonium chloride to crude platinum salt and Platinum Raw Powder, with other products | Centrifuge cell variant at LV, or LCR fluid variants at LV/HV |
| Salt processing | Crude salt sifted to refined salt. Refined salt returns metallic powder and chlorine | Sifter LV, then EBF MV at 900 K |
| Finished platinum dust | 4 Platinum Raw Powder dust plus 1 calcium dust to 2 platinum dust and calcium chloride | Universal Chemical, LV, 1.5 s |

[Platinum recipes][pt-recipes] [Concentrate feeds][pt-feeds]

The efficient chain can be preserved without claiming that it is the only legitimate source of platinum. The code explicitly offers a low-yield EBF alternative. Other late-game, recycling, loot or external-mod sources were not exhaustively audited. Finished platinum as an alloy ingredient accepts existing legitimate sources. Returning pure platinum dust directly from a new ore/enriched-fluid stage would instead skip the checked ore-output conversion, and that dust has a deliberate normal smelting allowance. [Conversion owner][pt-conversion] [Dust smelting][dust]

### Cobalt And Aluminium Constraints

Existing Cobaltite dust can be roasted with 3000 oxygen to roasted cobalt plus roasted arsenic and sulfur dioxide, at MV/1200 K. Roasted cobalt plus carbon then yields cobalt ingots at MV/1200 K. Cobalt oxide plus small carbon dust has an explicit ingot-producing reduction at the same power and heat. Cobaltite and cobalt oxide also declare electrolyzer decomposition. Their metal outputs are still dust-stage feedstock, not automatic permission to furnace-smelt cobalt. [Cobalt roasting][cobalt-recipes] [Roasted cobalt reduction][cobalt-reduction] [Oxide reduction][cobalt-oxide-reduction] [Cobalt compounds][cobalt-compounds]

The current GT bauxite composition is 2 Rutile, 16 Aluminium, 10 Hydrogen and 11 Oxygen. It declares electrolyzer decomposition and has grossular, rutile and gallium byproducts. It does not contain scandium. This defeats the claim that existing normal GT bauxite already provides an Al-Sc extraction line. [Bauxite definition][bauxite]

The efficient BauxiteRefineChain branch uses crushed or purified crushed bauxite, sodium hydroxide, quicklime and water in an MV Mixer to make Bauxite Slurry. An HV Fluid Heater makes Heated Bauxite Slurry. An HV LCR step uses aluminium hydroxide seed and carbon dioxide to produce alumina, sodium carbonate, calcite, Bauxite Slag and Sluice Juice. The slag centrifuge can return rutile, gallium, quicklime, silica and iron. These fluid and dust identities are existing reusable intermediates. [Bauxite refinement][bauxite-chain]

Alumina is `Materials.Aluminiumoxide`, internally named and displayed as Alumina. It requires blast processing at 2054 K and disables generic EBF generation. Aluminium itself is required-blast at 1700 K and also disables generic EBF generation. This bounded GT Java pass did not establish the complete normal pack's final aluminium ingot reduction recipe. Do not invent that missing link or call this a fully verified playable aluminium chain. Pack scripts and target-pack final recipes need a separate focused check when a concrete Al recipe is selected. [Aluminium definition][aluminium] [Alumina definition][alumina]

### Scandium Existence Is Not Acquisition

Scandium is a real GT material identity, element Sc, with dust/metal/ore declarations, mining level 2, a storage block and required blast heat of 1814 K. GT++ wraps the same material through `MaterialsElements.SCANDIUM`. This is not a new Galaxia element or an implemented scandium-rich lunar ore. [Scandium definition][scandium] [Storage block][sc-block] [GT++ wrapper][sc-wrapper]

The generic material defaults enable EBF and vacuum-freezer generation unless disabled. Scandium does not disable those in its definition. `ProcessingDust` generates an MV EBF recipe, producing hot ingot when required heat is above 1750 K. `ProcessingIngot` generates an MV vacuum-freezer recipe from registered hot ingot to normal ingot when enabled. These are inferred generated contracts from the common registrators, not an in-game recipe dump. Recipe electrical tier and heat requirement must be distinguished. [Defaults][defaults] [Dust EBF generation][dust] [Hot-ingot cooling][hot-ingot]

The EBF adds 100 K per input-voltage tier above MV to coil heat. Cupronickel's enum heat is 1801 K. A source-level consequence is that HV input provides 1901 K with that coil, sufficient for the scandium heat requirement, while MV input alone does not. This is not a proof of a complete HV scandium supply line, crafting progression or factory viability. [Coil heat][coils] [EBF heat capacity][ebf]

No scandium entry occurs in the checked current default `OreMixes` or `SmallOres`. Named usages in the local code search are sparse: material registration, GT++ wrapper, storage-block recognition, and a Scandium case in plasma-cell fuel registration. That fuel case runs under the `cellPlasma` branch and does not create an acquisition recipe or prove that scandium plasma is registered. No bespoke Sc acquisition recipe, Al-Sc alloy use or Sc output from BauxiteRefineChain was established. External configurations, magic, other mods and generated recipes remain outside that absence claim. [Default ore mixes][ore-mixes] [Default small ores][small-ores] [Conditional plasma fuel][sc-fuel]

An Al-Sc advanced alloy route therefore needs a separately proposed acquisition or recovery contract. Ordinary bauxite can remain the input identity if the owner selects a new recovery recipe, but its scandium yield would be new gameplay content, not an existing GT fact. This note neither proposes a specific yield nor endorses the old Discord scandium-rich bauxite.

### Lunar Placement Facts, Not Exclusivity

| Checked default mix | Relevant normal materials | Moon in this mix's enabled dimensions? |
| --- | --- | --- |
| Copper | Chalcopyrite, Iron, Pyrite, Copper | Yes |
| Bauxite | Bauxite, Ilmenite, Aluminium | Yes, and many other listed space dimensions |
| Gold | Magnetite, Vanadium Magnetite, Gold | No in this mix. Overworld and several other dimensions are enabled |
| Iron | Brown Limonite, Yellow Limonite, Banded Iron | No in this mix. Overworld, Nether and others are enabled |
| Nickel | Garnierite, Nickel, Cobaltite, Pentlandite | No in this mix. End, Twilight Forest and listed space dimensions are enabled |
| Platinum | Cooperite, Palladium, Platinum, Iridium | No in this mix. Asteroid-related dimensions are enabled |

[Ore mix defaults][ore-mixes]

This proves that normal lunar iron and bauxite-related placement is already represented in checked default GT mix definitions, not that these are exclusive to Luna or exhaustive sources. Galaxia's replacement celestial generation, crater authorship and target-pack configuration were not audited here. Adding a Moon gold/cobalt/platinum crater profile would be authored content, not confirmation that a matching GT default mix already enables Moon. Scandium declared ore forms alone do not establish default placement.

### Concrete Bypass Risks To Avoid In Proposals

| Proposed shortcut | Concrete affected consumer path | Practical risk |
| --- | --- | --- |
| New crater fluid directly emits pure platinum dust | PlatinumSludgeOutputs normally redirects ore outputs to metallic powder. ProcessingDust and convertSmelting deliberately allow finished platinum dust smelting | Skips the normal ore-stage conversion and the selected refining or poor-yield reduction work |
| Enriched cobalt fluid directly emits cobalt ingots | Existing Cobaltite roasting and roasted/oxide reduction in BlastFurnaceRecipes | Removes the real roasting/reduction stage instead of supplying ordinary feedstock |
| Enriched bauxite directly emits aluminium ingots | BauxiteRefineChain and the non-autogenerated Al/Alumina blast boundary | Bypasses refining/final reduction that has not yet been fully source-verified for the target pack |
| New enriched processing emits finished titanium or treats ilmenite as free titanium metal | Existing BauxiteRefineChain ilmenite chemical-bath path yields rutile. Titanium disables generic EBF and generic freezer generation | Cuts across the owner's explicitly preserved titanium chain rather than improving extraction |

[Conversion owner][pt-conversion] [Cobalt recipes][cobalt-recipes] [Bauxite refinement][bauxite-chain] [Titanium definition][titanium]

These are direct new-recipe output choices with reachable ordinary material consumers, not theoretical machine exploits. Ordinary ore/crushed outputs and finished-metal alloy inputs keep the distinction between extraction, refining and alloy manufacture. A scarce finished-metal promoter can preserve its normal acquisition routes, but its amount and efficiency remain balance proposals.

### Small Recipe-Shape Check

For the parallel draft, current `electrolyzerRecipes` supports 2 item inputs, 6 item outputs, 1 fluid input and 1 fluid output. Current `chemicalReactorRecipes` supports 2 item inputs, 2 item outputs, 1 fluid input and 1 fluid output. One fluid input with two item outputs and two item types plus one fluid input fit those map capacities. This checks map shape, not registered recipe execution or actual machine usability. [Electrolyzer capacity][maps] [Chemical Reactor capacity][chemical-map]

One Context Mode literal search for `TitaniumTetrachloride` or direct `Rutile.getDust` in ChemicalRecipes.java returned no matches. `rg` exited 1 and the wrapper reported an error. It was reported immediately. That absence is not evidence that the titanium chain is missing, and no broader titanium-chain audit or code change followed.

[commit]: https://github.com/GTNewHorizons/GT5-Unofficial/commit/bc7a940f5e6583b5c79d049635d1586c8f4ad764
[material-init]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/loaders/materials/MaterialsInit.java
[iron-gold]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/loaders/materials/MaterialsInit.java#L725-L897
[cobalt]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/loaders/materials/MaterialsInit.java#L473-L498
[platinum]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/loaders/materials/MaterialsInit.java#L1404-L1427
[aluminium]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/loaders/materials/MaterialsInit.java#L159-L183
[scandium]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/loaders/materials/MaterialsInit.java#L1568-L1587
[dirty]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/loaders/oreprocessing/ProcessingDirty.java#L36-L137
[crushed]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/loaders/oreprocessing/ProcessingCrushedOre.java#L29-L83
[ore-smelting]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/loaders/oreprocessing/ProcessingOreSmelting.java#L34-L113
[pt-conversion]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/bartworks/system/material/gtenhancement/PlatinumSludgeOutputs.java#L39-L86
[pt-recipes]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/bartworks/system/material/gtenhancement/PlatinumSludgeRecipes.java#L299-L393
[pt-feeds]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/bartworks/system/material/gtenhancement/PlatinumSludgeRecipes.java#L272-L297
[dust]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/loaders/oreprocessing/ProcessingDust.java#L84-L122
[cobalt-recipes]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/loaders/postload/recipes/BlastFurnaceRecipes.java#L583-L591
[cobalt-compounds]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/loaders/materials/MaterialsInit.java#L6167-L6197
[bauxite]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/loaders/materials/MaterialsInit.java#L9993-L10011
[bauxite-chain]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/loaders/postload/chains/BauxiteRefineChain.java#L24-L113
[alumina]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/loaders/materials/MaterialsInit.java#L9853-L9869
[sc-block]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/loaders/preload/LoaderGTBlockFluid.java#L818-L825
[sc-wrapper]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gtPlusPlus/core/material/MaterialsElements.java#L44
[defaults]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/api/enums/Materials.java#L1177-L1179
[hot-ingot]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/loaders/oreprocessing/ProcessingIngot.java#L195-L204
[coils]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/api/enums/HeatingCoilLevel.java#L7-L34
[ebf]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/common/tileentities/machines/multi/MTEElectricBlastFurnace.java#L226-L227
[sc-fuel]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/loaders/oreprocessing/ProcessingCell.java#L371-L373
[ore-mixes]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/api/enums/OreMixes.java#L132-L310
[small-ores]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/api/enums/SmallOres.java
[titanium]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/loaders/materials/MaterialsInit.java#L1824-L1849
[maps]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/api/recipe/RecipeMaps.java#L820-L821
[chemical-map]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/api/recipe/RecipeMaps.java#L1127-L1129
[cobalt-reduction]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/loaders/postload/recipes/BlastFurnaceRecipes.java#L102-L110
[cobalt-oxide-reduction]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/loaders/postload/recipes/BlastFurnaceRecipes.java#L363-L371
[hematite]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/loaders/materials/MaterialsInit.java#L3538-L3547
[banded-iron]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/loaders/materials/MaterialsInit.java#L5764-L5779

### Focused Follow-Up: Final Aluminium Reduction

The earlier GT-only limitation is now narrowed by a focused CoreMod check. The local pack checkout was clean at `965462fb102acf429818c07388bdf5f50137c662`, and local NewHorizonsCoreMod was clean at `38b12ce3d59f8061742e47a63c6f1f29b7959313`. Its existing graph located the BlastFurnaceRecipes owner without rebuilding indexes. The GitHub default-branch commits endpoint reported newer CoreMod `9aa0afc8711f3efbe3afc0d11ec44dcbf5b87442`, dated 2026-10-09 at 19:22:55 UTC. HTTP 200 immutable-source inspection confirmed the following recipes are the same in both checked CoreMod revisions. These are real pack-content recipes, not invented replacement reactions. [Current CoreMod source][core-al]

| Operation | Inputs | Outputs | Machine | EU/t | Base time | Required heat |
| --- | --- | --- | --- | ---: | ---: | ---: |
| Carbon reduction | 10 Alumina dust plus 3 Carbon dust | 4 Aluminium ingots plus 3000 carbon dioxide gas | EBF | 120, MV | 60 s | 2054 K |
| Cryolite-assisted operation | 10 Alumina dust plus 5 Cryolite dust | 4 Aluminium ingots | EBF | 120, MV | 80 s | 963 K |
| Hydroxide to alumina | 8 Aluminium Hydroxide dust, circuit 1 | 5 Alumina dust | EBF | 480, HV | 10 s | 1300 K |
| Sodium aluminate to alumina | 8 Sodium Aluminate dust plus 1000 carbon dioxide gas | 5 Alumina dust plus 6 Sodium Carbonate dust | EBF | 480, HV | 5 s | 1200 K |

These quantities are actual item counts, not just the chemistry comments above the recipes. `TierEU.RECIPE_MV` and `RECIPE_HV` resolve through the GT practical-voltage array to 120 and 480 respectively. [CoreMod aluminium operations][core-al] [Recipe voltages][recipe-voltage]

CoreMod also authors a pure aluminium-dust operation: 1 Aluminium dust to 1 Aluminium ingot, circuit 11, HV, base authored duration 60 s, 2054 K, additive amount 1000, through `BlastFurnaceWithGas`, with a no-gas variant enabled and its circuit set to 1. That helper adjusts generated recipe variants, so the 60 s value is the builder's base duration rather than a claim that every resulting gas/no-gas recipe has that duration. [CoreMod dust operation][core-al-dust]

The efficient GT bauxite branch already produces the normal Alumina identity consumed by these CoreMod reductions. A new enriched-fluid recipe returning aluminium ingots would therefore skip these existing final operations. Using normal bauxite or alumina feedstock preserves the distinction between extraction/refining and ingot production. This closes the normal final-operation source gap, not complete progression, logistics or runtime verification.

The initial pack search failed because there was no top-level `scripts` folder and reported a file-not-found I/O error. It was reported immediately. Bounded follow-up found no `.zs` or `.groovy` files in the inspected config/raw search scope. No script override of these operations was established, and no installed runtime recipe dump or full-pack override audit was performed. These limits should not be presented as proof that every target installation is identical. No checkout, index, recipe or dependency was changed.

### Focused Follow-Up: Sifter Fluid Shape

At the inspected current GT commit, `RecipeMaps.sifterRecipes` explicitly declares `.maxIO(1, 9, 1, 1)`: one item input, nine item outputs, one fluid input and one fluid output. A single fluid input with scandium as an item output is therefore not excluded by this map's capacity. The old proposal still has no established existing scandium-extraction recipe or verified actual machine execution. Map capacity alone does not prove a recipe exists or that every Sifter controller supports the intended runtime inputs. This corrects an assumed capacity objection without accepting the proposed recipe. [Current Sifter map][sifter-map]

[core-al]: https://github.com/GTNewHorizons/NewHorizonsCoreMod/blob/9aa0afc8711f3efbe3afc0d11ec44dcbf5b87442/src/main/java/com/dreammaster/gthandler/recipes/BlastFurnaceRecipes.java#L438-L468
[core-al-dust]: https://github.com/GTNewHorizons/NewHorizonsCoreMod/blob/9aa0afc8711f3efbe3afc0d11ec44dcbf5b87442/src/main/java/com/dreammaster/gthandler/recipes/BlastFurnaceRecipes.java#L470-L473
[recipe-voltage]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/api/enums/TierEU.java#L27-L28
[sifter-map]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/api/recipe/RecipeMaps.java#L484-L488
