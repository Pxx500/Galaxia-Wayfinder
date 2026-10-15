---
type: source
status: unreviewed
tags:
  - galaxia/alpha
  - wayfinder/source
---

# Lunar Fracking And Space Grade Alloy Recipe Draft

Source: agent recipe proposal
Imported: 2026-10-10

## Source Snapshot

This is a complete-chain proposal for owner redlining, not accepted content or an implementation plan. Every new recipe, composition, amount, power setting and duration below is PROPOSED. Existing GT recipes remain unchanged. The parent verified and inserted the existing drilling-fluid recipe after receiving the bounded source retrieval.

### Accepted Constraints Used

- One Crater Extractor mines the shared finite ordinary reserve first. Supplying fluid early does not bypass this stage. Fracking becomes available only after exhaustion.
- Any number of machines share the crater's reserve and fracking history. Replacing a machine does not reset that history.
- Fracking is unlimited. Input-fluid cost per operation rises gradually with that shared history.
- Each enriched-fluid variant has its own registered Fluid ID. Deposits are a general authored system, not a fixed set of three profiles.
- Downstream processing uses ordinary GT machines and recipe maps. Partial carrier recovery requires continuing fresh-fluid production.
- Space-Grade Alloy is one canonical product. Its production requires an atmosphere-free environment, with no gravity restriction. It is cheap bulk construction material, not a technology-tier gate.
- Titanium remains on its existing GT processing chain. No fluid separation recipe here outputs titanium metal.
- The imported platinum/scandium profile list and custom pressure chamber are not accepted content and are not used.

These constraints come from the current assignment and the accepted sections of Review Crater Nodes Proposal.md, Define Alpha Research and Production Floor.md, Design Early Orbital Production Recipe Chain.md and the relevant Crater Vocabulary in CONTEXT.md. Their exact recipe values remain open. This source note does not change those owning notes.

### Recommended Chain

Use existing GT drilling fluid as the fracking medium if its verified ordinary recipe and accessibility fit the first lunar stage. Produce it using the unchanged GT recipe, initially on the starting world if convenient. Ordinary crater mining requires no fracking fluid, rare lunar reagent or Space-Grade Alloy. This avoids a circular bootstrap.

After ordinary exhaustion, each fracking operation consumes its current crater-dependent quantity of drilling fluid but always produces 1,000 mB of the deposit's enriched variant. More fluid buys the same resource batch, not more minerals. Extra fluid is lost underground. That fixed output is a proposed gameplay abstraction that keeps standard downstream recipes stable while making old craters increasingly expensive.

Separate useful mineral dusts first. A shared spent-drilling-fluid output can then undergo an optional second recovery operation. Recovering carrier is useful but not required to obtain the minerals. This makes the second step a genuine supply-saving choice rather than a mandatory renamed intermediate. Players may reuse one Centrifuge sequentially or build a dedicated recovery line.

Fluid quantities are mB. Times are base times. All new settings are proposals. Ingredient acquisition retains existing GT processing requirements. No existing recipe is claimed solely from the presence of a material name.

| Status | Process | Inputs | Outputs | Machine | Proposed EU/t | Proposed time | Environment |
| --- | --- | --- | --- | --- | ---: | ---: | --- |
| PROPOSAL, parent addition | Extractor controller assembly | 1 HV machine hull + 2 HV electric motors + 1 HV pump + 2 HV pistons + 2 HV circuits + 4 steel plates + 144 molten tin | 1 Crater Extractor controller | Assembler | 480 | 45 s | Any |
| Existing recipe, source verified | Fresh carrier production | 5 water cells + 1 stone dust + 20 lubricant | 5,000 existing GT drilling fluid + 5 empty cells | Mixer | 15 | 3.2 s | No new restriction |
| PROPOSAL | Ordinary ferruginous mining | One finite reserve batch, power, no fracking fluid | 6 hematite dust + 2 silicon dioxide dust | Crater Extractor, ordinary mode | 120 | 30 s | Inside its bound crater |
| PROPOSAL | Ordinary aluminous mining | One finite reserve batch, power, no fracking fluid | 6 bauxite dust + 2 silicon dioxide dust | Same Crater Extractor, ordinary mode | 120 | 30 s | Inside its bound crater |
| PROPOSAL | Fracking | q(n) drilling fluid, where n is the next claimed position in the shared fracking history | 1,000 deposit-specific enriched drilling fluid | Same Crater Extractor, fracking mode | 120 | 30 s | Same crater, ordinary reserve exhausted |
| PROPOSAL | Ferruginous separation | 1,000 ferruginous enriched drilling fluid | 6 hematite dust + 2 silicon dioxide dust + 800 spent drilling fluid | Centrifuge | 120 | 20 s | Any |
| PROPOSAL | Aluminous separation | 1,000 aluminous enriched drilling fluid | 6 bauxite dust + 2 silicon dioxide dust + 800 spent drilling fluid | Centrifuge | 120 | 20 s | Any |
| PROPOSAL | Carrier cleanup, optional | 1,600 spent drilling fluid | 1,500 existing drilling fluid + 1 stone dust | Centrifuge | 30 | 30 s | Any |
| Existing routes retained, not redefined | Iron preparation | Extracted hematite dust plus the inputs required by the selected normal GT route | Ordinary iron ingots | Existing iron-processing machinery | Existing | Existing | Existing |
| Existing routes retained, not redefined | Aluminium preparation | Extracted bauxite dust plus all inputs required by normal GT aluminium processing | Ordinary aluminium ingots | Existing bauxite processing and aluminium smelting | Existing | Existing | Existing |
| Existing recipe recorded in the reviewed orbital-chain note | Silicon preparation | 3 silicon dioxide dust + 2 carbon dust | 1 silicon ingot + 2,000 carbon monoxide, with existing ash chance | EBF, 1,200 K | 120 | 4 s | Existing |
| PROPOSAL | Iron-feedstock alloy | 7 iron ingots + 1 silicon ingot | 8 Space-Grade Alloy ingots | EBF, 1,800 K | 120 | 30 s | No Atmosphere, any gravity |
| PROPOSAL | Aluminium-feedstock alloy | 7 aluminium ingots + 1 silicon ingot | The same 8 Space-Grade Alloy ingots | EBF, 1,800 K | 120 | 30 s | No Atmosphere, any gravity |
| PROPOSAL | Mixed-feedstock alloy | 4 iron ingots + 3 aluminium ingots + 1 silicon ingot | The same 8 Space-Grade Alloy ingots | EBF, 1,800 K | 120 | 30 s | No Atmosphere, any gravity |

The two example deposit profiles are content proposals, not an approved lunar resource list or a cap. Other deposits can use their own ordinary reserve output and enriched Fluid ID. A titanium-bearing deposit would output an appropriate mineral feedstock and retain every existing titanium chemistry and production gate. There is no proposed direct titanium-dust or titanium-ingot output and no titanium requirement for starting ordinary mining or making this alloy.

The parent added a proposed controller assembly recipe to make the content proposal include the initial extraction equipment. It needs no Space-Grade Alloy or lunar-exclusive ingredient, so the player can prepare the first extractor before mining a crater. Its six distinct item inputs and single tin input are ordinary HV component roles. This does not select singleblock versus multiblock topology, construction geometry or an implemented controller type. Resolve any structure-content requirements separately if needed, without treating this recipe as proof of machine implementation.

Using finished iron, aluminium and silicon ingots for alloying preserves their upstream smelting requirements. The aluminium variant cannot turn bauxite or aluminium dust directly into construction alloy to bypass ordinary metal preparation. The iron recipe is the cheap default. The alternatives let imported or locally processed stocks substitute without creating alloy-origin variants or requiring both example deposit kinds.

The alloy recipes create a fictional common construction specification, not a claim that these three real compositions are physically identical alloys. The vacuum requirement is an accepted environmental gameplay rule. None of the recipes needs a custom pressure chamber, Microgravity, a lunar-only recipe flag, a new technology tier, or a new blend item. Existing progression ingredients must still appear in equipment recipes where needed. This material must not replace titanium or other tier-defining ingredients indiscriminately.

### Fluid And Item Count

With the two example deposits, the proposal adds three fluids: ferruginous enriched drilling fluid, aluminous enriched drilling fluid and shared spent drilling fluid. Each has a separate Fluid ID. Fresh drilling fluid is reused, not re-registered. Every further deposit variant adds its corresponding enriched identity, without an arbitrary cap.

The core chain adds one Space-Grade Alloy ingot item and no custom impure solid family. Standard material forms may be defined when a concrete consuming recipe needs them, but this draft does not add an idle set of plates, rods, casings or structural blocks. Mineral and stone outputs use existing GT materials. This draft verifies material declarations, not every generated dust form or downstream recipe in a playable pack.

### Arithmetic Checks

- Two fracking operations at a proposed initial q of 1,000 consume 2,000 drilling fluid. Their 2,000 enriched fluid yields 1,600 spent fluid. One cleanup operation returns 1,500 drilling fluid. The combined recovery is 75%, and ongoing fresh makeup is 500 for the pair, or 250 per operation.
- At q = 1,250 the same two mineral batches consume 2,500 and return 1,500. Fresh makeup is 1,000, or 500 per operation. At q = 2,000 they consume 4,000 and return 1,500. Makeup is 2,500, or 1,250 per operation. Increasing cost therefore remains meaningful after recovery.
- In general, with full recycling, average fresh-fluid burden is q(n) minus 750 per operation. Cleanup has its own 1,600 mB batch, so buffering connects it to the 1,000 mB enriched batches. There is no need to stretch either recipe to match the other.
- These illustrations do not select a numerical history curve. The proposed q(n) starts above the recoverable 750 and rises slowly enough to keep continued work useful while eventually making relocation attractive. Unlimited fracking does not itself select an unbounded cost curve. The minimum starting value, growth schedule and worthwhile relocation threshold need owner redlining and later balance work.
- Each alloy recipe consumes eight ordinary metal/metalloid ingot units and produces eight canonical alloy ingots. There is no bulk multiplier in the final alloying operation. One silicon ingot per alloy batch requires three silicon dioxide dust through the recorded silicon route. The example deposit yields two silica dust per extraction or fracking batch, so the batches need not line up. Three extraction batches supply six silica dust, enough for two silicon runs, with four carbon dust supplied separately.
- Recovery consumes EU. Two 20-second separation runs at 120 EU/t plus one 30-second cleanup at 30 EU/t use 114,000 EU before overclocking. Each 30-second fracking operation at 120 EU/t adds 72,000 EU. These figures exclude normal mineral processing and alloying. They are tuning illustrations, not a measured factory-power budget.

### Three Choices For Redlining

1. Existing drilling fluid versus a new lunar carrier. Reusing drilling fluid avoids another upstream chemistry and fluid identity. It also connects lunar work to an existing supply line. A new carrier is justified only if the verified GT recipe or material semantics make reuse unsuitable. No recipe for that alternative is proposed merely to have another option.
2. Optional separate cleanup versus immediate recovery. Separate cleanup adds one spent-fluid identity and a useful powered recovery operation. Immediate 750 mB carrier return in the mineral-separation recipe would remove that identity and operation, but also remove the player's recovery investment choice. The draft recommends separate cleanup because its output reduces continuing supply burden rather than just advancing a mandatory chain.
3. Fixed output with growing losses versus proportionally growing output. Fixed mineral output makes deterioration easy to understand and retains ordinary GT recipe matching. It abstracts away the extra input fluid as unrecovered underground loss. Scaling enriched output with input would also scale ordinary fixed-ratio mineral recipes and could reward old sites rather than encourage relocation. The draft recommends fixed output.

### Evidence And Limits

The accepted environmental and content-ownership constraints were read from the named vault notes and CONTEXT.md on 2026-10-10. The current accepted staging direction places new GT-bound items, fluids and recipes temporarily in Galaxia for eventual GT ownership. This draft does not alter that decision or prescribe code structure.

Bounded local source checks used GT5-Unofficial at HEAD `2259bc64244f9f7fc58e039d8e89ca40dd17c929`:

- `src/main/java/gregtech/api/recipe/RecipeMaps.java:790` declares Centrifuge map limits of two item inputs, six item outputs, one fluid input and one fluid output.
- `src/main/java/gregtech/api/recipe/RecipeMaps.java:855` declares EBF map limits of six item inputs, six item outputs, one fluid input and one fluid output.
- `src/main/java/gregtech/api/recipe/RecipeMaps.java:535` declares Mixer map limits of nine item inputs, four item outputs, one fluid input and one fluid output.
- `src/main/java/gregtech/api/recipe/RecipeMapBuilder.java:186` confirms the parameter order of those limits.
- `src/main/java/gregtech/api/enums/Materials.java` declares Hematite at line 263, Stone at 388, SiliconDioxide at 516 and Bauxite at 688.

Every proposed Centrifuge recipe has only one fluid input and one fluid output. The separation recipes have two item output types. The alloy recipes have at most three item input types. These shapes fit the checked map declarations. This is not proof of exact single-block inventory capacity, recipe execution, environmental enforcement, the final dependency version or playable-pack accessibility.

The parent independently checked the retrieved drilling-fluid recipe using graph-backed source search in `src/main/java/gregtech/loaders/postload/recipes/MixerRecipes.java:641-649` at the same local SHA. It uses five water cells, one stone dust, 20 mB lubricant and returns five empty cells plus 5,000 mB `ItemList.sDrillingFluid`. Duration is 64 ticks and EU/t is half `TierEU.RECIPE_LV`, or 15. `LoaderGTBlockFluid.java:1130` registers the fluid. This is an existing upstream recipe, not permission to change it. Recheck the selected development dependency when implementation begins.

The attempted codebase-memory index refresh returned `persist_failed`. Existing graph lookup located symbols, and bounded local source reads supplied the actual capacity evidence. The parent subsequently reported a successful infrastructure repair and verified index rebuild. This proposal performed no further indexing or infrastructure work and does not use that repair as recipe verification.

The silicon row is transcribed from the previously source-audited existing recipe recorded in Design Early Orbital Production Recipe Chain.md. It was not freshly re-audited here. Exact retained iron and aluminium processing must be verified independently before an implementation or an exact full-factory cost claim. Their unresolved factual quantities are not new recipe proposals.

No code, build, in-game test, scientific-chemistry verification or publication was performed. Numerical balancing and content choices remain proposals. The drilling-fluid audit is integrated. This note remains source intake until a later Wayfinder review classifies it.

[[Sources]]
