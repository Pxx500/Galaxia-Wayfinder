---
type: source
status: unreviewed
tags:
  - galaxia/alpha
  - wayfinder/source
---

# Outer System Progression Gate Research

Source: GTNH 2.8.0 questbook and release-pinned NewHorizonsCoreMod and GT5-Unofficial sources cited below
Imported: 2026-09-16

## Source Snapshot

Bounded primary-source intake for Ore Tier 6, Enceladus, Miranda, Oberon, and Titan, Ore Tier 7, Proteus and Triton, and Ore Tier 8, Haumea, Kuiper Belt, Makemake, and Pluto. The ore groups come from the supplied Galaxia ore baseline. They are not GTNH rocket numbers or voltage tiers. This note identifies positive progression connections and specific earlier alternatives. It does not certify a complete ore audit or make Galaxia design decisions.

### Version And Method

All source facts below were read with `git show` at the supplied GTNH 2.8.0 release pins, without changing checkouts:

- GT-New-Horizons-Modpack `c3ba07ccba1b772777f6fc57e53bb70c8547adb7`
- NewHorizonsCoreMod `fe1a49ae577fee5ec4c1cf53d2545b475fb6b5af`
- GT5-Unofficial `000a4d9b24d77f40a79da7a105bb79ac7efca817`

Current graph results were used only to locate recipe owners. They were not treated as release evidence. Quest descriptions are progression guidance. The cited recipe registrations independently establish named inputs, outputs, recipe maps, and power requirements. Neither is an exhaustive check of the final running recipe registry.

### Summary

| Ore Group | Documented GTNH Entry | Progression-Bearing Resource Evidence | Important Qualification |
| --- | --- | --- | --- |
| 6: Enceladus, Miranda, Oberon, Titan | Tier 5 rocket, purple rocket fuel or better, Thermal Padding Tier 2 | Enceladus Mysterious Crystal feeds the Tier 7 hull. Enceladus, Oberon, and Titan supply small Neutronium ore used for UV progression and the Tier 7 hull | No distinct mandatory material gate was established for Miranda. The quest explicitly says not every destination is required |
| 7: Proteus, Triton | Tier 6 rocket, purple rocket fuel or better, Thermal Padding Tier 2 | Neutronium-bearing veins increase access. Triton has small Black Plutonium ore, which can feed the Tier 8 hull and Cosmic Neutronium route. Triton Yttrium supplies Cubic Zirconia production | Neutronium small ore is documented in Ore Tier 6. Yttrium has earlier rare-earth routes. Black Plutonium small ore precedes its Ore Tier 8 veins |
| 8: Haumea, Kuiper Belt, Makemake, Pluto | Tier 7 rocket, green rocket fuel, Thermal Padding Tier 2. Kuiper Belt also counts as zero gravity | The group adds Black Plutonium veins. The Tier 8 hull consumes Black Plutonium and opens onward extrasolar travel in GTNH | The inspected group quest does not assign each vein to a particular body. These veins are not proven first access to their materials |

Sources: [Planetary Tears][planetary], [Fusion Rocketry][group6], [Where No One Has Gone Before][group7], [All Good Things][group8], [Rocket Tier 5][rocket5], [Rocket Tier 6][rocket6], [Rocket Tier 7][rocket7], and the recipes below. The quests' term "new veins" is a route-level list, not proof that every constituent material first becomes obtainable there.

### Vehicle Manufacturing Is Not One Voltage Tier

The pinned [Assembly Line recipes][hulls] register the following hull intermediates. Each row produces one heavy-duty alloy ingot. The [Implosion Compressor recipes][implosion] then convert these ingots to the corresponding plates at LV recipe power with explosive additives.

| Hull | Material Inputs In Addition To The Previous Hull Plate | Assembly Line Recipe Power | Previous-Plate Scan | Control Computer Recipe Power |
| --- | --- | --- | --- | --- |
| Tier 5, entering Ore Tier 6 | Eight compressed quantium plates and eight europium bolts | ZPM, 15 seconds | IV, 100 seconds | LuV |
| Tier 6, entering Ore Tier 7 | Ten lead-oriharukon plates and eight tritanium bolts | UV, 15 seconds | LuV, 110 seconds | ZPM |
| Tier 7, entering Ore Tier 8 | Twelve compressed Mysterious Crystal plates and ten Neutronium bolts | UHV, 15 seconds | ZPM, 120 seconds | UV |
| Tier 8, leaving this slice | Fourteen compressed Black Plutonium plates and twelve Black Plutonium bolts | UEV, 15 seconds | UV, 130 seconds | UV |

These recipes also consume increasing solder quantities, 72, 144, 288, and 576 mB respectively. The actual fluid is selected by the existing recipe registration. The [computer recipes][computers] use the corresponding plate plus an OpenComputers case and keyboard, display, and matching emitter and sensor. All four require a cleanroom and take 30 seconds. Their soldering-alloy inputs are 2304, 3456, 4608, and 6912 mB respectively.

These are recipe power ratings, not proof that a player must already own a complete machine base of that voltage tier. In particular, [Rocket Tier 6][rocket6] explicitly says the GT++ Assembler multiblock is needed to make that rocket in ZPM. This is positive guidance about an alternative machine route. Minimum hatch configurations, multiblock discounts, and complete rocket bills of materials were not audited here. The apparent recipe-power differences must not be flattened into a single "rocket technology tier".

Original schematics are on Enceladus for Tier 6, Proteus for Tier 7, and Pluto for Tier 8, according to their [Enceladus][enceladus-dungeon], [Proteus][proteus-dungeon], and [Pluto][pluto-dungeon] dungeon quests. These are GTNH provenance only. They are not proposed Galaxia requirements.

### Ore Tier 6: Mysterious Crystal And Early Neutronium Matter More Than A Mandatory Tour

[Fusion Rocketry][group6] names Enceladus, Miranda, Oberon, and Titan among the newly reachable destinations. It lists Nickel, Tungsten, and Vanadium veins and explicitly permits skipping destinations. It also identifies small Neutronium ore on Enceladus, Oberon, and Titan. This is a positive earlier-source exception to treating Ore Tier 7 Neutronium veins as the first Neutronium access.

[Mysterious][mysterious] directs players to Enceladus crystals or ice for Mysterious Crystal dust. Pinned [Macerator recipes][macerator] turn Enceladus ice blocks into ice dust and include a chance of Mysterious Crystal dust at HV recipe power. [Centrifuge recipes][centrifuge] process Enceladus ice dust into, among other outputs, Mysterious Crystal dust at EV recipe power. These are two supported processing steps around a non-vein resource. The Tier 7 hull consumes its compressed plates, so the resource has a concrete onward-vehicle role even though the hull is two rocket numbers above initial Enceladus access.

The same resource has a documented optional electronics-supply role. [Mutating Things][mutagen] uses Mysterious Crystal dust to establish and feed a mutagen culture in a Bacterial Vat with LuV glass and plutonium rods. The quest presents mutagen and bacterial sludge as alternatives to repeated europium use for Raw Crystal Chips. This does not make the mutagen route universally mandatory.

Neutronium acquisition is not equivalent to usable Neutronium metal. [Wasn't This Only Four][neutronium] connects the material to UV and the Tier 7 rocket. The pinned [Mixer recipe][mixer] consumes one Neutronium dust and 144 mB helium plasma to produce Raw Neutronium at ZPM recipe power. The [Blast Furnace recipe][blast] then makes a hot Neutronium ingot at UV recipe power, 9000 K, and 380 seconds through the gas-assisted recipe map. Cooling and part production remain further steps outside this slice. The verified hull consumer is ten Neutronium bolts per Tier 7 alloy ingot.

### Ore Tier 7 Entry Adds Tritanium And A Lead-Oriharukon Composite

[Making Tritanium][tritanium] explicitly names the Tier 6 rocket, Gravisuit, Tier 4 mining multiblock, and UHV circuits as consumers. The [ZPM Energy Hatch quest][zpm-hatch] connects the next fusion upgrade to Americium and Tritanium.

Pinned [Fusion Reactor recipes][fusion] provide the concrete sequence. Gallium plus radon produces duranium at 16,384 EU/t with 140,000,000 EU startup energy. Titanium plus duranium produces tritanium at LuV recipe power with 200,000,000 EU startup energy. Each recipe takes 64 ticks. Startup energy is distinct from operating EU/t and is an infrastructure condition, not just an ingredient requirement. The Tier 6 hull directly consumes tritanium bolts.

The [Assembler recipe][lead-composite] combines one compressed lead plate, one compressed oriharukon plate, and 1000 mB IC2 coolant into two lead-oriharukon plates at UV recipe power for 15 seconds. The input metadata is confirmed by the [Implosion Compressor registrations][implosion], which map triple lead and oriharukon plates to GalaxySpace compressed-plate metadata 3 and 7. This is a processed composite, not evidence of a new Ore Tier 7 ore gate.

There is a concrete earlier oriharukon feedstock route. [Macerator recipes][macerator] turn Europa material into Europa Ice Dust at MV recipe power. [Centrifuge recipes][centrifuge] accept 36 Europa Ice Dust and include four Oriharukon dust as a chance output at HV recipe power. Europa belongs to Ore Tier 4 in the supplied baseline. This proves a recipe route from earlier-destination material, not its profitability or exclusive availability.

### Ore Tiers 7 And 8: Distinguish First Feedstock From Bulk Veins

[Where No One Has Gone Before][group7] lists Neutronium, Niobium, and Thorium veins for Proteus and Triton and specifically identifies small Black Plutonium ore on Triton. [Fetching Cubic Zirconia][zirconia] names Triton Yttrium as an easier later source, but also gives rare-earth processing through Xenotime and Yttriaite as earlier alternatives. Yttrium's usefulness for Cubic Zirconia is supported. Triton-exclusive first access is contradicted by the same guidance.

[All Good Things][group8] lists Black Plutonium, Garnet, and Red Garnet veins in the Haumea, Kuiper Belt, Makemake, and Pluto group. The specific progression link checked here is Black Plutonium. Its Tier 8 hull consumer is verified directly above, while the Triton small-ore source precedes those veins. The later veins can therefore improve supply without establishing first access. The economic value and exact per-body distribution remain open.

Black Plutonium also supports a separate material chain. [Neutrons From Space][cosmic] describes centrifuging it into Piles of Neutrons and compressing those into Cosmic Neutronium. Pinned [Centrifuge recipes][centrifuge] consume one Black Plutonium dust at EV recipe power for 60 seconds and register three chance outputs of Avaritia Resource metadata 2. The [Implosion Compressor recipes][implosion] convert nine of metadata 2 into metadata 3, and nine of metadata 3 into metadata 4, matching the quest's pile-to-nugget-to-ingot chain. Cosmic Neutronium is not ordinary GregTech Neutronium. As a specific downstream consumer, the pinned [Dyson Swarm Control Center Toroid Casing recipe][cosmic-consumer] consumes four Cosmic Neutronium screws. That later consumer establishes usefulness, not a claim that this whole later technology must be built within Ore Tier 8.

### Fuel And Target-Design Boundary

GTNH [Tier 5][rocket5] and [Tier 6][rocket6] rocket quests require purple fuel or better. [Tier 7][rocket7] and [Tier 8][rocket8] require green fuel. The [Green Rocket Fuel quest][green-fuel] specifies nitrogen tetroxide plus 1,1-dimethylhydrazine in a Laurenium, Tier 7, Chemical Plant. That is a named machine-casing requirement in quest guidance, not an independently audited recipe EU/t or proof of a complete ZPM machine base.

Galaxia removes mandatory bosses and dungeons and fixed rocket access tiers. The source schematics, fuel whitelists, and numbered rocket checks above must therefore remain provenance. This note does not select target recipes, restore those gates, assign final technology tiers, or decide whether each destination must be visited.

### Confidence And Remaining Limits

Confidence is high for the cited positive recipe registrations, quest-backed routes, and explicit earlier alternatives. The pass did not inspect runtime NEI, every recipe override, all mods and rewards, minimum power-hatch topologies, exact yields after full ore processing, or every highlighted vein. Mysterious Crystal dust-to-compressed-plate production and complete rocket component chains were not fully traced. The ordinary Neutronium hot-ingot cooling step was not independently checked. No exhaustive source-exclusivity claim follows.

The strongest supported resource relationships are Mysterious Crystal to later hulls, early small Neutronium ore plus helium-plasma and high-temperature processing to Neutronium parts, fusion-made tritanium to the Tier 6 hull, and Black Plutonium to the Tier 8 hull and Cosmic Neutronium. The named small-ore and rare-earth exceptions must survive any later gate discussion. Other ores are not declared irrelevant merely because this bounded pass did not identify a consumer.

## References

[planetary]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/MultipleQuestLine/PlanetaryTears-AAAAAAAAAAAAAAAAAAAIGA==.json
[group6]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier6LuV-AAAAAAAAAAAAAAAAAAAACA==/FusionRocketry-AAAAAAAAAAAAAAAAAAAKVQ==.json
[group7]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier7ZPM-AAAAAAAAAAAAAAAAAAAAHg==/WhereNoOneHasGon-AAAAAAAAAAAAAAAAAAAKVg==.json
[group8]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier8UV-AAAAAAAAAAAAAAAAAAAALQ==/AllGoodThings-AAAAAAAAAAAAAAAAAAAKVw==.json
[rocket5]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/SpaceRace-AAAAAAAAAAAAAAAAAAAAIg==/RocketTier5-AAAAAAAAAAAAAAAAAAAGvg==.json
[rocket6]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/SpaceRace-AAAAAAAAAAAAAAAAAAAAIg==/RocketTier6-AAAAAAAAAAAAAAAAAAAKUA==.json
[rocket7]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/SpaceRace-AAAAAAAAAAAAAAAAAAAAIg==/RocketTier7-AAAAAAAAAAAAAAAAAAAKUg==.json
[rocket8]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/SpaceRace-AAAAAAAAAAAAAAAAAAAAIg==/RocketTier8-AAAAAAAAAAAAAAAAAAAKVA==.json
[hulls]: https://github.com/GTNewHorizons/NewHorizonsCoreMod/blob/fe1a49ae577fee5ec4c1cf53d2545b475fb6b5af/src/main/java/com/dreammaster/gthandler/recipes/AssemblingLineRecipes.java#L86-L132
[implosion]: https://github.com/GTNewHorizons/NewHorizonsCoreMod/blob/fe1a49ae577fee5ec4c1cf53d2545b475fb6b5af/src/main/java/com/dreammaster/gthandler/recipes/ImplosionCompressorRecipes.java
[computers]: https://github.com/GTNewHorizons/NewHorizonsCoreMod/blob/fe1a49ae577fee5ec4c1cf53d2545b475fb6b5af/src/main/java/com/dreammaster/scripts/ScriptGalaxySpace.java#L195-L239
[enceladus-dungeon]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/SpaceRace-AAAAAAAAAAAAAAAAAAAAIg==/EnceladusDungeon-AAAAAAAAAAAAAAAAAAAKwA==.json
[proteus-dungeon]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/SpaceRace-AAAAAAAAAAAAAAAAAAAAIg==/ProteusDungeon-AAAAAAAAAAAAAAAAAAAKvg==.json
[pluto-dungeon]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/SpaceRace-AAAAAAAAAAAAAAAAAAAAIg==/PlutoDungeon-AAAAAAAAAAAAAAAAAAAKlA==.json
[mysterious]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier6LuV-AAAAAAAAAAAAAAAAAAAACA==/Mysterious-AAAAAAAAAAAAAAAAAAAKMQ==.json
[macerator]: https://github.com/GTNewHorizons/NewHorizonsCoreMod/blob/fe1a49ae577fee5ec4c1cf53d2545b475fb6b5af/src/main/java/com/dreammaster/gthandler/recipes/MaceratorRecipes.java
[centrifuge]: https://github.com/GTNewHorizons/NewHorizonsCoreMod/blob/fe1a49ae577fee5ec4c1cf53d2545b475fb6b5af/src/main/java/com/dreammaster/gthandler/recipes/CentrifugeRecipes.java
[mutagen]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier6LuV-AAAAAAAAAAAAAAAAAAAACA==/MutatingThingsis-AAAAAAAAAAAAAAAAAAAKeA==.json
[neutronium]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier7ZPM-AAAAAAAAAAAAAAAAAAAAHg==/WasntThisOnlyFou-AAAAAAAAAAAAAAAAAAAKbQ==.json
[mixer]: https://github.com/GTNewHorizons/NewHorizonsCoreMod/blob/fe1a49ae577fee5ec4c1cf53d2545b475fb6b5af/src/main/java/com/dreammaster/gthandler/recipes/MixerRecipes.java#L845-L850
[blast]: https://github.com/GTNewHorizons/NewHorizonsCoreMod/blob/fe1a49ae577fee5ec4c1cf53d2545b475fb6b5af/src/main/java/com/dreammaster/gthandler/recipes/BlastFurnaceRecipes.java#L1119-L1122
[tritanium]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier7ZPM-AAAAAAAAAAAAAAAAAAAAHg==/MakingTritanium-AAAAAAAAAAAAAAAAAAAKYg==.json
[zpm-hatch]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier7ZPM-AAAAAAAAAAAAAAAAAAAAHg==/ZPMEnergyHatch-AAAAAAAAAAAAAAAAAAAKQw==.json
[fusion]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/000a4d9b24d77f40a79da7a105bb79ac7efca817/src/main/java/gregtech/loaders/postload/recipes/FusionReactorRecipes.java
[lead-composite]: https://github.com/GTNewHorizons/NewHorizonsCoreMod/blob/fe1a49ae577fee5ec4c1cf53d2545b475fb6b5af/src/main/java/com/dreammaster/gthandler/recipes/AssemblerRecipes.java#L6950-L6956
[zirconia]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier6LuV-AAAAAAAAAAAAAAAAAAAACA==/FetchingCubicZir-AAAAAAAAAAAAAAAAAAAKLA==.json
[cosmic]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier8UV-AAAAAAAAAAAAAAAAAAAALQ==/NeutronsFromSpac-AAAAAAAAAAAAAAAAAAAKcQ==.json
[cosmic-consumer]: https://github.com/GTNewHorizons/NewHorizonsCoreMod/blob/fe1a49ae577fee5ec4c1cf53d2545b475fb6b5af/src/main/java/com/dreammaster/gthandler/recipes/AssemblingLineRecipes.java#L479-L493
[green-fuel]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/SpaceRace-AAAAAAAAAAAAAAAAAAAAIg==/H8N4C2O4GreenRoc-AAAAAAAAAAAAAAAAAAAAkw==.json

[[Sources]]
