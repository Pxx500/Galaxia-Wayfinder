---
type: source
status: reviewed
origin: "Repository AI/Current/GTNHPlanetDefinitionSources.md"
imported: 2026-08-01
tags:
  - galaxia/alpha
  - wayfinder/source
  - galaxia/progression
---

# Repo Source - GTNH Planet Definition Sources

Source: repository research map `AI/Current/GTNHPlanetDefinitionSources.md`
Imported: 2026-08-01

This research map is preserved as evidence and source provenance rather than accepted design. Ore progression conclusions remain subject to Verify GTNH Ore Tier Gates and the maintained GTNH Ore Sheet.

## Source Snapshot

Status: research notes from local source repos. Treat this as source mapping, not a Galaxia design decision.

Local repos inspected:

- `C:/Users/Pxx500/Documents/GitHub/Galacticraft`
- `C:/Users/Pxx500/Documents/GitHub/Galaxy-Space-GTNH`
- `C:/Users/Pxx500/Documents/GitHub/GT5-Unofficial`

## Main conclusion

There are at least three separate layers:

1. **Celestial body registration**: Galacticraft and GalaxySpace register planets/moons/stars/stations into `GalaxyRegistry`.
2. **Base mod ore generation**: Galacticraft/GalaxySpace dimensions often have their own hardcoded decorators for simple ores or special blocks.
3. **GTNH ore vein generation**: GT5-Unofficial/GalacticGreg defines the dimensions, tier display order, stone types, and GregTech ore mix allowed dimensions. This is the layer that appears closest to the GTNH ore spreadsheet/NEI view.

For Galaxia migration/design, do not model "planet resources" as one flat list on the celestial body without preserving source/layer. A body can have:

- starmap/celestial metadata,
- dimension/provider metadata,
- base worldgen metadata,
- GT ore vein metadata,
- NEI/spreadsheet progression tier metadata.

## Celestial body registration sources

### Galacticraft core

File: `Galacticraft/src/main/java/micdoodle8/mods/galacticraft/core/GalacticraftCore.java`

Important lines found:

- `solarSystemSol = new SolarSystem("sol", "milkyWay")` around line 285.
- `planetOverworld = new Planet("overworld")` around line 290.
- Overworld dimension/provider/tier: `setDimensionInfo(ConfigManagerCore.idDimensionOverworld, WorldProvider.class, false).setTierRequired(1)` around lines 293-294.
- `moonMoon = new Moon("moon").setParentPlanet(planetOverworld)` around line 298.
- Moon dimension/provider/tier: `setDimensionInfo(ConfigManagerCore.idDimensionMoon, WorldProviderMoon.class).setTierRequired(1)` around line 301.
- Registry calls: `registerSolarSystem`, `registerPlanet(planetOverworld)`, `registerMoon(moonMoon)` around lines 329-331.

Note: the same file also creates unreachable display planets such as Mercury/Venus/Mars/Jupiter later, but those are not the real reachable dimension registrations for GTNH progression.

### Galacticraft Mars

File: `Galacticraft/src/main/java/micdoodle8/mods/galacticraft/planets/mars/MarsModule.java`

- `new Planet("mars").setParentSolarSystem(GalacticraftCore.solarSystemSol)` around line 157.
- Relative distance/orbit around lines 159-160.
- Dimension/provider/tier: `setDimensionInfo(ConfigManagerMars.dimensionIDMars, WorldProviderMars.class).setTierRequired(2)` around lines 163-164.
- Registered with `GalaxyRegistry.registerPlanet(MarsModule.planetMars)` around line 168.

### Galacticraft Asteroids

File: `Galacticraft/src/main/java/micdoodle8/mods/galacticraft/planets/asteroids/AsteroidsModule.java`

- `new Planet("asteroids").setParentSolarSystem(GalacticraftCore.solarSystemSol)` around line 193.
- Dimension/provider/tier: `setDimensionInfo(ConfigManagerAsteroids.dimensionIDAsteroids, WorldProviderAsteroids.class).setTierRequired(3)` around lines 194-196.
- Relative distance/orbit around lines 197-199.
- Registered with `GalaxyRegistry.registerPlanet(AsteroidsModule.planetAsteroids)` around line 203.

### GalaxySpace Sol system

File: `Galaxy-Space-GTNH/src/main/java/galaxyspace/SolarSystem/SolarSystemPlanets.java`

Reachable/progression bodies found in this file:

| Body | Parent | Tier in registration | Dimension/provider source |
| --- | --- | ---: | --- |
| Mercury | Sol | 4 | `GSConfigDimensions.dimensionIDMercury`, `WorldProviderMercury` |
| Venus | Sol | 4 | `dimensionIDVenus`, `WorldProviderVenus` |
| Phobos | Mars | 2 | `dimensionIDPhobos`, `WorldProviderPhobos` |
| Deimos | Mars | 2 | `dimensionIDDeimos`, `WorldProviderDeimos` |
| Ceres | Sol | 3 | `dimensionIDCeres`, `WorldProviderCeres` |
| Io | Jupiter | 4 | `dimensionIDIo`, `WorldProviderIo` |
| Europa | Jupiter | 3 | `dimensionIDEuropa`, `WorldProviderEuropa` |
| Ganymede | Jupiter | 3 | `dimensionIDGanymede`, `WorldProviderGanymede` |
| Callisto | Jupiter | 3 | `dimensionIDCallisto`, `WorldProviderCallisto` |
| Enceladus | Saturn | 5 | `dimensionIDEnceladus`, `WorldProviderEnceladus` |
| Titan | Saturn | 5 | `dimensionIDTitan`, `WorldProviderTitan` |
| Miranda | Uranus | 5 | `dimensionIDMiranda`, `WorldProviderMiranda` |
| Oberon | Uranus | 5 | `dimensionIDOberon`, `WorldProviderOberon` |
| Proteus | Neptune | 6 | `dimensionIDProteus`, `WorldProviderProteus` |
| Triton | Neptune | 6 | `dimensionIDTriton`, `WorldProviderTriton` |
| Pluto | Sol | 7 | `dimensionIDPluto`, `WorldProviderPluto` |
| Kuiper Belt | Sol | 7 | `dimensionIDKuiperBelt`, `WorldProviderKuiper` |
| Haumea | Sol | 7 | `dimensionIDHaumea`, `WorldProviderHaumea` |
| Makemake | Sol | 7 | `dimensionIDMakemake`, `WorldProviderMakemake` |

Jupiter/Saturn/Uranus/Neptune are registered as starmap planets with providers, but the inspected file did not show `setTierRequired` on the planets themselves. Their moons/stations carry the progression tiers.

### GalaxySpace extra systems

Files:

- `Galaxy-Space-GTNH/src/main/java/galaxyspace/ACentauriSystem/ACentauriPlanets.java`
- `Galaxy-Space-GTNH/src/main/java/galaxyspace/BarnardsSystem/BarnardsPlanets.java`
- `Galaxy-Space-GTNH/src/main/java/galaxyspace/TCetiSystem/TCetiPlanets.java`
- `Galaxy-Space-GTNH/src/main/java/galaxyspace/VegaSystem/VegaPlanets.java`

Reachable T8 bodies found:

| Body in code | Display/GTNH dimension naming | Tier | Provider |
| --- | --- | ---: | --- |
| `CentauriBb` | `GalaxySpace_CentauriA` / `CentauriA` in NEI helper | 8 | `WorldProviderACentauri` |
| `Barnarda2` | BarnardC | 8 | `WorldProviderBarnardaC` |
| `Barnarda4` | BarnardE | 8 | `WorldProviderBarnardaE` |
| `Barnarda5` | BarnardF | 8 | `WorldProviderBarnardaF` |
| `TCetiE` | TcetiE | 8 | `WorldProviderTCetiE` |
| `Vega1` | VegaB | 8 | `WorldProviderVegaB` |

There are many visual/non-dimension planets/asteroid belts in these files. Do not assume every registered planet is a progression dimension.

## GalacticGreg dimension and tier source

### Dimension registration

File: `GT5-Unofficial/src/main/java/galacticgreg/SpaceDimRegisterer.java`

This registers dimensions into GalacticGreg mod containers:

- Moon: line 59.
- Mars: line 67.
- Asteroids: line 74.
- GalaxySpace Sol bodies: lines 99-122 plus Kuiper Belt at 124-130.
- AmunRa T9 bodies: lines 139-149.

This is the bridge that lets GregTech/GalacticGreg generate ore veins in space dimensions.

### Dimension definitions

File: `GT5-Unofficial/src/main/java/galacticgreg/api/enums/DimensionDef.java`

This enum maps dimension display names/chunk providers into `ModDimensionDef`.

Important details:

- `DimensionType.Planet` means normal ore veins.
- `DimensionType.Asteroid` means GalacticGreg asteroid generation.
- Asteroids, Kuiper Belt, EndAsteroids, and Mehen Belt are asteroid-type dimensions in this system.

### NEI/spreadsheet-like tier order

File: `GT5-Unofficial/src/main/java/gtneioreplugin/util/DimensionHelper.java`

This is the most useful local source for spreadsheet-style tier grouping and display order:

| Tier | Bodies |
| ---: | --- |
| T0 | Overworld, Nether, Twilight, The End, EndAsteroid, Everglades |
| T1 | Moon |
| T2 | Deimos, Mars, Phobos |
| T3 | Asteroids, Callisto, Ceres, Europa, Ganymede, Ross128b |
| T4 | Io, Mercury, Venus |
| T5 | Enceladus, Miranda, Oberon, Titan, Ross128ba |
| T6 | Proteus, Triton |
| T7 | Haumea, Kuiperbelt, MakeMake, Pluto |
| T8 | BarnardC, BarnardE, BarnardF, CentauriA, TcetiE, VegaB |
| T9 | Anubis, Horus, Maahes, MehenBelt, Neper, Seth |
| T10 | Underdark |

This confirms the user's spreadsheet interpretation: Moon is T1; moving right by color group is T+1.

## GTNH ore vein source

Main file: `GT5-Unofficial/src/main/java/gregtech/api/enums/OreMixes.java`

Each enum entry builds an `OreMixBuilder`:

- `heightRange(...)`
- `weight(...)`
- `density(...)`
- `size(...)`
- `enableInDim(...)`
- `primary(...)`
- `secondary(...)`
- `inBetween(...)`
- `sporadic(...)`

Runtime generation path:

- `GT5-Unofficial/src/main/java/gregtech/common/GTWorldgenerator.java`
  - gets effective dimension with `DimensionDef.getEffectiveDefForChunk(...)`;
  - skips if `!def.generatesOre()`;
  - finds random layer through `WorldgenQuery.veins().inDimension(dimensionName).findRandom(...)`.
- `GT5-Unofficial/src/main/java/gregtech/common/WorldgenGTOreLayer.java`
  - stores `mAllowedDimensions` from `OreMixBuilder.dimsEnabled`;
  - checks `mAllowedDimensions.contains(dimName)`.
- `GT5-Unofficial/src/main/java/gtneioreplugin/util/GT5OreLayerHelper.java`
  - reads the same builder data for NEI display.

### Space-relevant ore mixes found

This is the important "resource to dimensions" list from `OreMixes.java`.

| Mix | Main ores | Enabled dimensions |
| --- | --- | --- |
| Naquadah | Naquadah, NaquadahEnriched | EndAsteroids, Maahes, Asteroids, BarnardE, BarnardF, Haumea, KuiperBelt, Mercury, Oberon, Pluto, Titan, VegaB, Venus |
| Cassiterite | Tin, Cassiterite | EndAsteroids, MehenBelt, Seth, Moon, Io, Miranda, TcetiE, Venus |
| Copper | Chalcopyrite, Iron, Pyrite, Copper | EndAsteroids, Moon, BarnardE, BarnardF, Callisto, Ceres, Enceladus, Proteus |
| Bauxite | Bauxite, Ilmenite, Aluminium | Seth, Moon, Asteroids, Ganymede, Haumea, KuiperBelt, MakeMake, Mercury, Phobos, Pluto, Proteus, TcetiE, Titan |
| Platinum | Cooperite, Palladium, Platinum, Iridium | EndAsteroids, Asteroids, Maahes, MehenBelt |
| Pitchblende | Pitchblende, Uraninite | Mars, BarnardF, CentauriBb, Haumea, Io, KuiperBelt, MakeMake, Oberon, Phobos, VegaB, Venus |
| Monazite | Bastnasite, Monazite, Neodymium | Seth, Moon, BarnardF, Callisto, Deimos, Enceladus, Haumea, Io, MakeMake, Titan, Triton, Venus |
| Tungstate | Scheelite, Tungstate, Lithium | EndAsteroids, Asteroids, Mars, Callisto, Deimos, Enceladus, Ganymede, Haumea, KuiperBelt, MakeMake, Oberon, Pluto, Triton, VegaB |
| Diamond | Graphite, Diamond, Coal | BarnardF, Ganymede, KuiperBelt, Mercury, Miranda, Phobos, Pluto, Proteus, Titan |
| Apatite | Apatite, TricalciumPhosphate, Pyrochlore | TcetiE |
| Galena | Galena, Silver, Lead | Moon, Mars, Ganymede, Oberon, Triton, VegaB, Venus |
| Uranium | Uraninite, Uranium | MehenBelt, BarnardE, Ceres, Deimos, Enceladus, Ganymede, Haumea, KuiperBelt, MakeMake, Phobos, Proteus |
| Neutronium | Neutronium, Adamantium, Naquadah, Titanium | Maahes, MehenBelt, BarnardE, BarnardF, Haumea, KuiperBelt, MakeMake, Pluto, Proteus, Triton, VegaB |
| AquaIgnis | InfusedWater, InfusedFire, Amber, Cinnabar | Neper |
| TerraAer | InfusedEarth, InfusedAir, Amber, Cinnabar | Neper |
| TitaniumChrome | Ilmenite, Chromite, Uvarovite, Perlite | MehenBelt, Moon, Asteroids, Callisto, Ganymede, Mercury, Miranda, Pluto, Proteus, TcetiE, Titan |
| Mica | Kyanite, Mica, Cassiterite, Pollucite | Anubis, Neper, BarnardC |
| PlatinumChrome | Platinum, Chrome, Cooperite, Palladium | Asteroids, MehenBelt, Seth, Callisto, Ceres, Ganymede, Io, KuiperBelt, Mercury, Oberon, Pluto |
| IridiumMytryl | Nickel, Iridium, Palladium, Mithril | MehenBelt, Seth, Enceladus, Io, KuiperBelt, Mercury, Miranda, Titan, Triton, Venus |
| Osmium | Nickel, Osmium, Iridium | MehenBelt, Seth, BarnardC, Enceladus, KuiperBelt, Miranda, Oberon, Pluto, Proteus, Titan |
| Desh | Desh, Scheelite, Tungstate | Anubis, Mars, Miranda |
| Draconium | Draconium, Electrotine, Jade, Vinteum | Horus, Seth, Deimos, Mercury, Miranda, Phobos |
| Quantium | Quantium, Amethyst, Rutile, Ardite | Horus, Maahes, Venus |
| CallistoIce | CallistoIce, Topaz, BlueTopaz, Alduorite | Anubis, Maahes, Callisto |
| Mytryl | Mytryl, Jasper, Ceruclase, Vulcanite | Anubis, Horus, Io |
| Ledox | Ledox, Opal, Orichalcum, Rubracium | Horus, Enceladus, Europa |
| Oriharukon | Oriharukon, Tanzanite, Vyroxeres, Mirabilite | Horus, Deimos, Phobos |
| BlackPlutonium | BlackPlutonium, GarnetRed, GarnetYellow, Borax | Horus, BarnardC, CentauriBb, MakeMake, Pluto, TcetiE |
| InfusedGold | Gold, InfusedGold, Platinum | BarnardE, Haumea, Io, Proteus, Titan, VegaB |
| Niobium | Niobium, Yttrium, Gallium | BarnardF, MakeMake, Triton, VegaB |
| TungstenIrons | Tungsten, Silicon, DeepIron, ShadowIron | Neper, BarnardC, BarnardE, BarnardF, Oberon, Pluto, Proteus, Triton |
| UraniumGTNH | Thorium, Uranium, Plutonium241, Uranium235 | BarnardE, BarnardF, Haumea, Pluto, Triton, VegaB |
| VanadiumGold | Vanadium, Magnetite, Gold, Chrome | Maahes, BarnardF, Enceladus, MakeMake, Proteus, VegaB |
| NetherStar | GarnetSand, NetherStar, GarnetRed, GarnetYellow | Horus, BarnardE, Haumea, TcetiE, VegaB |
| Garnet | GarnetRed, GarnetYellow, Chrysotile, Realgar | Horus, BarnardF, MakeMake, VegaB |
| RareEarth | Cadmium, Caesium, Lanthanum, Cerium | BarnardE, BarnardF, CentauriBb, VegaB |
| RichNuclear | Uranium, Plutonium, Thorium | Callisto, Ceres, Ganymede, Io |
| HeavyPentele | Arsenic, Bismuth, Antimony | Neper, Mars, BarnardC, Mercury, Phobos, Titan, VegaB |
| Europa | Magnesite, BandedIron, Sulfur, Opal | Horus, Europa, TcetiE |
| EuropaCore | Chrome, Tungstate, Molybdenum, Manganese | Maahes, Europa, TcetiE |
| SecondLanthanid | Samarium, Neodymium, Tartarite | Seth, BarnardC, CentauriBb |
| QuartzSpace | Quartzite, Barite, CertusQuartz | Horus, Moon, Mars, CentauriBb, Io, Phobos, Proteus, TcetiE, Venus |
| Rutile | Rutile, Titanium, Bauxite, MeteoricIron | Anubis, Titan, Venus |
| LuVTantalite | Pyrolusite, Apatite, Tantalite, Pyrochlore | Io, Miranda |
| CertusQuartz | CertusQuartz, CertusQuartzCharged, QuartzSand | Horus, Neper |
| InfinityCatalyst | Neutronium, Adamantium, InfinityCatalyst, Bedrockium | Anubis |
| CosmicNeutronium | Neutronium, CosmicNeutronium, BlackPlutonium, Bedrockium | Horus |
| Dilithium | Dilithium, MysteriousCrystal, Vinteum | Neper |
| Naquadria | Naquadah, NaquadahEnriched, Naquadria, Trinium | Maahes |
| AwakenedDraconium | Draconium, DraconiumAwakened, NetherStar | MehenBelt |
| Tengam | TengamRaw, Electrotine, Samarium | Seth |

## Base mod ore generation sources

These are not the same as GT ore veins. They are hardcoded dimension decorators/special blocks from the planet mods.

### Galacticraft Moon

File: `Galacticraft/src/main/java/micdoodle8/mods/galacticraft/core/world/gen/BiomeDecoratorMoon.java`

- Copper: 26 attempts, y 0-60, if `!ConfigManagerCore.disableCopperMoon`.
- Tin: 23 attempts, y 0-60, if `!ConfigManagerCore.disableTinMoon`.
- Cheese: 12 attempts, y 0-128, if `!ConfigManagerCore.disableCheeseMoon`.
- Dirt: 20 attempts, y 0-200.

### Galacticraft Mars

File: `Galacticraft/src/main/java/micdoodle8/mods/galacticraft/planets/mars/world/gen/BiomeDecoratorMars.java`

- Ice: 4 attempts, y 60-120.
- Dirt: 20 attempts, y 0-200.
- Desh: 15 attempts, y 20-64, if `!ConfigManagerMars.disableDeshGen`.
- Copper: 26 attempts, y 0-60, if `!ConfigManagerMars.disableCopperGen`.
- Tin: 23 attempts, y 0-60, if `!ConfigManagerMars.disableTinGen`.
- Iron: 20 attempts, y 0-64, if `!ConfigManagerMars.disableIronGen`.

### Galacticraft Asteroids

File: `Galacticraft/src/main/java/micdoodle8/mods/galacticraft/planets/asteroids/world/gen/ChunkProviderAsteroids.java`

Special asteroid core blocks:

- Asteroid stone variants.
- Aluminum if `!ConfigManagerAsteroids.disableAluminumGen`.
- Ilmenite if `!ConfigManagerAsteroids.disableIlmeniteGen`.
- Iron if `!ConfigManagerAsteroids.disableIronGen`.
- Silicon if `ConfigManagerCore.enableSiliconOreGen`.
- Solid Meteoric Iron with no disable config in the inspected block.
- Diamond ore with no disable config in the inspected block.

### GalaxySpace hardcoded ore decorators

Source pattern: `Galaxy-Space-GTNH/src/main/java/galaxyspace/**/world/BiomeDecorator*Ore.java`

Examples found:

| Body | Hardcoded decorator ores |
| --- | --- |
| Deimos | Oriharukon, Tin |
| Europa | Ice |
| Ganymede | Magnesium, Ilmenite |
| Io | Wolframium, Copper, Sulfur |
| Miranda | Iron |
| Oberon | Adamantite |
| Phobos | Cobaltum, Desh |
| Proteus | Wolframium, Platinum |
| Triton | Mithril |
| Ceres | Meteoric Iron |
| Mercury | Lead, Iron, Nickel |
| Venus | Sulfur, Diamond |
| BarnardC | Coal, Diamond, Redstone, Lapis |
| BarnardE | Iron, Gold |

Some decorator classes are empty or do not define special ores, for example `BiomeDecoratorEnceladusOre.java` and `BiomeDecoratorTCetiEOre.java` in the inspected output.

## Open questions

- Need inspect AmunRa source if available locally to map T9 planet registrations and their base worldgen decorators.
- Need inspect `NewHorizonsCoreMod` and `GT-New-Horizons-Modpack` only if we need pack config overrides for disabled base ore generation or dimension IDs.
- Need decide whether Galaxia should import GTNH ore mix semantics as authored data, or keep resource distribution as a separate Galaxia-specific balance layer.



## Wayfinder Integration

- Evidence for [[GTNH Ore Progression Baseline]].
- Input to Verify GTNH Ore Tier Gates.
- Repository-layer observations remain evidence, not accepted Galaxia resource-model design.
