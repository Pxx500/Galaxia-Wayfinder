---
type: source
status: reviewed
tags:
  - galaxia/alpha
  - wayfinder/source
---

# Mars To Asteroids Progression Gate Research

Source: GTNH 2.8.0 questbook and release-pinned GT5-Unofficial, NewHorizonsCoreMod, and Galacticraft sources cited below
Imported: 2026-09-11

## Source Snapshot

Wayfinder review on 2026-09-11 classified this report as bounded GTNH 2.8.0 progression evidence. Its positive recipe requirements and documented alternatives support Verify GTNH Ore Tier Gates. This review does not certify exhaustive source exclusivity, runtime recipes, or final Galaxia recipe choices.

Bounded research intake for Mars -> Galacticraft Asteroids and the following technology step. These are original GTNH facts, not newly accepted Galaxia requirements. This note does not certify every Ore Tier 3-4 placement or all ways to bypass a recipe.

### Version And Stage Context

Sources were read with `git show` at the same release refs as the early-route investigation:

- GT-New-Horizons-Modpack `2.8.0`: `c3ba07ccba1b772777f6fc57e53bb70c8547adb7`
- GT5-Unofficial `5.09.51.470`: `000a4d9b24d77f40a79da7a105bb79ac7efca817`
- NewHorizonsCoreMod `2.7.260`: `fe1a49ae577fee5ec4c1cf53d2545b475fb6b5af`
- Galacticraft `3.3.12-GTNH`: `e3026156e3c8f626d409bba17fd927b447cb50aa`

The component mapping comes from the [2.8.0 manifest][manifest]. The existing ore baseline groups Mars, Phobos, and Deimos into Ore Tier 3, and Galacticraft Asteroids, Callisto, Ceres, Europa, and Ganymede into Ore Tier 4. That grouping is not a voltage assignment.

The [IV introduction][iv] requires tungstensteel for machines, recommends TPV coils, and lists Mars, Phobos, and Deimos as destinations. The [Asteroids trip quest][asteroids] is in the IV chapter. Galacticraft's pinned [`canSpaceshipTierPass`][provider] requires rocket tier >= 3 for Asteroids. Thus the ordinary route is EV-era Mars access, tungstensteel-backed IV manufacturing, then Tier 3 rocket access to Galacticraft Asteroids. Asteroids is not itself a declaration that LuV has been reached.

### Claim 1: Desh And Platinum Directly Feed The Tier 3 Rocket Hull

Pinned [GT5 AssemblerRecipes][assembler] registers a Tier 3 heavy ingot from one Tier 2 heavy-duty plate, four desh plates, circuit setting 1, and 72 mB molten platinum. It runs for 15 seconds at `TierEU.RECIPE_IV`. [ImplosionCompressorRecipes][implosion] turns this ingot into the Tier 3 heavy-duty plate at LV recipe power for one second, with explosive additive metadata 24. The final low-power operation does not make the whole manufacturing chain LV.

The [Tier 3 plate quest][plate3] asks for 38 plates and names Tier 2 plates plus desh. The recipe source makes the platinum requirement explicit too. Desh is therefore a direct material requirement of the ordinary next-rocket recipe, not merely an ore highlighted near Mars. [Critical Material][desh] identifies the relevant ore at Y 5-40 and describes desh as the important next-rocket material, while scheelite and tungstate expand tungsten supply.

Alternative routes and limits:

- [Phobos][phobos] explicitly has all the ores needed apart from the dungeon. Mars is not demonstrated to be the only Ore Tier 3 source of these materials.
- [Deimos][deimos] says the desired ores can be obtained on the other two destinations. Its ore visit is optional in that guidance.
- Critical Material says desh occurs as small ore elsewhere, but does not name those locations. This note does not turn that statement into an earlier-access bypass.
- The earlier research already established pre-Mars tungsten bootstrap routes. Larger Mars-tier tungsten deposits improve scale rather than create the first possible tungstensteel.
- EV [platinum-processing guidance][platinum] explicitly provides the chemical route to pure platinum. It is incorrect to make later platinum-vein access a prerequisite for this already-IV rocket recipe. Exact initial platinum feedstock exclusivity was not audited here.

Confidence: high for the positive recipe and named Phobos/Deimos alternatives. No universal desh-source exclusion is claimed.

### Claim 2: Rocket Electronics, Schematic Access, And Better Fuel Are Separate Gates

Pinned [ScriptGalaxySpace][electronics] makes the Tier 3 control computer from an OpenComputers case, keyboard, display, IV emitter, IV sensor, Tier 3 plate, and 1152 mB soldering alloy. It requires a cleanroom and IV recipe power for 30 seconds. Ore acquisition alone is insufficient.

The [Tier 3 rocket quest][rocket3] requires Dense Hydrazine Rocket Fuel or better. The [Dense Hydrazine quest][fuel] describes hydrazine plus methanol in a Titanium Chemical Plant. This is a positive documented fuel-processing route. The word "or better" means this particular fuel is not the only acceptable fuel grade. This slice did not audit all higher-grade fuels or alternative production recipes.

Original GTNH also has a non-material discovery gate. [Mars Dungeon][dungeon] directs the player to obtain the next schematic from the dungeon and to exchange extra schematics for cargo-rocket or astro-miner access. Pinned [`SchematicTier3Rocket.getRequiredItem()`][schematic] directly accepts `MarsItems.schematic` metadata 0. The destination provider then checks rocket tier >= 3.

Confidence: high for the electronics recipe and schematic item. The boss acquisition and fuel-production statements are pinned quest guidance, not a running recipe-registry audit. The original boss/dungeon requirement is not a Galaxia recommendation.

### Claim 3: Asteroid Naquadah Access And Usable Naquadah Are Different Milestones

[On Your Way To Asteroids][asteroids] specifically calls out naquadah. [Your First Naquadah][first-naq] says ordinary ore processing yields Naquadah Oxide Mixture, not usable naquadah dust. It explicitly permits inefficient EBF smelting of the mixture into naquadah nuggets at the IV stage, sacrificing byproducts. The full naquadah processing line is not required for this first product.

[The naquadah-doped boule quest][boule-quest] identifies a concrete consumer. Pinned [BlastFurnaceRecipes][boule-recipe] uses 16 solar-grade silicon blocks, one gallium-arsenide crystal, one naquadah ingot, and circuit setting 3, with EV recipe power, 4484 K heat metadata, and a 750-second duration through `BlastFurnaceWithGas`. The ore resource, purification step, and EBF temperature requirement must not be collapsed into a single destination unlock.

Alternative routes and limits:

- [Ceres Trip][ceres] names small naquadah ore at another Ore Tier 4 destination. Galacticraft Asteroids is not the only documented destination in this group that supplies it.
- The established ore-placement baseline records an earlier End Asteroids occurrence as an optional route. This note preserves that exception as baseline evidence, but does not independently re-verify its extraction and processing bootstrap.
- [Naquadah bees][bee] do not avoid the naquadah processing line according to the quest. Bee production is not evidence that usable-metal processing can be skipped.
- Naquadah is required for the named doped-boule recipe. This does not establish that every possible IV circuit or the entire LuV transition requires that particular wafer recipe. No universal LuV gate is inferred from a more efficient wafer route.

Confidence: high for the documented initial processing route and exact boule recipe. The mixture-to-nugget recipe's precise EU/t and heat were not independently checked in its release component, so those values are deliberately omitted.

### Claim 4: The Following LuV Step Also Requires Platinum-Group Processing And The Assembly Line

[Rhodium-Plated Palladium][rpp] is explicitly the LuV hull material. [Palladium Processing][palladium] describes palladium as necessary for LuV machines. These are processing and material requirements, not proof that a newly highlighted asteroid ore vein is mandatory. Earlier EV [platinum-residue guidance][residue] tells players to save residue containing rhodium, ruthenium, osmium, and iridium for IV and higher. That provides a documented continuity route from existing platinum processing.

The [Assembly Line quest][assembly-quest] says LuV machine components require this multiblock. Pinned [AssemblyLineRecipes][assembly-recipe] makes the LuV motor from magnetic samarium, HSS-S long rods, 128 fine ruridit wires, yttrium-barium-cuprate cable, indalloy, and lubricant. It requires scanning an IV motor and runs the assembly recipe at IV power. Component output tier and recipe voltage are not the same thing.

The [HSS-S quest][hsss] and [IV Mixer quest][mixer] separately identify HSS-S as an important LuV recipe material and IV mixing as its processing step. The [LuV introduction][luv] combines rhodium-plated-palladium machines with Assembly Line component production. It suggests later destinations, which are outside this slice's ore-placement audit.

Confidence: high for the named hull and motor requirements. This is an evidenced example of the next technology transition, not a complete LuV bill of materials or proof that any one asteroid vein supplies all of it.

### Galaxia Decision Boundary

The assignment supplied the current Galaxia policy: no mandatory bosses or dungeons, vehicle access based on capabilities, and team technologies initially acquired by crafting or using blueprints made from planet-unlocked material. Those are Galaxia decisions. They do not change what the original GTNH sources say.

This intake records the distinction without choosing a Galaxia blueprint ingredient, rewriting the gate structure, or assigning a new destination. In particular, the original Mars dungeon is a GTNH provenance fact, not a requirement to copy.

### Remaining Limits

No running GTNH 2.8.0 instance, final NEI registry, all-mod alternate-source audit, or full asteroid-vein classification was performed. The claims identify positive requirements and documented alternatives. They do not certify every highlighted Ore Tier 4 vein as mandatory, equate Galacticraft Asteroids with End Asteroids, or resolve Ore Tiers 5-10.

## References

[manifest]: https://github.com/GTNewHorizons/DreamAssemblerXXL/blob/035dc34a6199b51114cc142ccc7937e1c6872235/releases/manifests/2.8.0.json
[iv]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier5IV-AAAAAAAAAAAAAAAAAAAABw==/Tier5IV-AAAAAAAAAAAAAAAAAAAA1Q==.json
[asteroids]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier5IV-AAAAAAAAAAAAAAAAAAAABw==/OnYourWaytoAster-AAAAAAAAAAAAAAAAAAAA1w==.json
[provider]: https://github.com/GTNewHorizons/Galacticraft/blob/e3026156e3c8f626d409bba17fd927b447cb50aa/src/main/java/micdoodle8/mods/galacticraft/planets/asteroids/dimension/WorldProviderAsteroids.java
[assembler]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/000a4d9b24d77f40a79da7a105bb79ac7efca817/src/main/java/gregtech/loaders/postload/recipes/AssemblerRecipes.java
[implosion]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/000a4d9b24d77f40a79da7a105bb79ac7efca817/src/main/java/gregtech/loaders/postload/recipes/ImplosionCompressorRecipes.java
[plate3]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/SpaceRace-AAAAAAAAAAAAAAAAAAAAIg==/Tier3HeavyDutyPl-AAAAAAAAAAAAAAAAAAAFrQ==.json
[desh]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier4EV-AAAAAAAAAAAAAAAAAAAABg==/CriticalMaterial-AAAAAAAAAAAAAAAAAAAHYw==.json
[phobos]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier4EV-AAAAAAAAAAAAAAAAAAAABg==/DimensionalGoalP-AAAAAAAAAAAAAAAAAAAAuw==.json
[deimos]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier4EV-AAAAAAAAAAAAAAAAAAAABg==/DimensionalgoalD-AAAAAAAAAAAAAAAAAAAAvA==.json
[platinum]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier4EV-AAAAAAAAAAAAAAAAAAAABg==/PlatinumProcessi-AAAAAAAAAAAAAAAAAAAI-A==.json
[electronics]: https://github.com/GTNewHorizons/NewHorizonsCoreMod/blob/fe1a49ae577fee5ec4c1cf53d2545b475fb6b5af/src/main/java/com/dreammaster/scripts/ScriptGalaxySpace.java
[rocket3]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/SpaceRace-AAAAAAAAAAAAAAAAAAAAIg==/RocketTier3-AAAAAAAAAAAAAAAAAAAFrg==.json
[fuel]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/SpaceRace-AAAAAAAAAAAAAAAAAAAAIg==/DenseHydrazine-AAAAAAAAAAAAAAAAAAAKfg==.json
[dungeon]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/SpaceRace-AAAAAAAAAAAAAAAAAAAAIg==/MarsDungeon-AAAAAAAAAAAAAAAAAAAFpg==.json
[schematic]: https://github.com/GTNewHorizons/Galacticraft/blob/e3026156e3c8f626d409bba17fd927b447cb50aa/src/main/java/micdoodle8/mods/galacticraft/planets/asteroids/schematic/SchematicTier3Rocket.java
[first-naq]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier5IV-AAAAAAAAAAAAAAAAAAAABw==/YourFirstNaquada-AAAAAAAAAAAAAAAAAAAGgw==.json
[boule-quest]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier5IV-AAAAAAAAAAAAAAAAAAAABw==/NaquadahDopedMon-AAAAAAAAAAAAAAAAAAAGhg==.json
[boule-recipe]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/000a4d9b24d77f40a79da7a105bb79ac7efca817/src/main/java/gregtech/loaders/postload/recipes/BlastFurnaceRecipes.java
[ceres]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier5IV-AAAAAAAAAAAAAAAAAAAABw==/CeresTrip-AAAAAAAAAAAAAAAAAAAGAg==.json
[bee]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/BeeBreeding-AAAAAAAAAAAAAAAAAAAAEw==/Naquadah-AAAAAAAAAAAAAAAAAAABZg==.json
[rpp]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier5IV-AAAAAAAAAAAAAAAAAAAABw==/RhodiumPlatedPal-AAAAAAAAAAAAAAAAAAAJGQ==.json
[palladium]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier5IV-AAAAAAAAAAAAAAAAAAAABw==/PalladiumProcess-AAAAAAAAAAAAAAAAAAAI_w==.json
[residue]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier4EV-AAAAAAAAAAAAAAAAAAAABg==/PlatinumProcessi-AAAAAAAAAAAAAAAAAAAI-w==.json
[assembly-quest]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/MultiblockGoals-AAAAAAAAAAAAAAAAAAAADA==/AssemblyLine-AAAAAAAAAAAAAAAAAAAFhA==.json
[assembly-recipe]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/000a4d9b24d77f40a79da7a105bb79ac7efca817/src/main/java/gregtech/loaders/postload/recipes/AssemblyLineRecipes.java
[hsss]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier5IV-AAAAAAAAAAAAAAAAAAAABw==/HSSS-AAAAAAAAAAAAAAAAAAAGgQ==.json
[mixer]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier5IV-AAAAAAAAAAAAAAAAAAAABw==/IVMixer-AAAAAAAAAAAAAAAAAAAFgg==.json
[luv]: https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/c3ba07ccba1b772777f6fc57e53bb70c8547adb7/config/betterquesting/DefaultQuests/Quests/Tier6LuV-AAAAAAAAAAAAAAAAAAAACA==/Tier6LuV-AAAAAAAAAAAAAAAAAAAF1Q==.json

[[Sources]]
