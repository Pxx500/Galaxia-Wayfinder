---
type: wayfinder-ticket
ticket_type: grilling
status: open
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Alpha Scope]]"
secondary_areas:
  - Area - Destinations
  - Area - Automation and Infrastructure
blocked_by: []
claimed_by: wayfinder
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Design Lunar Crater Processing Recipe Chain

## Question

Which complete recipes connect lunar crater extraction, Drilling Fluid supply, enriched-fluid processing and carrier recovery to bulk Space-Grade Alloy without bypassing existing material progression?

## Scope And Ownership

[[Review Crater Nodes Proposal]] owns shared deposits, extraction stages, scanner integration and the generation model. This ticket owns lunar profiles, recipes and numerical tuning. [[Define Alpha Research and Production Floor]] supplies the standard GT machinery baseline. On 2026-10-23 the owner finalized a dedicated Crater Extractor reusing suitable GT infrastructure, without replacing existing miners. Downstream work uses normal GT machines and recipe maps unless an unmet requirement justifies an exception.

New items, materials, fluids and recipes follow [[Design Early Orbital Production Recipe Chain#Accepted Content Ownership And Temporary Staging]]. The settings below are accepted working content or explicitly unapproved proposals, not implemented recipes or demonstrated whole-chain balance.

## Accepted Material And Progression Rules

### Material Integration Contract

Use the canonical material name `SpaceGradeAlloy` for standard GT form lookup, including `plateSpaceGradeAlloy`, `frameGtSpaceGradeAlloy` and `foilSpaceGradeAlloy`. These names identify one material, not separate component registrations or approval to substitute another alloy. The Computer recipe delivery consumes these forms. Material registration and generated processing remain the lunar material responsibility, staged under the existing GT-bound content convention.

Prioritize the new MaterialLib-backed GT material model rather than preserving compatibility with the old `Materials` implementation on master. The environment integration work targets GT Material Unification (`mu`, PR 8414). This is an implementation target, not a claim that its APIs are released or verified here. Material and content ownership remain with lunar industry, while the shared environment API belongs to its integration work.

Lunar industry implementation is assigned, with SGA and its usable forms as the first integration milestone for Computer hardware. The 2026-10-23 pre-delivery inventory found no material implementation in the local main checkout and eight registered worktrees. Assignment does not establish a ready integration commit. Recipes that are skipped because their required OreDictionary input is absent do not establish a craftable survival feature.

### Material And Processing Rules

- Use normal GT mineral and metal forms, without origin-only ores or provenance metadata. Retain ordinary cobalt, platinum, aluminium and titanium refining. Adding the selected resources to lunar crater profiles is accepted even where default Moon ore mixes lack them.
- Space-Grade Alloy, abbreviated SGA, is one canonical material with normal GT metal forms and a selected melt-and-cast processing route. Do not enable the unrestricted default metal-conversion recipe set. It supplies mass construction, not technology-tier gates. Different compositions produce mechanically equivalent output, not different grades.
- A lower SGA output is not automatically processing loss or recoverable slag. Recycling preserves canonical SGA quantity and cannot select a source composition or produce precious metals from the iron route.
- SGA alloying, melting, casting and material recovery require No Atmosphere, including generated recipes for those operations. There is no Microgravity requirement. Direct bender, extruder and equivalent manual shape conversions are disabled. Frames are assembled from cast parts without an automatic vacuum requirement. Finished equipment assembly likewise does not inherit the requirement merely from consuming an SGA component. Use the shared environment mechanism rather than a separate SGA-specific condition checker.
- Use full dusts wherever this lunar chain selects dust. Recipe batches are independent and may accumulate or split between operations.
- All three compositions need credible uses under different supply, infrastructure or demand conditions. Better material return alone must not make one route universally preferable after automation. No requirement forces every player to build all three.
- Existing GT Drilling Fluid is the provisional carrier. Reuse its standard manufacture. Fracking keeps fixed enriched output while shared use raises input and replacement-fluid demand.

## Accepted Lunar Profiles And Separation

Each profile has a distinct enriched Fluid ID. All four are eligible in every size class. Separation uses a Centrifuge at 120 EU/t for 40 s and returns 16000 mB spent carrier per 16000 mB enriched input.

| Profile | Solid output per separation batch | Small occurrence | Medium occurrence | Large occurrence |
| --- | --- | ---: | ---: | ---: |
| Iron-silica | 8 crushed Banded Iron, 2 crushed Quartzite | 50% | 60% | 70% |
| Gold-cobalt | 2 crushed Gold, 1 crushed Cobaltite | 20% | 20% | 18% |
| Sc-bearing bauxite | 8 crushed Bauxite, 1 Sc concentrate dust | 25% | 16% | 10% |
| Platinum-bearing | 4 crushed Platinum | 5% | 4% | 2% |

Smaller craters are more likely to contain valuable profiles, while larger ones favor bulk feedstock. These are conditional profile probabilities within a size class, not crater density or finished-metal abundance. They sum to 100% in each class. No platinum companion is added to iron-silica.

The separate 70% Small, 25% Medium and 5% Large size-class mix remains **unapproved**. Overall crater density, standard deviations and richness-response coefficients remain open. The structural generation model stays in the crater review ticket.

### Initial Reserves

A reference portion equals the solid output from one accepted 16000 mB separation batch. These nominal reserves apply at the originating size class's mean diameter.

| Profile | Small portions | Medium portions | Large portions |
| --- | ---: | ---: | ---: |
| Iron-silica | 2000 | 6000 | 16000 |
| Gold-cobalt | 1000 | 3000 | 8000 |
| Sc-bearing bauxite | 500 | 1500 | 4000 |
| Platinum-bearing | 250 | 750 | 2000 |

Apply the profile's richness response to actual diameter, then a once-only initial-reserve multiplier of approximately 0.9 to 1.1. The result belongs to the shared crater. Binding, replacement, scanning and reload do not reroll it. Variation affects finite reserve only, not composition, operation output or fracking slope. At mean diameter, Small iron has 1800 to 2200 portions and Small platinum has 225 to 275.

### Linear Fracking Growth

The accepted working loop starts at 16000 mB Drilling Fluid per reference portion, with 16000 mB enriched output and 16000 mB usable carrier recovered. Startup still requires full circulating inventory. Subsequent input grows linearly with the crater's cumulative fracking portions. Extra input is lost underground, not converted to additional minerals.

| Profile | Preceding fracking portions at 32000 mB input | Input after 1000 preceding portions |
| --- | ---: | ---: |
| Iron-silica | 8000 | 18000 mB |
| Gold-cobalt | 4000 | 20000 mB |
| Sc-bearing bauxite | 2000 | 24000 mB |
| Platinum-bearing | 1000 | 32000 mB |

These costs apply to the next reference portion, not the cumulative average. Growth has no cutoff or reset. Finite mining does not advance fracking history. Multiple extractors share one history rather than independent cheap starts. Only successfully completed fracking advances the cost history. Failed work loses consumed inputs without increasing future cost, under [[Review Crater Nodes Proposal]]. At the doubling point, each portion needs 16000 mB replacement carrier. Accepted carrier-cleanup settings are recorded below.

## Accepted SGA Manufacturing

All three recipes use an EBF at 480 EU/t, require No Atmosphere and have no Microgravity requirement. They output molten SGA, superseding the earlier direct-ingot outputs. Finished metal inputs preserve ordinary refining and Sc metal finishing.

| Route | Inputs | Output | Base time | Heat | Target coil tier |
| --- | --- | --- | ---: | ---: | --- |
| Fe-Si | 10 Iron ingots, 1 full Silicon dust | 288 mB molten SGA | 40 s | 3600 K | Nichrome |
| Au-Co | 5 Gold ingots, 2 Cobalt ingots | 576 mB molten SGA | 80 s | 4500 K | TP Alloy |
| Al-Sc | 10 Aluminium ingots, 1 Scandium ingot | 1584 mB molten SGA | 220 s | 5400 K | HSS-G |

Use normal GT heat checks, including voltage bonuses, rather than a strict coil-material restriction. The starting infrastructure target is HV. Heat settings do not independently select a material melting point or hot-ingot stage. Material registration and generated processing must remain coherent with the final properties.

Each route uses 20 base seconds and 192000 EU per 144 mB SGA ingot-equivalent before overclocking and heat discounts, excluding subsequent casting. Fe-Si trades common supply for high material demand. Au-Co lowers input volume without a Sc refinery but competes with other precious-metal uses. Al-Sc has the best material-equivalence ratio and pays for aluminium refining, Sc chemistry and metal finishing. Supply, transport, competing demand and machine capacity must establish their situational value.

### Accepted Melt-And-Cast Forming

Cast plates and rods from molten SGA using the appropriate forms. Ingots may be cast for storage, but later shape changes return through melting and casting. Disable direct bender/extruder conversions and their manual equivalents so they cannot bypass this route. Both melting and casting require No Atmosphere.

Produce foil in the existing Fluid Solidifier: 144 mB molten SGA with a new non-consumed thin-strip mold yields four SGA foils under No Atmosphere. This is a gameplay abstraction inspired by melt spinning, not a new dedicated machine. The mold's crafting cost and the new casting recipes' times and EU/t remain unspecified.

Frames remain assembly of cast rods and plates, not casting of an entire frame or a requirement to remelt parts merely to join them. Frame assembly and final equipment assembly do not automatically require No Atmosphere. The owner accepted this forming direction on 2026-10-23 in the environment-integration discussion.

Optional residue processing may recover real impurities or byproducts. It must define their contents and costs, preserve No Atmosphere for SGA recovery, and avoid repeatedly processing the same residue. No residue identity, recovery ratio or automatic recovery of the input/output deficit is selected.

## Accepted Sc Supply And Processing Direction

New primary Galaxia Sc acquisition is crater-exclusive, starting with lunar Sc-bearing bauxite profiles. This is not a new ore identity. Sc is separated from enriched extraction fluid before ordinary Bauxite follows its unchanged refining line. Ordinary Bauxite Slag, general overworld refining and non-crater ore generation are not additional primary Sc sources. No lunar-origin tags are needed.

The existing late Blood Magic Chinfinity meteor source remains unchanged. It contains weighted endstone Scandium ore, consumes a ZPM Circuit Assembler focus and costs 80000000 life essence. Its gate does not set the new Galaxia supply gate. The checked Monazite/Bastnasite recipe owner supplies Samarium rather than a named Sc output. The bounded GT/CoreMod consumer audit did not find an authored progression-critical Sc ingredient. Neither finding proves all-mod absence.

### Finite Dry And Wet Mining

All four profiles support wet ordinary mining from the beginning and direct solid output without fluid. Dry mining yields the profile's accepted solid batch, such as 8 crushed Bauxite and 1 Sc concentrate dust, bypassing separation and carrier cleanup. Both modes consume the shared finite reserve. Dry mining has a 25% chance to consume twice the normal reserve portion and a 75% chance to consume the normal portion, with unchanged output. Its expected reserve cost is 1.25 portions. The penalty affects reserve only, not energy or duration.

Wet mining is more resource-efficient, not necessarily cheaper in every energy or infrastructure comparison. It cannot start fracking before exhaustion. Once the finite reserve is exhausted, only fluid-dependent fracking continues. Both finite mining modes use the same accepted 5 s base cycle.

### Accepted Chemistry Skeleton

| Stage | Inputs | Outputs |
| --- | --- | --- |
| Mineral separation | Enriched Sc-bearing bauxite fluid | Ordinary Bauxite, Sc concentrate, spent carrier |
| Leaching | Sc concentrate, Diluted Nitric Acid | Sc solution, mineral residue |
| Precipitation | Sc solution, Sodium Hydroxide | Scandium Oxide, spent solution |
| Calcium reduction | Scandium Oxide, Calcium | Normal Scandium dust, Quicklime |

Use one canonical Scandium Oxide. Oxide electrolysis is also a recovery option, including oxide from precipitation. Calcium reduction is an alternative, not an artificially mandatory final step. Metal ingot production remains separate. No blanket environmental prohibition is selected for every Sc chemical stage.

Defined compounds follow [GTNH Chemical Balance](https://wiki.gtnewhorizons.com/wiki/Chemical_Balance), including its different solid, fluid and compound rules. Undefined extraction mixtures have tunable concentrations, not invented formula-derived coefficients. Chemistry, carrier recovery and upstream reagent supply need separate accounting.

### Accepted Initial Sc Refinery Balance

On 2026-10-23 the owner accepted the presented input/output quantities, machines, EU/t and durations as initial balance, subject to later adjustment. The 12 s reduction and five-Quicklime output were already selected. The shorter duration favors the Calcium route over direct electrolysis, while the reduced Quicklime output creates continuing Calcium makeup. The reduction heat remains a technical tuning proposal distinct from the already selected 3650 K metal-finishing requirement.

| Operation | Inputs | Outputs | Machine | Base EU/t | Base time |
| --- | --- | --- | --- | ---: | ---: |
| Leaching | 12 Sc concentrate dust, 6000 mB Nitric Acid, 3000 mB Water | 9000 mB Sc solution, 10 Stone dust | LCR | 480 | 60 s |
| Precipitation | 9000 mB Sc solution, 18 Sodium Hydroxide dust | 5 Scandium Oxide dust, 9000 mB spent leach solution | Chemical Reactor | 120 | 30 s |
| Calcium reduction | 5 Scandium Oxide dust, 3 Calcium dust | 2 Scandium dust, 5 Quicklime dust | EBF, proposed 1814 K | 120 | 12 s |
| Direct electrolysis | 5 Scandium Oxide dust | 2 Scandium dust, 3000 mB Oxygen | Electrolyzer | 120 | 80 s |

Twelve separation batches supply two Sc dust alongside 96 crushed Bauxite from 192000 mB enriched fluid under the accepted initial quantities. This is a dilute coproduct yield, not a chemical formula or a proof of economic balance.

Existing Quicklime electrolysis remains unchanged. Two EBF batches consume six Calcium dust and produce ten Quicklime dust. Five existing 30 EU/t, 56-tick recycling operations return five Calcium dust, leaving one full Calcium dust of makeup demand per two EBF batches. Calcium recovery is therefore approximately 83.3%, not a closed startup-only loop. The lower Quicklime yield is deliberate unrecovered processing loss, not loss of Sc or a new residue item.

At the current recipe settings, those two EBF batches and Quicklime recycling use 66000 EU for four Sc dust before overclocking, excluding fresh Calcium production. Direct oxide electrolysis would use 384000 EU for the same Sc output. These figures compare only metal recovery and do not establish the full supply-chain energy advantage. Buffer whole dust batches rather than introducing fractional or small dust recipes.

The direct electrolysis cost is authored. It must not coexist with a cheaper accidental generated duplicate. Default source-derived generation would predict 30 EU/t for 6.5 s. Implementation must reconcile material generation with the accepted authored recipe. Fluid hatch capacities and actual throughput also need verification.

### Accepted Reagent Recovery

Recover approximately 90% of Nitric Acid and NaOH as initial working tuning. Lunar SaltWater is an accepted supply input for NaOH. Preserve existing pure-material reactions. Recovery loss belongs to separation of the undefined contaminated solution, not reduced outputs in existing chemistry.

| Status | Inputs | Outputs | Machine | Base EU/t | Base time |
| --- | --- | --- | --- | ---: | ---: |
| Accepted new recipe | 9000 mB spent Sc leach solution | 27 existing BartWorks Sodium Nitrate dust, 6000 mB Water | Distillery | 120 | 90 s |
| Existing acid exchange | 10 Sodium Nitrate dust, 1000 mB Sulfuric Acid, selector 1 | 2000 mB Nitric Acid, 7 Sodium Sulfate dust | Chemical Reactor or LCR | 480 | 10 s |
| Existing sulfate recovery | 7 Sodium Sulfate dust, 2 Hydrogen cells | 2 Sodium dust, 1000 mB Sulfuric Acid, 2 empty cells | Chemical Reactor or LCR | 30 | 1.5 s |
| Existing NaOH recovery | 1 Sodium dust, 1000 mB Water, selector 1 | 3 Sodium Hydroxide dust, 1000 mB Hydrogen | Chemical Reactor or LCR | 30 | 10 s |

Use the existing BartWorks nitrate and sulfate identities. Sulfuric Acid and Hydrogen circulate as startup inventories. Sulfate recovery consumes filled cells and returns empties. Sodium hydration returns gas, so ordinary filling or LCR cell conversion must handle it.

With the accepted initial refinery batches, ten batches yield twenty Sc dust and consume 60000 mB acid plus 180 NaOH dust before recovery. The loop returns 54000 mB acid and 162 NaOH dust, leaving 6000 mB acid and 18 full NaOH dust as replacement demand. Buffer whole reaction batches rather than using fractional dust. The three missing nitrate-dust equivalents per refinery batch are discarded contamination, not a repeatedly recoverable output.

Fresh acid still needs a supply route. An existing LCR recipe uses 3000 mB Hydrogen, 1000 mB Nitrogen and 4000 mB Oxygen for 1000 mB Nitric Acid and 1000 mB Water at 480 EU/t for 16 s. The ammonia-input acid recipe is 30 EU/t for 16 s before feedstock costs. Neither establishes local lunar Nitrogen or an unconditional energy advantage. Gas acquisition, transport and recovery capacity remain costs to verify.

## Accepted Recipe Family Model

Environmental alternatives belong to a first-class Recipe Family with common production inputs, one logical input registration and local variant selection. Reuse GT ingredient indexing and recipe ownership. Do not expand the family into independently colliding same-input recipes or rely on collision suppression and optional deduplication to admit them.

Select the complete immutable effective recipe before output protection and input consumption. A display may show alternatives without separate production registrations. Lock the family, not the current environmental variant. Each new operation selects from current conditions, while committed operations retain their selected outcome. Ambiguous eligible variants remain an open selection constraint. Collision, deduplication, cache and lock handling must preserve the family contract.

GT-only development omits Galaxia-dependent environmental variants from registration and recipe display. A family with no remaining variants is omitted too. No substitute outcome or synthetic environment is selected. This registration rule does not apply to unresolved environmental data while Galaxia is present. The intended integrated gameplay includes Galaxia, while GT must still launch conveniently without it for development.

### Accepted Initial Sc EBF Variants

The accepted initial batch uses four full Scandium dust as the common input and a 40 s duration. Both variants require the previously selected EV base power of 1920 EU/t and 3650 K heat. Nichrome provides 3601 K base heat and reaches 3701 K with the normal HV-input temperature bonus, so the intended combination is EV recipe power with Nichrome coils, not a requirement for TP Alloy coils. Multiple lower-tier energy hatches may supply the required power. Heat and electrical power remain independent checks. This applies to dust-to-hot-ingot processing, not the separate oxide-to-dust reduction at 120 EU/t for 12 s. It does not change Scandium's material melting point or establish implemented recipes.

| Environment | Common input | Accepted initial outputs |
| --- | --- | --- |
| No Atmosphere | 4 Scandium dust | 4 hot Scandium ingots |
| Atmosphere | 4 Scandium dust | 2 hot Scandium ingots, 5 Scandium Oxide dust |

Five full oxide dust contain two Sc units under the GT material convention, so both variants preserve four Sc units. Oxidation in atmosphere is an environmental gameplay abstraction, not a fully specified reaction with every ambient gas composition. Oxide returns through either recovery option and does not preserve its origin. Normal Vacuum Freezer cooling remains a separate existing operation. No tiny or small dusts are needed.

This family replaces the corresponding ordinary Sc dust-to-hot-ingot EBF entry, rather than coexisting as colliding same-input recipes. It does not change the preceding oxide-to-dust reduction or the SGA No Atmosphere requirement. Oxide may also supply future selected optical or ceramic consumers. The owner accepted the batch, output split and time as initial balance on 2026-10-23.

## Initial Sc Components And Wider Demand

RF Resonator for communication hardware and Laser Crystal for prospecting or optical hardware are retained component-design directions. Their compositions, benefits, recipes and availability remain open. Their proposed advanced or modular satellite consumers are deferred, not Alpha requirements. The opening progression must not acquire an implicit Sc requirement.

### Satellite Consumer Direction

The owner retained both component concepts but did not accept the proposed pair of fixed EV satellite upgrades with doubled output. [[Define Modular Satellite Construction]] preserves the deferred component-based construction direction. Current Alpha scope is one basic Communication Satellite type and one basic Prospecting Satellite type. Do not use the former upgrade recipes, their multipliers or modular construction as accepted lunar-chain prerequisites.

Metallic Sc and nitrogen-bearing thin-film manufacture provide the RF branch's inspiration. The optical branch should start from Scandium Oxide rather than reducing and then reoxidizing it. Exact feedstocks and component recipes remain open. A research laser host's rare-earth ingredients must not silently impose an unverified later progression gate.

Additional meaningful Sc uses, including non-Galaxia equipment, are wanted. Current unapproved candidates include reusing these RF and optical parts, oxide ceramics for selected high-temperature or electrochemical hardware, and Al-Sc structural hardware with a concrete benefit. Each needs an actual consumer and demand comparison. Installed components do not need arbitrary continuous Sc consumption. Broader use is not approval to replace unrelated GT progression gates.

RF targets, oxide ceramics, laser hosts and lightweight structural alloys provide scientific inspiration, not selected recipes. Metallic Sc reactivity may inform hot-metal handling or deposition. It does not justify restricting stable oxides, aqueous chemistry or installed equipment. Inert protection and vacuum are not physically identical.

## Working Extractor And Carrier Cleanup Settings

Dry/wet behavior applies to all four profiles. Both finite mining modes, fracking and carrier cleanup have accepted working costs and times. These are base settings before overclocking, not verified running-machine performance.

| Operation | Inputs | Outputs | Machine | Base EU/t | Base time |
| --- | --- | --- | --- | ---: | ---: |
| Dry ordinary mining | One reference portion, with dry loss rule | Profile's accepted solid batch | Crater Extractor | 480 | 5 s |
| Wet ordinary mining | One reference portion, 16000 mB Drilling Fluid | 16000 mB profile-specific enriched fluid | Crater Extractor | 480 | 5 s |
| Fracking after exhaustion | Current profile-dependent Drilling Fluid input | 16000 mB profile-specific enriched fluid | Crater Extractor | 480 | 10 s |
| Carrier cleanup | 4000 mB spent carrier | 4000 mB Drilling Fluid | Centrifuge | 120 | 8 s |
| Controller manufacture | 1 HV hull, 2 HV motors, 1 HV pump, 2 HV pistons, 2 HV circuits, 4 steel plates, 144 mB molten tin | 1 Crater Extractor Controller | Assembler | 480 | 45 s |

The controller recipe remains the working baseline and needs no lunar SGA. The dedicated Crater Extractor identity is now selected after comparing existing miner hosts. Reuse appropriate GT support without inheriting incompatible physical-ore or underground-fluid behavior. Geometry and integration remain open. Powerfail and finite-reserve completion accounting follow [[Review Crater Nodes Proposal]].

Cleanup runs four times per separator batch. This is distinct from mineral separation, which remains 16000 mB at 120 EU/t for 40 s. The faster extractor settings do not imply one downstream machine keeps pace.

Existing carrier manufacture is 5 water cells, 1 Stone dust and 20 mB Lubricant for 5000 mB Drilling Fluid plus five empty cells in a Mixer at 15 EU/t for 3.2 s. Startup needs full committed input and pipeline inventory, not only net makeup. Cleanup does not need an invented Stone coproduct.

## Accepted Construction Material Policy

Automated Stations and Automated Outposts are both built primarily from bulk SGA, with smaller amounts of specialist electronics and components. The owner accepted this on 2026-10-23. Exact bills of materials and quantities may differ by Facility type. Functional modules retain their separate function-appropriate costs. This does not require SGA in the first physical Station kit or turn SGA into a replacement for tiered vehicle materials.

SGA, Sc and fluoride products are reusable intermediates for Galaxia's expanding equipment catalogue. Additional applications may arrive with later vehicles, machinery and infrastructure. Do not invent immediate consumers for every intermediate as a prerequisite for the first complete progression path. Tiered androids, tiered Stations and megastructures are future possibilities, not new Alpha commitments.

Later bulk construction must preserve the first Station's non-SGA bootstrap and expansion route.

### Proposed Construction Recipes, Unapproved

| Recipe | Machine | EU/t | Base time | Environment |
| --- | --- | ---: | ---: | --- |
| 8 SGA plates + 4 Steel rods -> 4 Space Station Blocks | Assembler | 120 | 10 s | Any |
| 4 SGA plates + 2 Steel rods -> 8 Space Station Panels | Assembler | 120 | 10 s | Any |

The blocks and panels already have registry entries, not demonstrated recipes. These are alternative bulk recipes, not mandatory replacements. Compare their prices with actual construction demand and existing recipes.

## Existing Processing And Evidence

Retain ordinary mineral-to-metal paths. Banded Iron can smelt to Iron. Cobaltite roasting and reduction use MV, 1200 K EBF recipes. Platinum processing produces Metallic Powder and supports both efficient chemistry and an existing low-return option: 3 Platinum Metallic Powder dust -> 2 Platinum nuggets at MV, 2041 K for 30 s. [Platinum recipes](https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/bartworks/system/material/gtenhancement/PlatinumSludgeRecipes.java#L299-L393)

Existing aluminium reductions are 10 Alumina dust + 3 Carbon dust -> 4 Aluminium ingots + 3000 mB CO2 at 120 EU/t, 60 s, 2054 K, or 10 Alumina dust + 5 Cryolite dust -> 4 ingots at 120 EU/t, 80 s, 963 K. [CoreMod recipes](https://github.com/GTNewHorizons/NewHorizonsCoreMod/blob/9aa0afc8711f3efbe3afc0d11ec44dcbf5b87442/src/main/java/com/dreammaster/gthandler/recipes/BlastFurnaceRecipes.java#L438-L468)

Source-derived Sc metal processing uses an EBF at 120 EU/t, 1814 K for 90.7 s, then Vacuum Freezer cooling. [Meteor source](https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/83b3fb26cd9979e0256c7568bdf8c6f87579b532/config/BloodMagic/meteors/Chinfinity.json#L34-L39), [focus identity](https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/api/enums/MetaTileEntityIDs.java#L703), [carrier manufacture](https://github.com/GTNewHorizons/GT5-Unofficial/blob/2259bc64244f9f7fc58e039d8e89ca40dd17c929/src/main/java/gregtech/loaders/postload/recipes/MixerRecipes.java#L641-L649)

The [original nitric-acid research](https://pmc.ncbi.nlm.nih.gov/articles/PMC8779884/) concerns specially prepared red mud. It does not prove the game yields or concentrated lunar deposits. Commercial [Al-Sc specifications](https://nikon-slm-solutions.com/wp-content/uploads/2024/07/mds5143.pdf), [RF targets](https://www.materion.com/en/insights/blog/materions-aluminum-scandium-sputtering-targets-power-rf-mobile-and-broadband-devices), [oxide ceramics](https://infinitamaterials.com/material/scandia-stabilized-zirconia-alumina/), [laser-host research](https://link.springer.com/article/10.1007/s00340-013-5433-2) and [Sc properties](https://periodic-table.rsc.org/element/21/Scandium) ground candidate functions, not mandatory Alpha content. Detailed research remains intake under [[Sources]]. Source checks are not a running-pack production test.

## Remaining Decisions

### Proposed Economy And Consumer Package, Awaiting Approval

Balance the complete extraction site around a choice between maintaining an established crater with rising fluid demand and investing in another site. Dry startup, wet reserve conservation and indefinite fracking already supply the mechanics. Extra extractors increase throughput while sharing depletion and cost history.

Give the SGA routes different supply advantages: Fe-Si for common feedstock and lower initial heat requirements, Au-Co where those inputs are available without a Sc refinery, and Al-Sc for material-efficient production supported by chemical infrastructure. These are target economic roles, not demonstrated balance. In particular, the middle route needs a concrete situation in which its total supply cost is competitive.

Use SGA as an economical bulk option for Station expansion and Automated Facility construction while preserving the non-SGA bootstrap. Assess Sc demand beyond SGA through two concrete candidates: an alternative emitter/sensor manufacturing route using RF components, and oxide ceramics in Data Processor computing sections. Neither candidate is an accepted recipe or a replacement for existing GT progression gates. Compare actual consumers before committing new intermediates. Laser Crystal remains a future direction until it has a selected consumer.

The RF and processor-ceramic suggestions remain optional candidates, not prerequisites for closing the first complete progression path. Broader material demand may grow with later equipment. Evaluate actual consumers when tuning that economy. Installed parts do not gain arbitrary ongoing Sc consumption.

- Implement the selected dedicated extractor using appropriate GT support and the updated powerfail/finite-reserve contract
- Select size-class mix, spatial density, diameter deviations and richness-response tuning
- Validate the accepted initial Sc refinery and oxide recovery balance against actual registrations, capacities and throughput
- Assess wider Sc demand through concrete consumers without making deferred modular satellites a prerequisite for this chain
- Select construction recipes and demonstrate situational roles for all three SGA compositions
- Verify complete reagent availability, capacities, throughput and energy against actual recipes and the provisional transported-battery power route
- Resolve ambiguous environmental family variants and verify coherent collision, deduplication and operation-state handling

Sustained non-combustion generation remains a separate open power question. Existing HV lithium batteries have a nominal 1.6 million EU capacity, not an accepted factory battery count. No content or generator work starts merely because this design ticket records it.
