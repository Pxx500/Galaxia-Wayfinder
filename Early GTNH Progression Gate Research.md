---
type: source
status: reviewed
tags:
  - galaxia/alpha
  - wayfinder/source
---

# Early GTNH Progression Gate Research

Source: GTNH Ore Progression Baseline.md, GT-New-Horizons-Modpack 2.8.0 quest sources, and the release-pinned GT5-Unofficial, NewHorizonsCoreMod, and Galacticraft sources cited below
Imported: 2026-09-10

## Source Snapshot

This is bounded research intake for Overworld -> Moon -> Mars, corresponding to Ore Tiers 1-3 in the existing baseline. It is not an accepted Galaxia design, an exhaustive alternate-route audit, or resolution of Ore Tiers 4-10. The baseline was read before investigating. Its highlighted first occurrences are candidate gates, not proof that every highlighted vein must be visited.

### Version And Evidence Boundary

- Quest text: GT-New-Horizons-Modpack tag `2.8.0`, commit `c3ba07ccba1b772777f6fc57e53bb70c8547adb7`.
- Recipe source: GT5-Unofficial `5.09.51.470`, commit `000a4d9b24d77f40a79da7a105bb79ac7efca817`.
- Pack recipe overrides: NewHorizonsCoreMod `2.7.260`, commit `fe1a49ae577fee5ec4c1cf53d2545b475fb6b5af`.
- Destination and schematic source: Galacticraft `3.3.12-GTNH`, commit `e3026156e3c8f626d409bba17fd927b447cb50aa`.
- The parent investigation supplied the component mapping from the [2.8.0 release manifest](https://github.com/GTNewHorizons/DreamAssemblerXXL/blob/035dc34a6199b51114cc142ccc7937e1c6872235/releases/manifests/2.8.0.json). Recipe and quest contents in this note were inspected directly with `git show` at those tags. Current checkout code was used only to locate source owners through the graph, not as release evidence.
- No running 2.8.0 instance or generated NEI recipe registry was inspected. Source recipes demonstrate positive requirements and routes, not universal absence of every alternative across every mod.

### Claim 1: Ore Tier, Rocket Tier, And Voltage Tier Are Different Axes

The baseline's Ore Tier 1 contains Overworld, Nether, Twilight Forest, End, and End Asteroids. Moon is Ore Tier 2. Mars, Phobos, and Deimos are Ore Tier 3. These numbers describe destination grouping, not GregTech voltage.

The [HV Moon goal][hv-moon] describes reaching the Moon for titanium used in EV and AE2 machines. The [EV chapter goal][ev-goal] describes building a Tier 2 rocket and reaching Mars. [Rocket Tier 1][rocket1] is the Moon vehicle. The pinned Mars provider's [`canSpaceshipTierPass`][mars-provider] returns `tier >= 2`. Therefore, Moon is the ordinary late-HV resource step into EV, while Mars is reached with an EV-era Tier 2 rocket. Calling Moon "voltage tier 2" or Mars "rocket tier 3" would be wrong.

Confidence: high for the named ordinary progression route and the destination check. This is not a proof that every unusual challenge route obeys it. The HV quest explicitly acknowledges a "no-rocket run" and allows a stack of titanium to satisfy its progress trigger. A quest dependency is not necessarily a gameplay lock.

### Claim 2: Titanium Is The Important Lunar Technology Outcome, Not Two Independently Mandatory Veins

The [Bauxite quest][bauxite] identifies both bauxite and ilmenite as titanium inputs. The [Ilmenite quest][ilmenite] says the Bauxite vein actually yields more ilmenite and suggests the separate Ilmenite vein might instead be visited for chromite. This directly rules out treating the two highlighted veins as two sequential, individually mandatory stops.

The acquisition gate is obtaining a suitable titanium feedstock on the ordinary route. Processing is a separate chain. The [Rutile quest][rutile] describes rutile from a byproduct route or EBF processing of ilmenite, then rutile + chlorine + carbon -> titanium tetrachloride, followed by magnesium in an HV EBF -> hot titanium. [Titanium, Finally][titanium] requires cooling in a Vacuum Freezer. Merely reaching or mining the Moon does not produce machine-ready titanium.

Meaningful alternatives: bauxite processing and ilmenite processing are alternative feedstock routes. The [Titanium bee quest][titanium-bee] requires a titanium block, so it is an expansion route after an initial titanium supply, not demonstrated evidence of a titanium-free bootstrap. The acknowledged no-rocket run means this note does not label lunar mining an absolute universal titanium gate. Its exact non-rocket bootstrap was not investigated.

Confidence: high that titanium is the intended Moon-to-EV material outcome and that both veins are not independently required. Moderate on universal exclusivity, which is deliberately not claimed.

### Claim 3: Meteoric Iron And Pre-Mars Tungstensteel Feed The Actual Tier 2 Plate Recipe

Pinned [GT5 AssemblerRecipes][gt-assembler] registers one Tier 2 heavy ingot from one Tier 1 heavy-duty plate, two meteoric iron plates, circuit setting 1, and half an ingot of molten tungstensteel. It takes 15 seconds at `TierEU.RECIPE_EV`. [ImplosionCompressorRecipes][gt-implosion] converts that ingot to the Galacticraft Mars Tier 2 heavy-duty plate, with explosive additive metadata 16, at `TierEU.RECIPE_LV` for one second. The low EU/t of the final implosion step does not make the entire chain LV.

The [Meteoric Iron quest][meteor] explicitly connects this material to reaching Mars, Phobos, and Deimos. It identifies small lunar meteoric iron ore at Y 50-70 and fallen surface meteors as alternatives. Meteoric iron is therefore a directly evidenced material gate in this recipe, even though it is not one of the baseline's five highlighted lunar veins. Surface meteor collection means the small-ore route is not individually mandatory.

The [Tier 2 plate quest][plate2] and [Pulverize the Planet][pulverize] explain how to obtain tungsten before reaching a planet with its ore. Sources include centrifuging macerated Moon dust, centrifuging dust from an HV-or-better macerator processing end stone, and centrifuging ender goo. The quest explicitly says TPV coils are needed to smelt tungstensteel dust. [Just Enough Tungsten][just-tungsten] describes the tungsten-trioxide, tungsten, steel mixing, EBF, and freezing steps.

This separates a material and processing requirement from a vein-access requirement. A Mars tungsten vein cannot be the bootstrap prerequisite for crafting the ordinary Mars rocket. Moon rock is one bootstrap source, not the only one. The later tungsten-vein access improves supply scale.

Confidence: high for the positive recipe and the documented alternate feedstocks. No claim is made that every source of meteoric iron in the whole pack has been exhausted.

### Claim 4: Mars Entry Also Requires Schematic Access And EV Manufacturing, Not Just Lunar Ore

The [Moon Dungeon quest][moon-dungeon] directs the player to kill the boss, use its key on the next room's chest, and obtain the Tier 2 schematic. The pinned Galacticraft [`SchematicTier2Rocket.getRequiredItem()`][schematic] returns `GCItems.schematic` metadata 1 directly. It unlocks the Tier 2 NASA Workbench page.

The pinned [NewHorizonsCoreMod ScriptGalaxySpace][nh-galaxy] defines the Tier 2 control computer using an OpenComputers case, keyboard, display, two EV field generators, a Tier 2 heavy-duty plate, and 864 mB soldering alloy. It requires a cleanroom and an EV assembler recipe for 30 seconds. This is a concrete manufacturing gate beyond ore acquisition. The [Tier 2 rocket quest][rocket2] lists the rocket's control computer, Mars lander, fuel canisters, plating, engines, boosters, fins, and nose cone. A schematic alone is not a complete travel unlock.

An apparent source conflict was investigated within this boundary. [CircuitAssemblerRecipes in the same core version][nh-circuit] still registers a Tier 2 chip recipe using an IV circuit, a data stick with schematic data, and a Tier 2 plate. But ScriptGalaxySpace also converts the old Tier 2 chip plus a BuildCraft blueprint into the direct schematic in an HV cleanroom laser engraver. This matches the quest's old-chip conversion note and the Galacticraft page's required item. The existence of the old chip recipe does not establish that an IV-circuit chip route is mandatory for this page.

Confidence: high for the direct schematic item, EV control-computer recipe, and rocket-tier destination check. The ordinary dungeon acquisition path is quest-backed. No exhaustive loot, trading, magic, or final registered-recipe replacement audit was performed. Fuel, launch infrastructure, oxygen, and survival equipment remain separate practical needs. The [Thermal Cloth quest][thermal] says a full thermal-padding set protects on Mars and the Asteroids. This note does not classify survival equipment as a hard dimension-selection lock.

### Claim 5: The Other Highlighted Moon Veins Include Supply Improvements, Not Demonstrated Moon-Exclusive Gates

| Highlighted vein | Positive source evidence | Early-gate interpretation |
|---|---|---|
| Monazite | [HV Bastnasite/Monazite quest][monazite] says EV motors need neodymium, Rare Earth is an existing source, pure lunar neodymium is better, bastnasite supplies fluorine, and monazite supplies more Rare Earth | Neodymium is relevant, but this lunar vein is not shown to be mandatory. The quest itself provides the alternative |
| Galena | [Lead/Galena/Silver quest][lead] places lead, silver, and galena in a Twilight Forest Cryolite vein and notes small silver in Overworld and Nether | The constituents have pre-Moon routes inside Ore Tier 1. A new large lunar vein is not proof of first access to those materials |
| Quartz | [LV Quartzite Veins quest][quartz] directs players to Nether quartzite veins at Y 80-120 | Quartz-bearing supply exists before Moon. This does not prove that every member or economic role of the highlighted lunar vein is interchangeable |

For Monazite, [the HV PTFE quest][ptfe] also gives pre-Moon fluorine routes including cryolite, chemical-plant fluorite from sand or sandstone, biotite from stone/granite dust, and small quantities from lepidolite or mica. Bastnasite is added as an option after Moon access. Do not turn its convenient fluorine supply into a new lunar hard gate.

Confidence: high that the named constituent alternatives exist in the pinned quest guidance. The economic value of larger veins, processing yields, exact lunar-vein composition parity, and later uses remain unevaluated. "Not demonstrated mandatory" does not mean "irrelevant" or permission to delete the placement.

### What This Research Supports And Leaves Open

The ordinary early route is supported by a titanium feedstock and processing step, lunar meteoric iron, the Tier 2 schematic, and EV manufacturing. It is not supported as a checklist requiring all five highlighted Moon veins. Some material gates have multiple acquisition routes. Some pre-Mars processing requirements use resources obtainable in Ore Tier 1.

Remaining work includes runtime verification if exact universal locks are needed, a bounded investigation of any important no-rocket titanium route, and later Ore Tiers 4-10. No new Galaxia gameplay decision was made here. No code, pack configuration, or source index note was edited.

## References

[hv-moon]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier3HV-AAAAAAAAAAAAAAAAAAAABQ==/DimensionalGoalM-AAAAAAAAAAAAAAAAAAAAog==.json
[ev-goal]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier4EV-AAAAAAAAAAAAAAAAAAAABg==/Tier4EV-AAAAAAAAAAAAAAAAAAAAsA==.json
[rocket1]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/SpaceRace-AAAAAAAAAAAAAAAAAAAAIg==/RocketTier1-AAAAAAAAAAAAAAAAAAADKg==.json
[mars-provider]: https://github.com/GTNewHorizons/Galacticraft/blob/e3026156e3c8f626d409bba17fd927b447cb50aa/src/main/java/micdoodle8/mods/galacticraft/planets/mars/dimension/WorldProviderMars.java
[bauxite]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier3HV-AAAAAAAAAAAAAAAAAAAABQ==/FindBauxite-AAAAAAAAAAAAAAAAAAAD8w==.json
[ilmenite]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier3HV-AAAAAAAAAAAAAAAAAAAABQ==/FindIlmenite-AAAAAAAAAAAAAAAAAAAFkA==.json
[rutile]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier3HV-AAAAAAAAAAAAAAAAAAAABQ==/Rutile-AAAAAAAAAAAAAAAAAAAD9A==.json
[titanium]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier3HV-AAAAAAAAAAAAAAAAAAAABQ==/TitaniumFinally-AAAAAAAAAAAAAAAAAAADXA==.json
[titanium-bee]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/BeeBreeding-AAAAAAAAAAAAAAAAAAAAEw==/Titanium-AAAAAAAAAAAAAAAAAAAImQ==.json
[gt-assembler]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/000a4d9b24d77f40a79da7a105bb79ac7efca817/src/main/java/gregtech/loaders/postload/recipes/AssemblerRecipes.java
[gt-implosion]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/000a4d9b24d77f40a79da7a105bb79ac7efca817/src/main/java/gregtech/loaders/postload/recipes/ImplosionCompressorRecipes.java
[meteor]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/SpaceRace-AAAAAAAAAAAAAAAAAAAAIg==/FindSomeMeteoric-AAAAAAAAAAAAAAAAAAAFkg==.json
[plate2]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/SpaceRace-AAAAAAAAAAAAAAAAAAAAIg==/Tier2HeavyDutyPl-AAAAAAAAAAAAAAAAAAAFkw==.json
[pulverize]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier4EV-AAAAAAAAAAAAAAAAAAAABg==/PulverizethePlan-AAAAAAAAAAAAAAAAAAAA1A==.json
[just-tungsten]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier4EV-AAAAAAAAAAAAAAAAAAAABg==/JustEnoughTungst-AAAAAAAAAAAAAAAAAAAJVg==.json
[moon-dungeon]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/SpaceRace-AAAAAAAAAAAAAAAAAAAAIg==/MoonDungeon-AAAAAAAAAAAAAAAAAAAFmQ==.json
[schematic]: https://github.com/GTNewHorizons/Galacticraft/blob/e3026156e3c8f626d409bba17fd927b447cb50aa/src/main/java/micdoodle8/mods/galacticraft/planets/mars/schematic/SchematicTier2Rocket.java
[nh-galaxy]: https://github.com/GTNewHorizons/NewHorizonsCoreMod/blob/fe1a49ae577fee5ec4c1cf53d2545b475fb6b5af/src/main/java/com/dreammaster/scripts/ScriptGalaxySpace.java
[rocket2]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/SpaceRace-AAAAAAAAAAAAAAAAAAAAIg==/RocketTier2-AAAAAAAAAAAAAAAAAAAFlQ==.json
[nh-circuit]: https://github.com/GTNewHorizons/NewHorizonsCoreMod/blob/fe1a49ae577fee5ec4c1cf53d2545b475fb6b5af/src/main/java/com/dreammaster/gthandler/recipes/CircuitAssemblerRecipes.java
[thermal]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/SpaceRace-AAAAAAAAAAAAAAAAAAAAIg==/ThermalCloth-AAAAAAAAAAAAAAAAAAAFtg==.json
[monazite]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier3HV-AAAAAAAAAAAAAAAAAAAABQ==/FindBastnasiteMo-AAAAAAAAAAAAAAAAAAAGTA==.json
[lead]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/NoviceThaumaturg-AAAAAAAAAAAAAAAAAAAAFg==/LeadGalenaSilver-AAAAAAAAAAAAAAAAAAACYg==.json
[quartz]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier1LV-AAAAAAAAAAAAAAAAAAAAAw==/QuartziteVeins-AAAAAAAAAAAAAAAAAAAEjg==.json
[ptfe]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier3HV-AAAAAAAAAAAAAAAAAAAABQ==/TeflonDon-AAAAAAAAAAAAAAAAAAAHFA==.json

[[Sources]]
