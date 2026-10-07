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
claimed_by: local-wayfinder-orbital-recipes
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Design Early Orbital Production Recipe Chain

## Question And Status

Which complete recipes should connect early germanium and fluoride feedstocks to Rocket automation, functional satellites and Galaxia solar equipment?

The owner requested a complete recipe proposal on 2026-10-07 rather than individual tier questions. The 2026-10-08 round adds the selected fluoride production flow, satellite revisions and solar component recipes. Accepted direction and working recipe values are recorded below. Remaining proposals are identified explicitly. None of these recipes is implemented by this note.

The scope is both early orbital material chains and their opening-payload, Rocket-control, functional-satellite and solar branches. It does not redesign all Rocket structural parts, the Station Starter Kit, lunar Space-Grade Alloy, Hammers or later propulsion. Standard GT components retain their normal recipes.

[[Define Alpha Research and Production Floor]] owns material allocation and the GT machinery baseline. [[Define Satellite Manufacturing and Deployment Progression]] owns satellite behavior. [[Define Alpha Technology Knowledge Contract]] owns consumed team-knowledge blueprints.

## Proposed Progression

### Accepted Owner Revisions

The 2026-10-07 and 2026-10-08 rounds establish the following direction:

- Processing SiGe powder has a chance to produce a seed and a high chance to recover material. The later clarification replaces powder return with Poly SiGe as the common output.
- Poly SiGe is useful only as feedstock for melting in the Fluid Extractor. It is not a wafer material or an alternative seed source.
- The EBF grows a SiGe monocrystal from a seed plus molten SiGe.
- A monocrystal can be split into seeds, allowing further production to cycle seeds instead of repeatedly depending on a successful random seed roll.
- A SiGe seed can also be melted in the Fluid Extractor to recover molten SiGe. Its proposed yield uses the same material unit as Poly SiGe.
- The owner changed early germanium output to 8 mB and powder processing to one dust with a 10% chance of one seed and a 90% chance of one Poly SiGe. They explicitly accepted independent rolls, including both outputs on some operations, because average output balances over continued production.
- Powder processing also removes impurities as a small existing GT ash or slag byproduct. SiGe blend must pass through this EBF step before supplying usable melt. Adding a direct blend-to-molten recipe would bypass that intended treatment.
- SiGe chips must follow ordinary GTNH's mandatory Laser Engraver stage. The owner permits an HCl wash afterward. The detailed wash and cutting recipes below remain proposed.
- After engraving, electronic items should be named by their function rather than keeping SiGe as the name of every circuit stage. The working CLC names below answer that request but remain open to redlining.
- The fluoride chain uses melting, casting, solid preform preparation, softening and drawing. Item names omit the repeated Specialty prefix.
- Fluoride-glass blanks use two dust units each. The Lathe produces one preform and returns one dust unit for reuse.
- Sixteen fluoride optical fibers are packaged as one spool for larger recipes. Small recipes may continue using individual fibers.
- The EBF makes molten fluoride glass. A Fluid Solidifier casts a cold blank before the Lathe prepares the preform. The second EBF softens that preform for drawing. This sequence replaces the earlier direct EBF blank output and the proposed Cutter replacement for the Lathe.
- Glassmaking, casting, preform softening and drawing require microgravity. The owner wants a complete microgravity workshop, not a single remote processing operation. Ordinary machining and packaging can happen alongside it without an environmental restriction.
- The opening item is Primitive Telescope Satellite, with four ordinary Glass Lenses in its recipe.
- Communication and Prospecting Satellite recipes use distinct transmitter and scanning hardware, with the owner's counts in their comparison table below.
- Satellite recipes include solar hardware alongside their battery. Primitive Telescope Satellite uses an existing ground-made GT panel. Functional satellites use Space Grade Solar Panels. The working panel quantities are listed below.
- SiGe and fluoride glass also enable cheaper solar hardware for Galaxia. Space Grade Solar Panel is a shared manufactured component for later conversion into Galaxia generators of different tiers. Existing GTNH solar recipes and balance are preserved. Section 7 owns the selected working recipes.
- Each recipe has its own appropriate operation size. Do not multiply a recipe merely to match the previous output batch or make consecutive recipes exact multiples.

This draft proposes powder processing and seeded growth as the two microgravity-dependent SiGe recipes.

1. Craft the frame, dish and Primitive Telescope Satellite from starting-world ingredients. Deploy it to obtain the accepted shared achievement and Star Map access. The achievement provides passive Luna resource-scan progress, not a physical-world block scan.
2. Establish the first Station under its separately owned bootstrap contract. Neither it nor the opening payload requires these new orbital materials.
3. Prepare germanium, silicon and the fluoride-glass mixture. In microgravity, process SiGe dust to obtain seeds and Poly SiGe, then use melted Poly SiGe for seeded crystal growth. Establish the fluoride melting, casting, preform and drawing line in the same workshop.
4. Cut and process crystals, package electronics, acquire the proposed technologies and manufacture controllers, satellites or solar components. These later operations can happen on the surface or in space unless their row states an environmental requirement.

HV is the proposed first usable tier, with MV preparation where sufficient. This does not change the IV first Spaceship or accepted Hammer tiers. SiGe powder processing and seeded growth use microgravity. The four selected fluoride thermal and drawing operations also require microgravity. Ordinary remelting of SiGe, machining and final assembly have no location restriction.

## Recipe Conventions

Fluid quantities are mB. Durations are base times before overclocking. Selector circuits and the wire extrusion die are reusable. Electronic circuits listed as components are consumed. Cells return empty unless filled as outputs.

Recipe batch sizes are independent. Choose quantities for the process and balance, not to align adjacent operations. Buffering and repeated operations can connect different input and output counts.

All new assembly recipes use the ordinary GT Assembler, not Galaxia's Rocket Module Assembler. The working functional name is Control Logic Circuit, abbreviated CLC. Blank SiGe wafers keep their material name. Engraved electronics become CLC Wafer, Etched CLC Wafer, CLC Chip and CLC Module. These are Galaxia ingredients, not replacements for standard GT circuit tiers, ILCs or CPUs. The satellite battery ingredient is the existing rechargeable HV lithium battery, `ItemList.Battery_RE_HV_Lithium`. HV sensors and emitters use `ItemList.Sensor_HV` and `ItemList.Emitter_HV`. Their presence does not define a new charging or satellite-maintenance mechanic.

## 1. Existing Silicon Feedstock

These are existing audited GTNH 2.8 recipes, not additions. Other existing routes to the same materials remain usable.

| Process | Inputs | Outputs | Machine | EU/t | Time |
| --- | --- | --- | --- | ---: | ---: |
| Silica | 8 sand | 3 silicon dioxide dust | Electrolyzer | 25 | 25 s |
| Reduction | 3 silicon dioxide dust + 2 carbon dust | 1 silicon ingot + 2,000 mB carbon monoxide, with existing ash chance | EBF, 1,200 K | 120 | 4 s |
| Powder | Silicon ingot | Silicon dust | Existing Macerator recipe | Existing | Existing |
| Chlorination | 1 silicon dust + 4,000 mB chlorine, selector 2 | 1,000 mB silicon tetrachloride | Chemical Reactor | 30 | 20 s |
| Purification | 4 sodium dust + 1,000 mB silicon tetrachloride, selector 1 | 1 solar-grade silicon dust + 8 salt dust | Chemical Reactor | 30 | 5 s |
| Salt recycling | 2 salt dust | 1 sodium dust + 1,000 mB chlorine | Electrolyzer | 30 | 16 s |

`Materials.SiliconSG` means Silicon Solar Grade, not SiGe. Returned salt supplies the sodium and chlorine after the player seeds the chain.

## 2. Proposed Germanium And SiGe Electronics

| Product | Inputs | Output | Machine | EU/t | Time | Environment |
| --- | --- | --- | --- | ---: | ---: | --- |
| Early germanium | 1 purified crushed sphalerite + 4 carbon dust + 250 mB sulfuric acid | 8 mB existing molten germanium | Chemical Reactor | 480 | 30 s | Any |
| Blend | 7 solar-grade silicon dust + 144 mB molten germanium | 8 SiGe blend dust | Mixer | 120 | 20 s | Any |
| Powder processing | 1 SiGe blend dust | 1 SiGe seed at 10% chance, plus 1 Poly SiGe at 90% chance, plus 1 tiny pile of Ash | EBF, 1,784 K | 480 | 60 s | Microgravity |
| Remelting | 1 Poly SiGe | 144 mB molten SiGe | Fluid Extractor | 480 | 10 s | Any |
| Seed remelting | 1 SiGe seed | 144 mB molten SiGe | Fluid Extractor | 480 | 10 s | Any |
| Crystal growth | 1 SiGe seed + 1,008 mB molten SiGe | 1 SiGe monocrystal | EBF, 1,784 K | 480 | 120 s | Microgravity |
| Seed multiplication | 1 SiGe monocrystal | 8 SiGe seeds | Forge Hammer | 120 | 10 s | Any |
| Cutting | 1 SiGe monocrystal + 100 mB water | 16 SiGe wafers | Cutting Machine | 120 | 40 s | Any |
| Wafer engraving | 1 SiGe wafer + reusable Ruby lens | 1 CLC Wafer | Laser Engraver | 480 | 45 s | Any, cleanroom proposed |
| Wafer wash | 1 CLC Wafer + 250 mB hydrochloric acid | 1 Etched CLC Wafer | Chemical Bath | 480 | 30 s | Any |
| Chip cutting | 1 Etched CLC Wafer + 100 mB water | 4 CLC Chips | Cutting Machine | 120 | 45 s | Any, cleanroom proposed |
| Packaging | 4 CLC Chips + 2 copper plates + 8 fine copper wires + 144 mB molten tin | 1 CLC Module | Assembler | 480 | 30 s | Any |

The germanium recipe has no selector circuit because sphalerite and carbon fill the single-block reactor's two item-input slots. The growth heat requirement is already represented by existing silicon-boule progression. Ruby lenses are non-consumed tools. A normal Ruby plate-to-lens Lathe route supplies the proposed lens at MV. Chip fabrication keeps the GTNH distinction between blank wafer, patterned wafer and chips. In this draft the HCl wash is a fixed finishing operation after engraving and before chip cutting, not an optional quality branch or a replacement for engraving. Its inclusion, four-chip yield, water use and cleanroom settings are proposed gameplay choices, not claims about exact semiconductor fabrication.

The owner selected independent 10% seed and 90% Poly SiGe rolls for one input dust. Expected SiGe output is one material unit per operation, excluding the abstract trace-residue byproduct. Both SiGe products occur on 9% of operations and neither occurs on 9%. This per-operation variation is intentional, not a requirement for exclusive outcomes. Growth still consumes one seed and seven molten units because 1,008 mB is seven times 144 mB. The eight-unit monocrystal can be split into eight seeds. Those growth and splitting quantities remain proposed.

The proposed residue is one existing tiny pile of Ash per powder operation, guaranteed independently of the SiGe output rolls. It reuses `Materials.Ash` with `OrePrefixes.dustTiny`, not a new Galaxia waste item. The Ash represents unspecified processing impurities, not a verified carbon-combustion reaction. Its exact quantity remains proposed. The prefix and material exist in the audited GT5 source. Existing EBF Ash outputs provide a byproduct precedent, not an existing SiGe purification recipe.

SiGe blend is an unrefined mixture. The EBF treatment removes processing impurities before the material becomes suitable for crystal-growth melt. A direct blend-to-molten SiGe recipe is excluded, including automatically generated melting recipes that would bypass this treatment. Adding Ash as an output alone would not establish that restriction. Poly SiGe and SiGe seeds are permitted remelting feedstocks because they have passed through that treatment.

A monocrystal becomes either seeds or wafers, not both. Cutting yields 16 blank SiGe wafers, 64 CLC Chips and 16 CLC Modules. Sacrificing one monocrystal supplies eight seeds for later growth operations. Those seeds may instead be remelted, giving 1,152 mB in total at the proposed 144 mB per seed. No direct blend-dust melting recipe is included. Poly SiGe supplies the liquid feedstock and cannot be cut or turned directly into seeds.

At the selected 10% seed chance, the first seed takes ten powder runs on average. These consume ten fresh blend dust and produce an average of nine Poly SiGe alongside that seed. The Poly SiGe is useful growth-feedstock inventory, not returned powder that retries nucleation. The owner accepts statistical balance across continued production.

Keep the existing IV ABS recipe unchanged: 1 purified crushed sphalerite + 4 carbon dust + 250 mB sulfuric acid, selector 15, produces 36 mB molten germanium at 4,000 EU/t for 37.5 seconds.

| Supplying 144 mB germanium | Proposed HV route | Existing IV ABS |
| --- | ---: | ---: |
| Purified sphalerite | 18 | 4 |
| Carbon dust | 72 | 16 |
| Sulfuric acid | 4,500 mB | 1,000 mB |
| Base processing time | 9 min | 2.5 min |

With the owner's 8 mB early yield, the ABS is 4.5 times better per ore and reagent and 3.6 times faster at base recipe speed. It is not claimed to save energy. No existing germanium consumer or other gate is changed by this draft.

## 3. Existing Fluoride Feedstock

Use a fictional specialty sodium-aluminium oxyfluoride glass, not ZBLAN. Exact ZBLAN would require another supply discussion, particularly early lanthanum. These existing recipes supply the proposed formulation.

| Product | Inputs | Outputs | Machine | EU/t | Time |
| --- | --- | --- | --- | ---: | ---: |
| Fluorine | 20 lepidolite dust + 4 empty cells | 2,000 mB fluorine + 1 potassium dust + 3 lithium dust + 10 aluminium oxide dust + 4 oxygen cells | Electrolyzer | 120 | 13 s |
| Hydrofluoric acid | 1 hydrogen cell + 1,000 mB fluorine, selector 1 | 1,000 mB GT5U hydrofluoric acid + empty cell | Chemical Reactor | 8 | 3 s |
| Salt water | 2 salt dust + 1,000 mB water, selector 3 | 1,000 mB salt water | Mixer | 8 | 5 s |
| Sodium hydroxide | 1,000 mB salt water + empty cell, selector 1 | 3 sodium hydroxide dust + hydrogen cell + 1,000 mB chlorine | Electrolyzer | 30 | 36 s |
| Sodium fluoride | 3 sodium hydroxide dust + 1,000 mB hydrofluoric acid, selector 15 | 2 sodium fluoride dust + 1,000 mB water | Chemical Reactor | 30 | 60 s |
| Silicon tetrafluoride | 3 silicon dioxide dust + 4,000 mB hydrofluoric acid, selector 2 | 1,000 mB silicon tetrafluoride | Chemical Reactor | 30 | 15 s |
| Aluminium fluoride | 4 aluminium dust + 3,000 mB silicon tetrafluoride, selector 1 | 16 aluminium fluoride dust + 3 silicon dust | Chemical Reactor | 30 | 30 s |

Lepidolite and salt coexist in the audited Overworld salt veins. Standard aluminium, silica and hydrogen processing supply the remaining ingredients.

## 4. Selected Fluoride Flow And Working Recipes

| Product | Inputs | Output | Machine | EU/t | Time | Environment |
| --- | --- | --- | --- | ---: | ---: | --- |
| Batch preparation | 2 sodium fluoride dust + 4 aluminium fluoride dust + 3 silicon dioxide dust | 9 fluoride-glass mix | Mixer | 120 | 15 s | Any |
| Glassmaking | 1 fluoride-glass mix | 144 mB molten fluoride glass | EBF, 1,800 K | 480 | 120 s | Microgravity |
| Blank casting | 288 mB molten fluoride glass + reusable ingot mold | 1 fluoride-glass blank | Fluid Solidifier | 120 | 20 s | Microgravity |
| Preform shaping | 1 fluoride-glass blank | 1 fluoride-glass preform + 1 fluoride-glass mix | Lathe | 480 | 20 s | Any |
| Preform softening | 1 fluoride-glass preform | 1 heated fluoride-glass preform | EBF, 1,800 K | 480 | 20 s | Microgravity |
| Fiber drawing | 1 heated fluoride-glass preform + reusable wire extrusion die | 8 fluoride optical fibers | Extruder | 480 | 30 s | Microgravity |
| Spool winding | 16 fluoride optical fibers | 1 Fluoride Fiber Spool | Assembler | 120 | 10 s | Any |

The owner selected sixteen fibers per spool. The ordinary Assembler, power and duration are proposed. Winding is packaging, not another microgravity manufacturing requirement. Communication Satellite consumes two spools and Prospecting Satellite consumes one. The proposed Functional Satellites Blueprint also uses one spool.

The flow uses six manufacturing operations plus spool packaging. Melting supplies a new molten fluoride-glass fluid, casting produces manageable cold stock, the Lathe prepares the preform, the EBF softens it and the Extruder draws fibers. The proposed 144 mB per mix unit and 288 mB per blank retain the selected two-dust blank cost. Other numerical settings remain working proposals unless explicitly selected. The Lathe returns one powder unit to the melting loop. That powder represents reclaimed glass feedstock using the same mix item as a gameplay abstraction. Operation sizes are independent. No direct molten-glass-to-fiber recipe bypasses the prepared preform route. The process adds no custom machine or fiber-quality variants.

### Why Preform Preparation And Softening Are Separate

Casting gives the blank a solid form suitable for preparation. The Lathe produces the drawing preform and returns the selected dust quantity. The later EBF operation makes that prepared stock viscous and deformable for drawing. The proposed display name Softened Preform remains unselected, so the table retains heated fluoride-glass preform. The machine sequence is a gameplay abstraction, not a claim of a complete industrial optical-preform process.

### Finished Product Name Under Review

Lumen Fiber and Lumen Spool are proposed names introduced after drawing. Lumen is a fictional product name inspired by the unit of luminous flux, not a real fluoride-glass designation or a new physical property. The existing fluoride names remain in the recipe rows until a name is selected. Earlier material, blank and preform names would stay material-based.

### Why The Thermal Operations Require Microgravity

The optical fiber is glass, not a monocrystal. SiGe growth seeks a suitable crystal, whereas fluoride-glass drawing seeks to avoid unwanted crystal formation. NASA's ZBLAN fiber report describes crystallites that scatter light and make the fiber brittle. Microgravity slows their growth and reduces sedimentation, convection and buoyancy effects during drawing and cooling.

The owner additionally selected microgravity for glassmaking, casting and preform softening. The intended lore is preserving uniform glass while molten or softened, when gravity can cause settling and deformation. This supports a larger orbital production line. The machining and spool operations can remain beside it without forcing a return to a planet.

These restrictions are gameplay choices. Terrestrial production is possible. NASA's evidence concerns real ZBLAN drawing, so applying the rationale to this fictional formulation and its additional thermal operations is not experimentally verified chemistry. Primary source: [NASA, Optical Fiber Production](https://www.nasa.gov/missions/station/iss-research/optical-fiber-production/), verified again on 2026-10-07. Earlier reviewed evidence is preserved in [[Orbital Manufacturing Research]].

Each preform yields eight fibers. With returned dust recycled, the net cost is one fresh mix unit per preform, after establishing a one-unit circulating reserve. Nine mix units from a fresh start therefore yield eight preforms, 64 fibers and one remaining mix unit. Nine further fresh mix units yield nine additional preforms, or 72 fibers, while retaining the reserve. These totals explain the recycle loop, not a requirement to scale the EBF recipe to nine blanks.

Four current Mixer batches supply 36 mix units, consuming 8 sodium fluoride dust, 16 aluminium fluoride dust and 12 silicon dioxide dust. From a fresh start they yield 35 preforms, 280 fibers and one remaining mix unit with full recycling. Existing fluoride preparation consumes 16,000 mB hydrofluoric acid, 4 aluminium dust, another 12 silicon dioxide dust and 12 sodium hydroxide dust. Sodium-hydroxide electrolysis supplies four of the sixteen hydrogen cells for that acid. Ordinary hydrogen production supplies the other twelve.

## 5. Proposed Parts And Complete Payload Recipes

Every recipe below uses the ordinary GT Assembler at 480 EU/t. Assembly is unrestricted. All outputs are one item.

| Output | Inputs | Time |
| --- | --- | ---: |
| Satellite Frame | 4 aluminium plates + 2 steel rods + 2 aluminium rings | 30 s |
| Satellite Dish | 4 aluminium plates + 4 fine copper wires + 1 MV emitter + 144 mB molten tin | 20 s |
| Primitive Telescope Satellite | 1 frame + 1 dish + 4 Glass Lenses + 1 HV circuit + 1 MV sensor + 1 rechargeable HV lithium battery + 1 ordinary GT Solar Panel + 144 mB molten tin | 45 s |
| Rocket Automation Controller | 1 CLC Module + 2 HV circuits + 1 HV sensor + 1 HV emitter + 2 aluminium plates + 4 fine copper wires + 288 mB molten tin | 45 s |

The owner selected the following distinct satellite compositions. Their shared working Assembler settings are 480 EU/t and 60 seconds.

| Ingredient | Communication Satellite | Prospecting Satellite |
| --- | ---: | ---: |
| Satellite Frame | 1 | 1 |
| Satellite Dish | 2 | 0 |
| HV Emitter | 3 | 1 |
| HV Sensor | 1 | 3 |
| Diamond Lens | 0 | 2 |
| CLC Module | 1 | 2 |
| Fluoride Fiber Spool | 2 | 1 |
| Rechargeable HV lithium battery | 1 | 1 |
| Space Grade Solar Panel | 2 | 1 |
| Molten tin | 288 mB | 288 mB |

Communication hardware emphasizes antennas and transmission. Prospecting hardware emphasizes optics and a sensor array. Both retain control electronics and internal optical signal routing. Their fiber costs are 32 and 16 respectively.

On 2026-10-08 the owner requested panels in the satellite recipes. The working allocation is one ordinary panel for Primitive Telescope, two Space Grade Solar Panels for Communication and one for Prospecting. The ordinary panel is the existing `ItemList.Cover_SolarPanel`, with its normal ground-material GTNH recipe. The existing battery remains a separate input.

The pinned GT5 HV Assembler has nine item-input slots. Primitive Telescope uses seven distinct item types after this addition. Communication and Prospecting each use eight. Tin uses the fluid input. Multiple panels of the same type form one item input, so a combined battery-and-panel ingredient is not needed for capacity. The panels are onboard hardware ingredients. These recipes do not introduce a satellite EU-output or power-simulation contract.

The dish reuses `GalaxiaItemList.SATELLITE_DISH`, registered as `parts/satellite_dish`. Current inspection found the item entry, not a production recipe. Communication and Prospecting are existing satellite kinds, not proof that these proposed payload recipes or tier definitions exist.

The opening payload uses neither orbital material. It remains the limited achievement mission, not a cheap retargetable Prospecting Satellite. The controller adds automation to the same Rocket, not first-time reusability. Manual Luna flights remain possible without it.

Space-Grade Alloy is deliberately absent from this bootstrap. Requiring a lunar material for the first pre-Luna products would add an unwanted dependency. A later alloy-based construction recipe can be considered separately.

## 6. Proposed Knowledge Recipes

These are two proposed technology groups under the accepted consumed-blueprint mechanism. Each Assembler recipe produces one Technology Blueprint at 480 EU/t for 15 seconds, without an environmental restriction.

| Blueprint | Inputs | Unlocks |
| --- | --- | --- |
| Rocket Automation | 2 CLC Modules + 1 HV circuit + 1 book + 144 mB molten tin | Rocket Automation Controller production |
| Functional Satellites | 2 CLC Modules + 1 Fluoride Fiber Spool + 1 HV circuit + 1 book + 144 mB molten tin | Communication and Prospecting Satellite production |

Successful player activation consumes the blueprint and grants team knowledge. Later production consumes components, not another blueprint. Material processing, frames, dishes and the opening payload need neither of these technologies, so their acquisition is not circular. These are not reusable Rocket assembly Blueprints.

One SiGe monocrystal supplies 16 blank wafers to allocate between CLC Modules and Solar Cells. Learning both proposed technologies and building one controller uses five CLC Modules. A Communication Satellite uses one direct CLC Module and two more inside its solar panels. A Prospecting Satellite uses two direct modules and one more inside its panel. This worked example therefore needs eleven CLC Modules and six Solar Cells, using thirteen wafers at the current yields. It leaves three blank wafers and two Solar Cells. This does not also yield seeds. A different crystal must replenish seed stock.

Starting with nine glass-mix units and recycling the returned dust supplies 64 fibers. The proposed Functional Satellites Blueprint uses one spool, a Communication Satellite uses two and a Prospecting Satellite uses one. Those three crafts consume the 64 fibers together, with one mix unit left in the recycle loop. Their three solar panels additionally need three Solar Glass Sheets, obtained from a separate blank. These totals explain material demand, not a requirement to align recipe batch sizes.

## 7. Accepted Solar Component Recipes

On 2026-10-08 the owner selected SiGe and fluoride glass as an alternative material route to cheaper solar hardware for Galaxia equipment. They explicitly rejected making the recipe output an existing GT HV solar panel because the wider modpack balance should remain unchanged.

The following working recipes were accepted for recording. Final assembly and finishing are unrestricted. Their feedstocks already carry the relevant microgravity production requirements.

| Output | Inputs | Machine | EU/t | Base time |
| --- | --- | --- | ---: | ---: |
| 4 Solar Cells | 1 SiGe Wafer + reusable Glass Lens | Laser Engraver | 480 | 45 s |
| 3 Solar Glass Sheets | 1 fluoride-glass blank + 100 mB water | Cutting Machine | 120 | 20 s |
| 1 Space Grade Solar Panel | 2 Solar Cells + 1 Solar Glass Sheet + 1 CLC Module + 4 aluminium plates + 8 fine copper wires + 288 mB molten tin | Assembler | 480 | 60 s |

Space Grade Solar Panel is a common manufactured component. Later recipes convert it into Galaxia solar generators of different tiers. It is not itself the finished HV generator or an alternate recipe for a GT solar cover. Existing GTNH solar recipes and generation parameters remain unchanged.

### Remaining Solar Decisions

- Select the first finished Galaxia generator's recipe. HV with nominal 512 EU/t is the current recommendation, not a selected conversion recipe.
- Select its operating environment. Atmosphere-free operation with actual sunlight is the current recommendation, not a settled rule. [[Define Celestial Capability Rules]] owns the accepted solar availability and modifier contract.
- Close first-factory power without requiring its own SiGe and glass products. A conventional GT fuel generator is the proposed bootstrap option. The exact initial supply is not selected.
- Revisit working panel quantities during balance review if necessary. Satellite hardware now uses an ordinary ground-made panel for Primitive Telescope and the new component for functional satellites. The primitive mission has no orbital-material prerequisite.

## Standard Reagents And Components

Copper plates and fine wires, aluminium plates and rings, steel rods, molten tin, HV circuits, sensors, emitters and lithium batteries retain normal GT recipes. A book retains its crafting recipe. No parallel Galaxia copies are proposed.

Existing ore washing supplies purified crushed sphalerite using water. Graphite electrolysis gives four carbon dust per graphite dust. Sulfur oxidation through sulfur dioxide and sulfur trioxide supplies sulfuric acid. Hydrogen plus chlorine supplies hydrochloric acid. Water electrolysis supplies hydrogen and oxygen with ordinary cell handling. These are shared upstream production lines, not new Galaxia intermediates.

## Evidence And Decision Boundary

Upstream recipes were source-audited against GT5-Unofficial `000a4d9b24d77f40a79da7a105bb79ac7efca817` and NewHorizonsCoreMod `fe1a49ae577fee5ec4c1cf53d2545b475fb6b5af`. Current checkouts differ. Galaxia content inspection used `a9128e9ef21ff05254648190b4f79f94bdc9669d`. Source presence is not a tested playable-pack result.

No build or in-game production test was performed. Microgravity and team-knowledge requirements still need actual enforcement through the shared domain capabilities. Inert metadata would not establish them. Current Rocket Module Assembler stock and assembly tasks are not the GT recipes proposed here. The Rocket automation part itself is new content.

The draft is ready for owner redlining as a whole. The recorded rounds select the seed cycle, edited germanium and powder yields, mandatory engraving, fluoride thermal flow and microgravity requirements, revised satellites and the three solar-component recipes. Remaining proposals include residue quantity, wash and chip-cutting details, cleanroom settings, other working recipe values, blueprint costs and the solar decisions listed above. Numerical tuning should not become another series of isolated tier questions. Accepted edits should replace the relevant draft rows before implementation.
