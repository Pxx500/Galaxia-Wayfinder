---
type: source
status: unreviewed
tags:
  - galaxia/alpha
  - wayfinder/source
---

# GT5 Team Knowledge Recipe Enforcement Research

Source: Bounded primary-source inspection of current GT5 recipe execution and owner identity, plus current local Galaxia team integration
Imported: 2026-10-08

## Source Snapshot

The accepted requirement is that automated production uses the machine owner's team's Technology Knowledge and checks it before execution. This note identifies concrete integration points, not an accepted architecture or implementation plan. The owner chose temporary transferable GT content in `com.gtnewhorizons.galaxia.gt5`, with final materials, items, chains and balancing in GT. Team knowledge and space mechanics remain Galaxia responsibilities.

### Source Versions And Scope

GT primary source inspected at remote default-branch commit `5fd9d97ea95900655d6ffe521b6ac700fdcd58a5`, dated 2026-10-07. Latest published release identified during this research is `5.09.54.216`, tag commit `733c830470584e61d5245f84ce61197b052bf6e0`. Local GT HEAD is `2259bc64244f9f7fc58e039d8e89ca40dd17c929`. This research uses current source, not Galaxia's older declared `5.09.54.64` dependency.

Galaxia local HEAD: `a9128e9ef21ff05254648190b4f79f94bdc9669d`. Its graph was indexed once after the original main-project lookup failed. GT graph discovery supplied the relevant owners. Exact latest GT excerpts were verified through successful HTTP 200 retrievals at the immutable commit.

Inspection covered normal single-block recipe processing, shared multiblock processing, parallel consumption, normal machine ownership, recipe lookup filtering, metadata and Galaxia team compatibility. It did not establish coverage of every specialized or legacy multiblock implementation. No production changes, builds, server updates or publication were performed.

### Normal Single-Block Execution

[MTEBasicMachine.java](https://github.com/GTNewHorizons/GT5-Unofficial/blob/5fd9d97ea95900655d6ffe521b6ac700fdcd58a5/src/main/java/gregtech/api/metatileentity/implementations/MTEBasicMachine.java#L1096), `checkRecipe(boolean)`, lines 1096-1133:

```java
GTRecipe tRecipe = tMap.findRecipeQuery()
    .items(getAllInputs())
    .fluids(getFillableStack())
    .specialSlot(getSpecialSlot())
    .voltage(V[mTier])
    .cachedRecipe(mLastRecipe)
    .find();
```

Existing compression, gravity, output-space and cleanroom checks happen after selection. Input consumption occurs at line 1132:

```java
if (!tRecipe.isRecipeInputEqual(true,
    new FluidStack[] { getFillableStack() }, getAllInputs()))
    return FOUND_RECIPE_BUT_DID_NOT_MEET_REQUIREMENTS;
```

Concrete early rejection location: after selecting the recipe, before this consuming call. The method has recipe and `getBaseMetaTileEntity()` available. Its existing failure result is `FOUND_RECIPE_BUT_DID_NOT_MEET_REQUIREMENTS`, not the multiblock `CheckRecipeResult` API.

The existing query also has a [per-query predicate](https://github.com/GTNewHorizons/GT5-Unofficial/blob/5fd9d97ea95900655d6ffe521b6ac700fdcd58a5/src/main/java/gregtech/api/recipe/FindRecipeQuery.java#L142): `filter(Predicate<GTRecipe>)`. It can reject one candidate and let lookup try another. The predicate runs after backend lookup and voltage filtering, including cached candidates. The stock basic-machine query does not attach a knowledge predicate. Adding metadata to a recipe alone does not install one.

### Normal Multiblock Execution

[MTEMultiBlockBase.java](https://github.com/GTNewHorizons/GT5-Unofficial/blob/5fd9d97ea95900655d6ffe521b6ac700fdcd58a5/src/main/java/gregtech/api/metatileentity/implementations/MTEMultiBlockBase.java#L1099), `checkProcessing()`, lines 1099-1112, sets up processing logic, calls `doCheckRecipe()`, then performs `postCheckRecipe()` and updates slots. Inputs have already been consumed by that latter stage.

`setupProcessingLogic()` at 1136-1143 calls `logic.setMachine(this)`, sets the recipe-map supplier and recipe-locking context. The shared logic holds this as `protected IVoidable machine`, not directly as an owner UUID. For ordinary GT controllers this object is the metatile entity, whose base tile provides identity.

[ProcessingLogic.java](https://github.com/GTNewHorizons/GT5-Unofficial/blob/5fd9d97ea95900655d6ffe521b6ac700fdcd58a5/src/main/java/gregtech/api/logic/ProcessingLogic.java#L460), private `validateAndCalculateRecipe()`, lines 460-476:

```java
CheckRecipeResult result = validateRecipe(recipe);
if (!result.wasSuccessful()) {
    return CalculationResult.ofFailure(result);
}
ParallelHelper helper = createParallelHelper(recipe);
OverclockCalculator calculator = createOverclockCalculator(recipe);
helper.setCalculator(calculator);
helper.build();
```

This is the concrete pre-consumption seam for controllers using shared ProcessingLogic. Ordinary candidate iteration, recipe-locked execution and dual-input cached recipes all call this method at lines 411, 432 and 440. A gate at this common point therefore avoids relying only on fresh lookup.

The existing protected `validateRecipe()` is an extension point for individual machines. It is not an external registration hook. Patching only its default implementation would not establish blanket coverage because machine overrides can return without calling `super`, including the ordinary EBF heat validator already inspected.

[ParallelHelper.java](https://github.com/GTNewHorizons/GT5-Unofficial/blob/5fd9d97ea95900655d6ffe521b6ac700fdcd58a5/src/main/java/gregtech/api/util/ParallelHelper.java#L488) consumes inputs during its build path, with direct calls at 490, 495 and 497 and batch-mode calls at 523. `ProcessingLogic.createParallelHelper()` enables consumption at 570.

**Do not use the later start hook for authorization.** `onRecipeStart()` documentation at 592-595 states that inputs are already consumed and an unsuccessful result voids them. `MTEMultiBlockBase.postCheckRecipe()` documentation at 1302-1306 also warns about consumed inputs. These hooks are real but too late for this contract.

A machine can override `checkProcessing()` or use the legacy `checkRecipe(ItemStack)` path when no processing logic exists. Such machines need explicit coverage assessment if knowledge-gated recipes can execute there. This bounded audit does not imply all GT multiblocks pass through the shared seam.

### Recipe Metadata And Lookup

[GTRecipe.java](https://github.com/GTNewHorizons/GT5-Unofficial/blob/5fd9d97ea95900655d6ffe521b6ac700fdcd58a5/src/main/java/gregtech/api/util/GTRecipe.java#L802) supports typed `RecipeMetadataKey<T>` access through `getMetadata()` and `getMetadataOrDefault()`. This can carry a stable technology identifier without a Galaxia class in the recipe's value. It does not itself execute a knowledge check. No existing Technology Knowledge identifier/key was established by this audit.

The examined [RecipeMapBackend.filterFindRecipe](https://github.com/GTNewHorizons/GT5-Unofficial/blob/5fd9d97ea95900655d6ffe521b6ac700fdcd58a5/src/main/java/gregtech/api/recipe/RecipeMapBackend.java#L556) receives recipe, item/fluid inputs, special slot and stack-size mode, not a machine or owner. Builder/recipe transformers run at registration, not as per-team execution checks. Global `mEnabled` changes would affect every team, so they are not a per-owner authority seam.

`RecipeLookupValidator` is a diagnostic lookup-validation tool, not a runtime player/team gate. Recipe `owners` in diagnostic output means contributing mod containers, not the owner of a placed machine.

### Machine Owner Identity

[IGregTechTileEntity.java](https://github.com/GTNewHorizons/GT5-Unofficial/blob/5fd9d97ea95900655d6ffe521b6ac700fdcd58a5/src/main/java/gregtech/api/interfaces/tileentity/IGregTechTileEntity.java#L102) exposes `getOwnerUuid()`, `setOwnerUuid(UUID)`, `getOwnerName()` and `setOwnerName(String)`.

[BaseMetaTileEntity.java](https://github.com/GTNewHorizons/GT5-Unofficial/blob/5fd9d97ea95900655d6ffe521b6ac700fdcd58a5/src/main/java/gregtech/api/metatileentity/BaseMetaTileEntity.java#L117) stores player UUID and display name, not team UUID. UUID starts as `GTUtility.defaultUuid`. NBT persists both fields at 143-144. Invalid UUID parsing sets it to null at 188-191. Getter returns that stored UUID directly at 1818-1819.

[ItemMachines.java](https://github.com/GTNewHorizons/GT5-Unofficial/blob/5fd9d97ea95900655d6ffe521b6ac700fdcd58a5/src/main/java/gregtech/common/blocks/ItemMachines.java#L275) assigns placing-player display name and UUID after loading item NBT at 277-280, when a player is available. Non-player placement does not execute those assignments. Other existing ownership setters occur on lock installation and first-access paths. Consequently, owner availability is real but not guaranteed to be a valid current player for every placement path. Display-name lookup is not needed for recipe authorization.

### Galaxia Team Resolution And Dependency Direction

Local `src/main/java/com/gtnewhorizons/galaxia/compat/teams/GTTeamsCompat.java:27-29` already uses GTNHLib's UUID-based server lookup:

```java
Team team = TeamManager.getTeamByPlayer(player.getUniqueID());
return team.getTeamId();
```

The same existing `TeamManager.getTeamByPlayer(UUID)` operation can receive the machine owner's UUID directly. No online `EntityPlayer` is intrinsically required by that call signature. The current wrapper exposes player-taking methods, not a dedicated machine-owner lookup. Its other helpers handle nullable team lookup with `Optional` or permission denial. The Teams library's exact missing-player/default-team semantics were not separately inspected.

`GalaxiaTeamData.java` currently persists team color and permissions and defines transfer/merge handling. It does not establish a Technology Knowledge store. The graph found celestial discovery/resource knowledge and reusable Rocket Blueprints, not the accepted consumed Technology Blueprint implementation. Do not substitute those concepts for Technology Knowledge.

Dependency-neutral possibility, not a decision: a GT-owned execution contract can ask a caller-supplied policy about a stable requirement ID plus machine identity. Galaxia can own the team lookup and knowledge answer. GT need not import Galaxia's team/store classes. Such a registration contract is **new work**, not an existing API found here. Another temporary possibility is downstream instrumentation of the two concrete GT execution seams. That also adds integration code and must track GT changes. Merely putting content in `com.gtnewhorizons.galaxia.gt5` does not solve enforcement.

### Remaining Holes And Decisions

- Current team lookup versus captured placement-team semantics is not settled by GT's stored player UUID. The accepted wording is machine owner's team. Membership changes and ownership changes need an explicit policy, not an accidental cache behavior.
- Null/sentinel owner, non-player placement, and unresolved team outcomes need deliberate behavior for gated recipes.
- Recipe caches and locked recipes must still check current authority before each new execution. The multiblock shared seam covers their inspected entry paths.
- A parallel run's inputs are consumed together. This audit proves the start-time seam, not a mid-run revocation policy.
- Multiblock failure results must fit the registered `CheckRecipeResult` mechanism. `MTEMultiBlockBase.checkRecipe()` checks result registration. Single-block machines have a different integer failure/UI path.
- Neither a safe GT-neutral policy registration API nor the Galaxia Technology Knowledge storage/query was established as implemented.

### Parent-Supplied Environmental Evidence

Separately verified by the parent at Galaxia commit `a9128e9ef21ff05254648190b4f79f94bdc9669d`: `CelestialBodyProperties.java:20-25` owns `localGravityG` and `surfacePressurePa`. `GalaxiaCelestialAPI.findByDimension(int):54-57` resolves the machine's world dimension to a body. `CelestialDimensionMaterializer.materializeDefinition():58-82` derives dimension gravity from body properties. `GalaxiaAPI.getGravity(Entity):68-75` defaults to 1 for null/unknown entities, so a recipe check should not fabricate an Entity to obtain environment data. This is an environment source, not a finished recipe predicate or proof of station-local vacuum modeling.

[[Sources]]
