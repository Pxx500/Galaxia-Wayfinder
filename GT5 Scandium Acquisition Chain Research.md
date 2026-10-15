---
type: source
status: unreviewed
tags:
  - galaxia/alpha
  - wayfinder/source
---

# GT5 Scandium Acquisition Chain Research

Source: Current GT5-Unofficial, NewHorizonsCoreMod, GT-New-Horizons-Modpack and the Blood Magic meteor implementation
Imported: 2026-10-11

[[Sources]]

## Source Snapshot

### Result And Correction Boundary

An existing intended scandium acquisition path was found in pack content: the Blood Magic `Chinfinity` meteor profile supplies `oreEndstoneScandium`, which can be processed through normal ore/dust forms and GT blast/cooling operations. Its configured focus is a ZPM Circuit Assembler, and summoning consumes that focus plus 80000000 life essence. It is not an early Monazite or Bastnasite recipe.

The current Monazite and Bastnasite recipe owner was inspected directly. No scandium output was found there. Those branches do produce Samarium and other rare-earth materials. This does not prove that the owner's recollection was wrong about an older version or another pack, and it does not prove worldwide acquisition exclusivity.

The previous ore-definition audit only failed to establish acquisition within its checked scope. It must not be generalized into "Scandium is unobtainable" or "Scandium has no existing source." The meteor profile is positive counterevidence.

### Versions And Verification

| Repository | Local checkout used for graph/literal discovery | Current upstream source checked |
| --- | --- | --- |
| GT5-Unofficial | `2259bc64244f9f7fc58e039d8e89ca40dd17c929` | `03f76356146f497c6c8f21d9225fe28de57136a1`, committed 2026-10-10 19:19:48 UTC |
| NewHorizonsCoreMod | `38b12ce3d59f8061742e47a63c6f1f29b7959313` | `9aa0afc8711f3efbe3afc0d11ec44dcbf5b87442`, committed 2026-10-09 19:22:55 UTC |
| GT-New-Horizons-Modpack | `965462fb102acf429818c07388bdf5f50137c662` | `83b3fb26cd9979e0256c7568bdf8c6f87579b532`, committed 2026-10-10 04:04:30 UTC |
| BloodMagic | `6776676ef209d8c142a1a159519c40d06c7e0bc7` | `10a36f6413b8a7ce6ebf16ca8b04614ff15566cd`, committed 2026-09-29 06:45:57 UTC |

GT and CoreMod were fully reindexed at task start. Blood Magic was indexed after its first lookup reported that it had no index. Code discovery used the graph, with bounded literal searches for material/recipe/config strings. Relevant current files were checked through HTTP 200 immutable source reads. No code, dependency, game, build, test, commit or publication operation occurred. The only task document created is this source note.

This is source verification of a configured path, not a running-pack recipe dump or successful meteor summon. All four mods/configuration must actually be loaded, and ore dictionary registration must resolve the expected blocks. No absolute earliest tier across all optional mods is certified.

### Monazite And Bastnasite: What The Current Chains Produce

The graph traces `RecipeLoader.loadLanthanideRecipes` to `GTNHLanthanides.postInit`, which calls it directly. These are loaded recipe definitions, not unused proposal text. The full current `gtnhlanth/loader/RecipeLoader.java` and `WerkstoffMaterialPool.java` were fetched and checked for scandium references. Neither file contains the name. The output branches below were read explicitly. [Loader invocation][lanth-init] [Recipe owner][lanth-recipes] [Intermediate definitions][lanth-materials]

| Checked branch | Actual output | Exact relevant operation |
| --- | --- | --- |
| Monazite cooled concentrate | Monazite Rarer Earth Sediment and Europium III Oxide | Electromagnetic Separator, EV, 30 s. Sediment chance 90%, oxide chance 5% |
| Monazite sediment | Heterogenous Halogenic Rare Earth Mixture | 1 sediment dust plus 1000 chlorine, EBF, HV, 25 s, 1200 K |
| Saturated monazite mixture | Samaric Residue | 4 mixture dust to 3 residue dust plus 400 chloromethane, Centrifuge, EV, 157.5 s |
| Samaric Residue | 2 Samarium dust plus 1 Gadolinium dust | 3 residue dust, Sifter, EV, 6.65 s. Both outputs have 100% recipe chances |
| Saturated bastnasite oxides | Neodymic and Samaric Rare Earth Concentrates | 1000 fluid, Centrifuge, HV, 45 s. Chances 80% and 50%, plus 750 diluted acetone |
| Fluorinated samaric concentrate | Holmium and Samarium-Terbium Mixture | 8 concentrate plus 4 calcium to 1 holmium and 4 mixture dust, EBF, EV, 61 s, 1200 K |
| Samarium-Terbium mixture follow-up | Terbium Nitrate and Samaric Residue | Nitrate preparation uses HV. Copper separation uses EV, 160 s. Residue can feed the same Samarium/Gadolinium Sifter operation |
| Samarium Ore Concentrate side route | Samarium dust and Thorianite | Calcium dephosphating is EV. 6 dephosphated concentrate dust gives 1 samarium at 90% and 2 thorianite at 80%, Centrifuge, EV, 10 s |

[Monazite and residue operations][monazite-tail] [Bastnasite and side operations][bastnasite-tail]

No complete Monazite/Bastnasite-to-Sc path, scandium yield or associated earliest machine tier was established. It would be false precision to invent them. Samarium and Scandium are separate GT element identities. The similar names are a possible explanation for the recollection, not a conclusion about what the owner meant.

Additional checks included LanthanidesRecipeOutputs, the normal Rare Earth material definition, the ordinary ore-processing registrators, GT++'s Scandium wrapper and named CoreMod source hits. The conversion helper redirects Cerium and Samarium outputs to their mixture/concentrate stages, not to Scandium. The Scandium `TRANSMUTABLE_NUGGETS` tag was followed with a literal consumer search. In the checked local GT Java source, only the tag definition and material declarations matched, so this was not established as an active acquisition recipe. A conditional Scandium plasma-cell fuel case consumes an existing form and is not an acquisition route. [Conversion helper][lanth-conversion] [Scandium definition][sc-definition] [Conditional plasma consumer][sc-plasma]

CoreMod's named searches found only removal of old Monazite crafting recipes, not a named scandium producer. A current compare against the local CoreMod checkout returned 176 changed files with no Scandium patch hit. The analogous GT compare reached GitHub's 300-file response size, so it was not used as proof of complete current-repository absence. Current rare-earth owner files and positive path files were fetched directly.

### Positive Acquisition: Chinfinity Meteor

Current pack `config/BloodMagic/meteors/Chinfinity.json` explicitly includes `OREDICT:oreEndstoneScandium:100`, radius 16, cost 80000000, and focus `gregtech:gt.blockmachines:1186`. The same profile exists in the local pack checkout. [Meteor profile][meteor-profile]

Blood Magic's MeteorRegistry loads JSON files from exactly `config/BloodMagic/meteors` and registers each parsed meteor. Its component parser treats the final `100` as selection weight. It resolves the ore dictionary name to an ItemBlock. It is not a count of 100 ore blocks and not a 100% chance. [Config loading][meteor-registry] [Component parser][meteor-component]

The Mark of the Falling Tower ritual recognizes a matching dropped focus item, checks the owner's life essence against the profile cost, creates the meteor, decrements the focus stack by one, deactivates the ritual and syphons that cost from the soul network. Thus the focus is consumed, not a reusable recipe catalyst. The ritual is registered as `AW019FallingTower` with ritual level argument 2. This audit does not interpret that number as a specific altar tier or fully trace the magic unlock chain. [Activation handler][meteor-activation] [Ritual registration][meteor-ritual]

GT metadata ID 1186 is `CIRCUIT_ASSEMBLER_ZPM`. Its registered machine has tier 7, and MTERecipeLoader registers its tier-7 machine crafting recipe. The input pattern uses the tier's hull, conveyor, robot arm, wire, emitter and better circuit. This establishes a concrete high-tech focus gate, independently of unverified magic prerequisites. It does not prove the absolute earliest way to obtain that focus through every external mod. [Focus identity][focus-id] [Machine registration][focus-machine] [Focus recipe][focus-recipe]

At impact, Blood Magic selects weighted components and only places meteor blocks at air positions within the radius. The size can also be affected by ritual reagents. The actual scandium count is random and can be affected by available space, reagents, and successfully resolved ore entries. No fixed ore yield per summon is asserted. Its GT integration marks generated ore as natural. The profile is nevertheless an intended positive source, not merely a backpack acceptance list or a downstream conversion that assumes ore already exists. [Impact and selection][meteor-impact]

### Raw Ore To Usable Dust And Metal

The following is a concrete configured processing path from the meteor's normal ore identity. Ender IO conversions provide explicitly named ore recipes, while later steps follow common GT registrators. They do not depend on Monazite or Bastnasite.

| Step | Inputs to outputs | Machine and cost | Yield/time distinction |
| --- | --- | --- | --- |
| Raw ore crushing | 1 `oreEndstoneScandium` to 1 `crushedScandium`, plus a second crushed output at 50% and endstone dust at 50% | SAG Mill, configured `energyCost=3600` | One crushed unit is specified guaranteed. Bonuses are random. The XML's total energy cost is not a GT EU/t or fixed machine-time declaration |
| Crushed to impure dust | 1 crushed scandium to 1 impure scandium dust | SAG Mill, configured `energyCost=3600` | Fixed primary quantity in this explicit config recipe |
| Impure to normal dust | 1 impure scandium dust to normal scandium dust, with the generic byproduct branch | GT Centrifuge, 5 EU/t | Source-derived duration 360 ticks, 18 s. Primary dust chance is 100%, byproduct chance 11.11% in the relevant common branch |
| Dust to hot ingot | 1 scandium dust, circuit 1, to 1 hot scandium ingot | EBF, MV recipe EU/t 120, 1814 K | Source-derived duration 1814 ticks, 90.7 s |
| Hot to normal ingot | 1 hot scandium ingot to 1 scandium ingot | Vacuum Freezer, MV recipe EU/t 120 | Source-derived duration 135 ticks, 6.75 s |

[Ore crushing config][sag-ore] [Impure dust config][sag-dust] [Centrifuge registrator][dust-cleaning] [EBF registrator][dust-blast] [Cooling registrator][ingot-cooling]

The GT figures are derived from actual registrator formulas and Scandium's element mass of 45, not copied from a live NEI listing. Element Sc is defined as 21 protons, 24 neutrons and zero additional mass. ProcessingDust uses mass times 8 ticks for the relevant purification branch, integer mass/40 times required heat for blast processing, and ProcessingIngot uses mass times 3 ticks for cooling. Material defaults enable blast and freezer generation, and Scandium does not disable them. Form registration is required for these generated recipes to exist in the running pack. [Scandium definition][sc-definition] [Element mass][sc-element] [Default recipe generation][material-defaults]

Ordinary GT ore-processing owners also support normal crushed/washed/dust forms. The explicit SAG route above is one path with a named pack configuration, not a claim that SAG milling is mandatory or uniquely efficient.

Recipe electrical tier and heat are different gates. Cupronickel heat is 1801 K, below 1814 K at MV. Current EBF heating capacity adds 100 K per input-voltage tier above MV, so HV input with Cupronickel reaches 1901 K. A hotter coil is another possibility. The found source's ZPM focus gate is later than these final processing requirements. No new scandium recipe, balance number or machine rule is proposed. [Coil heat][coil-heat] [EBF capacity][ebf-capacity]

### Practical Scope Of The Result

- Existing source found: a configured Blood Magic meteor leading to usable normal Scandium through existing forms and common processing
- Monazite/Bastnasite source not found: direct inspection shows their checked named branches produce other elements, especially Samarium, not Scandium
- Earliest global availability unresolved: the documented route has a ZPM machine focus plus Blood Magic ritual and 80000000 life essence requirements. The full magic unlock chain and every optional source were not audited
- Random acquisition versus recipe yield distinguished: ore composition is weighted/random, while downstream primary outputs and chance bonuses are recorded separately
- No world-generation exclusivity, early lunar availability or Al-Sc alloy recipe is accepted by this note

### Cheap Local Verification Anchors

These paths refer to the local revisions listed above, so some line numbers differ from current upstream:

| Evidence | Local file and line |
| --- | --- |
| Sc ore and trigger profile | `C:/Users/Pxx500/Documents/GitHub/GT-New-Horizons-Modpack/config/BloodMagic/meteors/Chinfinity.json`, lines 34 and 37 to 39 |
| Raw ore SAG conversion | `C:/Users/Pxx500/Documents/GitHub/GT-New-Horizons-Modpack/config/enderio/SAGMillRecipes_User.xml`, recipe starts at 5451 |
| Crushed SAG conversion | Same XML, recipe starts at 1495 |
| Focus item ID | `C:/Users/Pxx500/Documents/GitHub/GT5-Unofficial/src/main/java/gregtech/api/enums/MetaTileEntityIDs.java`, line 703 |
| Focus machine tier | `C:/Users/Pxx500/Documents/GitHub/GT5-Unofficial/src/main/java/gregtech/loaders/preload/LoaderMetaTileEntities.java`, lines 8827 to 8830 |
| Monazite Samarium/Gadolinium output | `C:/Users/Pxx500/Documents/GitHub/GT5-Unofficial/src/main/java/gtnhlanth/loader/RecipeLoader.java`, lines 1541 to 1547 |
| Blast generator | `C:/Users/Pxx500/Documents/GitHub/GT5-Unofficial/src/main/java/gregtech/loaders/oreprocessing/ProcessingDust.java`, lines 100 to 118 |
| Ritual focus consumption | `C:/Users/Pxx500/Documents/GitHub/BloodMagic/src/main/java/WayofTime/alchemicalWizardry/common/rituals/RitualEffectSummonMeteor.java`, lines 50 to 77 |

### Tool Limitations Recorded

The first Blood Magic graph search returned "project not found or not indexed." It was reported immediately, the existing repository was indexed, and graph discovery then succeeded. A guessed plural GT registration method returned "symbol not found" and was resolved to the actual singular `registerCircuitAssembler`. A bounded Blood Magic search included a nonexistent guessed `Rituals.java` path, reported an I/O error, and continued through valid hits in the actual AlchemicalWizardry registration file. No failing MCP backend was silently bypassed or claimed fixed by shell results.

[lanth-init]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gtnhlanth/GTNHLanthanides.java#L53-L59
[lanth-recipes]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gtnhlanth/loader/RecipeLoader.java#L1178-L3207
[lanth-materials]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gtnhlanth/common/register/WerkstoffMaterialPool.java
[monazite-tail]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gtnhlanth/loader/RecipeLoader.java#L1462-L1547
[bastnasite-tail]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gtnhlanth/loader/RecipeLoader.java#L1678-L1771
[lanth-conversion]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gtnhlanth/util/LanthanidesRecipeOutputs.java#L39-L86
[sc-definition]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/loaders/materials/MaterialsInit.java#L1568-L1587
[sc-plasma]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/loaders/oreprocessing/ProcessingCell.java#L371-L373
[meteor-profile]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/83b3fb26cd9979e0256c7568bdf8c6f87579b532/config/BloodMagic/meteors/Chinfinity.json#L34-L39
[meteor-registry]: https://github.com/GTNewHorizons/BloodMagic/blob/10a36f6413b8a7ce6ebf16ca8b04614ff15566cd/src/main/java/WayofTime/alchemicalWizardry/common/summoning/meteor/MeteorRegistry.java#L25-L45
[meteor-component]: https://github.com/GTNewHorizons/BloodMagic/blob/10a36f6413b8a7ce6ebf16ca8b04614ff15566cd/src/main/java/WayofTime/alchemicalWizardry/common/summoning/meteor/MeteorComponent.java#L69-L105
[meteor-activation]: https://github.com/GTNewHorizons/BloodMagic/blob/10a36f6413b8a7ce6ebf16ca8b04614ff15566cd/src/main/java/WayofTime/alchemicalWizardry/common/rituals/RitualEffectSummonMeteor.java#L23-L80
[meteor-ritual]: https://github.com/GTNewHorizons/BloodMagic/blob/10a36f6413b8a7ce6ebf16ca8b04614ff15566cd/src/main/java/WayofTime/alchemicalWizardry/AlchemicalWizardry.java#L4052-L4057
[meteor-impact]: https://github.com/GTNewHorizons/BloodMagic/blob/10a36f6413b8a7ce6ebf16ca8b04614ff15566cd/src/main/java/WayofTime/alchemicalWizardry/common/summoning/meteor/Meteor.java#L57-L90
[focus-id]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/api/enums/MetaTileEntityIDs.java#L703
[focus-machine]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/loaders/preload/LoaderMetaTileEntities.java#L8827-L8838
[focus-recipe]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/loaders/load/MTERecipeLoader.java#L499-L505
[sag-ore]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/83b3fb26cd9979e0256c7568bdf8c6f87579b532/config/enderio/SAGMillRecipes_User.xml#L5437-L5446
[sag-dust]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/83b3fb26cd9979e0256c7568bdf8c6f87579b532/config/enderio/SAGMillRecipes_User.xml#L1481-L1488
[dust-cleaning]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/loaders/oreprocessing/ProcessingDust.java#L555-L569
[dust-blast]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/loaders/oreprocessing/ProcessingDust.java#L100-L118
[ingot-cooling]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/loaders/oreprocessing/ProcessingIngot.java#L195-L204
[sc-element]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/api/enums/Element.java#L38
[material-defaults]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/api/enums/Materials.java#L1177-L1179
[coil-heat]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/api/enums/HeatingCoilLevel.java#L7-L34
[ebf-capacity]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/common/tileentities/machines/multi/MTEElectricBlastFurnace.java#L226-L227

## 2026-10-11 Consumer Follow-Up

### Question And Result

The owner reports that Discord confirms Scandium has no meaningful progression use and that the Chinfinity entry is incidental. This follow-up checks concrete named consumers, not the acquisition path again. No authored GT or CoreMod progression recipe using Scandium as an ingredient was found in the bounded source collection. The recorded late meteor focus is an acquisition gate for that profile, not evidence that Scandium itself gates an important machine or technology.

Accordingly, giving normal Scandium an earlier source does not demonstrably bypass another important authored recipe in the checked evidence. This is a scoped conclusion, not certification that every mod, script or future version has no use. It does not approve a new lunar source or recipe.

### Collection And Current Source

GT and CoreMod were fully reindexed again before graph discovery. Case-insensitive Scandium literal collection over their local `src/main/java` returned 13 GT source lines and zero CoreMod lines. The GT hits were all accounted for below. Graph search likewise found only the Scandium material declarations, loader and GT++ wrapper, with no named CoreMod symbol. Compound-name and formula searches were included in the same bounded pass.

Fresh GitHub checks confirmed the upstream revisions remain GT `03f76356146f497c6c8f21d9225fe28de57136a1`, CoreMod `9aa0afc8711f3efbe3afc0d11ec44dcbf5b87442` and pack `83b3fb26cd9979e0256c7568bdf8c6f87579b532`. The relevant GT reference files were read again from current immutable HTTP 200 source. Local discovery uses the older clean checkouts listed earlier, so it is not a full literal search of a newly checked-out current tree. Current verification covered the concrete named references, not arbitrary reflective or generated consumers throughout the modpack.

### Concrete References Classified

| Reference | What it actually does | Classification and practical impact |
| --- | --- | --- |
| `MaterialsInit.loadScandium` | Declares the Sc element, dust/metal/ore forms and 1814 K required blast processing | Material and normal processing definition, not a machine or technology ingredient |
| `Materials.Scandium`, `MaterialsIDMap` and `Element.Sc` | Declare the material field, register internal material ID 27, and supply element data | Registry identity, not a progression recipe |
| `LoaderGTBlockFluid` | Includes Scandium in the normal metal storage-block family | Form/storage registration. The presence of a block is not a valuable downstream consumer |
| `Textures` | Registers the Scandium block texture and includes it in the storage-texture array | Rendering infrastructure, no material demand |
| `AssemblyLineServer.fillMap` | Maps storage-block localization identifiers to names such as Block of Scandium | Name/display lookup, not an Assembly Line recipe. The class name alone must not be counted as progression use |
| `MaterialsElements.SCANDIUM` | Wraps the normal GT material for GT++ | Wrapper identity. No named reader of this field appeared in the graph or literal source collection |
| `ProcessingCell` Scandium switch case | Inside the generic `cellPlasma` branch, assigns fuel value 193536 and fuel type 4 before adding to the fuel map | Conditional plasma fuel consumer, not an authored dust/ingot progression recipe |
| Generic ore/dust/ingot owners | Process normal ore, dust, hot ingot, ingot and other generated forms as described earlier | Form conversion and ordinary processing. Earlier supply changes quantity/availability, not a demonstrated independent tech unlock |

[Scandium declaration][sc-definition] [Material ID][consumer-id] [Storage forms][consumer-storage] [Name mapping][consumer-name-map] [GT++ wrapper][consumer-wrapper] [Plasma branch][consumer-plasma] [Scandium fuel value][sc-plasma]

The plasma case is conditional on a matching plasma-cell registration. Scandium's checked material builder does not call `addPlasma()`, and the collected source did not establish an actual Scandium dust/metal-to-plasma production path. The fuel number therefore must not be presented as proof that ordinary earlier Scandium unlocks a new power route. It is also not correct to erase the fuel case and say the source has literally no potential consumer. [Material builder][sc-definition] [Plasma branch][consumer-plasma]

The material retains `TRANSMUTABLE_NUGGETS`. The earlier bounded search found no active Java recipe consumer for this tag in the checked GT source. It is not evidence of a meaningful authored Scandium progression recipe or a confirmed transmutation route.

### Named Pack Configuration

The same case-insensitive collection over local pack `config` and `raw` found Scandium in exactly three files:

- `config/BloodMagic/meteors/Chinfinity.json`: one Sc ore-list entry. This is supply, not downstream demand
- `config/forestry/backpacks.cfg`: 25 item-name entries for accepted storage forms. Backpack acceptance is not consumption
- `config/enderio/SAGMillRecipes_User.xml`: 31 named references within ordinary Sc ore/crushed/dust conversion recipes. These supply or transform Sc forms, rather than making a technology component from Sc

No named alloy, circuit, machine, tool-progression, research or chemistry consumer appeared in that configuration collection. This does not cover the semantics of every dynamically generated recipe or every external mod. The already cited current meteor and SAG source excerpts show the actual role of those positive hits. [Meteor supply][meteor-profile] [SAG form conversion][sag-ore] [SAG dust conversion][sag-dust]

### Oxide, Chloride And Nitrate Reuse Check

No existing Scandium Oxide, Scandium Chloride or Scandium Nitrate material identity or recipe was found in the checked GT/CoreMod source. Graph symbol queries returned no matching compound names. The same literal collection had no longer Scandium compound names, and a small formula check also found no `Sc2O3`, `ScCl3` or `Sc(NO3)3` occurrence in their local Java source. The current canonical Scandium builder declares the elemental material and normal forms, not those compounds. [Canonical declaration][sc-definition]

This is a reuse finding, not permission to invent names, compositions, yields or reactions. A proposed short refinery using any of those compounds must label them as new proposed functional intermediates unless another authoritative existing definition is found. No universal absence across uninspected mods or aliases is asserted.

### Conclusion And Limits

The bounded evidence supports separating incidental acquisition from meaningful progression demand. The only concrete named fuel handling is generic and conditional, and the rest is registration, rendering, naming, storage or form processing. No important authored recipe bypass caused by earlier normal Scandium supply was demonstrated. Its 1814 K normal metal-processing contract remains a real source fact, but that alone does not establish a high-tier downstream role.

No recipe, material, design decision, code, build, test, commit or publication was added. No new tool failure occurred during this consumer follow-up. Expected zero-match searches were handled as zero matches, not backend failures. The acquisition audit and Blood Magic prerequisites were not repeated or expanded.

[consumer-id]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/api/enums/MaterialsIDMap.java#L33
[consumer-storage]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/loaders/preload/LoaderGTBlockFluid.java#L818-L825
[consumer-name-map]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/api/util/AssemblyLineServer.java#L231-L253
[consumer-wrapper]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gtPlusPlus/core/material/MaterialsElements.java#L44
[consumer-plasma]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/loaders/oreprocessing/ProcessingCell.java#L186-L201

### Small Residue-Identity Reuse Check

The coordinator additionally checked whether Red Mud or a Bauxite Sludge residue already exists. This was a literal identity check, not a new refinery design.

| Requested concept | Result in checked source |
| --- | --- |
| Red Mud | Yes, `Materials.RedMud` is defined by GT. CoreMod has named recipes using its fluid form |
| GT++ Red Mud | Yes, `GTPPFluids.RedMud` is also declared and registered. Do not assume it is the same registered identity as `Materials.RedMud` merely because both use the words Red Mud |
| Bauxite Sludge | No identity with that exact name was found in the checked GT/CoreMod Java source |
| Existing bauxite residue | Yes, `Materials.BauxiteSlag` is an existing dust material used by BauxiteRefineChain |

[GT Red Mud definition][consumer-residues] [Bauxite Slag definition][consumer-bauxite-slag] [GT++ fluid definition][consumer-gtpp-redmud] [CoreMod Red Mud consumer][consumer-core-redmud]

No Scandium content or recovery capability follows from those names. The owner can consider existing residues during design, but a new Sc-bearing composition or leach operation would remain proposed content unless a matching existing contract is separately established. No recipe or identity was added here.

[consumer-residues]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/loaders/materials/MaterialsInit.java#L11244-L11253
[consumer-bauxite-slag]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/loaders/materials/MaterialsInit.java#L15565-L15573
[consumer-gtpp-redmud]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gtPlusPlus/core/fluids/GTPPFluids.java#L115-L121
[consumer-core-redmud]: https://github.com/GTNewHorizons/NewHorizonsCoreMod/blob/9aa0afc8711f3efbe3afc0d11ec44dcbf5b87442/src/main/java/com/dreammaster/gthandler/recipes/CentrifugeRecipes.java#L71-L84
