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


# Lunar Crater Industry

Crater mining supplies ordinary minerals and Sc concentrate for lunar refining and bulk Space-Grade Alloy production. Recipe quantities below are accepted initial balance unless marked as proposals.

## Extraction

A dedicated Crater Extractor supports dry mining, wet mining and fracking. Downstream processing uses ordinary GT machines and recipe maps. [[Review Crater Nodes Proposal]] owns deposit identity, generation, shared reserves and scanner behavior.

- **Dry mining:** yields the profile's solid batch directly. Each successful operation has a 25% chance to consume two reserve portions instead of one, without extra output. Expected reserve cost: 1.25 portions.
- **Wet mining:** consumes one reserve portion and Drilling Fluid, producing enriched fluid for separation. Available from the beginning.
- **Fracking:** available only after finite reserves are exhausted. Continues indefinitely, with fixed output and increasing fluid consumption.
- Multiple extractors share the crater's reserve and fracking history.
- Only successful operations consume reserve or advance fracking history. Powerfail resets the operation and loses committed inputs, following [[Define Alpha Research and Production Floor#Native GT Machine Failure Semantics]].
- Dry mining's penalty affects reserve, not time or EU. Wet mining conserves the deposit but requires more processing infrastructure.

Existing GT Drilling Fluid is the provisional carrier. It is not a new fluid or manufacturing chain.

| Operation | Inputs | Outputs | Machine | Base EU/t | Base time |
| --- | --- | --- | --- | ---: | ---: |
| Dry ordinary mining | One reference portion, with dry loss rule | Profile's accepted solid batch | Crater Extractor | 480 | 5 s |
| Wet ordinary mining | One reference portion, 16000 mB Drilling Fluid | 16000 mB profile-specific enriched fluid | Crater Extractor | 480 | 5 s |
| Fracking after exhaustion | Current profile-dependent Drilling Fluid input | 16000 mB profile-specific enriched fluid | Crater Extractor | 480 | 10 s |
| Carrier cleanup | 4000 mB spent carrier | 4000 mB Drilling Fluid | Centrifuge | 120 | 8 s |
| Controller manufacture | 1 HV hull, 2 HV motors, 1 HV pump, 2 HV pistons, 2 HV circuits, 4 steel plates, 144 mB molten tin | 1 Crater Extractor Controller | Assembler | 480 | 45 s |

The controller recipe is the working baseline and requires no lunar SGA. Extractor geometry remains open. The dedicated machine reuses appropriate GT infrastructure without replacing existing miners.

Existing carrier manufacture: 5 Water cells, 1 Stone dust and 20 mB Lubricant → 5000 mB Drilling Fluid and 5 empty cells, Mixer, 15 EU/t, 3.2 s. Startup needs the full input and circulating inventory, not just replacement fluid.

## Crater Profiles

Each profile has a separate enriched Fluid ID. Separation consumes 16000 mB enriched fluid and returns the following solids plus 16000 mB spent carrier in a Centrifuge at 120 EU/t for 40 s.

| Profile | Solid output per separation batch | Small occurrence | Medium occurrence | Large occurrence |
| --- | --- | ---: | ---: | ---: |
| Iron-silica | 8 crushed Banded Iron, 2 crushed Quartzite | 50% | 60% | 70% |
| Gold-cobalt | 2 crushed Gold, 1 crushed Cobaltite | 20% | 20% | 18% |
| Sc-bearing bauxite | 8 crushed Bauxite, 1 Sc concentrate dust | 25% | 16% | 10% |
| Platinum-bearing | 4 crushed Platinum | 5% | 4% | 2% |

All profiles can occur in every size class. Small craters favor valuable materials, while large craters favor bulk feedstock. The percentages describe profile selection within a size class, not overall crater density. Iron-silica contains no platinum coproduct.

Carrier cleanup runs four times per separation batch. Extractor, separator and cleanup rates differ, so one machine at each stage does not necessarily keep pace.

### Finite Reserves

One reference portion equals one separation batch's solid output. Nominal reserves apply at the size class's mean diameter.

| Profile | Small portions | Medium portions | Large portions |
| --- | ---: | ---: | ---: |
| Iron-silica | 2000 | 6000 | 16000 |
| Gold-cobalt | 1000 | 3000 | 8000 |
| Sc-bearing bauxite | 500 | 1500 | 4000 |
| Platinum-bearing | 250 | 750 | 2000 |

Apply the profile's richness response to actual diameter, then a once-only reserve multiplier of approximately 0.9–1.1. At mean diameter, Small iron therefore holds 1800–2200 portions and Small platinum 225–275.

This variation affects finite reserve only. Composition, operation output and fracking slope stay unchanged. Scanning, replacing an extractor, binding and reloading do not reroll the shared reserve.

### Fracking Costs

The first portion consumes 16000 mB Drilling Fluid, yields 16000 mB enriched fluid and ultimately recovers 16000 mB usable carrier. Further input increases linearly with completed fracking portions. Extra fluid is lost underground rather than producing more minerals.

| Profile | Preceding fracking portions at 32000 mB input | Input after 1000 preceding portions |
| --- | ---: | ---: |
| Iron-silica | 8000 | 18000 mB |
| Gold-cobalt | 4000 | 20000 mB |
| Sc-bearing bauxite | 2000 | 24000 mB |
| Platinum-bearing | 1000 | 32000 mB |

These are costs for the next portion, not cumulative averages. Growth has no cutoff or reset. Finite mining does not advance it. At the doubling point, each portion needs 16000 mB replacement carrier after recovery.

**Unapproved generation tuning:** 70% Small, 25% Medium and 5% Large. Overall density, diameter deviations and richness-response coefficients also remain open.

### Proposed Stone Recovery

Treat spent carrier as Drilling Fluid with excess stone: centrifuging would return the full fluid volume and Stone Dust. This is a proposed addition to the carrier-cleanup recipe, not yet a selected solid yield. Use a name based on "spent", not "contaminated".

Finite wet extraction should retain the closed carrier loop. Increasing replacement demand begins with fracking. The stone-output quantity used in an implementation experiment is not approved balance.

Source: lunar extraction feedback, 2026-10-28. The accepted cleanup table above remains unchanged pending selection of the coproduct.

## Scandium Refinery

New primary Sc supply comes exclusively from crater profiles, initially lunar Sc-bearing bauxite. There is no separate bauxite ore item or origin tag. Ordinary Bauxite follows its existing refining chain, while the concentrate enters the Sc refinery.

Ordinary Bauxite Slag, general Overworld refining and non-crater ores are not additional primary sources. The existing late Blood Magic Chinfinity meteor remains unchanged and does not determine this chain's progression gate.

### Chemical Processing

| Operation | Inputs | Outputs | Machine | Base EU/t | Base time |
| --- | --- | --- | --- | ---: | ---: |
| Leaching | 12 Sc concentrate dust, 6000 mB Nitric Acid, 3000 mB Water | 9000 mB Sc solution, 10 Stone dust | LCR | 480 | 60 s |
| Precipitation | 9000 mB Sc solution, 18 Sodium Hydroxide dust | 5 Scandium Oxide dust, 9000 mB spent leach solution | Chemical Reactor | 120 | 30 s |
| Calcium reduction | 5 Scandium Oxide dust, 3 Calcium dust | 2 Scandium dust, 5 Quicklime dust | EBF, proposed 1814 K | 120 | 12 s |
| Direct electrolysis | 5 Scandium Oxide dust | 2 Scandium dust, 3000 mB Oxygen | Electrolyzer | 120 | 80 s |

Use full dusts throughout. Batches may accumulate between machines rather than matching each preceding output exactly. Defined compounds follow [GTNH Chemical Balance](https://wiki.gtnewhorizons.com/wiki/Chemical_Balance). Undefined extraction mixtures have tunable concentrations.

- One canonical Scandium Oxide serves precipitation, metal recovery and atmospheric finishing returns.
- Calcium reduction and direct electrolysis are alternatives. Reduction is faster but needs Calcium replacement.
- The reduction's **1814 K is proposed tuning**. It is separate from the accepted 3650 K metal-finishing requirement.
- No blanket No Atmosphere requirement applies to aqueous chemistry or oxide recovery.
- Twelve separation batches yield 96 crushed Bauxite and enough concentrate for two Sc dust from 192000 mB enriched fluid.
- The authored electrolysis recipe replaces any cheaper generated duplicate rather than coexisting with it.

Existing Quicklime electrolysis is unchanged. Two reduction batches consume six Calcium dust and return ten Quicklime dust. Five recycling operations at 30 EU/t for 56 ticks recover five Calcium dust. One full Calcium dust must be replaced per four Sc dust, giving approximately 83.3% Calcium recovery.

Those two reduction batches plus recycling consume 66000 EU, excluding fresh Calcium production. Direct electrolysis consumes 384000 EU for the same Sc output. This comparison does not include the rest of the refinery or prove a full-chain energy advantage.

### Acid And Alkali Recovery

Recover approximately 90% of Nitric Acid and NaOH. Lunar SaltWater supplies fresh NaOH feedstock. Loss occurs when separating contaminated spent solution, not by changing existing pure-material reactions.

| Status | Inputs | Outputs | Machine | Base EU/t | Base time |
| --- | --- | --- | --- | ---: | ---: |
| Accepted new recipe | 9000 mB spent Sc leach solution | 27 existing BartWorks Sodium Nitrate dust, 6000 mB Water | Distillery | 120 | 90 s |
| Existing acid exchange | 10 Sodium Nitrate dust, 1000 mB Sulfuric Acid, selector 1 | 2000 mB Nitric Acid, 7 Sodium Sulfate dust | Chemical Reactor or LCR | 480 | 10 s |
| Existing sulfate recovery | 7 Sodium Sulfate dust, 2 Hydrogen cells | 2 Sodium dust, 1000 mB Sulfuric Acid, 2 empty cells | Chemical Reactor or LCR | 30 | 1.5 s |
| Existing NaOH recovery | 1 Sodium dust, 1000 mB Water, selector 1 | 3 Sodium Hydroxide dust, 1000 mB Hydrogen | Chemical Reactor or LCR | 30 | 10 s |

Use the existing BartWorks nitrate and sulfate identities. Sulfuric Acid and Hydrogen circulate, requiring startup inventory. Sulfate recovery uses filled cells and returns empties, while Sodium hydration produces gas. Standard filling or LCR cell conversion handles the difference.

Across ten refinery batches:

| Material | Initial demand | Recovered | Replacement |
| --- | ---: | ---: | ---: |
| Nitric Acid | 60000 mB | 54000 mB | 6000 mB |
| Sodium Hydroxide | 180 dust | 162 dust | 18 dust |

The three missing nitrate-dust equivalents per refinery batch are discarded contamination, not another recoverable output. Buffer whole reaction batches.

Fresh acid still needs a supply route. Existing options include an LCR recipe using 3000 mB Hydrogen, 1000 mB Nitrogen and 4000 mB Oxygen for 1000 mB Nitric Acid and 1000 mB Water at 480 EU/t for 16 s, or the ammonia-input route at 30 EU/t for 16 s before feedstock costs. Local lunar Nitrogen availability is not established. Gas transport and reagent production remain part of the cost.

### Metal Finishing

One EBF recipe family consumes four Sc dust at **1920 EU/t, 3650 K and 40 s**. Output depends on the environment.

| Environment | Common input | Accepted initial outputs |
| --- | --- | --- |
| No Atmosphere | 4 Scandium dust | 4 hot Scandium ingots |
| Atmosphere | 4 Scandium dust | 2 hot Scandium ingots, 5 Scandium Oxide dust |

Both variants preserve four Sc units. Oxide returns through either recovery route without retaining its origin. Hot ingots require ordinary Vacuum Freezer cooling.

Heat and power are independent checks. The intended setup uses Nichrome coils and EV recipe power, potentially supplied by multiple lower-tier energy hatches. Nichrome's 3601 K base reaches 3701 K with the ordinary HV-input temperature bonus. This is not a TP Alloy requirement or a change to Scandium's material melting point.

Atmospheric oxidation is a gameplay abstraction, not a simulation of each gas composition.

### Recipe Family Contract

- Register common production inputs once, then select an environmental variant locally using GT's ingredient indexing.
- Select the complete effective recipe before output protection and input consumption.
- Recipe locking selects the family. Each new operation checks current conditions, while a committed operation retains its selected outcome.
- Replace the ordinary Sc dust-to-hot-ingot entry. Do not create independently colliding same-input recipes or depend on collision suppression.
- Recipe display may show the alternatives without separate production registrations.
- In GT-only development, omit Galaxia-dependent variants from registration and display. Omit an empty family. This does not define behavior for unresolved environment data when Galaxia is installed.
- Selection between multiple eligible variants remains open.

## Space-Grade Alloy

SGA is a single bulk construction material. Different compositions produce the same material, not separate grades. Lower-yield compositions require more input to provide equivalent mechanical properties. The difference is not automatically recoverable slag.

Ordinary GT metal and mineral forms remain the inputs. Cobalt, platinum, aluminium and titanium retain their normal refining routes. Adding selected materials to lunar crater profiles is accepted even where default lunar ore mixes lack them.

### Material Integration Contract

- Canonical material: `SpaceGradeAlloy`, including `plateSpaceGradeAlloy`, `frameGtSpaceGradeAlloy` and `foilSpaceGradeAlloy`.
- Use the MaterialLib-backed GT material model, targeting Material Unification (`mu`, PR 8414), rather than compatibility with the old `Materials` model. This names the integration target, not verified API availability.
- Material registration and generated processing belong to lunar industry. Computer hardware consumes the same forms.
- Follow [[Design Early Orbital Production Recipe Chain#Accepted Content Ownership And Temporary Staging]] for GT-bound content and the shared environment API for conditions.

### Alloying

All recipes use an EBF at **480 EU/t** and require **No Atmosphere**, but not Microgravity.

| Route | Inputs | Output | Base time | Heat | Target coil tier |
| --- | --- | --- | ---: | ---: | --- |
| Fe-Si | 10 Iron ingots, 1 full Silicon dust | 288 mB molten SGA | 40 s | 3600 K | Nichrome |
| Au-Co | 5 Gold ingots, 2 Cobalt ingots | 576 mB molten SGA | 80 s | 4500 K | TP Alloy |
| Al-Sc | 10 Aluminium ingots, 1 Scandium ingot | 1584 mB molten SGA | 220 s | 5400 K | HSS-G |

Coil names express infrastructure targets. Normal GT heat checks, including voltage bonuses, determine eligibility rather than a strict coil-material whitelist. Starting infrastructure targets HV.

Each route costs 20 base seconds and 192000 EU per 144 mB ingot-equivalent before overclocking, heat discounts and casting.

| Route | Intended supply advantage |
| --- | --- |
| Fe-Si | Common inputs and lower initial heat requirements, at high material demand |
| Au-Co | Lower input volume without a Sc refinery, competing with other precious-metal uses |
| Al-Sc | Best material return, supported by aluminium refining, Sc chemistry and metal finishing |

All three should remain situationally useful. No rule forces players to build every route. Compare ongoing material, energy, throughput and transport costs after automation and finite-reserve exhaustion, not only startup cost or a temporary surplus of precious metals. The middle route's competitive total cost still needs validation.

### Forming And Recycling

- Melt and cast SGA into plates, rods and ingots. Later shape changes return through melting and casting.
- Alloying, melting, casting and material recovery require No Atmosphere, including generated recipes. None requires Microgravity.
- Disable direct bender, extruder and equivalent manual shape conversions.
- Fluid Solidifier: **144 mB molten SGA → 4 foils**, using a new non-consumed thin-strip mold under No Atmosphere.
- Assemble frames from cast rods and plates. Frame and finished-equipment assembly do not automatically require vacuum.
- Recycling preserves SGA quantity. It cannot recover the original composition or turn iron-route SGA into precious metals.

Thin-strip mold cost and new casting times/EU remain open. Optional residue recovery has no selected identity or ratio. Any later route must account for actual impurities, preserve the recovery environment and avoid repeated recovery from the same residue.

## Construction And Other Consumers

Automated Stations and Automated Outposts use primarily bulk SGA, with smaller amounts of specialist electronics and components. Functional modules retain function-appropriate costs. Exact Facility bills remain open.

The first physical Station keeps a non-SGA bootstrap and expansion route. SGA does not replace tiered vehicle materials. Later equipment can expand demand without becoming prerequisites for the opening progression.

**Unapproved bulk construction recipes:**

| Recipe | Machine | EU/t | Base time | Environment |
| --- | --- | ---: | ---: | --- |
| 8 SGA plates + 4 Steel rods -> 4 Space Station Blocks | Assembler | 120 | 10 s | Any |
| 4 SGA plates + 2 Steel rods -> 8 Space Station Panels | Assembler | 120 | 10 s | Any |

These are alternatives, not mandatory replacements for existing construction recipes.

**Sc component directions:** RF Resonator for communication hardware and Laser Crystal for optical/prospecting hardware. Recipes, benefits and availability remain open. The optical branch should start from oxide rather than reduce and reoxidize it. Metallic Sc and nitrogen-bearing films inspire the RF branch.

Alpha retains one basic Communication Satellite and one basic Prospecting Satellite. Modular construction and advanced satellite consumers are deferred in [[Define Modular Satellite Construction]], not Sc-chain requirements. The opening satellite progression has no implicit Sc requirement.

Additional Sc uses, including non-Galaxia equipment, are wanted. Unapproved candidates include alternative emitter/sensor manufacture, oxide ceramics in Computer hardware and useful Al-Sc structural parts. Each needs a concrete consumer. Installed parts do not need arbitrary continuous Sc consumption.

## Open Decisions And Validation

- Extractor geometry and integration with shared crater accounting.
- Crater density, size-class mix, diameter variation and richness response.
- Thin-strip mold manufacture, casting costs and coherent generated material recipes.
- Facility construction bills and competitive total supply costs for all three SGA routes.
- Concrete wider Sc consumers, without making deferred satellite systems prerequisites.
- Ambiguous recipe-family variant selection.
- End-to-end reagent access, fluid capacities, throughput and energy requirements.

Sustained power supply belongs to [[Define Space Factory Power Supply]]. Transported batteries remain a provisional bootstrap, not a selected factory battery count.

## Sources

Mechanically equivalent SGA compositions, rather than recoverable yield deficits, were selected on 2026-10-11. SGA casting was selected in the environment-integration discussion on 2026-10-23. The same day's lunar decisions accepted the initial refinery balance, dedicated extractor and bulk-SGA Facility construction policy.

Pinned recipe evidence:

- [Platinum refining](https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/bartworks/system/material/gtenhancement/PlatinumSludgeRecipes.java#L299-L393) includes efficient processing and the low-return metallic-powder route.
- [Aluminium reductions](https://github.com/GTNewHorizons/NewHorizonsCoreMod/blob/9aa0afc8711f3efbe3afc0d11ec44dcbf5b87442/src/main/java/com/dreammaster/gthandler/recipes/BlastFurnaceRecipes.java#L438-L468) preserve ordinary feedstock processing.
- [Drilling Fluid manufacture](https://github.com/GTNewHorizons/GT5-Unofficial/blob/2259bc64244f9f7fc58e039d8e89ca40dd17c929/src/main/java/gregtech/loaders/postload/recipes/MixerRecipes.java#L641-L649).
- [Chinfinity meteor](https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/83b3fb26cd9979e0256c7568bdf8c6f87579b532/config/BloodMagic/meteors/Chinfinity.json#L34-L39) and [focus identity](https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/api/enums/MetaTileEntityIDs.java#L703). The late ZPM-focus source remains unchanged.
- [Nitric-acid research](https://pmc.ncbi.nlm.nih.gov/articles/PMC8779884/) concerns prepared red mud, not the game's deposit yields.
- [Al-Sc](https://nikon-slm-solutions.com/wp-content/uploads/2024/07/mds5143.pdf), [RF targets](https://www.materion.com/en/insights/blog/materions-aluminum-scandium-sputtering-targets-power-rf-mobile-and-broadband-devices), [oxide ceramics](https://infinitamaterials.com/material/scandia-stabilized-zirconia-alumina/), [laser hosts](https://link.springer.com/article/10.1007/s00340-013-5433-2) and [Sc properties](https://periodic-table.rsc.org/element/21/Scandium) inform potential uses, not approved recipes.

Detailed research remains under [[Sources]]. These references establish design inputs, not current runtime verification.

## Gameplay Flow

A player can begin extracting a crater without building a fluid-processing line. Dry mining immediately supplies useful solids, but consumes the finite deposit less efficiently. Adding Drilling Fluid and separation equipment preserves more of that reserve. Once it runs out, the same site can keep producing through fracking. Output stays predictable while replacement-fluid demand grows, creating a choice between expanding the site's fluid supply and moving extraction equipment to a fresh crater.

The extracted minerals feed ordinary refining, while Sc concentrate needs its own chemical line. Recovering acid, alkali and Calcium reduces repeated reagent production without eliminating it. Sc metal finishing then rewards a vacuum workshop: atmospheric processing returns part of the metal as oxide, which must pass through recovery again.

SGA turns these supplies into construction material for expanding space infrastructure. Common iron and silicon offer the lowest-heat entry, gold and cobalt offer another supply route, and aluminium with refined Sc gives the strongest material return. These are intended alternatives whose practical value depends on available resources and infrastructure, not three mandatory steps. Melt-and-cast production keeps shaping and recycling in vacuum, while finished parts can be transported and assembled elsewhere. Larger Automated Stations and Outposts create continuing bulk demand without making SGA the material that determines every equipment tier.
