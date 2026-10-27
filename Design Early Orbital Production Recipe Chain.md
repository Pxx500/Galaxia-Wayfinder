---
type: wayfinder-ticket
ticket_type: grilling
status: open
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Alpha Scope]]"
secondary_areas:
  - Area - Observation and Research
blocked_by: []
claimed_by: wayfinder
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Design Early Orbital Production Recipe Chain

## Question And Scope

Which complete recipes connect early germanium and fluoride feedstocks to Rocket automation, functional satellites and Galaxia solar components?

This ticket records accepted production direction and working recipes alongside explicitly unapproved details. It does not establish implemented behavior. Rocket structures, the Station Starter Kit, lunar SGA, Hammers and later propulsion are outside this chain.

[[Define Alpha Research and Production Floor]] owns the required material families and normal GT machinery baseline. [[Define Satellite Manufacturing and Deployment Progression]] owns satellite behavior. [[Define Alpha Technology Knowledge Contract]] owns consumed team-knowledge blueprints.

## Accepted Production Direction

- Silicon-germanium supplies Rocket and satellite electronics. Fluoride fibers supply satellites. Neither material is required for the opening Primitive Telescope Satellite or first Station bootstrap
- SiGe blend must pass through EBF powder treatment before supplying usable crystal-growth melt. A direct blend-to-molten route, including generated melting, is excluded
- One blend dust has independent 10% seed and 90% Poly SiGe output rolls. Both occur on 9% of runs and neither on 9%. Average output is one SiGe material unit. Poly SiGe is remelting feedstock only, not a wafer or seed source
- EBF growth consumes a seed and molten SiGe. Monocrystals can become seeds or wafers, not both. Seeds can also be remelted. Numerical growth and splitting values below remain proposals
- Powder processing removes impurities as an existing GT ash or slag byproduct. Its exact form and quantity remain proposed
- Wafer engraving is mandatory. Engraving and final chip cutting require a cleanroom, not microgravity. HCl washing is permitted, with its detailed recipe still proposed
- Fluoride manufacture uses melting, casting, Lathe preform preparation, EBF softening and drawing. Blanks cost two dust units, and the Lathe returns one dust unit for reuse
- Glassmaking, casting, preform softening and drawing require Microgravity. Ordinary machining, packaging and final assembly do not. Sixteen fibers form one spool, while small recipes may use individual fibers
- Primitive Telescope uses four ordinary Glass Lenses. Functional satellites have distinct transmitter and scanning hardware as recorded below. Satellites include solar hardware as well as a battery
- Space Grade Solar Panel is a shared recipe-component item, not a placeable generator or alternate GT solar cover. Existing GTNH solar recipes and output remain unchanged

The proposed early tier is HV, with MV preparation where sufficient. This does not alter the IV first Spaceship or accepted Hammer tiers. Powder processing and seeded growth are the proposed microgravity-dependent SiGe operations. Ordinary SiGe remelting has no location restriction.

## Recipe Conventions

Fluid amounts are mB and times are base values before overclocking. Selector circuits, lenses, molds and the wire extrusion die are reusable. Electronic circuits listed as ingredients are consumed. Cells return empty unless filled as outputs. Each recipe has an independent batch size. Accumulation and splitting connect the stages.

All new assembly uses the ordinary GT Assembler, not Galaxia's Rocket Module Assembler. Control Logic Circuit, abbreviated CLC, is a working functional name. Blank SiGe wafers become CLC Wafer, Etched CLC Wafer, CLC Chip and CLC Module. These are equipment ingredients, not replacements for standard GT circuit tiers, ILCs or CPUs. Final names remain open.

## Existing Silicon Feedstock

These are source-audited existing GTNH 2.8 routes. Other normal routes remain usable.

| Process | Inputs | Outputs | Machine | EU/t | Time |
| --- | --- | --- | --- | ---: | ---: |
| Silica | 8 sand | 3 Silicon Dioxide dust | Electrolyzer | 25 | 25 s |
| Reduction | 3 Silicon Dioxide dust + 2 Carbon dust | 1 Silicon ingot + 2000 mB Carbon Monoxide, with existing ash chance | EBF, 1200 K | 120 | 4 s |
| Powder | Silicon ingot | Silicon dust | Existing Macerator | Existing | Existing |
| Chlorination | 1 Silicon dust + 4000 mB Chlorine, selector 2 | 1000 mB Silicon Tetrachloride | Chemical Reactor | 30 | 20 s |
| Purification | 4 Sodium dust + 1000 mB Silicon Tetrachloride, selector 1 | 1 solar-grade Silicon dust + 8 Salt dust | Chemical Reactor | 30 | 5 s |
| Salt recycling | 2 Salt dust | 1 Sodium dust + 1000 mB Chlorine | Electrolyzer | 30 | 16 s |

`Materials.SiliconSG` is Silicon Solar Grade, not SiGe. Salt recycling supplies sodium and chlorine after startup inventory is established.

## Germanium And SiGe Electronics

The 8 mB early germanium yield, independent powder-output rolls, mandatory engraving and cleanroom requirements are accepted. Other numerical settings in this table remain working proposals, including the residue, growth quantities, wash and chip-cutting details.

| Product | Inputs | Outputs | Machine | EU/t | Time | Environment |
| --- | --- | --- | --- | ---: | ---: | --- |
| Early germanium | 1 purified crushed Sphalerite + 4 Carbon dust + 250 mB Sulfuric Acid | 8 mB existing molten Germanium | Chemical Reactor | 480 | 30 s | Any |
| Blend | 7 solar-grade Silicon dust + 144 mB molten Germanium | 8 SiGe blend dust | Mixer | 120 | 20 s | Any |
| Powder processing | 1 SiGe blend dust | 1 SiGe seed at 10%, 1 Poly SiGe at independent 90%, 1 tiny pile of Ash | EBF, 1784 K | 480 | 60 s | Microgravity |
| Remelting | 1 Poly SiGe | 144 mB molten SiGe | Fluid Extractor | 480 | 10 s | Any |
| Seed remelting | 1 SiGe seed | 144 mB molten SiGe | Fluid Extractor | 480 | 10 s | Any |
| Crystal growth | 1 SiGe seed + 1008 mB molten SiGe | 1 SiGe monocrystal | EBF, 1784 K | 480 | 120 s | Microgravity |
| Seed multiplication | 1 SiGe monocrystal | 8 SiGe seeds | Forge Hammer | 120 | 10 s | Any |
| Cutting | 1 SiGe monocrystal + 100 mB Water | 16 SiGe wafers | Cutting Machine | 120 | 40 s | Any |
| Wafer engraving | 1 SiGe wafer + reusable Ruby Lens | 1 CLC Wafer | Laser Engraver | 480 | 45 s | Cleanroom, any gravity |
| Wafer wash | 1 CLC Wafer + 250 mB Hydrochloric Acid | 1 Etched CLC Wafer | Chemical Bath | 480 | 30 s | Any |
| Chip cutting | 1 Etched CLC Wafer + 100 mB Water | 4 CLC Chips | Cutting Machine | 120 | 45 s | Cleanroom, any gravity |
| Packaging | 4 CLC Chips + 2 Copper plates + 8 fine Copper wires + 144 mB molten Tin | 1 CLC Module | Assembler | 480 | 30 s | Any |

The early reactor's two item slots hold sphalerite and carbon, so it has no selector. A normal MV Ruby plate-to-lens Lathe route supplies the proposed engraving tool. The proposed HCl wash is a fixed operation after engraving, not a quality branch or a replacement for engraving.

The proposed Ash is guaranteed independently of the two SiGe rolls and reuses `Materials.Ash` with `OrePrefixes.dustTiny`. It represents unspecified impurities, not a verified combustion reaction. Poly SiGe and seeds may melt because they have passed through treatment. A byproduct alone would not enforce exclusion of untreated blend melting.

At the working yields, one crystal becomes 16 wafers, then 64 CLC Chips or 16 CLC Modules. Alternatively it becomes eight seeds, which can grow later crystals or remelt to 1152 mB total. The first seed takes ten fresh powder operations on average, with nine Poly SiGe on average alongside it. Those products are growth inventory, not powder that retries nucleation.

Keep the existing IV ABS recipe unchanged: 1 purified crushed Sphalerite + 4 Carbon dust + 250 mB Sulfuric Acid, selector 15, produces 36 mB molten Germanium at 4000 EU/t for 37.5 s. Compared with that route, supplying 144 mB through the early recipe uses 18 rather than 4 ore, 72 rather than 16 Carbon dust, 4500 rather than 1000 mB acid, and 9 rather than 2.5 base minutes. ABS is 4.5 times better per ore and reagent and 3.6 times faster. No energy-saving claim or change to other Germanium consumers is selected.

## Existing Fluoride Feedstock

The proposed formulation is fictional sodium-aluminium oxyfluoride glass, not exact ZBLAN. It reuses the following existing recipes.

| Product | Inputs | Outputs | Machine | EU/t | Time |
| --- | --- | --- | --- | ---: | ---: |
| Fluorine | 20 Lepidolite dust + 4 empty cells | 2000 mB Fluorine + 1 Potassium dust + 3 Lithium dust + 10 Aluminium Oxide dust + 4 Oxygen cells | Electrolyzer | 120 | 13 s |
| Hydrofluoric Acid | 1 Hydrogen cell + 1000 mB Fluorine, selector 1 | 1000 mB GT5U Hydrofluoric Acid + empty cell | Chemical Reactor | 8 | 3 s |
| Salt Water | 2 Salt dust + 1000 mB Water, selector 3 | 1000 mB Salt Water | Mixer | 8 | 5 s |
| Sodium Hydroxide | 1000 mB Salt Water + empty cell, selector 1 | 3 Sodium Hydroxide dust + Hydrogen cell + 1000 mB Chlorine | Electrolyzer | 30 | 36 s |
| Sodium Fluoride | 3 Sodium Hydroxide dust + 1000 mB Hydrofluoric Acid, selector 15 | 2 Sodium Fluoride dust + 1000 mB Water | Chemical Reactor | 30 | 60 s |
| Silicon Tetrafluoride | 3 Silicon Dioxide dust + 4000 mB Hydrofluoric Acid, selector 2 | 1000 mB Silicon Tetrafluoride | Chemical Reactor | 30 | 15 s |
| Aluminium Fluoride | 4 Aluminium dust + 3000 mB Silicon Tetrafluoride, selector 1 | 16 Aluminium Fluoride dust + 3 Silicon dust | Chemical Reactor | 30 | 30 s |

Lepidolite and salt coexist in audited Overworld salt veins. Normal aluminium, silica and hydrogen processing supplies the other inputs.

## Fluoride Flow And Working Recipes

The machine sequence, two-dust blank, one-dust Lathe return, sixteen-fiber spool and four Microgravity operations are accepted. Other numerical values remain working proposals.

| Product | Inputs | Outputs | Machine | EU/t | Time | Environment |
| --- | --- | --- | --- | ---: | ---: | --- |
| Batch preparation | 2 Sodium Fluoride dust + 4 Aluminium Fluoride dust + 3 Silicon Dioxide dust | 9 fluoride-glass mix | Mixer | 120 | 15 s | Any |
| Glassmaking | 1 fluoride-glass mix | 144 mB molten fluoride glass | EBF, 1800 K | 480 | 120 s | Microgravity |
| Blank casting | 288 mB molten fluoride glass + reusable ingot mold | 1 fluoride-glass blank | Fluid Solidifier | 120 | 20 s | Microgravity |
| Preform shaping | 1 fluoride-glass blank | 1 fluoride-glass preform + 1 fluoride-glass mix | Lathe | 480 | 20 s | Any |
| Preform softening | 1 fluoride-glass preform | 1 heated fluoride-glass preform | EBF, 1800 K | 480 | 20 s | Microgravity |
| Fiber drawing | 1 heated fluoride-glass preform + reusable wire extrusion die | 8 fluoride optical fibers | Extruder | 480 | 30 s | Microgravity |
| Spool winding | 16 fluoride optical fibers | 1 Fluoride Fiber Spool | Assembler | 120 | 10 s | Any |

Casting creates cold stock for machining. The Lathe prepares a drawing preform and returns reusable mix. The later EBF softens it for drawing. No direct molten-glass-to-fiber bypass, custom machine or quality variants are selected. Softened Preform, Lumen Fiber and Lumen Spool are unapproved names. Earlier material-stage names stay material-based.

The returned mix represents reclaimed glass feedstock. With recycling, a fresh nine-unit mix batch yields eight preforms, 64 fibers and one circulating mix unit. Further fresh mix can then yield one preform per unit while retaining that reserve. Operations need not be scaled to match those totals.

Microgravity is a gameplay restriction inspired by reduced crystallization, sedimentation and convection during real ZBLAN drawing. It is extended here to the fictional glass's molten and softened stages, not a claim that terrestrial glass production is impossible. [NASA optical-fiber research](https://www.nasa.gov/missions/station/iss-research/optical-fiber-production/) supports the drawing rationale. Background remains in [[Orbital Manufacturing Research]].

## Parts And Payload Recipes

The Satellite Frame, Satellite Dish and Primitive Telescope Satellite recipes below are accepted working recipes, including quantities, duration and 480 EU/t. The Rocket Automation Controller recipe remains a working proposal. Each produces one item in an ordinary Assembler without an environmental restriction.

| Output | Inputs | Time |
| --- | --- | ---: |
| Satellite Frame | 4 Aluminium plates + 2 Steel rods + 2 Aluminium rings | 30 s |
| Satellite Dish | 4 Aluminium plates + 4 fine Copper wires + 1 MV Emitter + 144 mB molten Tin | 20 s |
| Primitive Telescope Satellite | 1 frame + 1 dish + 4 Glass Lenses + 1 HV circuit + 1 MV Sensor + 1 rechargeable HV Lithium Battery + 1 ordinary GT Solar Panel + 144 mB molten Tin | 45 s |
| Rocket Automation Controller | 1 CLC Module + 2 HV circuits + 1 HV Sensor + 1 HV Emitter + 2 Aluminium plates + 4 fine Copper wires + 288 mB molten Tin | 45 s |

The following functional-satellite compositions are selected, with working Assembler settings of 480 EU/t for 60 s. Panel inclusion is accepted, with quantities still working balance values.

| Ingredient | Communication Satellite | Prospecting Satellite |
| --- | ---: | ---: |
| Satellite Frame | 1 | 1 |
| Satellite Dish | 2 | 0 |
| HV Emitter | 3 | 1 |
| HV Sensor | 1 | 3 |
| Diamond Lens | 0 | 2 |
| CLC Module | 1 | 2 |
| Fluoride Fiber Spool | 2 | 1 |
| Rechargeable HV Lithium Battery | 1 | 1 |
| Space Grade Solar Panel | 2 | 1 |
| Molten Tin | 288 mB | 288 mB |

Communication uses antennas and transmission hardware, while Prospecting uses optics and sensors. Both use control electronics and optical routing, consuming 32 and 16 fibers respectively. Primitive Telescope uses the existing ground-made `ItemList.Cover_SolarPanel`. Batteries remain separate inputs. These ingredients do not introduce satellite EU generation, charging or maintenance simulation.

Use `ItemList.Battery_RE_HV_Lithium` for the named battery. Functional satellites use `ItemList.Sensor_HV` and `ItemList.Emitter_HV`. The accepted Primitive Telescope recipe instead uses an MV Sensor, and the dish recipe uses an MV Emitter. The dish reuses `GalaxiaItemList.SATELLITE_DISH`, registered as `parts/satellite_dish`. Its registration is not an existing production recipe. The pinned HV Assembler has nine item slots. Primitive Telescope uses seven distinct item types, and each functional satellite uses eight, with tin in the fluid slot.

The opening payload remains a limited achievement mission that grants Star Map access and passive Luna resource-scan progress, not a cheap retargetable Prospecting Satellite or physical block scan. The controller adds automation to the same reusable Rocket. Manual Luna flights remain possible without it. Lunar SGA is absent from this pre-Luna bootstrap.

## Accepted Technology Groups And Proposed Blueprint Costs

The Rocket Automation and Functional Satellites groups and the unlocks below are accepted. Their blueprint ingredient quantities, manufacturing costs and GT production-enforcement integration are not approved by that grouping decision. The consumed-blueprint mechanism itself is accepted.

The proposed recipes each produce one Technology Blueprint in an Assembler at 480 EU/t for 15 s, without an environmental restriction.

| Blueprint | Proposed inputs | Accepted unlocks |
| --- | --- | --- |
| Rocket Automation | 2 CLC Modules + 1 HV circuit + 1 book + 144 mB molten Tin | Rocket Automation Controller production |
| Functional Satellites | 2 CLC Modules + 1 Fluoride Fiber Spool + 1 HV circuit + 1 book + 144 mB molten Tin | Communication and Prospecting Satellite production |

Successful player activation consumes the blueprint and grants team knowledge. Later production consumes components, not another blueprint. Material processing, frames, dishes and the opening payload need neither proposed technology, so acquisition is not circular. These are not reusable Rocket assembly Blueprints.

## Accepted Solar Component Recipes

SiGe and fluoride glass provide an alternative route to cheaper solar hardware for Galaxia equipment. These working recipes are accepted. Finishing and assembly are unrestricted, with no cleanroom or gravity requirement added by these rows. Their feedstocks already carry the relevant Microgravity operations.

| Output | Inputs | Machine | EU/t | Base time |
| --- | --- | --- | ---: | ---: |
| 4 Solar Cells | 1 SiGe Wafer + reusable Glass Lens | Laser Engraver | 480 | 45 s |
| 3 Solar Glass Sheets | 1 fluoride-glass blank + 100 mB Water | Cutting Machine | 120 | 20 s |
| 1 Space Grade Solar Panel | 2 Solar Cells + 1 Solar Glass Sheet + 1 CLC Module + 4 Aluminium plates + 8 fine Copper wires + 288 mB molten Tin | Assembler | 480 | 60 s |

The panel is a manufactured component, not a block or generator. It does not output an existing GT HV solar panel or change GTNH generation parameters. Placeable solar equipment remains outside this content scope.

## Factory Power

Standard GT power infrastructure is the baseline. Combustion generation is prohibited in space, including oxygenated Station rooms. [[Define Celestial Capability Rules]] owns that condition. No oxygenator or ventilation exception is selected. Steam turbines, nuclear and other non-combustion machinery are not combustion merely because they generate power. Their upstream fuel-burning machinery must be considered separately.

Transported electrical energy is the provisional first-factory bootstrap. Charge ordinary GT batteries on the surface, bring them to the workshop and use a tier-appropriate GT Battery Buffer. Return depleted batteries for recharge. No orbital material or new generator is required to start this route.

Battery count, charge logistics and actual recipe demand still need verification. [[Define Space Factory Power Supply]] owns the accepted solar-generator direction, current prohibition on interplanetary wireless EU and remaining generation-equipment choices. Sustained local generation is not an accepted prerequisite for the initial battery route. Space Grade Solar Panel remains a component item, distinct from the placeable array hardware.

## Accepted Content Ownership And Temporary Staging

Temporarily develop GT-bound content under `com.gtnewhorizons.galaxia.gt5`. New item, material and fluid definitions, recipe chains and balance ultimately belong in GT5 before Alpha. Their textures and translations move with them, even though resources live outside the Java package.

Galaxia retains celestial environments, missions, satellite behavior and research mechanics. Keep that integration outside the transfer package. Use normal GT registration and recipe capabilities, without a parallel production system or reverse hard dependency.

The initial environment prototype was hosted in Galaxia. The owner subsequently authorized native GT environment API work in the separate integration delivery, with MaterialLib-backed material compatibility as its priority. This does not move ownership of content definitions or authorize independent GT infrastructure changes by each content task. Coordinate API adoption with that delivery and use its verified dependency target rather than inventing a parallel integration.

Developer worlds may break before Alpha. Transfers need no old-ID preservation, dual registration or save migration. Remove temporary Galaxia definitions when GT replacements become authoritative.

## Shared Supply And Verification Boundary

Normal GT recipes supply Copper plates and wire, Aluminium plates and rings, Steel rods, molten Tin, circuits, sensors, emitters and Lithium Batteries. Books retain normal crafting. Ore washing supplies purified Sphalerite. Graphite electrolysis gives four Carbon dust per Graphite dust. Standard sulfur oxidation supplies Sulfuric Acid. Hydrogen and Chlorine supply Hydrochloric Acid. Water electrolysis and normal cell handling supply gases. No parallel Galaxia reagent copies are selected.

The existing recipes were audited against GT5-Unofficial `000a4d9b24d77f40a79da7a105bb79ac7efca817` and CoreMod `fe1a49ae577fee5ec4c1cf53d2545b475fb6b5af`. Galaxia registry checks used `a9128e9ef21ff05254648190b4f79f94bdc9669d`. Current checkouts differ. Source presence is not a playable-pack production test.

## Remaining Decisions

- Review unapproved working quantities, power and durations, especially the residue, growth cycle, wash and chip-cutting details
- Select final CLC and fiber/preform names
- Select the two blueprint recipes and resolve GT team-knowledge production enforcement, preserving the accepted groups and unlocks
- Verify early feedstock and component availability, environmental enforcement and complete production throughput
- Verify transported battery power against actual charge demand and logistics, then design sustained non-combustion supply separately
- Tune working panel quantities if needed while preserving the ground-made opening payload
