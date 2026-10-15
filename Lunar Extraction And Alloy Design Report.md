---
type: wayfinder-proposal
status: ready-for-owner-review
date: 2026-10-10
revised: 2026-10-14
tags:
  - galaxia/alpha
  - wayfinder/proposal
---

# Lunar Extraction And Alloy Design Report

## Purpose And Authority

This is the broad AFK design report requested by the owner. It compares complete recipe families, their costs, their original inspiration and their unresolved tradeoffs. It is not an implementation plan or approval to change production code.

[[Design Lunar Crater Processing Recipe Chain]] owns the current decisions. [[Review Crater Nodes Proposal]] owns the extraction and canonical-product rules. Tables remain proposals unless explicitly marked as accepted working settings. Existing upstream recipes are labelled separately. Evidence snapshots are not permanent dependency pins. Development still targets current GT.

The report was assembled from parallel research and source checks. Raw inputs remain unreviewed intake under [[Sources]]. Their existence does not make the proposed content accepted. The owner's 2026-10-11 corrections are incorporated below. Original numerical drafts remain historical proposals in the source notes, not current recipe recommendations.

## Executive Recommendation

Use independent composition routes to one canonical GT5 material. More capable feedstock supplies more mechanically equivalent SGA per input batch. The owner's comparison is not chiefly about processing loss. Residue recovery may supplement the routes, but must not erase their composition differences. Use full dusts, not tiny or small piles.

The owner subsequently clarified that all three compositions should be credible situational alternatives, not a progression ladder with one universally dominant endpoint. Greater equivalent output is only one advantage. Availability, competing ingredient demand, recurring operating cost and production capacity must supply reasons to prefer different recipes. Broad cheap Sc recovery from ordinary refinery waste is therefore under reconsideration, not the selected recommendation.

Give generated SGA processing and recycling the same No Atmosphere requirement as first manufacture. The material generator needs shared environmental-requirement support. SGA is the common bulk construction material for space industry and must scale to sustained mass production without replacing tier-specific materials.

Fracking buys a constant mineral batch with profile-dependent rising carrier demand. Initial recovery should be approximately closed, with a perfect or slightly lossy start. Choose resource output and downstream usable yield first, then tune fluid cost and deterioration. Existing Drilling Fluid is provisionally accepted as the carrier, with its normal GT manufacture, despite the owner's lore reservations.

The owner subsequently selected crater-exclusive primary Sc acquisition for the new Galaxia supply, starting with lunar profiles, and required craters to participate meaningfully in progression. Broad Bauxite Slag recovery is no longer a candidate source. The existing much later Blood Magic meteor is explicitly retained as irrelevant to the planned early gate. On 2026-10-14 the owner accepted the three SGA manufacturing recipes below as working settings, including Al-Sc. Concrete consumer evidence remains bounded to the checked code and pack content.

## 1. What Is Already Decided

- There is one canonical Space-Grade Alloy GT5 material with ordinary generated metal forms, not different grades or origin metadata.
- It is the common bulk construction material for space industry and must support sustained mass manufacture. It does not replace titanium, desh or another technology gate.
- Producing, processing and recycling SGA requires No Atmosphere. It does not require Microgravity.
- Normal GT deposits and materials provide iron, platinum, gold, cobalt and aluminium. No Rough Asteroidal Gold, Natural Asteroidal Cobalt or new origin-only ore family is wanted.
- Composition routes have different equivalent-output ratios and meaningful processing differences. Fe-Si, Au-Co and Al-Sc have accepted working manufacturing recipes below. Full dusts are used wherever dust is selected, without tiny or small piles.
- One extractor mines the shared finite crater reserve first, then fracks after exhaustion. Multiple machines share the same history.
- Fracking output stays fixed as its input cost rises. Initial carrier recovery is approximately closed. Cost growth depends on resource profile. Exact outputs, initial loss and curves remain open.
- Existing GT Drilling Fluid is the provisionally accepted carrier. Its standard manufacture remains the supply route.
- Adding the selected normal resources to lunar crater profiles is accepted even where default Moon mixes do not contain them. Exact abundance remains open.
- Enriched variants have separate Fluid IDs. This is not an NBT-fluid-subtype design.
- Existing GT processing remains the downstream baseline. Titanium processing stays unchanged.
- Charged GT batteries and a Battery Buffer are the provisional factory bootstrap. Combustion generation is prohibited in space even inside oxygenated Station rooms. New Space Grade Solar Panels remain recipe components.

## 2. Original Proposal: Keep The Idea, Not Every Recipe

The original paired Fe-Pt, Au-Co and Al-Sc deposits with distinct processing economies. It offered ordinary metals, secondary alloy inputs, residue reuse and a reason to build sustained lunar industry. Those are useful ideas.

Its weak points for our current direction are the origin-labelled replacement ores, three interchangeable alloy identities, a separate pressure chamber and unfinished branches. Those choices are not carried into this proposal. Low output from a weaker composition is not itself a design flaw. The owner explicitly wants different equivalent-output ratios.

The original author did attach research. The Markdown import lost the targets behind its source labels. The public Google Docs model retained both a Dhofar 007 meteorite table and the exact [Shoppert et al. scandium-extraction paper](https://pmc.ncbi.nlm.nih.gov/articles/PMC8779884/). The latter supports dilute-nitric-acid leaching of specially prepared red mud, not every step or quantity in the proposed game chain. The ResearchGate table was inaccessible, so its contents were not used as evidence.

The old timing descriptions also need caution. If the listed reserve counts mean individual resources and the listed outputs mean items per operation, the default Fe-Pt example lasts about 16.7 hours, Au-Co about 11.7 hours, and Al-Sc about 19.4 hours. Those values do not match the accompanying claims of roughly a week, five days and eight days. A different reserve unit would need to be stated explicitly. Do not reuse those numbers as tested balance.

## 3. Verified GT Grounding And Placement Limits

| Material | Existing source-backed processing | Consequence for the new chain |
| --- | --- | --- |
| Iron | Ordinary iron processing exists. Banded Iron has iron-oxide composition and direct smelting to Iron | Prefer a confirmed iron feedstock. Do not assume the separate Hematite identity is an interchangeable alias |
| Gold | Normal Gold forms and ordinary smelting exist | No special asteroidal gold item is needed |
| Cobalt | Cobaltite roasting and roasted/oxide reduction use actual MV, 1,200 K EBF recipes | Supply ordinary ore, then preserve its roasting and reduction |
| Platinum | Ordinary outputs become Platinum Metallic Powder. Efficient chemistry and a poor-yield EBF alternative exist | Do not emit pure platinum from the crater separator or falsely require every player to use the full efficient refinery |
| Aluminium | Existing bauxite slurry, heating, LCR and alumina processing feed CoreMod reductions | Reuse the normal chain rather than inventing scandium-rich bauxite or direct fluid-to-Al output |
| Scandium | Material, ore forms and 1,814 K processing exist. The prior bounded default-ore audit did not establish a source | Audit recipe chains and pack acquisition before proposing a new source |

One existing platinum option consumes 3 Platinum Metallic Powder dust and yields 2 platinum nuggets at MV, 2,041 K and 30 seconds. The ordinary efficient refining routes remain available. This is a real low-return alternative, not a new Galaxia shortcut. [GT platinum recipes](https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/bartworks/system/material/gtenhancement/PlatinumSludgeRecipes.java#L299-L393)

The final aluminium reduction gap was closed through current CoreMod source:

| Existing recipe | Output | EU/t | Time | EBF heat |
| --- | --- | ---: | ---: | ---: |
| 10 Alumina dust + 3 Carbon dust | 4 Al ingots + 3,000 mB CO2 | 120 | 60 s | 2,054 K |
| 10 Alumina dust + 5 Cryolite dust | 4 Al ingots | 120 | 80 s | 963 K |

These are existing recipes, not proposed replacements. Recipe voltage and required heat are independent. [CoreMod aluminium recipes](https://github.com/GTNewHorizons/NewHorizonsCoreMod/blob/9aa0afc8711f3efbe3afc0d11ec44dcbf5b87442/src/main/java/com/dreammaster/gthandler/recipes/BlastFurnaceRecipes.java#L438-L468)

Default GT Moon-enabled mixes already provide iron through the Copper mix and bauxite/ilmenite/aluminium through the Bauxite mix. The checked Gold, Nickel/Cobaltite and Platinum mixes do not enable Moon. On 2026-10-11 the owner accepted adding the selected normal resources to lunar craters. Missing default placement is no longer a decision blocker. Abundance, operation outputs and retained normal refining still need concrete balance. This acceptance does not claim that the whole chain has been tested for progression neutrality.

Map checks support the proposed recipe shapes, not runtime proof. Chemical Reactor has two item inputs and one fluid input. Electrolyzer accepts one fluid input. EBF and Centrifuge have the needed output shapes. The current Sifter map also allows a fluid input, so the original liquid-to-scandium step cannot be rejected merely from the word Sifter. Its chemistry and existence are separate questions.

## 4. Extraction And Carrier Loop

### Equipment And Existing Carrier

The controller recipe below is a proposal and does not settle machine geometry. It needs no lunar-exclusive alloy to avoid a bootstrap cycle.

| Status | Product | Input | Machine | EU/t | Time |
| --- | --- | --- | --- | ---: | ---: |
| Proposed | Crater Extractor Controller | 1 HV hull, 2 HV motors, 1 HV pump, 2 HV pistons, 2 HV circuits, 4 steel plates, 144 mB molten tin | Assembler | 480 | 45 s |
| Existing GT recipe | 5,000 mB Drilling Fluid | 5 water cells, 1 stone dust, 20 mB lubricant | Mixer | 15 | 3.2 s |

The existing Mixer recipe returns five empty cells. It was checked in local GT source at `2259bc64244f9f7fc58e039d8e89ca40dd17c929`. [Drilling-fluid recipe](https://github.com/GTNewHorizons/GT5-Unofficial/blob/2259bc64244f9f7fc58e039d8e89ca40dd17c929/src/main/java/gregtech/loaders/postload/recipes/MixerRecipes.java#L641-L649)

### Candidate Deposit Families

Use normal registered ore forms and their retained processing. Adding selected normal resources to lunar craters is accepted. The following families are not final abundance tables:

| Family | Normal mineral feedstock examples | Economic role |
| --- | --- | --- |
| Iron-bearing | Iron or confirmed Banded Iron, possibly a small platinum-group companion where justified | Cheap bulk feed, valuable secondary stock |
| Gold/cobalt-bearing | Gold and Cobaltite | Precious/electronic stock plus the medium route's additives |
| Platinum-bearing | Ordinary platinum-group ore | Existing refinery stock, optional advanced addition |
| Sc-bearing bauxite profile | Enriched extraction fluid separates into ordinary Bauxite and Sc-bearing products, without a new ore identity | Selected source direction for normal aluminium feed and crater Sc |

Do not produce pure Pt, Co, Al or Ti ingots in the separator. Different enriched fluids identify actual profile contents. Silicon supply may come from a normal silica companion or another existing supply line. Deposit composition, richness and GT refining determine ore-to-metal yields, so a ten-item ore batch is not automatically ten metal ingots.

The owner selected both wet and dry alternatives during finite ordinary mining of the Sc-bearing bauxite profile. Wet extraction consumes Drilling Fluid and supplies the enriched-fluid branch from the beginning. Dry extraction gives ordinary Bauxite and Sc concentrate directly, but less usable output per reserve consumed. No new ore item is needed. After exhaustion, only fluid-dependent fracking continues. [[Design Lunar Crater Processing Recipe Chain]] owns this accepted choice. Exact extraction quantities and the small dry-loss percentage remain tuning.

### Accepted Working Lunar Profiles And Separation, 2026-10-14

On 2026-10-14 the owner accepted the revised four-profile packet and its separation recipes as working content settings, including four crushed Platinum. It does not replace the existing Small/Medium/Large model or equate crater diameter with a particular composition. Profile occurrence weights remain independent for each size class. The accepted qualitative abundance ordering is common iron-silica, less common gold-cobalt, uncommon Sc-bearing bauxite and rare platinum. All four may occur in any size class, without a new large-crater-only Sc rule. Exact generation weights are still open.

| Accepted working profile | Enriched-fluid input | Solid separation output | Spent carrier | Centrifuge base EU/t | Base time |
| --- | ---: | --- | ---: | ---: | ---: |
| Iron-silica | 16000 mB | 8 crushed Banded Iron, 2 crushed Quartzite | 16000 mB | 120 | 40 s |
| Gold-cobalt | 16000 mB | 2 crushed Gold, 1 crushed Cobaltite | 16000 mB | 120 | 40 s |
| Sc-bearing bauxite | 16000 mB | 8 crushed Bauxite, 1 Sc concentrate dust | 16000 mB | 120 | 40 s |
| Platinum-bearing | 16000 mB | 4 crushed Platinum | 16000 mB | 120 | 40 s |

Every profile has a distinct enriched Fluid ID. The common volume is a comparison baseline, not a chemical formula or a rule forcing adjacent recipe batches to match. Normal GT processing follows separation. These are crushed mineral outputs, not equivalent ingot counts. The Sc row retains the earlier quantitative proposal rather than silently accepting the complete downstream Sc refinery. Platinum's ordinary refining is preserved. No free Pt companion is added to the abundant iron profile in this packet.

On 2026-10-14 the owner challenged the proposed one-crushed-Platinum yield because the deposit is rare and is expected to have a relatively small finite reserve before fracking. They then accepted four crushed Platinum per 16000 mB separation batch, with the other profiles unchanged. The correction does not select a numerical reserve. Avoid stacking rarity, a small initial reserve and an unrewarding operation yield. A found site should justify its infrastructure, while the established faster growth of platinum fracking cost remains the long-term operating constraint. Do not automatically offset the higher mineral yield by increasing initial carrier cost and erasing the benefit.

The existing Sc proposal needs twelve concentrate dust for two Sc dust. At the proposed separation yield, this is 192000 mB enriched fluid and 96 crushed Bauxite. Before refining losses, one Sc unit corresponds to 96000 mB and 48 crushed Bauxite. This explains the proposed dilute coproduct relationship, not total energy cost, Sc availability or a proof that Al-Sc remains situational. Competing Sc consumers and whole-chain economics still need comparison.

Extraction duration, finite reserves, numerical occurrence weights and fracking deterioration are not selected by this table. Recovered carrier and initial fracking input must preserve the accepted approximately closed start. Additional fracking input is lost underground and never increases this fixed mineral output. The accepted dry Sc mining batch is the same eight crushed Bauxite and one concentrate, with the previously accepted 10% chance of double reserve consumption. Dry and early wet behavior for other profiles is not silently changed by this separator packet.

### Proposed Operations

| Operation | Input | Output | Machine | EU/t | Time |
| --- | --- | --- | --- | ---: | ---: |
| Ordinary mining | Shared reserve batch | Profile's normal solid batch | Crater Extractor | 120 | 30 s |
| Fracking | Current profile-dependent q(n) carrier | Fixed enriched batch | Same extractor | Open | Open |
| Mineral separation | Enriched batch | Profile's normal solids + spent carrier | Centrifuge candidate | Open | Open |
| Carrier cleanup | Spent carrier | Recovered usable carrier | Centrifuge candidate | Open | Open |

Fracking is available only after normal reserve exhaustion. Extra input is lost underground rather than increasing mineral output. Recovery should initially return approximately the supplied amount, then leave progressively larger makeup demand as input cost grows. The previous 1,000 input and 750 recovered example is superseded as the recommended starting point.

For a simple arithmetic illustration, 1,000 initial input and 1,000 recovered gives zero ongoing initial makeup after supplying working inventory. Input rising to 1,100 with the same 1,000 recovery needs 100 fresh carrier per operation. These are illustrative accounting values, not approved recipes. A slight initial loss is also acceptable.

Cleanup need not create stone. If mineral gangue is wanted, identify it as extracted material rather than inventing a claim that more carrier solids were recovered than originally supplied. Recovery has power, equipment and transport tradeoffs that depend on actual recipes.

## 5. Selected Concept: Composition And Equivalent Construction Output

### What The Ratio Means

SGA is one usable construction specification. A less capable feedstock needs more material to supply that specification. The owner describes the resulting ingot as needing more physical input to obtain equivalent mechanical properties. This is gameplay equivalence, not a claim that all input dusts and canonical output items have identical physical mass.

The former primary recovery ladder interpreted the missing output as lost bulk material. That is not the selected model. Do not automatically assign every missing unit to recoverable slag or use a later reclaim process to normalize all compositions.

The owner gave the following illustrations. These are not final quantities, established chemistry or a selected Sc source. Full dusts replace tiny and small piles throughout the current proposal.

| Composition | Illustrative full-dust input | Equivalent SGA output | Input units per SGA |
| --- | --- | ---: | ---: |
| Basic iron/silicon | 10 Iron + 1 Silicon | 2 | 5.5 |
| Intermediate gold/cobalt | 5 Gold + 2 Cobalt | 4 | 1.75 |
| Advanced aluminium/scandium candidate | 10 Aluminium + 1 Scandium | 11 | 1 |

These ratios illustrate increasing equivalent output, not 18%, 57% and 100% metal recovery. A higher output ratio does not by itself prove lower total production cost. Normal refining, feedstock abundance and machine work still matter. The basic iron route must remain feasible for bulk demand, not become unusable because every better composition exists.

Normal feedstock preparation comes first. Mixing, thermal alloying and any extra refinement can give different compositions meaningful process depth. Exact intermediate forms, machine rows, quantities and durations will be proposed as a complete table after Sc acquisition is checked. Do not retain the obsolete tiny-additive ladder merely by multiplying every row by nine.

### Accepted Working SGA Manufacturing Packet, 2026-10-14

On 2026-10-14 the owner accepted this complete manufacturing packet as working content settings, including input forms, output quantities, power and duration. These are settings to test and tune, not implemented recipes or immutable balance. Use finished metal ingots for Iron, Gold, Cobalt, Aluminium and Scandium. Ingot inputs preserve existing metal finishing without provenance metadata. The basic route uses one full Silicon dust. The checked GT Silicon ingot declaration requires 2273 K, but the revised 3600 K basic alloy requirement means avoiding a hotter preparation threshold is no longer the reason to use dust. This decision does not change ordinary Silicon recipes or permit recycling SGA into Silicon.

All three operations use an EBF and require No Atmosphere, without Microgravity. On 2026-10-14 the owner accepted successive coil tiers for all three routes: Fe-Si at Nichrome with 3600 K, Au-Co at TP Alloy with 4500 K and Al-Sc at HSS-G with 5400 K. This supersedes the shared baseline for Fe-Si and Au-Co. The intended starting progression stage remains HV, with Cupronickel explicitly rejected as too early. Normal GT EBF heat includes a voltage bonus, so these are heat requirements, not new strict checks of coil material. Output is ordinary canonical SGA ingots. These are gameplay settings, not verified physical melting points or an implemented material declaration. Raising recipe heat does not by itself change the shared material's melting point or select a hot-ingot cooling stage. GT material registration and its generated processing must remain coherent with the selected final properties when implemented.

All three accepted recipes use 480 EU/t rather than the earlier 120 EU/t draft, making their base power HV as well as targeting HV starting infrastructure. Voltage does not increase between the routes. Each recipe keeps its independent batch size.

| Accepted working route | Inputs | Output | Base EU/t | Base time | Heat | Thermal EU per SGA |
| --- | --- | --- | ---: | ---: | ---: | ---: |
| Basic Fe-Si | 10 Iron ingots, 1 full Silicon dust | 2 SGA ingots | 480 | 40 s | 3600 K | 192000 |
| Intermediate Au-Co | 5 Gold ingots, 2 Cobalt ingots | 4 SGA ingots | 480 | 80 s | 4500 K | 192000 |
| Al-Sc | 10 Aluminium ingots, 1 Scandium ingot | 11 SGA ingots | 480 | 220 s | 5400 K | 192000 |

The shared 20-second base finishing time per SGA is an intentional comparison baseline. Large output alone does not give Al-Sc a 5.5-times faster furnace than Fe-Si. This does not impose matching batches on upstream recipes or claim identical complete production cost. Existing ingredient preparation, Sc metal finishing, supply, transport and competing consumers remain separate costs. Different recipe heat requirements can also affect GT heat discounts and overclocking. Future adjustments must be identified as tuning changes rather than reopening the composition model.

Fe-Si trades abundant common feed for a high input bill. Au-Co offers lower feedstock volume when those metals are available, without a Sc refinery, but competes with their other uses. Al-Sc gives the best material-equivalence ratio, while paying for aluminium refining, Sc extraction/chemistry and ordinary Sc dust-to-ingot finishing. The existing Sc EBF atmospheric variants therefore remain relevant to metal preparation rather than being skipped by a dust-only alloy recipe.

This accepted three-option manufacturing packet is not evidence that all three are already economically balanced in a running pack. Concrete crater profiles and whole-chain costs still need comparison. Do not append reclaimable slag equal to the apparent input/output deficit, add a fixed reverse composition to canonical SGA, or make the different input routes separate grades. Standard material forms and No Atmosphere processing remain the accepted shared path.

### GT Material Registration And Generated Recipes

Register SGA as a material using GT's normal metal-form and recipe-generation machinery. Processing and recycling require No Atmosphere, including generated recipes such as applicable forming, remelting and scrap recovery. First manufacture alone is insufficient enforcement. There is no Microgravity requirement.

The material generator needs environmental-requirement support that attaches the shared recipe condition to generated SGA operations. Do not implement independent machine-specific checks or one hardcoded SGA exception. Concrete API shape and coverage are implementation questions. This requirement does not change the existing Galaxia-only staging and maintainer-coordination boundary or launch GT work now.

Ordinary form changes preserve canonical SGA amount. Material origin is not retained, so decomposition cannot let the player select gold, cobalt, platinum or scandium as an output. A fixed reverse composition would either erase meaningful feedstock choice or manufacture rare material from the basic route.

The generator requirement concerns material conversion and recycling. It does not by itself specify that every finished equipment-assembly recipe consuming an SGA component inherits No Atmosphere. Those authored consumer recipes need their own selected conditions.

## 6. Optional Residue Processing, Not A Replacement For Composition

Slag and chemical recovery remain useful possible additions. They can represent actual impurities or process byproducts and provide secondary industrial work. The owner's positive response to that idea does not approve the original residue ratios, tiny-metal additions or 80% recovery table.

Keep two quantities distinct: the amount of mechanically equivalent SGA obtained from a composition, and genuine recoverable material in a process residue. The first does not imply the second. For the illustrative 11-input iron batch yielding 2 SGA, there is no automatic entitlement to 9 more SGA through slag recovery.

A future residue route must define what the residue contains, how much canonical output it can actually supply, its reagents and its No Atmosphere processing requirements. Use full dusts. It must not manufacture selected precious metals from a common unidentified residue, nor make weaker feedstock equivalent to advanced feedstock simply by reclaiming an assumed deficit.

The earlier chemical-stage ideas remain brainstorming provenance under Sources. They are not current recipe rows. No new residue identity or recovery machinery is selected merely to preserve an older table.

## 7. Scandium: Real Inspiration, Explicit Content Choice

Al-Sc aerospace use is real. A verified commercial Scalmalloy sheet lists Sc at 0.68-0.84 wt%, with aluminium as the balance and other additions. The original linked paper supports nitric-acid extraction of trace Sc from specially prepared red mud. Neither proves rich lunar deposits, the original large game ratios or a universal space-vacuum requirement. [Nikon datasheet](https://nikon-slm-solutions.com/wp-content/uploads/2024/07/mds5143.pdf), [original paper](https://pmc.ncbi.nlm.nih.gov/articles/PMC8779884/)

In the earlier checked GT snapshot, ordinary bauxite and its audited refinery did not yield Sc. Declared Sc ore forms and generated EBF/freezer support are not themselves an acquisition source. The broader 2026-10-11 audit found one configured existing source in the pack: Blood Magic's Chinfinity meteor includes endstone Scandium ore and consumes a ZPM Circuit Assembler focus plus 80,000,000 life essence. Its actual ore output is weighted and random. This is not an attractive assumed early bulk source. It is also not proof that every other source is absent. [Meteor profile](https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/blob/83b3fb26cd9979e0256c7568bdf8c6f87579b532/config/BloodMagic/meteors/Chinfinity.json#L34-L39), [focus identity](https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/api/enums/MetaTileEntityIDs.java#L703)

The current Monazite/Bastnasite recipe owner and its material pool contain no named Scandium output. Their checked branches produce Samarium and other rare-earth elements. One EV Sifter row makes 2 Samarium plus 1 Gadolinium from 3 Samaric Residue. This is a scoped current-source result, not a claim about the owner's memory of every version. [Actual residue output](https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gtnhlanth/loader/RecipeLoader.java#L1541-L1547)

The configured ore can supply crushed Scandium, impure dust and normal dust. If metal ingots are needed, generated processing uses an EBF row at 120 EU/t, 1,814 K and 90.7 seconds, followed by Vacuum Freezer cooling. These are source-derived generator values, not a live recipe dump. Dust-input alloy recipes do not automatically require a separate ingot-making cycle. The full Blood Magic unlock sequence and absolute earliest access were not established.

| Sc option | What it would add | Advantage | What remains unapproved |
| --- | --- | --- | --- |
| Existing acquisition, if established | Reuse the actual GT or pack supply chain | Avoids inventing a redundant source | Current access gates and whether supply fits this bulk construction route |
| Do not require Sc for Alpha SGA | Select a complete non-Sc advanced composition | Closes the chain without another acquisition dependency | Whether an optional Sc branch is wanted later |
| Industrial residue recovery | New trace-Sc recovery from a named normal refinery residue, leaching, separation and metal preparation | Strong real-world inspiration and a useful industrial byproduct | Feed actually carrying Sc, output scale, exact compounds and interaction with existing GT sources |
| Authored trace mineral companion | Existing normal Sc mineral form as a rare deposit component, with normal processing | Fewer new functional intermediates and no fake bauxite item | Placement, abundance and whether simple processing makes it too easy |

An Al-Sc candidate must use full dusts, ordinary aluminium preparation and the actual selected Sc supply chain. Do not copy the real datasheet's weight percentage into game dust ratios or preserve a tiny-pile recipe from the obsolete draft. The owner's 10 Al plus 1 Sc example is an equivalence illustration, not confirmed real composition. Existing GT Sc processing must not be bypassed by directly emitting finished metal from a new low-tier fluid.

NASA records support trace Sc measured in lunar and meteoritic samples, not a demonstrated exploitable scandium-rich crater. GT's lunar bauxite is already authored game content. Scientific caveats are not a reason to delete existing accepted GT resources. Explain any new concentration and the No Atmosphere rule as deliberate gameplay where evidence does not establish them. [NASA lunar record](https://ntrs.nasa.gov/search.jsp?R=19750003769), [NASA meteorite record](https://ntrs.nasa.gov/search.jsp?R=19640009687)

### Original Al-Sc Sequence Recovered

This is the original developer's source proposal, not current content approval:

| Original step | Original input and output | Machine |
| --- | --- | --- |
| Crush | 1 Unprocessed Scandium-Rich Bauxite -> 1 Crushed Scandium-Rich Bauxite | Macerator |
| Alkali treatment | 2 crushed bauxite + 2 Sodium Hydroxide -> 1 Dirty Scandium-Alumina Mixture | New Vacuum-Rated Pressure Chamber |
| Separate | 6 dirty mixture -> 5 Dirty Alumina + 8 Low-Scandium Red Mud | Sifter |
| Leach | 8 red mud + 1,000 mB Diluted Nitric Acid -> 2 Iron III Oxide + 12 Sodium Hydroxide + 1,000 mB Leached Scandium Solution | Chemical Reactor |
| Recover Sc | 1,000 mB solution -> 1 Poor Scandium Dust + 1,000 mB Diluted Nitric Acid | Sifter |
| Make alloy | 20 Dirty Alumina + 4 Poor Scandium Dust -> 1 SGA + 24 Scandium-Rich Slag | EBF, outside atmosphere |

An alternative alkali row consumed 2 crushed bauxite, 2 Scandium-Rich Slag and 4 Sodium Hydroxide to make 2 dirty mixture. The sequence did not state processing durations. Keep this as provenance, not a recipe set to copy unchanged. Full acid return and alkali coproduct quantities need actual accounting, not automatic acceptance from the cited leaching paper.

### Revised Short-Chain Candidate

This former ordinary Bauxite Slag supply candidate is superseded. The owner selected the crater-fluid branch and accepted the following four-stage skeleton in [[Design Lunar Crater Processing Recipe Chain]]. Exact quantities and machines remain proposals.

| Accepted stage | Inputs | Outputs |
| --- | --- | --- |
| Separate | Enriched Sc-bearing bauxite extraction fluid | Ordinary Bauxite, Sc concentrate and spent carrier |
| Leach | Sc concentrate and Diluted Nitric Acid | Sc solution and mineral residue |
| Precipitate | Sc solution and Sodium Hydroxide | Scandium Oxide and spent solution |
| Reduce | Scandium Oxide and Calcium | Normal Scandium dust and Quicklime |

The concentrate is a functional intermediate rather than a special ore. Carrier cleanup remains a separate branch. The historical table below retains the chemical inspiration but is not an alternative source approval.

### Working Quantitative Sc Recipe Proposal, Needs Tuning

The owner clarified that the recipes and their original order should be retained. The criticism concerns numerical tuning, not rejection of the complete chain. Eight crushed ore plus a Sc-bearing product need not be reduced to a smaller output batch. They can instead require more enriched fluid. The owner's 10000 mB example illustrates that freedom and is not an approved amount. The former rejected-table status and the coordinator's proposed one-mineral-per-operation limit are withdrawn.

All amounts, costs and unspecified mixture compositions remain tunable proposals. The earlier assumption that eight concentrate dust and their solution batch yield two Sc units is a gameplay-yield choice, not a formula-derived composition requirement. Sc-bearing bauxite, concentrate and extraction fluids with no defined formula do not have fixed Chemical Balance coefficients. Do not invent a chemical formula solely to constrain their quantities. Defined compounds such as Sc2O3 and Quicklime must instead follow the applicable solid, fluid and compound rules in [GTNH Chemical Balance](https://wiki.gtnewhorizons.com/wiki/Chemical_Balance).

Recipe batches are independent. Outputs may be accumulated or split before the next operation. Neither small batches nor direct one-operation-to-one-operation quantity matching is required. Select the fluid amount and useful mineral yield together instead of treating one bucket as one mandatory processing unit. The revised numerical proposal below retains the accepted recipe direction. It is not approved tuning, a verified running factory or a new extraction-mode decision.

| Proposed operation | Inputs | Outputs | Machine | Base EU/t | Time |
| --- | --- | --- | --- | ---: | ---: |
| Mineral separation | 16000 mB enriched Sc-bauxite fluid | 8 crushed Bauxite, 1 Sc concentrate dust, 16000 mB spent carrier | Centrifuge | 120 | 40 s |
| Leaching | 12 Sc concentrate dust, 6000 mB Nitric Acid, 3000 mB Water | 9000 mB Sc solution, 10 Stone dust | LCR | 480 | 60 s |
| Precipitation | 9000 mB Sc solution, 18 Sodium Hydroxide dust | 5 Scandium Oxide dust, 9000 mB spent leach solution | Chemical Reactor | 120 | 30 s |
| Calcium reduction option | 5 Scandium Oxide dust, 3 Calcium dust | 2 Scandium dust, 6 Quicklime dust | EBF | 120 | 24 s |
| Direct electrolysis option | 5 Scandium Oxide dust | 2 Scandium dust, 3000 mB Oxygen | Electrolyzer | 120 | 80 s |
| Carrier cleanup | 4000 mB spent carrier | 4000 mB Drilling Fluid | Centrifuge | 30 | 8 s |

The proposed reduction heat is 1814 K as a working game setting, not a demonstrated chemical minimum. Both recovery alternatives retain the same Sc. Existing Quicklime electrolysis can recover Calcium, so reduction's reagent is circulating inventory rather than necessarily a continuing loss. The intended comparison is fewer machines for direct electrolysis versus additional EBF and recycling machinery for lower recovery energy, not artificial metal destruction.

Direct oxide electrolysis uses deliberately authored costs in this proposal. It does not enable an additional cheap default-generated recovery alongside that recipe. Source-derived default generation would instead predict 30 EU/t for 6.5 seconds. No recipe-generator change or choice of these alternative costs is approved merely by this table.

The revised wet-processing batch requires twelve separation operations, consuming 192000 mB enriched fluid and yielding 96 crushed Bauxite plus the twelve concentrate dust used to obtain two Sc dust. This is a proposed yield relationship for undefined mixtures, not a chemical formula or selected final crater abundance. Ordinary Bauxite still requires its normal downstream processing. Carrier quantities must preserve the approximately closed initial loop and later rising losses under the established fracking rule. The independent 4000 mB cleanup runs four times per separator output. The selected dry finite-mining branch bypasses separation and carrier cleanup. Its solid batch remains proposed, while its probabilistic reserve penalty is selected below.

A working dry alternative would yield the same 8 crushed Bauxite and 1 concentrate as this wet-processing batch. These output quantities remain a proposal. On 2026-10-12 the owner selected a 10% chance for a dry operation to consume twice its normal reserve charge, with unchanged output. The remaining 90% use the normal charge. This replaces a fixed 10% extra charge and gives the same expected 1.1 reserve multiplier. Dry mining trades easier startup and less processing for shorter useful site life. Wet mining's accepted advantage is resource efficiency, not guaranteed dominance in every cost comparison. [[Design Lunar Crater Processing Recipe Chain]] owns this setting.

At base recipe settings, direct oxide electrolysis uses 192000 EU per two Sc dust. Proposed calcium reduction uses 57600 EU, and recycling its six Quicklime through three existing 30 EU/t, 56-tick operations adds 5040 EU. The combined recovery cost is 62640 EU, about one third of direct recovery, with more machinery and a circulating Calcium inventory. These are arithmetic comparisons before overclocking, not measured factory throughput or an assertion that every total-chain cost differs by that ratio.

Fluid-hatch and singleblock tank capacities, reagent availability and actual processing throughput need verification before these amounts are implemented. The reagent-recovery loop below is accepted as initial working tuning, not verified final balance. Do not assume perfect nitric-acid or NaOH return. Every proposed machine and number can be redlined as a group.

### Accepted Working Reagent Recovery Loop

The owner accepted this recovery loop and approximately 90% recovery as initial working content settings. These values remain subject to testing and finetuning, not a claim of implemented behavior. [[Design Lunar Crater Processing Recipe Chain]] owns the accepted decision. Lunar SaltWater is the owner's accepted supply input for NaOH. Their concern is upstream energy and local gas availability, not a request to change the established extraction or Sc chemistry stages.

Use one accepted new recovery operation for the undefined spent mixture, then existing GT pure-material chemistry. The first step recovers 27 full Sodium Nitrate dust per refinery batch, compared with the 30 dust corresponding to six acid formula units and six NaOH formula units in the current reagent proposal. This is the accepted working 90% recovery target, not a chemical formula for the contaminated fluid.

| Status | Inputs | Outputs | Machine | Base EU/t | Time |
| --- | --- | --- | --- | ---: | ---: |
| Accepted new recipe, working tuning | 9000 mB spent Sc leach solution | 27 existing BartWorks Sodium Nitrate dust, 6000 mB Water | Distillery | 120 | 90 s |
| Existing GT acid exchange | 10 Sodium Nitrate dust, 1000 mB Sulfuric Acid, selector 1 | 2000 mB Nitric Acid, 7 Sodium Sulfate dust | Chemical Reactor or LCR | 480 | 10 s |
| Existing GT sulfate recovery | 7 Sodium Sulfate dust, 2 Hydrogen cells | 2 Sodium dust, 1000 mB Sulfuric Acid, 2 empty cells | Chemical Reactor or LCR | 30 | 1.5 s |
| Existing GT NaOH recovery | 1 Sodium dust, 1000 mB Water, selector 1 | 3 Sodium Hydroxide dust, 1000 mB Hydrogen | Chemical Reactor or LCR | 30 | 10 s |

The three existing reactions are ordinary GT recipes, not new Sc-specific regeneration shortcuts. Reuse the BartWorks nitrate/sulfate identities consumed by those recipes. Source checks also found a Distillery saltwater recipe with simultaneous solid salt and water outputs, and the map permits that output shape. The accepted spent-solution recipe is still new and untested.

Sulfuric Acid and Hydrogen are startup inventories which circulate. The sulfate recovery uses filled cells and returns empties. Sodium hydration returns Hydrogen gas, so use ordinary cell filling or the existing LCR cell conversion rather than assuming that gas becomes filled cells for free. Include that handling in actual energy and throughput verification.

Over ten refinery batches yielding twenty Sc dust, the proposal consumes 60000 mB Nitric Acid and 180 NaOH dust, then recovers 54000 mB acid and 162 NaOH dust. Makeup is therefore 6000 mB acid and 18 NaOH dust. Average makeup per two Sc dust is 600 mB acid and 1.8 NaOH dust, but no recipe uses fractional dust. Buffered intermediates and whole existing reaction batches produce the aggregate ratio.

This recovers about 90% of both reagents. There is no need for an artificial lower NaOH ceiling when the existing pure-nitrate path can recover both. The three missing nitrate-dust equivalents are treated as unrecoverable discarded contamination in the spent-mixture contract, not an output that can be repeatedly processed. The loss belongs to separating the contaminated mixture, not modified existing pure-material recipes. Water return and exact separation settings remain tunable. Recovery consumes EU and machinery, and is not proven to minimize total energy across every fresh-acid route.

Existing GT also has an LCR recipe using 3000 mB Hydrogen, 1000 mB Nitrogen and 4000 mB Oxygen to make 1000 mB Nitric Acid and 1000 mB Water at 480 EU/t for 16 s. It avoids a separately produced ammonia intermediate, but does not establish local lunar Nitrogen availability. The ammonia-input acid recipe is 30 EU/t for 16 s, before the cost of producing its feedstock. Do not equate the acid operation's own EU/t with the complete supply-chain cost. This proposal reduces replacement nitrogen supply without inventing a lunar atmosphere.

The consumer follow-up found no important authored Sc ingredient in the checked GT/CoreMod recipes. Remaining positive references cover forms, storage/display and conditional generic plasma-fuel handling. The owner therefore no longer treats the incidental meteor focus as a required progression gate for newly authored Sc supply. This does not certify all-mod absence.

Normal GT bauxite processing already creates Aluminium Oxide and Bauxite Slag. The parent checked both graph source and current immutable upstream code. This is a stronger concrete reuse point than assuming every red-mud-named fluid is interchangeable. Sc recovery from it would be a NEW recipe, not an existing property of the slag. [Actual residue producer and current centrifuge option](https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/loaders/postload/chains/BauxiteRefineChain.java#L55-L80)

| Proposed step | Proposed input and output roles | Machine candidate |
| --- | --- | --- |
| Existing upstream | Ordinary Bauxite -> normal Aluminium Oxide and Bauxite Slag through unchanged refining | Existing GT line |
| Sc leaching | Bauxite Slag + Diluted Nitric Acid -> Leached Scandium Solution and ordinary mineral coproducts | Chemical Reactor, or LCR if selected coproducts require it |
| Concentrate preparation | Leached Scandium Solution + Sodium Hydroxide -> full Scandium Oxide dust and spent leaching solution | Chemical Reactor |
| Reduction | Scandium Oxide dust + Calcium dust -> normal Scandium dust and existing Quicklime dust | EBF |
| Alloy manufacture | Normally refined Aluminium dust + Scandium dust -> canonical SGA at the selected equivalence ratio | EBF, No Atmosphere |

There are three new Sc-refining operations, not a new pressure machine or an entire parallel aluminium refinery. Scandium Oxide and the solution states are proposed functional intermediates. No existing Sc oxide, chloride or nitrate identity was found in the bounded GT/CoreMod reuse check. Precipitation and preparation are intentionally compressed into one proposed gameplay operation, not represented as a verified industrial procedure. The calcium finishing row is an authored reduction candidate whose full accounting still needs recipe design.

The ordinary bauxite-to-aluminium path stays unchanged. SGA uses normally refined metal, not Dirty Alumina as a direct substitute. Do not return the original Bauxite Slag unchanged after Sc extraction, which would permit repeatedly extracting Sc from the same material. Retained titanium-bearing and other coproduct quantities need an explicit balance alongside the new recovery option.

This uses full dusts and retains the original residue-leaching inspiration without origin-only ore variants. Optional partial reagent recovery can be added if useful. It is independent of the approximately closed initial Drilling Fluid loop, and no perfect nitric-acid recovery is selected.

Using ordinary Bauxite Slag also creates a Sc source for bauxite refined outside Luna. The owner subsequently selected crater-exclusive primary Galaxia supply, rejecting this broad acquisition option. The table above is historical chemical inspiration, not a current source proposal. Adapt any retained chemical stages to selected crater feedstock rather than adding origin metadata to ordinary bauxite. Crater abundance, processing cost and useful competing demand remain open. The existing late Blood Magic source is explicitly retained.

### Existing Crater Parameter Model

The owner recalled an already recorded generation design. It is preserved under Review Crater Nodes Proposal rather than replaced by this report's examples. The older replaceable tuning model has three size classes, per-destination class weights, normal diameter distributions and per-profile weights for each class. Working lunar mean diameters are about 1, 3 and 8 chunks, not fixed bounds.

Every profile has a reserve multiplier and a size-response value. Realized diameter relative to its originating class mean modifies richness through that response. Different profiles can amplify, dampen or reverse the size effect. The initial reserve is shared, and each ordinary-mining operation claims its batch from it. All fracking machines claim successive steps of the same crater history.

The 2026-10-11 profile-dependent fracking-cost direction fits this model. Concrete output batches, reserve numbers, standard deviations and loss curves are not resolved merely because the model exists. Distinguish reserve exhaustion from increasing fluid cost in the subsequent unlimited stage.

## 8. Fracking Deterioration And Relocation

Start from the profile's normal mineral output per operation and usable yield after ordinary refining. Then choose a fixed recovered-carrier amount, zero or slight initial makeup, and profile-dependent growth in makeup demand. Operating-hour estimates are a consequence, not the first balance target.

One simple proposed accounting form is q_p(n) = R_p + L_p + G_p(n). R_p is recovered carrier, L_p is zero or small initial loss, and G_p is increasing loss for profile p with G_p(0) = 0. This is an illustration, not a selected implementation formula. It works with a perfectly closed start and does not multiply zero initial loss by a growth factor, which would remain zero forever.

The owner accepts gentler growth for common iron and faster growth for valuable platinum. Resource value, normal refining and expected usable output are authored balance inputs. No runtime market-price system is needed or selected. Do not automatically charge every ore the same slope simply because machines share one operation duration.

On 2026-10-14 the owner accepted the linear profile-dependent growth packet below as working tuning. Square-root and logarithmic shapes are no longer active alternatives for these four profiles. Do not reuse the obsolete 25%-loss example as the selected initial condition.

Several machines advance shared production history faster. They do not receive independent cheap starts. Parallel claimed operations pay their successive cost steps. Extra input stays unrecovered loss while enriched output and mineral yield per operation stay fixed. No NBT concentration grades or output-decay system is added.

### Accepted Working Initial Reserve And Linear Fracking Costs, 2026-10-14

On 2026-10-14 the owner accepted these nominal initial reserves and linear fracking costs as working tuning, with an added approximately plus or minus 10% variation in each crater's initial finite reserve. These are content settings to test, not implemented behavior or demonstrated final balance. Measure reserves in reference portions equal to the mineral output from one accepted 16000 mB separation batch. This is a balance scale, not a requirement that every extractor and downstream recipe use matching operation sizes. The dry Sc double-charge rule affects consumed reserve portions without changing its solid output.

| Accepted working profile | Small nominal reserve | Medium nominal reserve | Large nominal reserve |
| --- | ---: | ---: | ---: |
| Iron-silica | 2000 portions | 6000 portions | 16000 portions |
| Gold-cobalt | 1000 portions | 3000 portions | 8000 portions |
| Sc-bearing bauxite | 500 portions | 1500 portions | 4000 portions |
| Platinum-bearing | 250 portions | 750 portions | 2000 portions |

These are reference reserves at each originating class's mean diameter. The retained per-profile richness response modifies the nominal reserve for actual generated diameter. Apply the additional bounded 0.9 to 1.1 reserve multiplier once when the deposit is created, after that size/profile calculation. The final initial reserve belongs to the shared crater, not each machine. Do not reroll it on extractor binding, replacement, scanning or reload. This variation changes the finite initial reserve, not output per portion, composition or fracking growth. At the mean-diameter reference, Small iron ranges from 1800 to 2200 portions and Small platinum from 225 to 275 portions. The size-related effect can separately shift those reference ranges. Richness coefficients and numeric occurrence weights remain open. These quantities do not select operating lifetimes or a maximum number of extractors. Normal refining still applies.

The selected working model starts with a perfectly closed carrier loop after supplying startup inventory, followed by linear increase in underground fluid loss. For each reference portion, enriched output remains 16000 mB and recovered usable carrier remains 16000 mB. Exact cleanup machine settings remain separate. Only input rises with cumulative shared fracking production. Growth is not exponential and has no cutoff or reset when an extractor is replaced. Initial reserve depletion does not itself advance the later fracking history.

| Accepted working profile | Shared fracking portions until input reaches 32000 mB | Input after 1000 preceding fracking portions |
| --- | ---: | ---: |
| Iron-silica | 8000 | 18000 mB |
| Gold-cobalt | 4000 | 20000 mB |
| Sc-bearing bauxite | 2000 | 24000 mB |
| Platinum-bearing | 1000 | 32000 mB |

At that doubling point, half the input returns and 16000 mB per portion needs replacement. These costs describe the next reference portion after the stated cumulative production, not the cumulative average input. Multiple extractors accelerate the same history and still receive their successive cost steps. This packet does not prove the acceptable cost of fresh carrier, machine tank capacity, whole-chain energy or relocation logistics. Select and measure extractor settings when testing the content rather than asserting a site lifetime from these reference counts.

### Lunar Occurrence Weights Proposal, 2026-10-14

The next packet proposes relative generation frequencies. These percentages describe selection among generated craters, not crater density, a guarantee about surveyed terrain or a quota in each region. It does not alter mean diameters, overlapping distributions or profile-based richness.

Proposed class weights are 70% Small, 25% Medium and 5% Large. Within each selected class, use the following proposed profile weights. Profile weights total 100% within each class, and every profile stays eligible in every class.

| Proposed profile | Small | Medium | Large |
| --- | ---: | ---: | ---: |
| Iron-silica | 70% | 60% | 50% |
| Gold-cobalt | 18% | 20% | 20% |
| Sc-bearing bauxite | 10% | 16% | 25% |
| Platinum-bearing | 2% | 4% | 5% |

This keeps small common-resource sites frequent and gives larger finds a greater chance of Sc or Pt without locking either resource to large craters. The resulting marginal profile probabilities are 66.5% iron-silica, 18.6% gold-cobalt, 12.25% Sc-bearing bauxite and 2.65% platinum. These remain proposals, not accepted placement or demonstrated exploration cost. Overall spatial generation density and transport access still affect practical scarcity.

## Situational Route Comparison

This comparison follows the owner's 2026-10-11 correction. The higher equivalent-output recipe must not be assumed to be the cheapest overall. A good proposal should identify a credible supply or infrastructure situation in which each composition is preferred. It does not require every player to manufacture SGA through every route.

| Sc supply candidate | Potential advantage | Failure mode to check |
| --- | --- | --- |
| Scarce lunar Sc or a low-yield coproduct, with useful competing consumers | Early access without plentiful supply. The player allocates Sc between bulk construction and other useful hardware | Cheap scalable refinery waste can remove scarcity. Other uses alone may only make the player build more extractors |
| Sc on a later destination | Adds an exploration and logistics reason to establish other compositions first | Once the destination is reached, Al-Sc may replace everything anyway. Unlock order does not preserve long-term alternatives |
| Broad feedstock access with demanding ongoing processing | No geographic lock, but material return trades against real reagent, energy and capacity costs | A long chain may become cheap after automation. Extra steps are not enough unless their recurring cost or throughput matters |

These are alternatives to evaluate, not selected gates. A limited combination may fit the eventual resource model, but do not accumulate every restriction by default.

For the basic route, abundant iron and silicon can make low equivalent output acceptable. The intermediate route needs an actual Au/Co supply advantage or a selected processing advantage, since precious inputs can outweigh its better ratio. Al-Sc can save common feedstock but should face a meaningful Sc acquisition or allocation cost. Prove those situations using concrete profile outputs and actual selected recipes rather than assigning attractive labels to uneconomic routes.

Using only the owner's illustrative ratios, equal processing overhead and equal unit acquisition costs for Fe, Si and Al, Fe/Si costs 5.5 common units per SGA. Al/Sc matches it even when one Sc unit costs 50.5 common units. This is a relative-effort example, not a game currency or accepted ratio. Mild Sc rarity can leave the advanced composition dominant. With the same equal common assumptions for Co, Au/Co ties Fe/Si when one Au unit costs 4 common units. Actual operating, transport and allocation costs change these thresholds.

Identical time and energy per batch would also give the eleven-output composition 5.5 times the basic route's throughput and 2.75 times the medium route's throughput. Do not copy identical processing settings into every row and assume the material ratios alone create useful alternatives. These are comparison warnings, not selected penalties or machine tiers.

### Real Industrial Uses And Candidate Competing Demand

Primary sources support several distinct applications. These are not existing GT recipes or selected Galaxia components:

| Actual application | Form and role | Evidence status | Possible Galaxia role |
| --- | --- | --- | --- |
| Lightweight structural alloys | Metallic Sc addition in aluminium alloy | Commercial material specifications | Optional lightweight reinforcement or later structural hardware, not a replacement for tier-specific metals |
| RF device manufacture | High-purity Al-Sc sputtering targets consumed while depositing device films | Commercial manufacturer shipments | Later communication or sensing hardware |
| Solid-oxide cell electrolyte ceramics | Sc2O3 dopant in zirconia, providing oxygen-ion conductivity | Commercial principal use and supplier formulation | Ceramic component for selected power or electrolysis equipment, if that equipment is actually in scope |
| Ultrafast laser hosts | Sc-containing oxide host with a separate active Yb dopant | Demonstrated original research, not assumed mass-market production | Possible later optical/scanning component, not a mandatory Alpha chain |
| High-intensity lamps | Sc iodide additive in mercury-vapour lamps | Established application described by RSC | Possible specialty lighting, probably weak bulk demand on its own |

The parent verified current RF-target manufacturer and electrolyte-supplier pages independently. A device's Sc content is generally an installed component, not fuel continuously burned during operation. Target material is consumed during manufacturing. Do not force constant Sc consumption into operating hardware just to create a sink. [RF target supplier](https://www.materion.com/en/insights/blog/materions-aluminum-scandium-sputtering-targets-power-rf-mobile-and-broadband-devices), [ceramic formulation](https://infinitamaterials.com/material/scandia-stabilized-zirconia-alumina/), [laser-host research](https://link.springer.com/article/10.1007/s00340-013-5433-2), [RSC element applications](https://periodic-table.rsc.org/element/21/Scandium)

The coordinator's leading candidate uses are advanced RF hardware and useful oxide ceramics. They need a real equipment consumer before recipes are selected. They do not replace the accepted early SiGe controls, create an obligatory new Alpha generator, or make every technology consume Sc. The oxide intermediate could branch into ceramics, while reduced metal supplies SGA and RF-target manufacture. This makes the refinery serve more than a single bulk-alloy recipe without inventing provenance variants.

The owner subsequently accepted RF Resonator for upgraded Communication Satellites and Laser Crystal for upgraded Prospecting Satellites as the first component-design direction. Their exact compositions, benefits and recipes remain open. Already accepted first-satellite recipes stay unchanged without Sc. Scientifically inspired functions are sufficient, and a complete thin-film or laser-industry simulation is not required.

The owner wants further meaningful Sc uses, including recipes outside Galaxia-specific content. These two parts are a starting point rather than a permanent cap. Broader proposals must identify actual benefits and demand, and retain the current GT staging and maintainer-coordination boundary. The direction is not blanket approval to alter existing GT progression recipes.

Candidate future uses include reusing the same RF and optical parts in non-Galaxia equipment, a Sc-containing ceramic for selected high-temperature or electrochemical hardware, and an Al-Sc structural option with a concrete mechanical benefit. These are comparison candidates, not approved extra items, generators or replacements for tiered materials. Broader use should not require a separate Sc-specific intermediate for every consumer.

Demand must be compared at actual gameplay scale. A handful of occasional hardware crafts will not necessarily compete with a mass-construction line. Likewise extra uses do not create scarcity when their supply scales cheaply. Research supports candidate functions, not automatic balance.

### Oxidation And Possible Environmental Requirements

RSC describes metallic Sc as tarnishing in air, burning easily and reacting with water. The parent verified that readable element page. This supports concern about protecting fresh metal and hot processing. It does not establish that every solid sample spontaneously ignites, or that every Sc compound is similarly reactive. Powder-specific rates and surface-passivation behavior are not established by that short description. [Element properties](https://periodic-table.rsc.org/element/21/Scandium)

The coordinator proposes considering No Atmosphere for final reduction to metal, hot-metal handling and high-purity deposition, not blanket gating of aqueous leaching, stable oxide preparation, cold machining or installed equipment. These remain owner choices, not new accepted tags or recipe rows. Protective inert gas is another physical approach. Choosing vacuum as the game condition does not claim that terrestrial manufacturing is impossible.

The selected No Atmosphere requirement on SGA itself remains unchanged. New Sc restrictions must be justified separately. They can influence factory location and logistics, but do not by themselves prove that Al-Sc has a meaningful recurring disadvantage when the player already manufactures SGA in vacuum.

### Owner's Sc Blast-Processing Variant Example

The owner proposed an alternative to blocking the Sc operation outright: identical blast-processing feed produces pure metal output in No Atmosphere, but mixed metal and oxide output in atmosphere. The oxide can be electrolyzed back to normal Sc dust. The coordinator treats the spoken ABF as the existing Sc EBF context. The proposal does not change the mandatory No Atmosphere condition for SGA.

This supplies a different gameplay tradeoff: an atmospheric factory can still obtain Sc metal but must fund recovery and additional throughput. A vacuum factory avoids that extra loop. Sc itself is retained, not destroyed. Exact output split, electrolysis yield, energy and duration remain undecided.

If the owner selects an oxide-consuming optical or ceramic branch, the atmospheric coproduct can also be used directly instead of always being recycled. This may make mixed-output production useful for a different equipment demand, rather than making atmosphere only a universal penalty. Those consumers and their quantities still need selection.

For an illustrative Sc2O3-style accounting convention, a five-unit Sc dust batch could yield five metal units in vacuum, or three metal units plus five oxide-dust units representing the remaining two Sc units in atmosphere. Electrolysis of that oxide batch would return two Sc dust plus its oxygen content. The existing Sc blast recipe produces hot ingots at its required temperature, so these metal outputs should retain the normal cooling stage rather than silently become finished ingots. This is an internally stated example, not a registered GT recipe or approved material unit definition. Match actual generated recipes when implementation begins. Do not casually equate one oxide dust with one Sc dust.

GT feasibility research compares independent tagged recipes with dynamic recipe parameters. Duplicate-input registration, candidate filtering, cache and operation snapshot behavior need evidence before implementation. No runtime change or new behavior for the approved absent-Galaxia development case is selected by this proposal.

The initial 2026-10-11 read-only pass recommended two ordinary static recipe definitions as the least-change representation for fixed inputs and different outputs. The owner subsequently rejected independent colliding registrations and selected a first-class family in [[Design Lunar Crater Processing Recipe Chain]]. That accepted direction supersedes the earlier recommendation. GT's existing multi-candidate storage and query predicate remain reuse evidence. Basic-machine selection, dual-input caches, recipe locks/restoration and retained-operation requirements still need coherent handling. Changing outputs only after consumption is too late for the existing output guards. This does not expand the current Galaxia-only implementation task.

The owner's follow-up clarifies a stronger desired model: one indexed common input signature leads to a recipe family, then the machine chooses an immutable output profile from that subset using environmental facts. This is not late dynamic output replacement. Follow-up research separates the existing shared lookup leaf containing ordinary recipes from an explicit first-class family with common input validation. Top-level display entries, stored output profiles and input-index paths are different counts. Do not infer a full-map scan or inevitable lag solely from the number of registered recipe objects.

The current `2856a652b29ecf17dd5529880d589bea92a83b9f` source confirms that GT reuses the same ordered normalized input path and keeps additional candidates at its terminal node. This is not a full-map scan. Aliases and frequency-based ordering can create more than one physical path for a logical input signature, so an existing leaf is not automatically a canonical semantic family. The backend's 256 hash-cache slots each retain one recipe hint, not a family. The parent independently verified those insertion and cache excerpts. [Existing shared lookup path](https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/api/recipe/lookup/GTRecipeLookup.java#L43-L107)

A first-class family can own and validate common inputs once, then choose among its small profile set. Keep that responsibility in the existing GT recipe/backend/lookup owners. It is a materially larger native data-model and interface change than admitting ordinary variants, because query results, cache, category discovery and saved locks currently refer to GTRecipe. Processing can still receive a complete frozen ordinary effective recipe before output protection and consumption. There is no reason to duplicate GT indexing or replace its execution engine.

The owner subsequently selected family-level recipe locks and omission of Galaxia-dependent environmental variants during GT-only development without Galaxia. Families with no remaining variants are omitted from registration and NEI. No substitute outcome or mandatory development default is needed. These accepted decisions are maintained in [[Design Lunar Crater Processing Recipe Chain]], not in the earlier unreviewed feasibility recommendations.

Runtime lookup, registration/rebuild, memory and NEI are separate costs. A family still needs its different output data. NEI may still expose every profile. No benchmark established a measurable speedup or slowdown, and no universal logarithmic or constant bound based solely on recipe count is claimed. For a located fixed-input family, the desired extra work is local profile selection, not checking every recipe in the map.

## 9. Factory Power, Capacity And Startup

On 2026-10-11 the owner deferred voltage, duration, transported charge and throughput tuning to the actual chosen recipes. The former 129,048 EU operation estimate and roughly 198-operation battery example depended on obsolete recovery settings. They are not current targets.

Measure extraction, carrier processing, ordinary refining and alloy manufacture together once recipe rows exist. Shared machines may become throughput bottlenecks. Buffers cannot repair a sustained capacity deficit. Higher-voltage stages need an appropriate power arrangement rather than assuming an HV buffer directly supplies every machine.

Existing HV lithium batteries have a verified nominal 1.6 million EU capacity. This fact does not determine how many batteries the revised factory needs. Charge logistics remain necessary under the provisionally accepted transported-power bootstrap.

Startup needs full committed carrier input and working inventory, not merely net makeup. Several machines can commit fluid before the recovery batch returns. Keep machine and tank capacity proportional to that pipeline. No numerical base-capacity choice is made here.

Standard steam turbines are non-combustion, but a fuel-burning boiler is a different upstream machine. Their existence does not establish a selected continuous space-power solution or justify bypassing the space combustion ban. Batteries remain the approved provisional first route.

## 10. Concrete Construction Uses

Give the bulk material an actual outlet without putting it in the first Station bootstrap. The existing Galaxia registry contains `SPACE_STATION_BLOCK` and `SPACE_STATION_PANEL`. The coordinator checked those entries in `GalaxiaBlocksEnum` at Galaxia `a9128e9ef21ff05254648190b4f79f94bdc9669d`. Registration is not evidence of the following recipes or of an existing price to compare against.

| Proposed recipe | Machine | EU/t | Time | Environment |
| --- | --- | ---: | ---: | --- |
| 1 SGA ingot -> 1 SGA plate | Generated Bender candidate | Open | Open | No Atmosphere |
| 8 SGA plates + 4 Steel rods -> 4 existing Space Station Blocks | Assembler | 120 | 10 s | Any |
| 4 SGA plates + 2 Steel rods -> 8 existing Space Station Panels | Assembler | 120 | 10 s | Any |

These are proposed alternative bulk recipes, not replacement bootstrap recipes. The first kit and its expansion stock retain a non-SGA route. Steel rods keep their ordinary recipe. The owner selected GT material registration and generated basic processing, which supersedes the earlier standalone-ingot and hand-added-plate approach. Four blocks and eight panels are independent working batches, not ratios forced by the previous output.

At this proposed wall recipe, 1,000 Space Station Blocks consume 2,000 SGA ingots and 1,000 Steel rods. Composition and full-dust quantities determine the upstream material bill once accepted. The old tiny-additive comparisons no longer apply. Panels have a different consumption rate and should be compared against their actual building use, not treated as the same wall block.

These quantities still need gameplay balance against real existing recipes, inventories and intended Station sizes. Calling SGA a bulk filler does not justify making it mandatory for every controller, satellite or Rocket part.

## 11. Boundaries To Preserve

- Canonical SGA and unidentified common slag must never yield a player's choice of Au, Co, Pt or Sc. Otherwise the iron route can manufacture precious metals through reverse recipes.
- Lower equivalent output is not an entitlement to recover the input/output count difference as more SGA. Genuine process residues require separate accounting.
- Recovery cannot return the same recoverable slag again alongside a full recovered output. No repeated accounting of one batch.
- GT autogenerated melting or decomposition must not turn unfinished powder into usable SGA without the required production environment or convert shared material into a chosen rare component.
- Generated SGA processing and recycling must carry No Atmosphere. Existing finished material is not a ground-processing exception.
- Normal extraction feedstock does not mean finished metal. Keep ore conversion, cobalt reduction, platinum powder/refining, aluminium reduction and titanium processing intact.
- Do not expand the independent recipe-environment implementation task to generator restrictions or lunar content without a separate scope agreement.
- Do not add a custom pressure chamber, three SGA grades, default save migrations or a new research minigame to make these recipes work.
- Preserve the first Station bootstrap. Replacing all ground-made Station construction recipes with lunar SGA would create a circular prerequisite. Bulk SGA should offer later construction value without invalidating the initial kit.

## 12. One Review Packet For The Owner

The owner can redline the complete tables or answer these choices together:

1. Select actual independent composition recipes and equivalent-output ratios. The composition-first principle is settled, not another vote on the old recovery ladder.
2. Review verified existing Sc acquisition before selecting Al-Sc or proposing a new source.
3. Select normal mineral outputs per operation and their refining yields for the accepted lunar profile direction.
4. Select processing rows with approximately closed initial recovery around the provisionally accepted Drilling Fluid carrier.
5. Tune profile-specific deterioration after outputs are known. Iron should grow more gently than platinum. A curve or site lifetime is not selected.
6. Select actual space-construction consumer recipes and measure their complete material, power and capacity demands. The ordinary GT material-generation direction and atmosphere-free SGA processing are settled.

These are coherent content choices, not requests to select every isolated duration or voltage. Numeric tuning can be revised as a group and measured when implementation begins.

## Evidence And Completion Limits

Key code facts were checked in GT at `bc7a940f5e6583b5c79d049635d1586c8f4ad764`, CoreMod at `9aa0afc8711f3efbe3afc0d11ec44dcbf5b87442`, and the existing local drilling-fluid source at `2259bc64244f9f7fc58e039d8e89ca40dd17c929`. The coordinator independently checked the Drilling Fluid source, current Sc definition, CoreMod aluminium reductions, recovered original citation links and the original PMC paper. Formula and batch arithmetic were also checked independently.

Sources support the stated bounded facts, not exhaustive pack access or playable performance. No new recipe registration, full factory build, Horizons QA, game test or scientific validation of the fictional alloy recipes was performed. The revised equivalent-output illustrations are not implemented recipes. The Sc acquisition audit checked current GT `03f76356146f497c6c8f21d9225fe28de57136a1`, pack `83b3fb26cd9979e0256c7568bdf8c6f87579b532` and Blood Magic `10a36f6413b8a7ce6ebf16ca8b04614ff15566cd`. Detailed intake remains under Sources. Source discovery does not select the advanced composition or its supply policy.

The earlier Codebase Memory publication failure was repaired by deleting and rebuilding only the GT index. Rebuild, repeated indexing, search, snippet and trace checks passed. The custom server executable was not updated. That infrastructure recovery is not evidence that the recipe proposals work in game.

The report and supporting research remain local and uncommitted. No GitHub publication or GT production-source change was performed.
