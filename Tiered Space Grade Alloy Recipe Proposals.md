---
type: source
status: unreviewed
tags:
  - galaxia/alpha
  - wayfinder/source
---

# Tiered Space Grade Alloy Recipe Proposals

Source: AFK agent brainstorming
Imported: 2026-10-10

## Source Snapshot

This is an AFK proposal for a broad owner redline, not accepted content or an implementation plan. The latest request replaces the earlier equal-yield alloy recipes with a simple low-yield route, a more involved medium-yield route and an advanced highest-yield route. Iron is the working low-route direction. Gold and cobalt are the working medium idea. The high route is unresolved. No aluminium-scandium recipe is selected here.

All newly proposed compositions, reactions, yields, powers and durations are fictional gameplay choices. They are not verified industrial chemistry. Existing GT materials and upstream processes stay authoritative. In particular, gold, cobalt, platinum and aluminium inputs to new alloy recipes are finished metal obtained through legitimate normal recipes, not metal extracted directly by a new low-tier fluid recipe.

The recommendation is Approach B, a common iron-based batch with progressively better residue reclamation. Approach A is a genuinely different alternative that rewards metal substitution and powder compaction. Neither makes SGA a technology-tier gate. A player may keep the low route indefinitely. All routes produce the same canonical Space-Grade Alloy ingot and require No Atmosphere whenever they produce finished SGA. They require no gravity condition. An artificial vacuum chamber on an atmospheric world does not satisfy that environmental rule.

### Accepted Rules Preserved

- One Crater Extractor first mines one shared finite ordinary reserve. Only after exhaustion does that same machine frack when supplied with fluid.
- Any number of extractors share reserve and fracking history. Fluid cannot bypass ordinary exhaustion, and new machines do not reset history.
- Each fracking operation produces the same fixed volume of its enriched fluid. Carrier input rises with shared operation history, so older sites create greater ongoing supply burden.
- Each enriched subtype has a separate Fluid ID. The deposit system has no permanent three-profile or four-profile cap.
- Downstream recipes use ordinary GT machines and maps. Only the accepted extractor is custom machinery.
- Carrier recovery is partial. No recipe closes the drilling-fluid loop, recovers all scarce promoters or generates free replacement ingredients.
- Ordinary titanium processing remains unchanged. Titanium-bearing deposits must provide normal mineral feedstock, not a low-tier route to finished titanium. No SGA recipe here uses or replaces a titanium progression gate.
- No Rough Asteroidal Gold, Natural Asteroidal Cobalt, Scandium-Rich Bauxite, custom pressure chamber or provenance-only raw item is introduced.

The accepted rules were checked against Agent Briefing.md, Review Crater Nodes Proposal.md and Design Lunar Crater Processing Recipe Chain.md. Machinery and temporary GT-content ownership remain as recorded in Define Alpha Research and Production Floor.md and Design Early Orbital Production Recipe Chain.md. This intake does not change their decisions.

## Shared Extraction And Carrier Chain

### Existing Carrier Production

The parent supplied a verified GT recipe from local GT5 revision `2259bc64244f9f7fc58e039d8e89ca40dd17c929`:

| Existing recipe | Inputs | Outputs | Machine | EU/t | Base time |
| --- | --- | --- | --- | ---: | ---: |
| Drilling Fluid | 5 water cells + 1 stone dust + 20 mB lubricant | 5,000 mB Drilling Fluid + 5 empty cells | Mixer | 15 | 64 ticks, 3.2 s |

Use this existing fluid and recipe. Its stone, lubricant and cell inputs remain ordinary GT supplies. Ordinary crater mining needs none of them, so the lunar bootstrap does not require fracking, precious metals or SGA in advance. Drilling Fluid can be manufactured on the starting world and transported. There is no new lunar carrier recipe.

### Proposed Normal Deposit Examples

These are authored content examples, not a claim that these exact vein compositions already occur on Luna. Every solid is an ordinary GT ore-processing form. Matching fluid names distinguish normal deposit contents, not invented origin-specific ores.

| Example deposit | Proposed solid batch, shared by ordinary mining and enriched-fluid separation | Role |
| --- | --- | --- |
| Iron and silica | 8 crushed banded iron ore + 2 silicon dioxide dust | Cheap construction-metal and silicon supply |
| Gold and cobalt | 6 crushed cobaltite ore + 2 crushed gold ore | Normal cobalt and gold supply, including small medium-route consumables |
| Platinum-bearing | 4 crushed platinum ore + 4 crushed iron ore | Normal platinum feedstock and a useful bulk-metal companion |
| Bauxite-bearing | 8 crushed bauxite ore + 2 silicon dioxide dust | Normal aluminium supply and the optional substitution route |

Keep the ordinary GT refining and smelting steps after these raw outputs. Ore output quantities, composition, frequency and ordinary-reserve size remain proposals. Other normal deposits can be added. The examples do not guarantee rare-material access before the normal refining machinery, and material occurrence itself still needs progression review.

| PROPOSED process | Input | Output | Machine | EU/t | Time | Condition |
| --- | --- | --- | --- | ---: | ---: | --- |
| Ordinary mining | One shared finite reserve batch, no drilling fluid | The deposit's ordinary solid batch above | Crater Extractor | 120 | 30 s | Bound crater, ordinary reserve remains |
| Fracking | q(n) Drilling Fluid | Fixed 1,000 mB deposit-specific enriched fluid | Same Crater Extractor | 120 | 30 s | Ordinary reserve exhausted, shared history n |
| Mineral separation | 1,000 mB enriched fluid | The corresponding ordinary solid batch + 800 mB shared Spent Drilling Fluid | Centrifuge | 120 | 20 s | Any environment |
| Optional carrier cleanup | 1,600 mB Spent Drilling Fluid | 1,500 mB existing Drilling Fluid | Centrifuge | 30 | 30 s | Any environment |

Extra fracking input is lost underground rather than increasing enriched output. Mineral separation and cleanup also retain losses. Cleanup has no stone-dust output. That avoids presenting drilling-fluid solids as an endlessly replenished replacement feedstock. Cleanup represents removing unusable contamination, with the discarded portion abstracted rather than packaged as another custom waste item.

### Carrier Arithmetic Shared By Both Approaches

Two proposed baseline operations at q = 1,000 consume 2,000 carrier. Separation produces 1,600 spent fluid, and cleanup returns 1,500 reusable carrier. Fresh makeup is 500 for two operations, or 250 per operation. At q = 1,250, average makeup becomes 500 per operation. A 25% rise in gross carrier input therefore doubles fresh-fluid demand. At q = 2,000, makeup becomes 1,250 per operation.

Average fresh makeup is q(n) minus 750 per fracking operation with full cleanup. A fixed numerical curve is not selected. Tune the growing net replacement burden, not just the gross-fluid percentage. Unlimited fracking does not itself require an unbounded curve, and no operation-count relocation threshold is approved.

At q = 1,000, 100 fracking operations require 25,000 mB ongoing fresh makeup. Five existing Mixer runs supply it using 25 water cells, 5 stone dust and 100 mB lubricant, returning 25 empty cells. This excludes the initial circulating fluid inventory. Average makeup ingredient burden is 250 mB water-equivalent, 0.05 stone dust and 1 mB lubricant per operation. Ingredient manufacturing and transport have their own costs.

The proposed extractor, separator and half a cleanup operation consume 129,000 EU per fracking operation before overclocking. The proportional fresh Mixer share adds only 48 EU at baseline makeup. This excludes water-cell handling, lubricant production, ore refining and all SGA production. These are arithmetic checks, not measured factory power.

## Approach A: Substitute Metals And Improve Powder Processing

This approach rewards different material supplies. Iron gives the shortest low-yield recipe. Gold and cobalt change the medium composition. Aluminium is an optional advanced feedstock, with compaction and shared residue reclamation improving its return. Switching feedstocks is a real logistics decision, not three names for the same ore.

Use finished metals for the new recipe inputs. Where dust or tiny dust is required, ordinary maceration and dust-size conversion prepare it from legitimate finished metal. Do not use these preparation operations to sidestep normal cobalt or aluminium smelting.

Three new functional intermediates are proposed: Construction Alloy Powder, Green Construction Compact and Construction Alloy Dross. Powder is mixed metal feedstock. One compact holds four powder units for low-loss sintering. Dross is a recoverable but contaminated side stream, not a final alloy form or an ore named by origin. A later Recovery Solution is the acid-reclamation fluid described below.

| Route | PROPOSED operation | Inputs | Outputs | Machine | EU/t | Time | Condition |
| --- | --- | --- | --- | --- | ---: | ---: | --- |
| Low | Direct alloying | 10 iron ingots + 2 silicon ingots | 6 SGA ingots + 6 Construction Alloy Dross | EBF, 1,800 K | 120 | 30 s | No Atmosphere |
| Medium | Powder mixing | 9 iron dust + 2 cobalt dust + 8 tiny silicon dust + 1 tiny gold dust | 12 Construction Alloy Powder | Mixer | 120 | 15 s | Any |
| Medium | Powder alloying | 12 Construction Alloy Powder | 9 SGA ingots + 3 Construction Alloy Dross | EBF, 1,800 K | 480 | 45 s | No Atmosphere |
| Advanced | Alternative powder mixing | 9 aluminium dust + 2 cobalt dust + 1 silicon dust | 12 of the same Construction Alloy Powder | Mixer | 120 | 15 s | Any |
| Advanced | Compaction | 4 Construction Alloy Powder | 1 Green Construction Compact | Compressor | 120 | 10 s | Any |
| Advanced | Low-loss sintering | 3 Green Construction Compacts | 10 SGA ingots + 2 Construction Alloy Dross | EBF, 2,400 K | 480 | 60 s | No Atmosphere |
| Advanced | Dross reclamation | Use the shared advanced chemical recovery below | Recovered powder, then SGA | Chemical Reactor, Electrolyzer and EBF | See below | See below | Finished SGA still needs No Atmosphere |

The compact holds four material units. Three compacts consume twelve powder units. This intermediate changes the form used for sintering and reduces the direct powder route's losses. It is not an arbitrary quality label. The high route can also compact powder from the medium composition. Aluminium is another feedstock option, not a forced new material gate.

### Approach A Yield And Cost Comparison

| Route | Gross incorporated feedstock | SGA before chemical recovery | Dross | SGA with 80% shared dross reclamation | Useful distinction |
| --- | ---: | ---: | ---: | ---: | --- |
| Low | 12 metal units | 6, 50% | 6 | 10.8, 90% | Minimal factory and cheap feedstock |
| Medium | 12 metal units | 9, 75% | 3 | 11.4, 95% | Different metal supply, Mixer and powder processing |
| Advanced | 12 metal units | 10, 83.33% | 2 | 11.6, 96.67% | Compaction plus chemical sidestream recovery |

These are steady-state averages. A medium mixing batch contains twelve units because eight tiny silicon dust plus one tiny gold dust total one unit. Before shared reclamation, medium gold use is 1/81 metal unit per SGA, but cobalt use is 2/9. That substantial cobalt fraction makes this a surplus-site option rather than an obviously cheap global default. Advanced aluminium feedstock similarly consumes 2/10 cobalt per direct SGA, plus its normal aluminium refining cost.

Shared recovery adds consumed platinum and acid, so all-input efficiency is slightly below the bulk figures. It lets later factories reclaim stockpiled low-route dross. There is no rule preventing a low-route factory from benefiting once the player builds that recovery equipment. Selecting this approach accepts the higher item count and a composition-driven economy.

## Approach B: One Cheap Bulk Recipe, Better Residue Recovery

Recommended. Keep one iron-based primary batch, and reward actual reclamation work. Gold and cobalt help recover half of its dross in one thermal sidestep. The advanced route uses acid treatment, electrolysis and a final vacuum-production step to recover four fifths. Platinum is a small consumed processing promoter, not the bulk body of the material. Aluminium stays on the table as a future alternative base composition rather than being silently coupled to scandium.

This approach adds Construction Alloy Dross and Recovered Construction Powder. The powder is recovered feedstock awaiting finishing, not usable SGA, a new quality of SGA or an automatically interchangeable ingot. Recovery Solution is one common new fluid. An unrecoverable low-value residue uses existing GT stone dust as an explicit gameplay abstraction for trapped gangue. It is not returned dross and cannot repeatedly enter these recovery recipes.

| Route | PROPOSED operation | Inputs | Outputs | Machine | EU/t | Time | Condition |
| --- | --- | --- | --- | --- | ---: | ---: | --- |
| All, low route by itself | Primary batch | 10 iron ingots + 2 silicon ingots | 6 SGA ingots + 6 Construction Alloy Dross | EBF, 1,800 K | 120 | 30 s | No Atmosphere |
| Medium | Promoted dross reduction | 4 Construction Alloy Dross + 1 carbon dust + 1 tiny gold dust + 1 tiny cobalt dust | 2 SGA ingots + 2 stone dust | EBF, 1,800 K | 480 | 60 s | No Atmosphere |
| Advanced | Dross leaching | 5 Construction Alloy Dross + 250 mB hydrochloric acid + 1 tiny platinum dust | 250 mB Recovery Solution | Chemical Reactor | 120 | 30 s | Any |
| Advanced | Recovery electrolysis | 1,000 mB Recovery Solution | 16 Recovered Construction Powder + 4 stone dust | Electrolyzer | 480 | 60 s | Any |
| Advanced | Recovered-feedstock finishing | 4 Recovered Construction Powder | 4 SGA ingots | EBF, 1,800 K | 120 | 20 s | No Atmosphere |

Gold/cobalt-assisted reduction and platinum-assisted leaching are explicitly fictional reactions. Tiny promoters are consumed and are not recovered by these recipes. Their purpose is to make different normal material supplies relevant without making precious metals a large fraction of cheap bulk construction stock. Their lore and even their inclusion are redlining choices, not scientific claims.

The advanced Chemical Reactor has two item input types, dross and platinum, plus one fluid input. The Electrolyzer has one fluid input and two solid output types. The medium EBF has four item input types. No custom downstream machine is required.

### Approach B Full-Route Arithmetic

| Route | Comparable bulk batch | Finished SGA | Bulk utilization | Extra consumables | Irrecoverable residue |
| --- | --- | ---: | ---: | --- | --- |
| Low | 10 Fe + 2 Si, 12 units | 6 | 50% | None | 6 dross retained, not automatically waste |
| Medium | Two primary batches, 24 units | 12 direct + 6 reclaimed = 18 | 75% | 3 carbon dust + 3 tiny gold + 3 tiny cobalt | 6 stone dust |
| Advanced | Ten primary batches, 120 units | 60 direct + 48 reclaimed = 108 | 90% | 3,000 mB HCl + 12 tiny platinum | 12 stone dust |

Medium: two primary batches produce twelve dross. Three four-dross reductions recover six SGA. Each scarce promoter averages 1/54 whole-metal unit per finished SGA. Carbon averages 1/6 dust per finished SGA. Including the consumed gold and cobalt, product divided by all metal inputs is 18 divided by (24 + 2/3), or about 72.97%, rather than 75%.

Advanced: ten primary batches produce sixty dross. Twelve leaching runs produce 3,000 mB solution. Three electrolysis runs produce forty-eight recovered powder and twelve stone dust. Twelve finishing runs yield forty-eight more SGA. Platinum averages 1/81 whole-metal unit per finished SGA. HCl averages 27.78 mB per finished SGA. Counting platinum gives 108 divided by (120 + 4/3), or about 89.01% all-metal utilization rather than 90%.

These game material-unit ratios are not kilograms or conserved atom counts across different elements. No recipe multiplies the incorporated metal stock into unlimited construction material. Carbon and acid are process reagents. Scarce promoters are lost or incorporated in the unspecified process residues. They do not return as an infinitely cycling catalyst.

The advanced line replaces the medium dross reduction. A given dross batch chooses one recovery route. Running both in sequence cannot recover it twice, because the medium output is SGA plus stone, not fresh dross. Stored dross makes later investment useful without a bootstrap requirement to build that investment first.

### Yield Versus Fresh-Carrier Burden

Let F be the number of fracking operations needed to supply one primary twelve-unit Fe/Si batch after all unchanged ore refining. F is not assumed to be one. Exact ore conversion and any imported metal supplies determine it. Because Approach B uses the same primary batch for all three methods, its comparison stays valid without inventing ore-to-metal yields.

| Route | SGA per primary batch, long-run | Makeup per SGA at q = 1,000 | Makeup per SGA at q = 1,250 | Makeup per SGA at q = 2,000 |
| --- | ---: | ---: | ---: | ---: |
| Low | 6 | 41.67 F mB | 83.33 F mB | 208.33 F mB |
| Medium | 9 | 27.78 F mB | 55.56 F mB | 138.89 F mB |
| Advanced | 10.8 | 23.15 F mB | 46.30 F mB | 115.74 F mB |

For example, if the verified ore processing and chosen profile later establish F = 3, multiply the entire row by three. This is a conditional illustration, not a selected deposit yield. Fracking of separate gold/cobalt/platinum deposits adds its own carrier cost and normal refining, so the table above is the bulk Fe/Si burden, not a complete scarce-material supply total. Imported finished promoters avoid that local fracking cost but add transport and origin-production costs.

For Approach A use separate F values for its different compositions. Before shared chemical recovery, bulk makeup per SGA is F_low times (q minus 750) divided by 6, F_medium times (q minus 750) divided by 9, and F_advanced times (q minus 750) divided by 10. With reclamation the denominators become 10.8, 11.4 and 11.6. Different cobalt and aluminium supply costs prevent assuming equal F.

### Approach B Energy And Base Throughput

Exclude metal/reagent manufacturing and fracking here. These are arithmetic checks at proposed base recipe speed, not claims of real factory throughput.

| Route | Alloy/recovery EU per finished SGA | Sum of recipe-seconds per finished SGA | Factory difference |
| --- | ---: | ---: | --- |
| Low | 12,000 | 5.00 s | One EBF, little local processing |
| Medium | 104,000 | 13.33 s | Same primary EBF plus slower promoted dross reduction |
| Advanced | 36,000 | 10.00 s | Chemical Reactor, Electrolyzer, acid supply and finishing EBF |

Low: one primary batch uses 72,000 EU. Medium: two primary batches plus three reductions use 1,872,000 EU for eighteen SGA. Advanced: ten primary batches use 720,000 EU, twelve leaches 864,000 EU, three electrolysis runs 1,728,000 EU and twelve finishing runs 576,000 EU. Total 3,888,000 EU for 108 SGA. Its summed base recipe time is 1,080 seconds. The advanced line has higher capital and material dependencies but beats the medium line's proposed running energy. That is intentional in this example and remains a balance choice.

## Resource And Byproduct Comparison

| Choice | Main value | Main cost or risk | Residue behavior |
| --- | --- | --- | --- |
| Approach A | Different normal material supplies produce useful alternative compositions | Major cobalt fraction and aluminium refining can outweigh better yield | All routes create reclaimable dross, advanced compacting reduces it |
| Approach B | Iron stays cheap and useful, better factories recover more from the same bulk supply | Promoter chemistry is fictional, residue output needs final lore and balance | Low dross can be stockpiled, medium permanently loses half, advanced loses one fifth |
| Direct carrier return alternative | Removes one spent-fluid ID and cleanup operation | Removes the separate recovery-investment choice | Could return 750 mB carrier directly during separation |
| Current separate cleanup proposal | Useful powered supply-saving choice using one shared spent fluid | Adds tanks, a recovery operation and one fluid identity | No free stone output and no closed fluid loop |

Approach B adds three items including the final ingot: SGA, Construction Alloy Dross and Recovered Construction Powder. With the four example deposits, it adds six fluids: four enriched variants, shared Spent Drilling Fluid and Recovery Solution. Existing Drilling Fluid is reused. Every additional authored deposit adds its required enriched identity, not another family of raw items.

Approach A instead needs the final ingot plus mixed powder, compact and dross, or four items. Its reclamation may reuse Construction Alloy Powder as recovered feedstock, so a separate recovered-powder item is not essential. The same six-fluid count applies with the same four deposit examples. These counts do not commit to a full unused set of material forms.

## Direct Redlining Choices

1. Prefer the recommended same-feedstock recovery ladder, or the composition-and-compaction alternative? The first makes better return a factory decision. The second makes it partly a destination and metal-supply decision.
2. Should gold/cobalt act as small consumed recovery inputs, as proposed in B, or become significant medium-route alloy fractions, as in A? The latter is easier to explain as composition but harder to keep cheap.
3. Should the advanced route use ordinary platinum as a small consumed promoter, or should its advantage come from acid/electrolysis infrastructure alone? Removing platinum avoids a rare-metal dependency but reduces the distinct platinum-deposit use. Neither option approves scandium.
4. Keep 50%, 75% and 90% bulk utilization as a first balance illustration, or choose different gaps? Review these together with scarce consumables, energy, processing time, factory capital and net drilling-fluid makeup. Higher percentage alone does not prove the medium route is attractive.
5. Retain common recoverable dross and separate carrier cleanup? These are useful recycling systems, but they add two fluid/item-handling side streams. Direct carrier return can simplify the fluid side without changing the material-recovery choice.
6. Is aluminium wanted as a competing advanced bulk feedstock now, or should it remain an open later recipe while B establishes the first complete chain? Do not fill the uncertain high route with Al-Sc merely because scandium exists as a GT material.

## Evidence And Unverified Boundaries

The exact Drilling Fluid recipe above comes from the parent's supplied local225 source audit. The initial source-capacity checks at the same revision established Centrifuge map limits of 2 item inputs, 6 item outputs, 1 fluid input and 1 fluid output, EBF limits of 6, 6, 1 and 1, and Mixer limits of 9, 4, 1 and 1. RecipeMapBuilder.maxIO confirmed parameter order. These facts do not establish physical inventory capacity or gameplay execution.

The concurrent gt_environment_research agent supplied current upstream GT facts at revision prefix `bc7a940` on 2026-10-10:

- Normal iron, gold, cobalt, aluminium, platinum and scandium identities exist. Gold, cobaltite, platinum and bauxite crushed forms fit normal ore-processing declarations.
- Banded Iron has existing ore/dust definitions, Fe2O3 composition and direct-smelting ownership pointing to normal Iron. The example uses that verified mineral. Hematite's identity exists, but its declaration alone did not establish a hematite-to-iron recipe, so this draft does not assume one.
- Cobaltite roasting uses oxygen at MV and 1,200 K. Roasted Cobalt plus carbon has an explicit MV, 1,200 K ingot recipe. Cobalt Oxide has an explicit corresponding reduction route. The new recipes do not replace them.
- Normal platinum ore/byproduct processing is redirected through existing platinum intermediates. An explicit poor-yield EBF route converts three PT Metallic Powder dust to two platinum nuggets at MV, 2,041 K and thirty seconds. It would be inaccurate to claim that every legitimate platinum ingot requires the entire efficient refining line. These proposals preserve whatever normal routes GT supports.
- Existing bauxite refining uses Bauxite Slurry, Heated Bauxite Slurry, Bauxite Slag, Alumina, aluminium hydroxide and Sluice Juice. Its slurry Mixer is MV, fluid heating is HV and the efficient slurry reaction is HV LCR. The final normal aluminium-ingot route was not fully established by that GT-only audit, so Approach A's exact upstream cost is unresolved.
- Current bauxite composition does not contain scandium. Scandium exists, but no default placement or acquisition chain was established in the checked source. Al-Sc is not an existing accepted production path.
- Current RecipeMaps.java declares Electrolyzer limits of 2 item inputs, 6 item outputs, 1 fluid input and 1 fluid output at lines 820-821, and Chemical Reactor limits of 2, 2, 1 and 1 at lines 1127-1129. The proposed advanced recipe shapes fit these declarations.

These shared audit findings are evidence supplied by the agent responsible for that materials work, not another independent completed audit by this draft. The parent will integrate its final evidence and full revision references. New recipes are not claimed to exist. No graph reindexing, production edit, build, runtime test, publication or infrastructure work was performed for this proposal.

Open factual work includes final profile availability/progression review, exact unchanged ore-to-metal conversion, final aluminium acquisition cost, supported dust-size conversions and runtime environment enforcement. Those facts affect complete factory totals, not the validity of comparing the stated fictional recipe batches. No implementation detail or migration policy is prescribed here.

[[Sources]]
