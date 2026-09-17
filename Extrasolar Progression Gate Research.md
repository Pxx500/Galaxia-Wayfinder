---
type: source
status: unreviewed
tags:
  - galaxia/alpha
  - wayfinder/source
---

# Extrasolar Progression Gate Research

Source: GTNH 2.8.0 release manifest and the version-pinned GTNH repositories cited below
Imported: 2026-09-16

## Source Snapshot

This is a bounded primary-source investigation of Ore Tiers 9 and 10. Ore Tier means the destination grouping in the accepted Ore Sheet 2.8.0 baseline. Rocket Tier means the original travel access check. Recipe voltage means the explicit recipe EU/t tier, not a claim about the minimum hatch arrangement or the player's overall technology tier.

| Destination Group | Source-Backed Entry | Progression-Bearing Outcome | Limit |
| --- | --- | --- | --- |
| Ore Tier 9: Barnarda C/E/F, Alpha Centauri Bb, Tau Ceti E, Vega B | Tier 8 Rocket. Its hull alloy combines Tier 7 plating and black plutonium in a UEV-rated Assembly Line recipe. The rocket computer recipe is UV-rated | Barnarda C logs and biological culture participate in Xenoxene and Radox production. Tau Ceti E seaweed supplies Bio Medium. Vega B small Infinity Catalyst supplies the ore-based catalyst route | These are not six independently proven mandatory visits. The UHV quest chapter does not make the whole rocket production chain UHV-rated |
| Ore Tier 10: Anubis, Horus, Maahes, Mehen Belt, Neper, Seth | Shuttle and Mothership. Amun-Ra destinations have configured Rocket Tier 9. The navigation console, shuttle schematic, and lightweight hull alloy have UEV-rated Assembly Line recipes | Seth Raw Tengam is processed into Attuned Tengam and consumed directly by the UEV motor recipe. Other new veins offer bulk access to materials, several already required to construct the Mothership route | The source route is not an ordinary Tier 9 Rocket recipe. A vein first occurring here does not establish first access to all its constituent materials |

These are original GTNH mechanics, not accepted Galaxia recipes or destination requirements. Mandatory dungeon, boss, and schematic gates remain source provenance only. Galaxia's accepted boss-free and capability-based progression replaces those mechanisms.

## Pinned Baseline

The [GTNH 2.8.0 manifest](https://github.com/GTNewHorizons/DreamAssemblerXXL/blob/035dc34a6199b51114cc142ccc7937e1c6872235/releases/manifests/2.8.0.json) pins the component versions. Local release tags were resolved without changing checkouts. Claims below use `git show` at these commits, not current working trees.

| Repository | Release | Commit |
| --- | --- | --- |
| GT-New-Horizons-Modpack | 2.8.0 | `c3ba07ccba1b772777f6fc57e53bb70c8547adb7` |
| GT5-Unofficial | 5.09.51.470 | `000a4d9b24d77f40a79da7a105bb79ac7efca817` |
| NewHorizonsCoreMod | 2.7.260 | `fe1a49ae577fee5ec4c1cf53d2545b475fb6b5af` |
| Galaxy-Space-GTNH | 1.1.121-GTNH | `2a7b220dec76560ef0af109c4b6cb53c8470c3fa` |
| amunra | 0.8.2 | `7ee2411bfa2abcbe8a7bf3d4053c1d012b86bc8d` |

## Ore Tier 9 Entry

The original destination registrations set Rocket Tier 8 for [Barnarda C/E/F](https://github.com/GTNewHorizons/Galaxy-Space-GTNH/blob/2a7b220dec76560ef0af109c4b6cb53c8470c3fa/src/main/java/galaxyspace/BarnardsSystem/BarnardsPlanets.java#L57), [Alpha Centauri Bb](https://github.com/GTNewHorizons/Galaxy-Space-GTNH/blob/2a7b220dec76560ef0af109c4b6cb53c8470c3fa/src/main/java/galaxyspace/ACentauriSystem/ACentauriPlanets.java#L48), [Tau Ceti E](https://github.com/GTNewHorizons/Galaxy-Space-GTNH/blob/2a7b220dec76560ef0af109c4b6cb53c8470c3fa/src/main/java/galaxyspace/TCetiSystem/TCetiPlanets.java#L74), and [Vega B](https://github.com/GTNewHorizons/Galaxy-Space-GTNH/blob/2a7b220dec76560ef0af109c4b6cb53c8470c3fa/src/main/java/galaxyspace/VegaSystem/VegaPlanets.java#L39).

The [Tier 8 hull-alloy recipe](https://github.com/GTNewHorizons/NewHorizonsCoreMod/blob/fe1a49ae577fee5ec4c1cf53d2545b475fb6b5af/src/main/java/com/dreammaster/gthandler/recipes/AssemblingLineRecipes.java#L122-L132) consumes one Tier 7 heavy-duty plate, fourteen compressed black plutonium plates, twelve black plutonium bolts, and 576 mB solder. It runs at `TierEU.RECIPE_UEV` and uses UV-rated scanning research. The [rocket-computer table](https://github.com/GTNewHorizons/NewHorizonsCoreMod/blob/fe1a49ae577fee5ec4c1cf53d2545b475fb6b5af/src/main/java/com/dreammaster/gthandler/recipes/CircuitAssemblerRecipes.java#L42-L64) assigns UV to the Tier 8 computer. These are separate recipe requirements.

The [Pluto dungeon quest](https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/SpaceRace-AAAAAAAAAAAAAAAAAAAAIg==/PlutoDungeon-AAAAAAAAAAAAAAAAAAAKlA==.json#L11) names the original Tier 8 schematic. This is not a recommendation to add a Galaxia dungeon or schematic gate.

## Ore Tier 9 Resources And Consumers

The pinned [UHV Final Frontier quest](https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier9UHV-AAAAAAAAAAAAAAAAAAAALg==/TheFinalFrontier-AAAAAAAAAAAAAAAAAAAKWA==.json#L11) identifies the destination group, Cadmium and Samarium veins, small-ore exceptions, and biological resources. Its prose is source guidance, not an exhaustive acquisition proof.

| Resource And Location | Concrete Downstream Use | Earlier Or Alternate Access Established Here |
| --- | --- | --- |
| Barnarda C logs, saplings, and dirt | Logs plus Xenoxene make Raw Radox in a UV-rated Pyrolyse recipe. The Radox chain produces polymer used by the UEV-rated lightweight shuttle-alloy recipe | Saplings and dirt support renewable logs after acquisition. No pre-extrasolar bootstrap alternative was verified |
| Tau Ceti E seaweed | Seaweed extract is consumed by all three inspected Raw Bio Medium recipes. The first uses a LuV-rated Bacterial Vat with stemcells, Unknown Crystal, tritanium, and plutonium-level radiation. Sterilized Bio Medium is consumed by the UV-rated cleanroom Bio Board recipe | Industrial cultivation is a documented repeat-supply route, but the quest explicitly requires initial seaweed. This is not evidence of a pre-visit alternative |
| Barnarda and Tau Ceti biological cultures | Their plasmid and DNA combine into Xenoxene Xenoxsis. The inspected Xenoxene Bacterial Vat recipe is UEV-rated. Xenoxene and Barnarda logs participate in the Radox chain | This pass did not establish that every possible Xenoxene route has the same bootstrap requirements |
| Vega B small Infinity Catalyst ore | Sixty-four dust produce one Avaritia Infinity Catalyst in the inspected HV-rated Neutronium Compressor recipe. Infinity Catalyst also appears in the shuttle schematic inputs and more efficient Bio Medium recipes | The catalyst quest explicitly documents an alternate Avaritia crafting recipe. Therefore Vega B is the documented ore route, not a proven universal mandatory visit |
| Barnarda E/F, Tau Ceti E, Vega B small Awakened Draconium, and Barnarda F small Bedrockium | Both materials are explicit inputs to the shuttle schematic before the Amun-Ra system | Multiple same-Ore-Tier small-ore destinations are documented. The later Mehen and Anubis/Horus veins cannot automatically be treated as initial access |
| Alpha Centauri Bb and the group’s Cadmium/Samarium veins | The shuttle schematic explicitly consumes ore-form Samarium, Tartarite, Cadmium, Caesium, Lanthanum, and Cerium | This proves a source recipe consumer, not that Alpha Centauri Bb is mandatory or that each constituent material is new. Its unique mandatory material role remains unresolved |

Recipe evidence: [culture composition](https://github.com/GTNewHorizons/NewHorizonsCoreMod/blob/fe1a49ae577fee5ec4c1cf53d2545b475fb6b5af/src/main/java/com/dreammaster/bartworksHandler/BacteriaRegistry.java#L83-L102), [Radox chain](https://github.com/GTNewHorizons/NewHorizonsCoreMod/blob/fe1a49ae577fee5ec4c1cf53d2545b475fb6b5af/src/main/java/com/dreammaster/bartworksHandler/BacteriaRegistry.java#L212-L264), [Xenoxene and Bio Medium vats](https://github.com/GTNewHorizons/NewHorizonsCoreMod/blob/fe1a49ae577fee5ec4c1cf53d2545b475fb6b5af/src/main/java/com/dreammaster/bartworksHandler/BacteriaRegistry.java#L269-L306), [Bio Board](https://github.com/GTNewHorizons/NewHorizonsCoreMod/blob/fe1a49ae577fee5ec4c1cf53d2545b475fb6b5af/src/main/java/com/dreammaster/gthandler/recipes/CircuitAssemblerRecipes.java#L94-L106), and [Infinity Catalyst compression](https://github.com/GTNewHorizons/NewHorizonsCoreMod/blob/fe1a49ae577fee5ec4c1cf53d2545b475fb6b5af/src/main/java/com/dreammaster/gthandler/recipes/NeutroniumCompressorRecipes.java#L381-L384).

Documented alternatives: [Industrial Scale Seaweed Production](https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier9UHV-AAAAAAAAAAAAAAAAAAAALg==/IndustrialScaleS-AAAAAAAAAAAAAAAAAAAKeQ==.json#L11) and [Compressing The Cosmos](https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier9UHV-AAAAAAAAAAAAAAAAAAAALg==/CompressingtheCo-AAAAAAAAAAAAAAAAAAAKcg==.json#L11). The cultivation quest says Unknown Water comes from the same planet, while Final Frontier points to Barnarda C. Fluid placement was not independently resolved in this pass.

## Ore Tier 10 Entry

The [Mothership quest](https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/SpaceRace-AAAAAAAAAAAAAAAAAAAAIg==/CanIBuildAMother-1R8whL35Qnm93uBUpchI0A==.json#L15) identifies it as the route to Amun-Ra. The [Shuttle quest](https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/SpaceRace-AAAAAAAAAAAAAAAAAAAAIg==/AT0RocketWhat-Oiy66UDmTVeZ95pN0yunBg==.json#L19) explains that the shuttle creates and accesses the Mothership rather than flying directly to planets.

The [pack configuration](https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/GalacticraftAmunRa.cfg) sets Amun-Ra `default_tier=9`, `maxMothershipTier=10`, fixed mass 1500 kg, and jet fuel to Naquadah Based Liquid Fuel Mk II. The [pinned Amun-Ra provider](https://github.com/GTNewHorizons/amunra/blob/7ee2411bfa2abcbe8a7bf3d4053c1d012b86bc8d/src/main/java/de/katzenpapst/amunra/world/AmunraWorldProvider.java#L56-L58) checks the configured destination tier. Rocket Tier 9 does not mean Ore Tier 9 or voltage Tier 9.

The [Mothership integration recipes](https://github.com/GTNewHorizons/NewHorizonsCoreMod/blob/fe1a49ae577fee5ec4c1cf53d2545b475fb6b5af/src/main/java/com/dreammaster/scripts/ScriptAmunRa.java#L376-L504) establish several independent requirements:

- The navigation console uses researchable Assembly Line manufacturing at UEV recipe voltage. Inputs include Infinity, enriched naquadah alloy, Mutated Living Solder, UHV circuits and components, and Tier 8 rocket computers
- Rocket Engine Jet production is UHV-rated and consumes Infinity, UHV pumps and circuits, Super Coolant, and Mutated Living Solder
- The shuttle schematic is a UEV-rated researchable Assembly Line recipe. It consumes the six ore forms listed above plus Bedrockium, Awakened Draconium, Cosmic Neutronium, Infinity Catalyst, Infinity, and UHV components
- Lightweight alloy for the shuttle uses Tier 8 plating, fourteen Kevlar plates, twelve neutronium screws, and four ingots of molten Radox Polymer. Its Assembly Line recipe is UEV-rated

These establish production gates but not a complete bill of materials or minimum machine-hatch topology.

## Ore Tier 10 Resources And Consumers

The [UEV Final Frontier quest](https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier10UEV-D_aFb1hFQH2PDkN0_KvAEQ==/TheFinalFrontier-X1tb5rwVSVi5SR5rY7vQIw==.json#L11) and the [pinned vein definitions](https://github.com/GTNewHorizons/GT5-Unofficial/blob/000a4d9b24d77f40a79da7a105bb79ac7efca817/src/main/java/gregtech/api/enums/OreMixes.java#L933-L1001) agree on these named veins.

| Destination | Named Vein | Gate Interpretation Supported By This Pass |
| --- | --- | --- |
| Anubis | Infinity Catalyst, with neutronium, adamantium, and bedrockium | Bulk catalyst supply. Vega B small ore and the quest's Avaritia recipe already provide alternatives before this system |
| Horus | Cosmic Neutronium, with neutronium, black plutonium, and bedrockium | Cosmic Neutronium is a concrete UEV motor input. It is also already a shuttle-schematic input, so this vein is not the initial-access requirement for that route |
| Maahes | Naquadria, with naquadah, enriched naquadah, and trinium | Naquadria-level radiation supports the efficient Bio Medium recipe. An exclusive Maahes progression requirement or complete earlier-source route was not established |
| Mehen Belt | Awakened Draconium, with draconium and nether star | A later vein route for a material already available as Ore Tier 9 small ore and required by the shuttle schematic |
| Neper | Dilithium, with mysterious crystal and vinteum | Placement is verified. A concrete mandatory downstream dilithium gate was not established in this bounded pass |
| Seth | Raw Tengam, with electrotine and samarium | Strong positive component gate: Raw Tengam becomes Purified Tengam in a UHV-rated Electromagnetic Separator recipe, then Attuned Tengam in a UHV-rated Polarizer recipe. Eight long Attuned Tengam rods are consumed by the UEV motor recipe |

The Tengam chain is directly visible in [ElectromagneticSeparatorRecipes](https://github.com/GTNewHorizons/GT5-Unofficial/blob/000a4d9b24d77f40a79da7a105bb79ac7efca817/src/main/java/gregtech/loaders/postload/recipes/ElectromagneticSeparatorRecipes.java#L23-L32), [ProcessingTransforming](https://github.com/GTNewHorizons/GT5-Unofficial/blob/000a4d9b24d77f40a79da7a105bb79ac7efca817/src/main/java/gregtech/loaders/oreprocessing/ProcessingTransforming.java#L160-L169), and [ResearchStationAssemblyLine](https://github.com/GTNewHorizons/GT5-Unofficial/blob/000a4d9b24d77f40a79da7a105bb79ac7efca817/src/main/java/tectech/loader/recipe/ResearchStationAssemblyLine.java#L1477-L1506). The motor is a UEV component, while its inspected assembly recipe is UHV-rated. These labels must remain distinct.

There is also a [Tengam asteroid space-mining recipe](https://github.com/GTNewHorizons/GT5-Unofficial/blob/000a4d9b24d77f40a79da7a105bb79ac7efca817/src/main/java/gtnhintergalactic/recipe/SpaceMiningRecipes.java#L845-L864) listing UEV through UXV drone tiers. This confirms another supply route exists. Its full infrastructure and bootstrap requirements were not audited, so it is not established as an earlier substitute for Seth.

## Limits And Open Questions

- This pass identifies positive recipe dependencies and documented alternatives. It does not certify all first occurrences, all ore-processing routes, all small ores, or universal source exclusivity
- No runtime world generation, recipe-browser state, machine hatch arrangement, or in-game travel was tested
- Graphs were used for structural discovery. Some current-tree coverage metadata was stale or unavailable. Every substantive source claim above was checked in pinned Git objects, so current HEAD behavior is not substituted for release behavior
- Recipe EU/t ratings are not proof that every machine part of that voltage tier is required before running the recipe. In particular, the UEV-rated Tier 8 hull must not be converted into an unsupported claim that UEV motors are needed before extrasolar travel
- Earlier Cosmic Neutronium manufacturing, Maahes alternatives, Neper's concrete downstream role, and complete biological bootstrap alternatives remain outside this pass
- Ore-form inputs in the original shuttle schematic are real source dependencies. They do not automatically become Galaxia material gates after Galaxia removes schematic gating
- The original research ticket remains broader than this note. This note does not close the full Ore Tier 4 through 10 audit or select final Galaxia technology gates

[[Sources]]
