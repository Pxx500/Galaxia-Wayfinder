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
blocked_by:
  - "[[Review Crater Nodes Proposal]]"
claimed_by: local-wayfinder-lunar-recipes
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Design Lunar Crater Processing Recipe Chain

## Question

Which complete recipes connect lunar crater extraction, Drilling Fluid supply, enriched-fluid processing and carrier recovery to bulk Space-Grade Alloy without bypassing existing material progression?

## Decision Boundary

[[Review Crater Nodes Proposal]] owns the accepted shared-deposit, extractor-mode, scanner, fluid-identity and canonical-alloy rules. Do not reopen them. This ticket selects concrete production content under those rules, not machine implementation or another room system.

[[Define Alpha Research and Production Floor]] owns the standard GT machinery baseline. Only the already selected crater extractor is a custom extraction machine. Downstream processing should use normal GT machines and recipe maps unless a demonstrated requirement needs an explicit exception.

## Current Round

Opened on 2026-10-10 after the owner provisionally accepted battery-powered orbital bootstrap. Prepare the lunar chain as a complete recipe proposal to redline, not a sequence of isolated voltage or quantity questions.

Verify whether existing GT drilling-fluid production can supply the carrier before inventing another feedstock chain. Propose the processing steps, material forms, recovery loop and alternative recipes for the same Space-Grade Alloy. Example deposit profiles are proposals, not approval of the original Discord profiles or a permanent three-profile limit.

Ordinary extraction and fluid processing must not silently bypass the existing titanium chain or other progression-relevant refining requirements. Atmosphere-free alloy production does not require microgravity. Numerical settings remain working values until accepted or measured.

## Accepted Owner Revisions, 2026-10-10

The owner prefers the new extraction and recovery direction while retaining more of the original proposal's material variety. This does not approve the initial flat-yield recipe table as a whole.

- Use normal GT deposits and material forms for iron, platinum, gold, cobalt and aluminium as the material direction. Do not create origin-only raw variants such as Rough Asteroidal Gold or Natural Asteroidal Cobalt. Existing normal processing and progression requirements remain in place.
- Scandium is uncertain, not selected. Investigate the original Al-Sc inspiration, real sources and existing GT acquisition before recommending an advanced route.
- Fracking produces a fixed amount of enriched output per operation while its input-fluid requirement increases with the crater's shared history. The owner explicitly accepted this behavior. It does not select a 1,000 mB output batch, the initial cost or a growth curve.
- Space-Grade Alloy needs several ways of entering production with different processing complexity and returns. The simple route is less efficient, the intermediate route is more efficient, and the demanding advanced route offers the best return. These are routes to one product, not different item grades.
- The iron-based route should be the weakest return. Gold and cobalt are the owner's working intermediate example, not final quantitative recipes. The advanced composition remains open. Do not silently choose aluminium-scandium.
- The chemistry should have meaningful stages and recovery choices. The previous equally simple, equal-yield Fe/Al/Si alternatives are insufficient as the final content proposal.

## AFK Design Round

The owner authorized a broad write-up, parallel investigation and brainstorming while away. Produce a complete comparison of alternative route sets, full proposed recipes, yields, material and energy costs, fracking behavior, real-world inspiration and progression risks. Distinguish existing-code facts from proposed gameplay values. The owner will review the report on return. This authorization does not approve new content choices or implementation.

Use [[Sources]] for unreviewed research intake. The final recommendations remain proposals until reviewed with the owner. Do not turn this round into a stored implementation plan.

[[Lunar Extraction And Alloy Design Report]] contains the AFK proposal packet and the owner's subsequent revisions. The 2026-10-11 direction below supersedes its former primary recovery-ladder recommendation. Historical calculations are not accepted balance or a resolution of this ticket.

## Accepted Owner Revisions, 2026-10-11

### Material Role And Feedstock Equivalence

- Register Space-Grade Alloy as a GT5 material with ordinary metal forms and generated basic processing, rather than a standalone ingot item. Final content ownership remains GT5 under [[Design Early Orbital Production Recipe Chain]]. This decision selects the intended material and generator capability, not immediate upstream implementation.
- The alloy is the common bulk construction material for space equipment and infrastructure. Its production must support sustained mass manufacture as the project grows. Do not store speculative megastructure designs or fixed future consumption targets as Alpha requirements.
- Different feedstock compositions provide different amounts of the same mechanically equivalent construction material. Less capable feedstock needs more input for the same useful SGA output. The lower output is not automatically processing loss or recoverable waste.
- Independent composition routes are the main design. Slag recovery remains a possible addition, not the mechanism that defines every efficiency band or erases their differences.
- The owner's examples are 10 Iron + 1 Silicon yielding 2 SGA, 5 Gold + 2 Cobalt yielding 4 SGA, and 10 Aluminium + 1 Scandium yielding 11 SGA. These illustrate equivalent-output ratios, not selected recipe quantities, confirmed chemistry or approval of a Sc supply line.
- Use full dusts in this lunar alloy and recovery chain. Do not design around tiny or small dust piles. This does not automatically revise unrelated previously recorded production chains.
- The owner accepts adding the selected normal mineral resources to lunar crater profiles even where the checked default Moon ore mixes do not contain them. Exact abundance, profile composition and operation yields remain open. Missing default placement is no longer an owner-approval blocker.
- Existing ordinary refining still applies. Do not bypass platinum, cobalt, aluminium or titanium processing by emitting finished metal directly from an enriched fluid.

### Generated Material Processing And Recycling

- No Atmosphere applies to SGA processing and recycling, including its generated basic metal-processing recipes, not only first alloy manufacture. No gravity requirement is added.
- The GT material recipe generator must accept environmental requirements and attach them to the recipes it generates for a material. Use the shared recipe-environment condition, not a separate per-machine or hardcoded SGA-only check.
- The former proposal allowing unrestricted SGA plate-making, remelting or recycling on an atmospheric world is superseded.
- Material conversion and recycling preserve canonical SGA quantity. Do not decompose the shared material into a chosen source composition or precious metals, since origin is not retained.
- Concrete form coverage, generator integration and the location of the temporary prototype are implementation concerns under the existing content-staging policy. This discussion does not launch or expand the separate recipe-environment implementation task.

### Fracking Recovery And Balance Order

- Initial fracking should recover approximately as much carrier fluid as it consumes. A perfect initial loop or slight initial loss is acceptable. Progressive shared crater use creates an increasing replacement-fluid requirement while enriched mineral output remains fixed.
- This supersedes a mandatory continuing fluid loss from the very first operation and the report's proposed 25% initial loss. It does not select an exact zero-loss ratio. The owner subsequently accepted Drilling Fluid provisionally as recorded below.
- First select normal resource output per extraction operation and downstream usable yield. Then balance fluid cost and deterioration around the value and abundance of that output. Do not begin by choosing a fixed number of operating hours for every crater.
- Fracking cost growth is profile-dependent. Common iron-bearing material should have gentler growth than valuable platinum-bearing material. A single identical numerical growth schedule for all profiles is not selected.
- Voltage, duration, battery requirements and processing capacity will be evaluated against actual chosen recipes. The AFK energy and throughput examples are not accepted targets.

## Scandium Acquisition Investigation

The owner recalls an existing Monazite or Bastnasite processing source and requested a GT5, CoreMod and pack acquisition audit. The prior bounded default-ore audit did not establish a source and must not be generalized to all recipe chains. Findings enter [[Sources]] first. Aluminium-scandium remains a composition candidate until its supply line and recipe are reviewed.

The 2026-10-11 audit found positive acquisition in the pack's Blood Magic Chinfinity meteor profile. It includes endstone Scandium ore, consumes a ZPM Circuit Assembler focus and costs 80,000,000 life essence. Actual ore yield is weighted and random. Normal ore conversion can supply Sc dust, with generated EBF and cooling routes available when metal ingots are needed. This is source evidence, not a demonstrated running-pack summon or approval to require Blood Magic for SGA. [Meteor configuration](https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/83b3fb26cd9979e0256c7568bdf8c6f87579b532/config/BloodMagic/meteors/Chinfinity.json#L34-L39), [focus identity](https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/api/enums/MetaTileEntityIDs.java#L703)

Direct inspection of the current Monazite/Bastnasite recipe owner found Samarium-related outputs and no named Scandium output in that owner or its material pool. This is bounded current-source evidence, not proof of all-version or all-mod exclusivity. The absolute earliest Sc access and full magic unlock chain were not established. Choose whether an existing high-gate source, a newly authored ordinary-resource source or a non-Sc advanced composition supplies the eventual bulk route. Do not treat source discovery as owner approval of one option.

## Follow-Up Owner Direction, 2026-10-11

The owner reports that Discord review resolved their earlier Scandium/Samarium confusion. Sc is not the progression-critical rare-earth material they had feared changing. The incidental meteor source does not require Galaxia's future bulk alloy chain to inherit its acquisition gate. Consider adding normal lunar Sc feedstock and a short processing line inspired by the original Al-Sc proposal. This is authorization to design the candidate, not approval of exact placement, intermediate identities, yield or recipes. Record the consumer audit's bounded evidence separately rather than asserting that every possible Sc interaction is absent.

The follow-up found no authored Sc ingredient in the checked GT/CoreMod progression recipes. Positive named references are registration, form conversion, display/storage and conditional generic plasma-fuel handling. No active ordinary Sc-to-plasma route was established. This supports removing the assumed unrelated technology-gate blocker, not a guarantee about every external mod or future recipe.

The coordinator's earlier short-chain candidate uses existing Bauxite Slag from normal bauxite refining, nitric-acid leaching, a proposed Scandium Oxide intermediate and EBF reduction to normal Sc dust. [[Lunar Extraction And Alloy Design Report]] contains the original six-stage comparison and the candidate. No oxide or leach recipe is approved. Following the owner's situational-route requirement below, broad cheap byproduct recovery is an option to compare, not the selected recommendation. Reusing ordinary Bauxite Slag would also permit non-lunar feedstock. Do not add origin metadata to normal bauxite or claim that the existing slag already yields Sc.

Drilling Fluid is accepted as the initial fracking carrier for now. The owner considers it a reasonable gameplay compromise despite reservations about the lore. Reuse its existing standard GT manufacture rather than introducing a parallel replacement-fluid recipe by default. This provisional choice does not approve the older carrier-loss ratio, processing rows or deterioration curve.

The existing three-size generation and profile model remains the starting point for concrete balance. [[Review Crater Nodes Proposal]] owns the recorded Small/Medium/Large distributions, per-size profile weights, richness response and shared reserve accounting. Do not ask the owner to select these structural relationships again when tuning the output of a profile.

## Accepted Situational-Route Goal, 2026-10-11

The owner requires three credible alternative ways to manufacture the same SGA, not a ladder whose highest output universally replaces the others. Feedstock equivalence remains the model, but output ratio alone is not the complete production cost. Each composition should have a meaningful reason to be preferred under different supply, infrastructure or demand conditions. Do not assume players will voluntarily use an inferior route or require every player to build all three.

Sc supply must be considered together with its actual demand. A new Sc line used only for plentiful SGA could make the advanced route an obvious default once automated. Real-world industrial applications are being researched to identify worthwhile competing uses. Such applications are proposals, not permission to add unrelated mandatory Alpha chains.

The owner also requested a check of Sc oxidation as a possible rationale for No Atmosphere processing. Investigate metal, powder and heated processing separately from stable oxides and aqueous compounds. No new Sc environmental restriction is accepted yet. Reactivity could justify selected metal-processing stages, not automatically every recipe with a Sc-containing ingredient. Physical inert-gas protection and vacuum are not assumed to be the same condition.

The owner raised several possible supply constraints: a source outside Luna, later access, low abundance, or rationing between several useful consumers. None is selected merely by being mentioned. Compare their advantages and failure modes before selecting source placement, processing and recipe values. No unsupported claim of unrelated GT progression risk is needed to justify a deliberately constrained Galaxia source.

Late access alone does not establish a continuing role for older routes after unlock. Competing uses alone do not establish scarcity if production scales cheaply. Extra processing steps alone do not establish a meaningful recurring cost once the factory is built. Evaluate complete ingredient, operating and throughput costs with representative local supply conditions.

## Working Satellite And Furnace Variant Direction, 2026-10-11

The owner suggested satellite uses for RF and laser-inspired Sc parts. Treat RF hardware as a candidate for later Communication Satellite components and Sc-containing optics as a candidate for later Prospecting Satellite components. They want scientifically inspired gameplay, not a complete industrial simulation. These are proposed consumers, not approved changes to the established early satellite recipes or new mandatory Alpha chains. Components need an actual selected equipment benefit before becoming mere extra ingredients.

The owner supplied a concrete example for the GT recipe-variant feasibility investigation: blast-processing Sc dust without atmosphere produces Sc ingots, while processing in atmosphere produces some Sc ingots and some Sc oxide that can be electrolyzed back into Sc dust. This is a working alternative to a hard No Atmosphere prohibition for that Sc operation. It does not relax the accepted SGA restriction. The coordinator understands the spoken ABF reference as the Sc EBF discussed in this chain, not a selected different machine.

The output split is not quantified or implemented. Atmospheric processing should retain Sc through the ingot and oxide outputs, with recovery costing extra machine work rather than deleting the element. Oxide quantities must be consistent with the chosen material definition and electrolysis recipe. Equal raw item counts do not establish elemental conservation. Use full dusts, including complete batches for oxide recovery.

The initial read-only feasibility pass recommended two ordinary static variants as the least-change representation for this fixed-input case. The owner subsequently rejected that representation as recorded below. Existing query filtering and multi-candidate storage remain useful evidence about reuse, not approval to admit duplicate recipes. Basic-machine selection, dual-input caches, recipe locks/restoration and retained-operation requirements still need coherent handling. Keep this research separate from the already bounded environment-integration implementation task. Detailed unreviewed evidence remains under [[Sources]].

The owner then clarified the desired lookup model: one common input entry identifies a recipe family, and environmental selection happens only inside that family's subset. They are concerned about avoidable search overhead from independently indexed duplicate recipes, not proposing global recipe mutation or choosing outputs only after processing. Shared input matching, variant selection and operation execution are separate responsibilities. This is a design requirement to evaluate against the existing GT index, not approval of a new recipe store or a native GT implementation.

The follow-up confirms that ordinary GT lookup already reuses normalized input paths and leaf candidate lists. More recipe objects do not inherently imply a full-map scan. An explicit family adds common-input ownership, once-per-family validation and clearer cache/profile semantics, rather than merely inventing indexing that GT lacks. It is a larger native GT data-model change than the earlier ordinary-variant option. The performance requirement remains a local choice within the found family, with no separate feature-local search system. No speedup or lag claim is benchmarked.

### Accepted Recipe Family Direction, 2026-10-11

The owner selected a first-class Recipe Family with common production inputs and explicitly represented environmental variants. Do not implement this as independent same-input recipes admitted through collision suppression, or as an authoring wrapper that expands into those entries. Such duplicate registration is unacceptable to the owner, including when optional recipe deduplication is enabled.

The family is one logical input registration with local variant selection. This does not promise exactly one physical trie node, since existing alias indexing can create several paths. Reuse the existing GT ingredient index and recipe ownership rather than creating a parallel Galaxia search system. The reason for this choice is explicit ownership and compatibility with collision and deduplication handling, not a demonstrated need to replace the optimized lookup.

Select the complete applicable variant before output protection and input consumption. A display may expose alternative outcomes without turning them into independent colliding production registrations. Family support must preserve intentional alternatives through collision and deduplication handling. The optional deduplication implementation was not inspected in the preceding research, so that compatibility is a requirement to verify, not an established implementation fact.

The owner accepted locking the family, not the currently selected environmental variant. A lock preserves the production definition while each new operation selects an applicable variant from current conditions. This does not authorize replacing the outputs of an operation that has already committed its inputs. Ambiguous eligible variants remain an unresolved selection constraint. The absent-Galaxia development case is settled below. This decision approves the model, not implementation, a new GT modification scope or exact Sc recipe values.

### GT-Only Development Boundary, 2026-10-11

The owner clarified the intended deployment: Galaxia depends on GT, and the intended GTNH gameplay includes Galaxia. Playing this future integrated pack without Galaxia is not a supported gameplay target. This is an intended deployment boundary, not a claim that current GTNH releases already require Galaxia.

GT must still be convenient to develop and launch without Galaxia. The owner selected omission of Galaxia-dependent environmental family variants in that case. Do not register those variants for production or recipe display. If no variants remain, omit the family itself rather than retaining an empty or disabled entry. This is registration-time omission, not removal of source definitions or a runtime switch.

No synthetic environment, substitute output, per-family development default or visible-but-disabled family is required. Testing those variants requires Galaxia. The earlier absent-mod rule for ordinary environmental requirements remains distinct and unchanged. Unresolved environmental data while Galaxia is present must not trigger this omission rule.

## Accepted Crater Progression And Sc Supply, 2026-10-11

The owner requires crater extraction to be important to Galaxia progression, not merely an optional source of cheap construction feedstock. Scandium is selected as a crater-exclusive primary resource. Selected lunar crater profiles are the current starting source direction. This does not restrict every future Sc-bearing crater to Luna or approve numerical abundance, operation yields or the Al-Sc recipe ratio.

Do not add primary Sc acquisition from ordinary Bauxite Slag, general overworld refining or non-crater ore generation. The former broad slag-recovery candidate is rejected under this source rule, not still awaiting an economic comparison. Processing, oxide recovery and recycling of already acquired Sc remain valid and must not create additional elemental Sc. No lunar-origin metadata or separate origin-labelled Sc material is wanted.

The owner explicitly excluded the existing Blood Magic Chinfinity meteor from this source restriction. Its acquisition is much later than the planned Galaxia Sc access, so it is irrelevant to the intended early progression gate. Leave that source unchanged. Crater-exclusive acquisition applies to the newly designed Galaxia supply routes, not an absolute prohibition on every later external source in the pack.

Crater-specific resources must have actual selected progression uses. Exact research, equipment or technology consumers remain to be chosen. Do not make SGA itself a technology-tier gate, require every player to use every alloy composition, or turn all Galaxia progression into one fixed crater itinerary. Shared reserve and fracking history remain the cost model. Source exclusivity alone does not establish continuing economic balance between the three SGA routes.

### Accepted Sc-Bearing Bauxite Profile

The owner selected a crater deposit concept described as scandium-rich bauxite without creating a new ore block or origin-specific raw item. Its resource-enriched extraction fluid is processed into ordinary Bauxite and Sc-bearing products. The deposit composition is represented by the Crater Material Profile and its distinct enriched-fluid identity, not by tagging ordinary Bauxite with its origin.

Recover Sc from that fluid before the normal Bauxite branch. Ordinary Bauxite and its normal refining remain unchanged and do not become generic Sc sources. Do not substitute direct Sc ore output for the selected fluid-processing branch or revive the rejected global Bauxite Slag recovery route. Chemical intermediates with an actual processing role remain possible, but their identities, recipes and yields are not selected by this decision.

The owner selected two alternatives during finite ordinary mining of this profile. With Drilling Fluid, the extractor produces enriched fluid and uses the crater reserve efficiently. Without the fluid, it directly produces ordinary Bauxite and Sc concentrate, with a small irreversible loss of useful deposit material. The dry branch joins the accepted chemistry after mineral separation. It does not require a new ore identity or yield directly usable Sc metal.

Both alternatives consume the same shared initial reserve. Dry mining must reduce usable yield per unit of reserve, not merely run more slowly while eventually recovering the same material. Wet extraction is available from the beginning but does not bypass exhaustion or begin unlimited fracking early. After the finite reserve is exhausted, dry extraction cannot continue, and the existing fluid-dependent fracking stage with increasing input cost remains.

On 2026-10-12 the owner selected a 10% chance for a dry ordinary-mining operation to consume twice its normal share of the crater reserve. The other 90% consume the normal share. Output is unchanged in either outcome. The doubled charge applies to reserve consumption, not energy, duration or output, and replaces the coordinator's proposed fixed 1.1 multiplier. It gives an expected reserve cost of 1.1 times the normal charge. This is accepted working tuning, not an implemented feature.

Operation quantities remain open. The coordinator's same-solid-batch proposal is still a proposal. Compare the saved separator and carrier-cleanup work with the cost of using up the site sooner. The owner selected better resource efficiency for wet mining, not a requirement that it dominate every energy or infrastructure comparison.

### Accepted Sc Processing Skeleton

The owner accepted the following four-stage processing direction. It replaces the prior broad Bauxite Slag acquisition candidate. It does not approve quantities, voltage, duration, exact material definitions or selected recipe maps.

| Stage | Inputs | Outputs |
| --- | --- | --- |
| Mineral separation | Enriched Sc-bearing bauxite extraction fluid | Ordinary Bauxite, Sc concentrate and spent carrier |
| Leaching | Sc concentrate and Diluted Nitric Acid | Sc solution and mineral residue |
| Precipitation | Sc solution and Sodium Hydroxide | Scandium Oxide and spent solution |
| Reduction | Scandium Oxide and Calcium | Normal Scandium dust and Quicklime |

The concentrate is a useful production intermediate, not a new ore identity. The ordinary Bauxite branch retains its existing aluminium processing. Carrier cleanup is separate from the four Sc stages. Chemical residues and reagent recovery must be accounted for in concrete recipes, not silently treated as perfectly recycled.

The selected skeleton can supply Sc dust to alloy manufacture and other parts. Metal ingot production remains distinct and may use the discussed environmental EBF family. Do not add another environmental prohibition to every chemical stage merely because the chain contains Sc. Detailed recipes must use full dust batches and remain coherent with GT material units and any generated compound processing.

The earlier oxide-to-Sc electrolysis direction also applies to oxide from precipitation. Use one canonical Scandium Oxide rather than provenance variants. Calcium reduction is therefore an alternative metal-recovery route, not an artificially mandatory final step. Compare its operating cost and capacity with electrolysis when proposing concrete recipes. This consequence does not select energy or throughput values.

The owner clarified that the quantitative draft needs finetuning, not rejection of its recipes or their order. Retain the original separation, leaching, precipitation and recovery direction. Larger useful output batches can require larger fluid input batches. The owner's example of 10000 mB for eight Bauxite and a Sc-bearing product is illustrative, not a chosen volume or output form. The coordinator's rejected-table status and proposed one-mineral-per-operation cap are withdrawn in [[Lunar Extraction And Alloy Design Report]].

Input and output batches need not be identical, small or matched directly between consecutive recipes. Accumulation and splitting are allowed. For materials with defined chemical formulas, follow [GTNH Chemical Balance](https://wiki.gtnewhorizons.com/wiki/Chemical_Balance), including its different solid, fluid and bracketed-compound rules. The owner explicitly excludes undefined mixtures such as scandium-rich bauxite from fixed formula-derived coefficients. Their concentrations and extraction yields are design and tuning choices. This does not approve any particular number or turn raw mineral extraction into a closed material-creation loop.

### Accepted Initial Sc Components And Wider Use Goal

The owner accepted RF Resonator for upgraded Communication Satellites and Laser Crystal for upgraded Prospecting Satellites as the initial component-design direction. Established first-satellite recipes remain unchanged and do not gain a Sc prerequisite. Exact component compositions, device benefits, recipes and upgrade availability remain open.

These two parts are not the desired limit of Sc use. The owner wants additional meaningful Sc applications, including recipes outside Galaxia-specific content. Future proposals should compare actual consumers, benefits and supply impact rather than adding arbitrary Sc ingredients. This direction does not authorize immediate GT source changes, replacement of unrelated progression gates or every suggested industrial application. Existing content-staging and maintainer-coordination boundaries remain in force.

### Accepted Reagent Supply And Recycling Requirement

The owner requires accounting for upstream reagent production and local lunar supply, not just energy used by the Sc refinery. They identify lunar SaltWater as an available source for NaOH, but require at least some reagent recycling. No recovery ratio is selected by that requirement.

Nitric Acid supply is a greater concern because Luna lacks atmosphere and ammonia production is expensive. Prefer investigating recovery of nitrogen-bearing spent chemistry and reuse of existing GT recipes before assuming continuous fresh acid manufacture or adding another parallel reagent chain. This does not claim that every existing Nitric Acid recipe requires ammonia or an atmospheric location. Gas acquisition, processing and transport remain separate costs to verify.

The prior proposed once-through acid and NaOH handling is superseded by the owner's accepted recovery direction below. Preserve chemical-balance rules for defined compounds and do not change existing pure-material recovery recipes merely to enforce a lower yield. Inefficiency is represented in separating usable compounds from the new undefined contaminated solution.

The owner accepted the nitrate recovery loop with approximately 90% recovery of both Nitric Acid and NaOH as the initial working tuning. The new Distillery step processes 9000 mB spent Sc solution into 27 existing BartWorks Sodium Nitrate dust and 6000 mB Water at 120 EU/t for 90 s. Reuse the existing nitrate-to-acid, sulfate-to-sodium and sodium-to-NaOH recipes without changing their outputs. Sulfuric Acid and Hydrogen are circulating startup stocks, with gas/cell handling supplied by ordinary GT capabilities. These are accepted content settings to test, not implemented or immutable balance.

For ten current refinery batches producing twenty Sc dust, working replacement demand is 6000 mB Nitric Acid and 18 full NaOH dust rather than 60000 mB acid and 180 dust. Recipe batching and buffered leftovers remain independent. [[Lunar Extraction And Alloy Design Report]] retains the full recipe table and arithmetic. No new ammonia-free lunar gas source or unconditional energy-saving claim is selected by this recovery decision.

## Remaining Content Decisions

On 2026-10-14 the owner accepted the complete three-recipe SGA manufacturing packet in [[Lunar Extraction And Alloy Design Report]] as working content settings. Fe-Si uses 10 Iron ingots and 1 full Silicon dust for 2 SGA at 3600 K for 40 s. Au-Co uses 5 Gold ingots and 2 Cobalt ingots for 4 SGA at 4500 K for 80 s. Al-Sc uses 10 Aluminium ingots and 1 Scandium ingot for 11 SGA at 5400 K for 220 s. All use the EBF at 480 EU/t with No Atmosphere and no Microgravity requirement. Target coil tiers are Nichrome, TP Alloy and HSS-G, using normal GT heat checks rather than a new coil-material restriction. These settings are accepted for testing and tuning, not implemented or demonstrated whole-chain balance.

On 2026-10-14 the owner also accepted the revised four-profile lunar packet in that report. Per 16000 mB enriched fluid, separation yields eight crushed Banded Iron and two crushed Quartzite, two crushed Gold and one crushed Cobaltite, eight crushed Bauxite and one Sc concentrate, or four crushed Platinum respectively. Each uses the Centrifuge at 120 EU/t for 40 s and outputs 16000 mB spent carrier. The qualitative abundance order and eligibility in all three size classes are selected. These are working settings, not verified final balance. The matching dry Sc solid batch is selected under the existing loss rule. Numeric occurrence weights, initial reserves, extraction timing and fracking deterioration remain open.

On 2026-10-14 the owner accepted that report's nominal initial-reserve table and linear profile-dependent fracking growth as working tuning. The four profiles start at 2000/1000/500/250 reference portions for Small, 6000/3000/1500/750 for Medium and 16000/8000/4000/2000 for Large. Input begins at 16000 mB per reference portion and reaches 32000 mB after 8000/4000/2000/1000 shared fracking portions respectively, while recovered carrier and mineral output stay fixed. The owner added approximately plus or minus 10% random initial reserve variation. Apply it once to the size/profile-adjusted reserve, shared by all extractors, without rerolls or variation in operation outputs and fracking slopes. Exact cleanup and extractor settings still require review.

The current round proposes relative class and per-class material occurrence weights in that report. Overall crater density and richness response coefficients remain separate open tuning. Preserve the selected shared-state, initial-reserve and fracking-cost rules.

- Complete carrier cleanup and extractor operation settings around the accepted mineral separation recipes and provisionally accepted Drilling Fluid supply.
- Select numeric occurrence weights, overall generation density, richness response and extraction throughput for the four accepted profiles, preserving ordinary processing and the selected dry Sc batch.
- Complete enriched-fluid carrier cleanup around the accepted initially closed loop and linear progressive loss. Increased fracking input creates a higher continuing supply burden rather than proportionally duplicating resource output.
- Evaluate the accepted three alloy recipes against concrete feedstock supply and actual construction uses. Any supplementary residue processing must preserve their different equivalent-output ratios and the alloy's non-tier-gate role.
- Select crater Sc abundance, processing and useful competing consumers, then demonstrate why the three compositions can remain situationally preferable after automation. Primary Galaxia crater sourcing is selected and broad Bauxite Slag recovery is rejected. The existing late Blood Magic meteor is explicitly retained.

No new recipes are accepted or implemented by opening this ticket.
