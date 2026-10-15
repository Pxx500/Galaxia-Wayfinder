---
type: source
status: unreviewed
tags:
  - galaxia/alpha
  - wayfinder/source
---

# GT5 Environment Recipe Variant Feasibility Research

Source: Primary GT5-Unofficial source, with accepted Galaxia owner requirements supplied for comparison
Imported: 2026-10-11

## Source Snapshot

This is read-only feasibility research. It does not approve a new GT capability, material, recipe or lifecycle policy. No production source, dependency, build, test, commit or publication was changed.

The local GT checkout was clean at `2259bc64244f9f7fc58e039d8e89ca40dd17c929`. Its graph was fully reindexed at the start of this investigation. Graph search, snippets and call traces identified the existing owners. GitHub's commits API returned current upstream `03f76356146f497c6c8f21d9225fe28de57136a1`, dated 2026-10-10 19:19:48 UTC. The decisive source excerpts below were fetched successfully with HTTP 200 at that immutable upstream SHA. The local index is discovery evidence, not a claim that its older checkout is current. [Inspected upstream commit][commit]

Context was read from Agent Briefing, Define Celestial Capability Rules and Recipe Environment Implementation Handoff. The accepted boundaries are neutral optional environment metadata, convenient typed authoring constants, Galaxia-owned evaluation and multiblock controller position for Alpha. Unknown or unresolved data while Galaxia is loaded does not satisfy a required tag. It is neither Atmosphere nor No Atmosphere. Absent-Galaxia ignoring of Galaxia-supplied requirements is a separate approved development convenience. The existing SGA No Atmosphere rule is unchanged.

### Main Finding

Same-input environmental variants are feasible, but not through recipe metadata and validation alone. Current registration treats the pair as a collision. Selection also has first-match, cache and locking assumptions that must be accounted for. Two ordinary static recipes are the lightest credible general model for the immediate output-only Sc use case. They reuse more existing behavior than a new runtime-effective recipe model.

This is moderate shared-path work, not a recipe-only change or a single validation hook. A fully general effective-recipe model has a larger blast radius. A restricted EBF output-only slice is smaller than universal variable-input variants, but the cache, lock and active-operation constraints below still apply.

### Registration And Candidate Selection

| Existing owner | Verified behavior | Consequence |
| --- | --- | --- |
| `RecipeMapBackend.doAdd`, lines 223-245 | Transforms the builder, emits recipes, transforms each recipe, then skips a colliding recipe when collision checks are enabled | An ordinary same-input pair is not admitted by default |
| `checkCollision`, lines 371-374 | Queries matching item/fluid inputs with stack-size checks disabled | Environment metadata, outputs, chances, duration and EU/t do not distinguish this pair |
| Lookup trie node, lines 93-102 | Stores a first recipe and an additional-recipe list | Existing storage can represent several candidates. A separate variant store is not inherently required |
| `GTRecipeBuilder.ignoreCollision`, lines 689-692 | Disables the builder's collision check | Existing escape hatch, not proof of safe environmental exclusivity or correct selection |
| Backend stream, lines 469-484 | Explicit cached recipe, shared input-hash cache, then lookup candidates, with input validation and modification | A previously selected variant can be offered first again |
| Backend hash and input filter, lines 536-570 | Hashes item/fluid identity, then checks enabled/nonfake inputs and optional special slot | No environment key or environment eligibility check exists here |
| `FindRecipeQuery`, lines 66-96 and 141-148 | Applies a caller-supplied predicate before `findFirst`. Its documentation explicitly says rejection attempts the next recipe | Useful existing selection capability. A machine-context predicate can reject an ineligible cached candidate and continue |

[Registration][registration] [Collision][collision] [Existing multi-candidate storage][lookup] [Collision escape hatch][ignore-collision] [Candidate order][candidate-order] [Input hash and filter][input-filter] [Query filtering][query] [Predicate contract][query-filter]

Merely adding environment metadata to a hash would not fix collision admission or every caller. Conversely, a correctly applied query predicate does not require a new environment-specific trie for this same-input case. The backend's `modifyFoundRecipe` is an existing modification seam, but receives only recipe, items, fluids and special slot, not world or controller. Its documentation warns not to mutate the found recipe. It is not already an environment resolver. Backends that overwrite search can return a singleton instead of the normal stream. They were not broadly audited. [Modification seam][modify] [Custom search escape path][overwrite]

### First-Match, Cached And Locked Paths

| Path | Does rejection try another candidate now? | Verified limitation |
| --- | --- | --- |
| Ordinary singleblock `MTEBasicMachine.checkRecipe` | No | Calls `.find()`, then runs requirement/output checks. A failure returns immediately |
| Normal `ProcessingLogic.process` stream | Yes, before inputs have successfully been consumed | Loops candidates and remembers interesting validation failures |
| Dual-input pattern cache | No for the first input-compatible cached candidate | Returns its validation/calculation result immediately |
| Existing single-recipe lock | No | Checks recorded input costs, then validates/calculates its one saved recipe |
| Saved-lock reconstruction | No | Finds the first input match, then compares its outputs/chances/EU/time/special value against saved data |

[Singleblock selection][basic-check] [Multiblock branches][processing-branches] [Saved-lock reconstruction][lock-restore]

The saved-lock case is a reachable blocker. If another same-input variant is returned first, reconstruction returns null even though the saved variant still exists. `MTEMultiBlockBase.loadNBTData` disables working when the saved checker cannot be reconstructed. Environment metadata is not compared by this restoration routine. Whether locking means one exact environmental variant or an input family that may select variants is an open product contract, not selected here. [Lock restoration consequence][multi-load]

Pattern caching adds another constraint. `tryCachePossibleRecipesFromPattern` caches `findRecipeMatches` results in a linked set and reuses it on later checks. Filtering that construction to the current environment can omit the alternative permanently from that cache. Eligibility must remain correct when the environment later changes. This is not solved by adding a predicate at only the normal live query call. [Pattern cache][pattern-cache]

### Selection Must Precede Output Checks And Consumption

For a singleblock, `canOutput(GTRecipe)` examines the selected recipe's static outputs. The machine then consumes inputs, rolls its outputs and calculates overclocking. Changing only the final roll would leave the output-space check describing a different output profile. [Output checks][basic-output] [Singleblock order][basic-check]

For a multiblock, `validateAndCalculateRecipe` validates, builds ParallelHelper and OverclockCalculator, then applies the result. ParallelHelper reads recipe outputs and chances for void protection before consuming inputs. It also uses the selected recipe for power limits, parallel input costs and locking. Batch processing consumes further inputs and lengthens the calculated operation. Ordinary recipe duration and EU/t feed the existing overclock calculator, including the EBF's heat behavior. [Processing calculation][processing-calculate] [Parallel protection and consumption][parallel-protect] [Parallel and batch owner][parallel-owner] [Overclock owner][processing-overclock] [EBF heat handling][ebf]

ParallelHelper has a custom final output-calculation function, but that function is called after the earlier protection setup. By itself it is not sufficient for introducing a new oxide output type with correct output-space protection. `onRecipeStart` is also too late to select the variant safely. Its own documentation says inputs have already been consumed and a failure voids them. [Late custom output function][parallel-output] [Late start callback][late-start]

An effective output profile therefore has to be fixed before the checks and consumption that depend on it. It must not be implemented by mutating the globally registered GTRecipe. Registered recipes are shared through the map and caches. `GTRecipe.copy` and `copyShallow` are not automatically safe metadata-preserving specialization tools either. Their shared copy constructor assigns empty metadata storage. `GTRecipeMapUtil.asTemplate(...).derive()` uses the same shallow-copy path. [Recipe copy][recipe-copy] [Template derivation][template]

### Active Operations And Environment Changes

Existing machine owners already separate recipe discovery from a running operation. A singleblock stores rolled outputs, EU/t and progress/duration, then its tick loop delivers those stored outputs. A multiblock copies ProcessingLogic's outputs/duration into its own operation fields and delivers them on completion. Their NBT writers retain those outputs and progress. These inspected normal paths do not rerun variant selection on each tick. [Singleblock active operation][basic-runtime] [Singleblock persistence][basic-save] [Multiblock operation setup][multi-setup] [Multiblock runtime][multi-runtime] [Multiblock persistence][multi-save]

The selected output profile cannot safely switch midway when inputs are already consumed. Re-selecting from current inventory cannot reconstruct the original operation because those ingredients may be gone. Search caches and recipe locks are not interchangeable with an active-operation requirement record. The inspected base operation fields do not retain a general selected environment requirement.

The accepted pause-and-resume rule for retained operations is a separate constraint to preserve, not replaced by this research. A variant-capable implementation needs to distinguish the frozen operation's eligibility from selection for the next operation. This note does not choose policies for switching environments, lock-family behavior or unknown data beyond the already accepted rules.

Legacy gravity and cleanroom checks are evidence of late selected-recipe checks, not precedent for alternative matching. BasicMachine returns failure after its one selected recipe fails those checks. EBF's special value represents heat in both validation and overclocking. No reuse of `mSpecialValue` for environment variants is justified. Existing gravity and cleanroom behavior remains in scope only as behavior to preserve. [Existing singleblock special checks][basic-check] [EBF heat owner][ebf]

### Display

NEI builds its cache from recipe-category collections, filters hidden recipes, sorts and creates a cached display for each. The inspected path does not collapse recipes merely because their inputs match. Item outputs and their chances come from each recipe's static data. RecipeMapFrontend separately renders energy, duration, special information and each metadata key's `drawInfo`. An ordinary admitted pair can therefore show two faithful output profiles with separate environment descriptions using existing owners. [NEI cache][nei-cache] [Static output display][nei-output] [Metadata display][frontend]

A single recipe with runtime-selected outputs is not automatically shown as both possibilities. It needs faithful display semantics instead of presenting only the registered base outputs. Display-only entries are not a runtime selection fix. A typed `requiresEnvironment` convenience method would improve authoring but would not change matching by itself.

### Design Comparison

| Design | What it genuinely reuses | Remaining difficulty | Relative effort |
| --- | --- | --- | --- |
| A. Ordinary recipes with mutually exclusive requirements | RecipeMap, existing metadata, candidate stream, static outputs/chances, overclock, parallel/batch and ordinary NEI | Collision admission, context-aware eligibility, cached and locked branches, restoration and retained-operation requirements | Lowest credible general solution for fixed identical inputs. Moderate shared work |
| B. One recipe with an environment-selected effective profile | One input registration, existing processors if the complete effective recipe reaches them early enough | Isolated effective data, metadata-safe copying, guards, caching, lock identity/restoration, persistence requirements and display of alternatives | Larger conceptual and shared-path change for a general capability. A narrow output-only custom machine could be smaller, but that is not the requested shared EBF capability |
| C. Declarative alternatives expanded into ordinary recipes | Existing builder and recipe-emitter support can emit several recipes | Same runtime admission, matching, cache and lock problems as A | A plus authoring convenience, not a third runtime design |

RecipeMapBuilder already accepts a recipe emitter returning several recipes. Its combine emitter retains existing emitted recipes. That matters for generated content because blindly combining a pair with its unconditional base would retain the bypass. Direct addRecipe overloads are not covered by this builder emitter. [Emitter owner][emitter]

Recommendation: use A as the reference direction for the simplest useful slice, specifically a fixed identical-input pair with output differences only. Keep optional environment metadata and machine-context evaluation on their existing owners. C is optional convenience once actual authoring needs justify it. Do not begin with B or a new variant store merely to avoid the collision check. This is a feasibility recommendation, not an accepted architecture or an implementation sequence.

Changes to output chances, duration and EU/t fit ordinary static recipe fields once selection is correct. Different reagents or input quantities introduce extra consumption, lock-cost and parallel semantics. They are not needed for the owner's current example and were not expanded into a universal design here.

### Concrete Sc Blast Example

Scandium is defined as a normal elemental dust/metal material requiring 1814 K blast processing. The ordinary dust registrator generates an unconditional one-dust plus circuit-1 blast recipe when automatic blast recipes are enabled. Materials above 1750 K produce hot ingots. The generated builder uses MV recipe EU/t and a duration derived from mass and heat. It supplies COIL_HEAT, not an environment requirement. The existing EBF map permits six item inputs and six item outputs, so two different item output forms fit that map's declared shape. [Sc definition][sc] [Generated blast owner][sc-blast] [EBF map shape][ebf-map]

The owner's requested example is No Atmosphere producing full metal yield, and Atmosphere producing some metal plus proposed Scandium Oxide that can be recovered to Sc dust. The existing hot-ingot stage should not silently be bypassed by calling its outputs finished ingots. The oxide identity and recovery recipe are proposed new content, not approved or existing-code facts from this investigation.

A larger fixed batch can still have identical inputs in both variants. The supplied example of five Sc dust to five metal units in vacuum versus three metal units plus an oxide batch carrying two Sc units in atmosphere illustrates elemental conservation. It is not a finalized recipe or a proof that raw oxide item counts imply that composition. Sc content must be conserved through oxidation and recovery.

An explicitly authored pair is lighter for this one material than adding environmental specialization to every automatically generated blast recipe. Its authoring must account for the generated original. Keeping the unconditional one-dust Sc recipe beside a five-dust variant pair leaves a straightforward bypass through five ordinary operations. Merely giving the original or one new recipe an environment label is not enough if another unrestricted producer remains. This investigation identified the concrete generator owner, not every pack override or alternate metal-producing machine.

### Absence And Unresolved Data

With Galaxia loaded, an unresolved environment fails required tags. Atmosphere and No Atmosphere are actual alternatives, not two ways to represent unknown data. Tag conjunction cannot express an OR by listing both requirements.

If future GT-owned variant content remains registered without Galaxia and its environment requirements are silently ignored, both same-input recipes become eligible. Current first-match and cached ordering can then choose one without a gameplay-defined reason. Hiding requirement text does not remove this ambiguity. The approved absent-mod convenience does not already specify which output profile should win. That decision remains open. No silent new fallback is recommended here.

Current Galaxia-only content and mixins disappearing when the mod is absent is different from future GT-owned recipes persisting with ignored metadata. The current gate checkpoint is not evidence that variants, generated recipe replacement or the two-recipe absent-mod case have been implemented.

### Scope And Verification Limits

This consolidated pass covered normal BasicMachine, ProcessingLogic, its pattern cache and single-recipe lock branches, SingleRecipeCheck persistence, ParallelHelper, the ordinary RecipeMap backend/query/lookup/builders, NEI and the existing EBF/Sc generator owners. It did not audit every specialized controller, backend, pack script, third-party machine or recipe map. A custom path that bypasses these owners is not certified covered.

No MCP failure occurred in this variant investigation. One narrow graph filename filter returned no nodes, then a qualified-name query found the owner normally. That is a query coverage gap, not a tool outage. There was no runtime validation, build or game test because production code stayed read-only. The conclusions are supported source feasibility and concrete reachable constraints, not a claim that a variant implementation works.

[[Sources]]

[commit]: https://github.com/GTNewHorizons/GT5-Unofficial/commit/03f76356146f497c6c8f21d9225fe28de57136a1
[registration]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/api/recipe/RecipeMapBackend.java#L223-L245
[collision]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/api/recipe/RecipeMapBackend.java#L371-L374
[lookup]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/api/recipe/lookup/GTRecipeLookup.java#L93-L102
[ignore-collision]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/api/util/GTRecipeBuilder.java#L686-L692
[candidate-order]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/api/recipe/RecipeMapBackend.java#L469-L484
[input-filter]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/api/recipe/RecipeMapBackend.java#L536-L570
[query]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/api/recipe/FindRecipeQuery.java#L66-L96
[query-filter]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/api/recipe/FindRecipeQuery.java#L141-L148
[modify]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/api/recipe/RecipeMapBackend.java#L393-L398
[overwrite]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/api/recipe/RecipeMapBackend.java#L424-L428
[basic-check]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/api/metatileentity/implementations/MTEBasicMachine.java#L1096-L1155
[processing-branches]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/api/logic/ProcessingLogic.java#L407-L450
[lock-restore]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/api/recipe/check/SingleRecipeCheck.java#L392-L431
[multi-load]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/api/metatileentity/implementations/MTEMultiBlockBase.java#L430-L437
[pattern-cache]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/api/logic/ProcessingLogic.java#L145-L176
[basic-output]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/api/metatileentity/implementations/MTEBasicMachine.java#L769-L784
[processing-calculate]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/api/logic/ProcessingLogic.java#L459-L517
[parallel-protect]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/api/util/ParallelHelper.java#L449-L503
[parallel-owner]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/api/util/ParallelHelper.java#L375-L535
[processing-overclock]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/api/logic/ProcessingLogic.java#L559-L588
[parallel-output]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/api/util/ParallelHelper.java#L552-L570
[late-start]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/api/logic/ProcessingLogic.java#L591-L599
[recipe-copy]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/api/util/GTRecipe.java#L161-L183
[template]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/api/util/GTRecipeMapUtil.java#L182-L190
[basic-runtime]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/api/metatileentity/implementations/MTEBasicMachine.java#L603-L626
[basic-save]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/api/metatileentity/implementations/MTEBasicMachine.java#L537-L570
[multi-setup]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/api/metatileentity/implementations/MTEMultiBlockBase.java#L1098-L1124
[multi-runtime]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/api/metatileentity/implementations/MTEMultiBlockBase.java#L813-L856
[multi-save]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/api/metatileentity/implementations/MTEMultiBlockBase.java#L344-L384
[nei-cache]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/nei/GTNEIDefaultHandler.java#L163-L205
[nei-output]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/nei/GTNEIDefaultHandler.java#L771-L787
[frontend]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/api/recipe/RecipeMapFrontend.java#L213-L245
[emitter]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/api/recipe/RecipeMapBuilder.java#L126-L152
[sc]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/loaders/materials/MaterialsInit.java#L1568-L1586
[sc-blast]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/loaders/oreprocessing/ProcessingDust.java#L100-L118
[ebf-map]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/api/recipe/RecipeMaps.java#L851-L858
[ebf]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/03f76356146f497c6c8f21d9225fe28de57136a1/src/main/java/gregtech/common/tileentities/machines/multi/MTEElectricBlastFurnace.java#L188-L206

## Clarified Family Lookup Follow-Up, 2026-10-11

The owner clarified that the desired model is one indexed common input signature, a matching recipe family and local environment selection among output profiles. It is not unrestricted top-level recipe multiplication and not output replacement at completion. This clarification makes explicit family ownership a legitimate requirement even where the existing index can already group ordinary variants efficiently. The earlier recommendation identifies the least-change runtime representation, not a reason to reject a first-class family contract.

The graph was fully reindexed again. Local GT stayed clean at `2259bc64244f9f7fc58e039d8e89ca40dd17c929`. The current upstream commits API now returned `2856a652b29ecf17dd5529880d589bea92a83b9f`, dated 2026-10-11 11:04:58 UTC. All new cited lookup, builder, cache, query, recipe-data and NEI excerpts were read successfully with HTTP 200 at that SHA. ProcessingLogic, SingleRecipeCheck, ParallelHelper and ProcessingDust were also byte-compared against the earlier inspected upstream and are unchanged. BasicMachine changed only in the inspected Waila energy-bar placement diff, outside its recipe selection, output, persistence and tick methods. Older citations above remain immutable evidence, not a claim that the old commit is still latest. [Follow-up commit][family-commit]

### What The Existing Index Already Does

GT's lookup is a trie of normalized item/fluid ingredient groups. It is not a flat list scan for every ordinary recipe query. `addRecursive` asks an existing branch for a node and reuses it when found. At an existing terminal node it appends another recipe instead of creating a parallel full path. The node holds one recipe plus an optional additional-recipe list. A node can also have a child branch, so terminal recipes and longer signatures can coexist. [Shared path insertion][family-insertion]

Thus a fixed pair with the same ordered normalized ingredient groups shares the corresponding path and leaf. It adds recipe references to that leaf, not a whole independent trie. This statement has two limits:

- A logical input may have item, ore-dictionary, item-data and unification aliases. The builder recursively indexes combinations of ingredient alternatives, so a logical signature can have several physical paths.
- The builder sorts ingredient groups by frequency. A full rebuild computes frequencies once for all entries, then equal ordered input definitions get the same ordering. Incremental registration updates frequencies before each addition. Changes in those frequencies or original input order can give the same logical signature different ordered paths. The current index is not a strict one-canonical-signature-to-one-family registry.

[Ingredient normalization][family-flatten] [Frequency pooling and sorting][family-order] [Incremental versus full build][family-build] [Backend rebuild owner][family-rebuild]

The runtime iterator deduplicates its query ingredient list, explores matching branch nodes and emits the node's first recipe followed by its additional recipes. It can encounter the same recipe through different paths. The backend stream combines cache hints and trie candidates, then applies `.distinct()` before input validation. Ordinary GTRecipe has Object identity equality, so this removes repeated occurrences of the same ordinary recipe object. It does not merge different output variants merely because their inputs match. Custom subclasses can alter equality and were not audited here. [Traversal][family-traversal] [Candidate deduplication][family-stream] [Ordinary recipe class][family-recipe-class]

Branch lookup uses two inline entries for small branches and a HashMap when promoted. During traversal it looks up query ingredients, not every child or every registered recipe. It still may visit many branches when input aliases and overlapping recipes create ambiguity. There is no honest universal logarithmic lookup bound based only on recipe count. [Branch representation][family-branch]

### The Input Hash Cache Is Not A Family Bucket

RecipeMapBackend has 256 cache slots. Each slot stores one GTRecipe selected for a commutative hash of runtime item/fluid identities. It is a collision-prone hint, not a map from exact signatures to all variants and not a semantic family registry. Quantities and environment are not part of that hash. Entries are validated again through the candidate filter. [Cache storage][family-cache-storage] [Cache write and hash][family-cache-hash]

The stream offers an explicit machine cached recipe first, then the backend cache slot, then lazily supplies trie candidates. A successful early `findFirst` can avoid constructing the trie candidate stream. An ineligible cached variant need not force a full-map scan. With an appropriate predicate the query can continue into the indexed candidates. Switching environments or machines sharing an input signature can reduce cache-hit usefulness, but this source alone does not establish measurable slowdown. [Lazy candidate order][family-stream] [Query result contract][family-query]

Existing pattern-cache and lock limitations from the first pass still apply. A family concept does not automatically change what those paths cache or restore. In particular, current SingleRecipeCheck stores and reconstructs one recipe, not a family plus profile identity.

### Honest Cost Model

These are qualitative source-derived work parameters, not benchmarks or guaranteed bounds:

| Parameter | Meaning and relevance |
| --- | --- |
| Distinct normalized signatures and physical paths | Determine much of the trie shape. Alias combinations, input ordering and prefix sharing matter, not only recipe total |
| `U` runtime ingredient aliases | Ingredient preparation and the number of lookup attempts within each visited branch |
| `B` visited branches | Query ambiguity. Each frame can test up to the query ingredient list |
| `R` emitted candidate occurrences | Includes repeated references reached through aliases before backend deduplication |
| `C` distinct candidate recipes actually examined | Input, special-slot, voltage and environment checks before success or exhaustion |
| `M` common input-validation work | Ordinary variant objects repeat that input check for each examined candidate |
| `V` profiles in a matching family | Local environment choice still has a cost. One indexed family is not zero-cost profile selection |

A rough ordinary miss/trie-query work model is visited-branch ingredient probes plus emitted references and candidate validation, approximately `B * U + R + C * M`, with environment predicate work added. Input preparation, alias construction and hash lookup costs are additional. Lazy success can stop much earlier. In broad ambiguous cases the matching subset can be large, even close to the map size, but total map recipe count alone does not imply that happens on every lookup. This follows from the iterator and lazy stream, not a measured timing result.

Registration and rebuild are separate from hot lookup. Model 1 still flattens, pools, sorts and inserts every ordinary variant. Terminal duplicate-membership checks scan existing leaf references. Inserting many distinct variant objects in one leaf can therefore accumulate quadratic reference-check work in that leaf, although a two-profile example has only a very small number of such checks. Alias expansion can multiply insertion work and references. Current collision admission must also be addressed before a same-input pair is accepted. [Leaf membership check][family-insertion] [Builder work][family-build]

Full backend rebuilds iterate all recipe objects. NEI cache creation likewise iterates visible recipes and sorts them, rather than performing a hot machine input lookup. More static variants do grow those collections and that cold-path work even when the trie path is shared. [Backend rebuild][family-rebuild] [NEI cache construction][family-nei]

### Two Different Family Representations

| Concern | 1. Ordinary static variants grouped by existing leaf and authoring | 2. First-class indexed family with common inputs and immutable output profiles |
| --- | --- | --- |
| Input lookup memory | Shared path nodes where normalized order matches, plus recipe references per variant and alias path | One family reference per indexed common-input path. Existing alias normalization still applies |
| Recipe-data memory | One full GTRecipe per profile, including its input arrays, metadata and recipe state | Can own common input data once plus per-profile outputs/requirements. If all profiles are also materialized as full GTRecipes, much of that saving disappears |
| Registration | Processes each variant and must permit the intentional collision | Can register/index the common signature once and account for alternatives within that owner. Existing collision rules still need a coherent family meaning |
| Hot selection | Input validation repeats per distinct candidate until one passes environment checks | Can validate common inputs once per matching family, then select locally among profiles before producing an effective recipe |
| NEI | Naturally creates a static display per profile | Can still expose all profiles. If each remains a display page, output/display data and page count still scale with profile count |
| Query/cache | Existing public results and hints are GTRecipe objects | Needs an explicit distinction between family lookup and selected effective GTRecipe. Current cache slots do not already encode that distinction |
| Locks and persistence | Must handle duplicate first-match restoration and define exact-variant versus family lock behavior | Must define family/profile identity for caches, locks and restoration. Indexing once does not answer that contract |
| Processing callers | Already receive an ordinary recipe, provided selection occurs early enough | Can retain that processing contract if an ordinary effective recipe is selected before validation/protection/consumption. Current queries lack world/controller context, so the selection context still has to enter the existing owner coherently |

The input-memory saving in model 2 is conditional, not automatic. GTRecipe currently exposes mutable input/output arrays and recipe fields. A genuinely immutable family/profile owner cannot safely assume every existing consumer treats those arrays as immutable. Materializing an effective recipe at each start trades retained object memory for construction work. Retaining full effective recipes for each profile keeps more object memory. Neither choice was made or benchmarked here. [Existing recipe data contract][family-recipe-fields]

Model 1 is close to the owner's requested runtime shape when a common leaf contains only that family, but a generic leaf can also hold unrelated recipes with different quantities, special-slot behavior or overlapping aliases. The trie deliberately omits quantity checks. A bucket is therefore not automatically a semantic family with one complete common-input contract. Authoring grouping can hide repeated recipes from authors, but does not by itself remove their runtime objects, registration work or NEI entries.

Model 2 has a real additional semantic benefit: the family owns what is common and what varies. It can make named alternatives, exclusivity, common-input validation and selected-profile identity explicit. That is a valid reason to prefer it independent of a performance claim. It is more native GT API/data-model work than letting existing leaves retain ordinary candidates. The main difficulty is shared contract changes, not building a fast new search engine.

### Native GT Fit And Difficulty

The cohesive owners remain RecipeMapBackend, GTRecipeLookup and its builder, FindRecipeQuery, and GT's recipe authoring/data model. The current node and iterator payloads, backend cache, category collections and query return types are all GTRecipe-oriented. A first-class family deepens those existing responsibilities. A separate Galaxia lookup/store would duplicate normalization, indexing, collision admission, rebuilds, cache behavior and display discovery, while leaving normal GT callers able to bypass it. No such duplicate path is justified by the observed index behavior.

Relative difficulty is moderate shared work for grouped ordinary variants, and materially larger shared API/data-model work for a true first-class family. The latter is feasible in native GT, but not a small extra metadata flag. Processing can still reuse ordinary static recipe calculations after selection, so it does not require replacing overclocking, parallel, batch or output protection with a second engine. Actual effort depends on the chosen family/profile lock and saved-identity contracts and the supported special machine paths, not on a fabricated hour estimate.

The earlier copy, consumption and lifecycle constraints remain. Selection must return the complete effective output profile before output checks and consumption. It must not mutate the globally indexed recipe or switch outputs after an operation starts. Unknown data and absent-Galaxia behavior remain distinct. A first-class family makes ambiguity easier to represent but does not decide what should happen when all environment requirements are ignored in a GT-only development run.

### Fixed-Input Sc Example

The two models can both express one fixed input batch, for example five Sc dust plus the same circuit and any common fluids, with identical base EU/t, duration and heat. No Atmosphere selects full hot-metal yield. Atmosphere selects reduced hot-metal yield plus a proposed oxide profile carrying the remaining elemental Sc. The supplied five metal units versus three metal units plus an oxide batch carrying two Sc units remains an illustrative conservation example, not approved recipe numbers or compound registration.

Model 1 can put two complete static recipes on a shared normalized lookup path. Model 2 indexes the common batch once, then chooses the corresponding immutable output profile before exposing an ordinary effective recipe to EBF processing. Both retain the same output protection, heat/overclock, parallel and batch requirements. Neither may leave the generated unconditional one-dust Sc blast recipe as a bypass. The concrete generator owner is ProcessingDust, unchanged at the new inspected upstream. [Current generated blast owner][family-sc-blast]

Recommendation under the clarified intent: do not reject model 2 merely because model 1 is cheaper to integrate. Prefer model 1 only if authoring-level family grouping plus existing shared buckets genuinely satisfies the desired contract. Prefer model 2 when one common-input owner with explicit output-profile identity is itself required. Keep either representation within GT's existing recipe/index owners. There is no source-backed claim that two ordinary variants cause a full-map search, and no benchmark evidence that explicit families are required for performance.

This follow-up stayed read-only, with no tests, benchmarks, new framework or implementation sequence. No MCP failure occurred. The reported index parse gaps are outside these owning Java files. Only this source note was appended and it remains unreviewed.

[family-commit]: https://github.com/GTNewHorizons/GT5-Unofficial/commit/2856a652b29ecf17dd5529880d589bea92a83b9f
[family-insertion]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/api/recipe/lookup/GTRecipeLookup.java#L43-L107
[family-flatten]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/api/recipe/lookup/GTRecipeLookupBuilder.java#L144-L180
[family-order]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/api/recipe/lookup/GTRecipeLookupBuilder.java#L103-L134
[family-build]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/api/recipe/lookup/GTRecipeLookupBuilder.java#L49-L100
[family-rebuild]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/api/recipe/RecipeMapBackend.java#L319-L348
[family-traversal]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/api/recipe/lookup/GTRecipeLookup.java#L127-L187
[family-stream]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/api/recipe/RecipeMapBackend.java#L469-L516
[family-recipe-class]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/api/util/GTRecipe.java#L50
[family-branch]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/api/recipe/lookup/GTRecipeLookupBranch.java#L7-L54
[family-cache-storage]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/api/recipe/RecipeMapBackend.java#L92-L98
[family-cache-hash]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/api/recipe/RecipeMapBackend.java#L530-L553
[family-query]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/api/recipe/FindRecipeQuery.java#L66-L96
[family-nei]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/nei/GTNEIDefaultHandler.java#L163-L205
[family-recipe-fields]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/api/util/GTRecipe.java#L64-L109
[family-sc-blast]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/2856a652b29ecf17dd5529880d589bea92a83b9f/src/main/java/gregtech/loaders/oreprocessing/ProcessingDust.java#L100-L118
