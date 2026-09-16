---
type: source
status: reviewed
tags:
  - galaxia/alpha
  - wayfinder/source
---

# Inner Planets Progression Gate Research

Source: GTNH 2.8.0 questbook and release-pinned GT5-Unofficial and NewHorizonsCoreMod recipes listed below
Imported: 2026-09-11

## Source Snapshot

Wayfinder review classified the corrected report as bounded GTNH 2.8.0 evidence. The IV ice-composite and LuV hull steps are distinct. Source exclusivity and minimum machine-hatch arrangements remain unverified. Galaxia target decisions are not inferred from original recipes.

Bounded intake for Ore Tier 5, containing Io, Mercury, and Venus in the established ore baseline. This is original GTNH research, not a new Galaxia design decision. The completed Mars-to-Asteroids findings are not repeated here.

### Version And Scope

Sources were read directly with `git show` at these release refs, using the existing [2.8.0 component mapping][manifest]:

- GT-New-Horizons-Modpack `2.8.0`, commit `c3ba07ccba1b772777f6fc57e53bb70c8547adb7`
- GT5-Unofficial `5.09.51.470`, commit `000a4d9b24d77f40a79da7a105bb79ac7efca817`
- NewHorizonsCoreMod `2.7.260`, commit `fe1a49ae577fee5ec4c1cf53d2545b475fb6b5af`

This slice checks positive quest and recipe requirements. It does not claim all-mod source exclusivity or inspect a running NEI registry. Ore Tier 5 is a destination group, not rocket tier 5 or voltage tier 5.

### 1. Entry Uses A Tier 4 Rocket With An Ice Composite And LuV-Rated Hull Assembly

[Ceres Dungeon][ceres-dungeon] says the Tier 4 schematic opens Venus, Mercury, and Io. [Callisto Trip][callisto] identifies Callisto ice at Y 40-60 as a material needed for Tier 4 rockets. [Tier 4 Heavy Duty Plates][plates4] names Tier 3 plates plus compressed ice plates as the hull inputs.

The pinned [ScriptGalaxySpace recipe][computers] makes the Tier 4 control computer with an OpenComputers case and keyboard, display, IV emitter and sensor, Tier 4 plate, and 1728 mB soldering alloy. It requires a cleanroom, IV recipe power, and 30 seconds. [Rocket Tier 4][rocket4] specifies Dense Hydrazine Rocket Fuel.

The exact ice input is a processed derivative, not raw Callisto ice. Pinned [AssemblerRecipes][ice-composite] consumes one `CustomItemList.CallistoIceCompressedPlate`, one `CustomItemList.LedoxCompressedPlate`, and 1000 mB `ic2coolant` to produce two `CustomItemList.IceCompressedPlate`. This assembler recipe runs at IV power for 15 seconds. In original GTNH, IC2 coolant is a separate consumed input used to make the solid ice composite. This recipe does not demonstrate Callisto ice being used directly as engine coolant.

Pinned [BW_Recipe_Loader][hull4] then consumes one Tier 3 heavy-duty plate (`GalacticraftMars:item.itemBasicAsteroids`, metadata 0), six `IceCompressedPlate`, four ruridit bolts, and 36 mB molten indalloy 140 to make one `HeavyDutyAlloyIngotT4`. It requires scanning the Tier 3 plate at EV power for 90 seconds, followed by an Assembly Line recipe at `TierEU.RECIPE_LuV` for 15 seconds. The same source converts that ingot into `HeavyDutyPlateTier4` in an LV-rated implosion recipe lasting one second, with explosive additive metadata 32.

The entry chain therefore combines IV-rated composite and computer recipes with LuV-rated hull assembly. It cannot be summarized as IV-only manufacturing. The [LuV chapter][luv] recommends Io, Venus, and Mercury, but recipe power does not by itself prove a complete LuV machine base is required. The minimum energy-hatch arrangement was not checked. Rocket tier, recipe voltage, and destination grouping remain distinct.

Confidence: high for the pinned composite, hull, computer, and quest requirements. The raw-resource-to-`CallistoIceCompressedPlate` and raw-resource-to-`LedoxCompressedPlate` steps were not fully traced. Callisto is a documented source of Callisto ice, not a proven universally mandatory visit. No exhaustive alternate-source check was performed. The dungeon requirement describes GTNH only.

### 2. Mercury Supplies The Documented Trinium Feedstock For Fusion Infrastructure

[Mercury Trip][mercury] directs players to collect Deep Iron from small ores to obtain trinium. [Naquadah Alloy][naq-alloy] explicitly connects that route to making a fusion reactor and also names naquadah coils and LuV energy hatches as processing prerequisites.

This is a stronger progression connection than a highlighted vein alone: a named destination resource feeds an alloy needed by the next major machine. Acquisition is still not sufficient. The player must obtain trinium from the feedstock, make the alloy, and have suitable heat and power infrastructure.

Confidence: high for the documented Mercury -> trinium -> naquadah-alloy -> fusion progression route. The precise Deep Iron processing recipe and universal exclusivity of that trinium source were not independently verified. Do not translate the quest's recommendation into proof that no alternative exists.

### 3. Venus And Io Include Meaningful Supply Improvements, Not Only First-Access Gates

[Venus Trip][venus] highlights quantium and titanium and recommends more naquadah if needed. But [Ceres Trip][ceres] already supplies small quantium ore in Ore Tier 4 and explicitly connects it to Tier 5 rockets. Thus quantium is progression-relevant, while Venus is not its demonstrated first possible acquisition. Earlier work already established titanium and naquadah routes before these inner planets.

[Io Trip][io] identifies niobium from the pyrolusite vein, samarium from mytryl and rubracium, infused gold, and small firestone. Samarium has a documented alternative processing route: [Finally Samarium][samarium], in the IV lanthanide quest sequence, supplies samarium and points to the bastnasite line as another option. It identifies magnetic samarium rods as useful from LuV onward. Io's samarium sources therefore should not automatically become a mandatory first-access gate.

Venus has a separate survival requirement. Its quest says a full set of armor with the Spacesuit capability is needed on entry. [Journey To The Bottom][venus-suit] also recognizes multiple suitable armors. That is a supported armor capability requirement in quest guidance, not evidence that one particular suit recipe must be preserved.

Confidence: high for these named routes and the explicit quest alternatives. Relative yields, mining economics, first availability of every constituent, and a complete Io/Venus ore inventory are outside this slice. No claim is made that an unevaluated resource is irrelevant.

### 4. Europium Is A Concrete Fusion-To-Tier-5-Rocket Material Gate

[Getting Europium][europium] says europium is needed for the Tier 5 rocket, Mk2 fusion, and the ZPM transition. It explains that europium-bearing ore becomes accessible after a Tier 5 rocket, so the initial route is reactor production rather than that later ore.

Pinned [FusionReactorRecipes][fusion] registers molten neodymium plus hydrogen gas -> molten europium. The recipe outputs one nugget-volume per 32 ticks at 24,576 EU/t with a 150,000,000 EU fusion startup threshold. These are separate operating-power and startup-energy requirements. Merely having the input elements does not satisfy the processing gate.

Pinned [AssemblingLineRecipes][hull5] confirms the consumer. One Tier 5 heavy-duty alloy ingot uses one Tier 4 plate, eight compressed quantium plates, eight europium bolts, and 72 mB solder fluid selected by the existing recipe. It requires scanning the Tier 4 plate at IV power for 100 seconds and an Assembly Line recipe at `TierEU.RECIPE_ZPM` for 15 seconds. [ImplosionCompressorRecipes][implosion] then converts the alloy ingot into the Tier 5 plate at LV recipe power with explosive additive metadata 40.

This links a real material requirement to both processing infrastructure and an onward vehicle. It also shows why calling every Tier 5 rocket recipe simply "LuV" is imprecise. The control computer is LuV-rated, but this hull assembly recipe is ZPM-rated. The minimum energy-hatch topology was not audited, so no claim is made that a complete ZPM machine base must exist first.

Confidence: high for the exact positive fusion and hull recipes. The claim that the initial europium route must use fusion is pinned quest guidance, reinforced by the direct recipe, not an exhaustive absence proof across all optional mods or rewards.

### 5. Onward Travel Adds LuV Electronics And A New Fuel Grade

Pinned [ScriptGalaxySpace][computers] makes the Tier 5 computer using LuV emitter and sensor, a Tier 5 plate, the case, keyboard, display, and 2304 mB soldering alloy. It requires a cleanroom and LuV recipe power for 30 seconds.

[Rocket Tier 5][rocket5] requires CN3H7O3 purple rocket fuel or better. The [Purple Rocket Fuel quest][purple] gives monomethylhydrazine plus nitric acid in a Chemical Plant with tungstensteel casings as the production route. "Or better" is an explicit alternative fuel-grade allowance, not proof that this one fuel recipe is universally mandatory.

[Io Dungeon][io-dungeon] supplies the original Tier 5 schematic and says it opens the moons of Saturn and Uranus. This establishes the immediate onward progression edge without auditing the next ore group.

Confidence: high for the electronics recipe and quest-backed onward requirements. Fuel alternatives, the complete Tier 5 rocket bill of materials, and later destinations were not exhaustively checked.

### Galaxia Boundary And Remaining Questions

Current Galaxia policy supplied to this research removes mandatory bosses and dungeons, uses capability-based vehicle access, and initially grants team technologies through crafted or used blueprints based on planet-unlocked material. The GTNH dungeon facts above are provenance only. They do not propose restoring those mechanics or choose Galaxia blueprint ingredients.

The owner separately approved Callisto Ice as provisional engine coolant, an asteroid orbiting Callisto as an alternative Automated Outpost extraction source, and higher-tier europium without choosing its vehicle part. These are Galaxia target choices, not findings about original GTNH recipes or source locations. In particular, the GTNH recipe above consumes compressed Callisto ice in a solid composite alongside IC2 coolant. It does not establish the proposed coolant use or asteroid extraction route.

The original GTNH chain supported here is compressed Callisto ice plus compressed Ledox and IC2 coolant -> IV-rated ice-composite production -> LuV-rated Tier 4 hull assembly, alongside IV-rated electronics -> inner-planet access -> documented Mercury trinium route and fusion infrastructure -> europium -> onward rocket construction. This does not certify that each destination is mandatory or that every material has only one acquisition route.

Unresolved details include the raw-resource-to-compressed-plate steps for Callisto ice and Ledox, exact trinium extraction, exhaustive Callisto-ice alternatives, final registered recipe overrides, the minimum power-hatch arrangements for the Tier 4 and Tier 5 hulls, and the economic roles of repeated ores. The IV composite and LuV Tier 4 hull recipe steps are now directly checked, not unresolved. Those remaining limits prevent a universal exclusivity claim. Ore Tiers 6-10 remain outside this note.

## References

[manifest]: https://github.com/GTNewHorizons/DreamAssemblerXXL/blob/035dc34a6199b51114cc142ccc7937e1c6872235/releases/manifests/2.8.0.json
[ceres-dungeon]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/SpaceRace-AAAAAAAAAAAAAAAAAAAAIg==/CeresDungeon-AAAAAAAAAAAAAAAAAAAF-g==.json
[callisto]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier5IV-AAAAAAAAAAAAAAAAAAAABw==/CallistoTrip-AAAAAAAAAAAAAAAAAAAF_Q==.json
[plates4]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/SpaceRace-AAAAAAAAAAAAAAAAAAAAIg==/Tier4HeavyDutyPl-AAAAAAAAAAAAAAAAAAAF_A==.json
[ice-composite]: https://github.com/GTNewHorizons/NewHorizonsCoreMod/blob/fe1a49ae577fee5ec4c1cf53d2545b475fb6b5af/src/main/java/com/dreammaster/gthandler/recipes/AssemblerRecipes.java
[hull4]: https://github.com/GTNewHorizons/NewHorizonsCoreMod/blob/fe1a49ae577fee5ec4c1cf53d2545b475fb6b5af/src/main/java/com/dreammaster/bartworksHandler/BW_Recipe_Loader.java
[computers]: https://github.com/GTNewHorizons/NewHorizonsCoreMod/blob/fe1a49ae577fee5ec4c1cf53d2545b475fb6b5af/src/main/java/com/dreammaster/scripts/ScriptGalaxySpace.java
[rocket4]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/SpaceRace-AAAAAAAAAAAAAAAAAAAAIg==/RocketTier4-AAAAAAAAAAAAAAAAAAAF_w==.json
[luv]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier6LuV-AAAAAAAAAAAAAAAAAAAACA==/Tier6LuV-AAAAAAAAAAAAAAAAAAAF1Q==.json
[mercury]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier5IV-AAAAAAAAAAAAAAAAAAAABw==/MercuryTrip-AAAAAAAAAAAAAAAAAAAGtA==.json
[naq-alloy]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier6LuV-AAAAAAAAAAAAAAAAAAAACA==/NaquadahAlloy-AAAAAAAAAAAAAAAAAAAKLw==.json
[venus]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier5IV-AAAAAAAAAAAAAAAAAAAABw==/VenusTrip-AAAAAAAAAAAAAAAAAAAGtQ==.json
[ceres]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier5IV-AAAAAAAAAAAAAAAAAAAABw==/CeresTrip-AAAAAAAAAAAAAAAAAAAGAg==.json
[io]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier5IV-AAAAAAAAAAAAAAAAAAAABw==/IoTrip-AAAAAAAAAAAAAAAAAAAKig==.json
[samarium]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier5IV-AAAAAAAAAAAAAAAAAAAABw==/FinallySamarium-AAAAAAAAAAAAAAAAAAAMEA==.json
[venus-suit]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/SpaceRace-AAAAAAAAAAAAAAAAAAAAIg==/JourneytotheBott-AAAAAAAAAAAAAAAAAAAGxQ==.json
[europium]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier6LuV-AAAAAAAAAAAAAAAAAAAACA==/GettingEuropium-AAAAAAAAAAAAAAAAAAAEvQ==.json
[fusion]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/000a4d9b24d77f40a79da7a105bb79ac7efca817/src/main/java/gregtech/loaders/postload/recipes/FusionReactorRecipes.java
[hull5]: https://github.com/GTNewHorizons/NewHorizonsCoreMod/blob/fe1a49ae577fee5ec4c1cf53d2545b475fb6b5af/src/main/java/com/dreammaster/gthandler/recipes/AssemblingLineRecipes.java
[implosion]: https://github.com/GTNewHorizons/NewHorizonsCoreMod/blob/fe1a49ae577fee5ec4c1cf53d2545b475fb6b5af/src/main/java/com/dreammaster/gthandler/recipes/ImplosionCompressorRecipes.java
[rocket5]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/SpaceRace-AAAAAAAAAAAAAAAAAAAAIg==/RocketTier5-AAAAAAAAAAAAAAAAAAAGvg==.json
[purple]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/SpaceRace-AAAAAAAAAAAAAAAAAAAAIg==/CN3H7O3PurpleRoc-AAAAAAAAAAAAAAAAAAAKgA==.json
[io-dungeon]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/SpaceRace-AAAAAAAAAAAAAAAAAAAAIg==/IoDungeon-AAAAAAAAAAAAAAAAAAAGuw==.json

[[Sources]]
