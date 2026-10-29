---
type: source
status: unreviewed
tags:
  - galaxia/alpha
  - wayfinder/source
---

# GT5 Cleanroom And Low Gravity Requirements Research

Source: Current primary source in GTNewHorizons/GT5-Unofficial, commit `bc7a940f5e6583b5c79d049635d1586c8f4ad764`
Imported: 2026-10-10

[[Sources]]

## Source Snapshot

> Current-use note, 2026-10-23: the retained-work pause requirement below was withdrawn. Native GT machine-specific failure behavior is now required by Define Alpha Research and Production Floor. Preserve the dated code findings, but do not implement the superseded pause proposal.

### Scope And Provenance

This is research, not an accepted architecture decision or an implementation plan. It covers ordinary recipe-backed singleblocks, common multiblock processing, the EBF as a concrete heat-owning multiblock, cleanroom references and NEI display. It is not an exhaustive audit of custom controllers, every recipe registration or all machines in the modpack.

Inspected GT revisions were upstream `bc7a940f5e6583b5c79d049635d1586c8f4ad764` and local `2259bc64244f9f7fc58e039d8e89ca40dd17c929`. [Inspected commit][commit]

These findings establish source-level behavior, not in-game verification.

### What LOW_GRAVITY Actually Means

`LOW_GRAVITY` is Boolean recipe metadata with identifier `low_gravity`. Authors use `.metadata(LOW_GRAVITY, true)` or `.requiresLowGravity()`. `CLEANROOM` is another Boolean metadata key, authored directly or with `.requiresCleanRoom()`. Neither key supplies a gravity magnitude, pressure, atmosphere, local volume or position. [Constants][constants] [Builder][builder]

The common singleblock predicate `MTEBasicMachine.isValidForLowGravity` does not query physics. Apart from the explicit developer bypass, it accepts a dimension whose provider class name contains `Orbit`, `SpaceStation` or `Mothership`, or ends with `Space`, `Asteroids` or `SS`. The recipe argument is unused. Therefore the name is not a numeric low-gravity threshold and is not a reliable zero-gravity contract. A Galaxia zero-gravity rule should not be presented as the existing GT predicate without an explicit semantic change. No separate zero-gravity predicate appears in the inspected common paths. [Singleblock gravity predicate][basic-gravity]

### How Flags Are Encoded And Where They Collide

When a built recipe has a zero `mSpecialValue`, `applyDefaultSpecialValues` encodes low gravity as `-100`, cleanroom as `-200`, and both as `-300`. A pre-existing nonzero special value bypasses this encoding. Numeric special-value aliases subsequently replace the flag-derived value. `COIL_HEAT` is in that alias set. Thus cleanroom or gravity metadata can remain attached while their negative sentinel is replaced by heat, and the old consumers only inspect the sentinel. [Encoding][builder-encoding] [Alias registration][constants-aliases]

The EBF reads `mSpecialValue` as required recipe heat. Its validation override only compares that heat against machine heating capacity, and its overclock calculator also uses it as recipe heat. The blast furnace map uses a heating-coil special-info formatter. Adding old flags to a heat recipe does not create an independent environment contract. [EBF][ebf] [Recipe map][maps] [Heat formatter][heat-display]

### Existing Singleblock Validation

The normal `MTEBasicMachine.checkRecipe` path behaves as follows:

- Low gravity is checked for exactly `-100` and `-300`, and only while `GTMod.proxy.mLowGravProcessing` is true
- Cleanroom is checked for exactly `-200` and `-300`. It needs a reference, `isValidCleanroom()` and nonzero cleanness
- These checks occur before `isRecipeInputEqual(true, ...)` consumes ingredients, so a failure at this gate leaves recipe inputs untouched
- After consumption, item outputs are rolled. For cleanroom recipes, each non-null item output may be voided when a random value from the 10000 scale is greater than room cleanness
- The inspected fluid-output branch does not apply the cleanroom yield roll

This is a start-time check and yield model, not an ongoing cleanroom permission check. Common singleblock `onPostTick` advances the running operation without revisiting these environmental checks. A room becoming invalid does not, through these base paths, pause the operation already in flight. [Singleblock recipe check][basic-check] [Singleblock runtime][basic-runtime]

### Existing Multiblock Validation

Common `ProcessingLogic.validateRecipe` returns success by default. `validateAndCalculateRecipe` invokes the override before `ParallelHelper.build()`. The normal helper has consumption enabled. This is a useful pre-consumption extension point, but adding logic only to the overridable default method would not cover controllers whose overrides do not call `super`, such as the EBF. A mandatory shared gate belongs in the common dispatch around the override, not in the default override body alone. [Processing dispatch][processing-dispatch] [Validation and consumption][processing-validation] [EBF][ebf]

The same common dispatch is used by ordinary recipe iteration, the dual-input pattern cache and single-recipe locking. This is more useful than changing one controller's `checkRecipe`. `MTEMultiBlockBase.checkProcessing` sets up common processing, then transfers its calculated duration, EU use and pending outputs after inputs have been consumed. A legacy branch is used when no `ProcessingLogic` exists. Legacy and custom paths are a coverage limit, not a reason to claim universal enforcement. [Processing dispatch][processing-dispatch] [Multiblock check processing][multi-processing]

This research does not propose enabling the existing GT cleanroom or low-gravity flags on all multiblocks. Some differences are intentional. For example, the universal chemical-recipe helper explicitly sets `CLEANROOM` false for the large chemical reactor version. Globally changing old flag semantics would be a separate gameplay change. [Chemical recipe helper][chemical]

### NEI And Absent Mods

Default special-value display shows low gravity for `-100` only if `mLowGravProcessing` is enabled. It shows cleanroom for `-200` only if `mEnableCleanroom` is enabled. The combined `-300` message is gated only by `mEnableCleanroom`, not independently by low-gravity enforcement. Consequently the combined line can still mention low gravity when that part is disabled. The EBF's heat formatter displays heat instead of using this default formatter. [Default display][default-display] [Heat formatter][heat-display]

The current English labels are `Needs Low Gravity`, `Needs Cleanroom` and `Needs Cleanroom & LowGrav`. They are rendered through translation keys, not authored as recipe descriptions. [English localization][english]

During preload, `mLowGravProcessing` is set to `GalacticraftCore.isModLoaded() && Gregtech.general.lowGravProcessing`. Initialization also forces it false when cleanroom is disabled. Without Galacticraft Core, existing low-gravity enforcement is already ignored in common singleblocks. This is specifically tied to Galacticraft, not to whichever space mod might provide suitable dimensions. [Preload][preload] [Initialization][init] [Configuration][config]

Cleanroom belongs to GT and does not depend on Galaxia or Galacticraft being installed. The cleanroom config controls registration and display, but the inspected singleblock `-200`/`-300` validation is not guarded by that config. Hiding a cleanroom label does not prove that an explicitly authored sentinel recipe will be allowed without a room. Do not describe config disablement as a universal cleanroom bypass. [Singleblock check][basic-check] [Default display][default-display] [Configuration][config]

GT also has explicit `FakeCleanroom` developer bypasses. The fake room is valid with cleanness 10000, and the low-gravity predicate accepts its separate bypass flag. `gt cleanroom_bypass` changes these flags. This is not the requested absent-Galaxia policy, since it affects GT's existing requirements. [Fake cleanroom][fake] [Bypass command][bypass]

### Cleanroom Ownership And Lifecycle Reuse

`ICleanroom` exposes cleanness, validity and pollution. `MTECleanroom.getCleanness` returns efficiency, while validity means the controller is valid and its structure is formed. Pollution sets efficiency to zero and clears its maintenance flags. The room has its own powered processing cycle that increases efficiency. [Cleanroom interface][room-interface] [Cleanroom owner][room]

Every `MetaTileEntity` already owns a `cleanroomReference` and exposes the `ICleanroomReceiver` capability. `CleanroomReference` returns the attached room unless the explicit fake-room bypass is enabled. This inherited capability can apply to a multiblock controller without inventing a second cleanroom index or changing machine ownership. [Machine capability][meta] [Reference][reference]

At each room structure check, the owner first clears its previous receivers, validates the structure, then finds receiver capabilities on tile entities in the interior and attaches itself. It schedules another check with `mUpdate = 100`. An open door reduces efficiency by 200 during the structure check. This is the existing spatial and lifecycle authority to reuse. Do not equate room membership with an airtight habitat, numeric purity threshold or immediate invalidation guarantee. These are different contracts. [Cleanroom structure and receivers][room-receivers]

For Alpha, the selected environmental lookup point is the multiblock controller position. Existing room membership already locates the receiver tile. `ProcessingLogic.setMachine` currently accepts `IVoidable`, which is for output handling rather than an environmental/location contract. Although setup supplies `this`, a neutral environment integration should expose controller world/position deliberately rather than pretending every `IVoidable` has a location. [Processing context][processing-context] [Multiblock setup][multi-setup]

### Feasible Neutral Extension Boundary

The following is an inference from the inspected extension points, not a final API design:

- GT can hold extra environmental requirements as recipe metadata independent of `mSpecialValue`, preserving heat and old sentinel semantics
- GT owns a neutral opt-in validator boundary. Galaxia registers an implementation that evaluates its tags at the machine or controller location. GT must not import Galaxia classes or interpret Galaxia's celestial and habitat model
- The common dispatch checks extra requirements before consuming inputs, including controller-specific validation overrides. Ordinary singleblocks need their corresponding start gate
- NEI's metadata rendering is already independent of the special-value formatter. `RecipeMapFrontend.drawMetadataInfo` invokes each key's `drawInfo`, so extra labels need not replace heat or cleanroom display
- With no Galaxia implementation registered, its extra requirements are successful and produce no labels. This is the user-requested absent-mod behavior for the extra extension only, not a global fallback or bypass of existing GT requirements

The existing `SimpleRecipeMetadataKey` renders nothing. A neutral typed key can choose registered-provider display, or Galaxia can supply its own key when it is the author. If GT-side authors must retain Galaxia-tagged requirements in GT-only development, their data and keys must be GT-owned neutral values that do not load Galaxia types. Client display and server enforcement must use the same availability policy. Custom frontends that replace metadata drawing remain a coverage question. [Recipe metadata][recipe-metadata] [Metadata display][frontend] [Simple metadata key][simple-key]

One concrete metadata pitfall needs attention if recipe-copy paths are part of the accepted implementation scope. At the inspected commit, `GTRecipe.copy()` and `copyShallow()` call a constructor that assigns `EmptyRecipeMetadataStorage.INSTANCE`, rather than copying the source metadata. Builder construction does copy metadata. The required authoring and copy path must be checked before relying on metadata surviving recipe transformation. This research does not establish that an intended Galaxia recipe traverses such a copy path, and does not authorize a broad copy fix. [Recipe copy constructor][recipe-copy]

### Retained-Work Pause Gaps

The user accepts pausing when local requirements cease, with inputs and progress retained. GT's ordinary transaction consumes inputs at recipe start and stores pending outputs and progress. Retaining work therefore naturally means retaining that in-flight transaction, not returning consumed items to hatches. Literal input reservation until completion would be a different, larger transaction design. [Multiblock processing][multi-processing] [Processing apply][processing-apply]

Existing `MTEMultiBlockBase.stopMachine` is unsuitable for that pause. It clears pending item and fluid outputs, EU use, efficiency, progress and duration, sets shutdown status and disables work. Reusing it would lose the operation. Common singleblocks also have an energy-stutter mechanism that can replace progress with `-100`. That is not a retained-progress environmental pause. [Multiblock stop][multi-stop] [Singleblock runtime][basic-runtime]

A retained-work environment pause needs these capabilities, none established by the current environment checks:

- An active-operation requirement record, separate from the optional search cache. `ProcessingLogic.lastRecipe` is null for non-bufferable recipes, so it is not a universal active-operation record
- A runtime gate before energy drain, maintenance side effects, pollution and progress advance. It must skip the work branch without calling destructive shutdown
- Automatic retries and a visible suspended status that do not require a new recipe search or fresh input consumption
- Preserve progress, duration and already-rolled outputs across temporary loss of environmental validity
- Save enough active requirement data to keep the same contract after unload/reload if resumable operations across reload are included
- Clear active requirement data on completion and deliberate cancellation. Existing fault shutdowns stay distinct

The multiblock base sets its active flag from `mMaxProgresstime > 0`, so a retained operation needs explicit suspended-state presentation rather than leaving it visibly running merely because duration remains positive. Structure-invalid and power-loss paths are separate existing shutdown reasons. This research does not propose changing those behaviors. [Runtime and active flag][multi-runtime] [Runtime work branch][multi-run] [Processing cache][processing-apply]

### Bounded Conclusion

Existing GT low gravity is not a zero-gravity API. Existing cleanroom references and metadata display provide reusable ownership and rendering capabilities, but common multiblock enforcement and retained-work pause require new shared behavior. Independent extra metadata plus a neutral, optional evaluator can satisfy absent-Galaxia hidden-and-ignored behavior without a reverse dependency or a global bypass. The API shape, coverage of custom processing paths and reload contract remain design decisions.

[commit]: https://github.com/GTNewHorizons/GT5-Unofficial/commit/bc7a940f5e6583b5c79d049635d1586c8f4ad764
[constants]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/api/util/GTRecipeConstants.java#L45-L56
[builder]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/api/util/GTRecipeBuilder.java#L750-L756
[builder-encoding]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/api/util/GTRecipeBuilder.java#L1174-L1199
[constants-aliases]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/api/util/GTRecipeConstants.java#L788-L800
[basic-gravity]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/api/metatileentity/implementations/MTEBasicMachine.java#L1061-L1088
[basic-check]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/api/metatileentity/implementations/MTEBasicMachine.java#L1096-L1156
[basic-runtime]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/api/metatileentity/implementations/MTEBasicMachine.java#L595-L638
[ebf]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/common/tileentities/machines/multi/MTEElectricBlastFurnace.java#L188-L207
[maps]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/api/recipe/RecipeMaps.java#L851-L858
[heat-display]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/nei/formatter/HeatingCoilSpecialValueFormatter.java#L22-L30
[processing-dispatch]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/api/logic/ProcessingLogic.java#L385-L477
[processing-validation]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/api/logic/ProcessingLogic.java#L548-L572
[processing-apply]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/api/logic/ProcessingLogic.java#L479-L516
[processing-context]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/api/logic/ProcessingLogic.java#L90-L96
[multi-processing]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/api/metatileentity/implementations/MTEMultiBlockBase.java#L1098-L1124
[multi-setup]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/api/metatileentity/implementations/MTEMultiBlockBase.java#L1138-L1146
[multi-runtime]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/api/metatileentity/implementations/MTEMultiBlockBase.java#L614-L666
[multi-run]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/api/metatileentity/implementations/MTEMultiBlockBase.java#L813-L875
[multi-stop]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/api/metatileentity/implementations/MTEMultiBlockBase.java#L1434-L1458
[chemical]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/api/util/GTRecipeConstants.java#L396-L400
[default-display]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/nei/formatter/DefaultSpecialValueFormatter.java#L20-L35
[preload]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/loaders/preload/GTPreLoad.java#L348-L349
[init]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/GTMod.java#L402-L405
[config]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/common/config/Gregtech.java#L292-L300
[fake]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/api/util/FakeCleanroom.java
[bypass]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/common/misc/GTMiscCommand.java#L210-L254
[room-interface]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/api/interfaces/ICleanroom.java
[room]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/common/tileentities/machines/multi/MTECleanroom.java#L122-L141
[room-receivers]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/common/tileentities/machines/multi/MTECleanroom.java#L610-L709
[meta]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/api/metatileentity/MetaTileEntity.java#L175-L184
[reference]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/common/capability/CleanroomReference.java
[recipe-metadata]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/api/util/GTRecipe.java#L802-L827
[recipe-copy]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/api/util/GTRecipe.java#L161-L183
[frontend]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/api/recipe/RecipeMapFrontend.java#L213-L245
[simple-key]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/api/recipe/metadata/SimpleRecipeMetadataKey.java#L15-L26
[english]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/resources/assets/gregtech/lang/en_US.lang#L10437-L10439
