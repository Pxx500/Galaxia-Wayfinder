---
type: source
status: unreviewed
tags:
  - galaxia/alpha
  - wayfinder/source
---

# GT5 Combustion Generator Oxygen Requirements Research

Source: Current primary source in GTNewHorizons/GT5-Unofficial, commit `bc7a940f5e6583b5c79d049635d1586c8f4ad764`
Imported: 2026-10-10

[[Sources]]

## Source Snapshot

### Purpose And Evidence

The initial request was to stop combustion-based generators when oxygen is unavailable. The owner then selected a complete combustion-generator ban in space, including inside oxygenated Stations. Ventilation, exhaust and new direct oxygen-input solutions are not part of this task. This note records current generator behavior and a bounded check of existing non-combustion power near HV. It does not decide the machine-family boundary, design hooks or expand the separate recipe-environment implementation.

On 2026-10-10 the GitHub commits API reported upstream master at `bc7a940f5e6583b5c79d049635d1586c8f4ad764`, committed 2026-10-09 at 20:39:09 UTC. The sibling local checkout remained clean at `2259bc64244f9f7fc58e039d8e89ca40dd17c929`. Its graph was fully reindexed for discovery. The consumption methods, family definitions and registrations below were then checked using successful HTTP 200 reads of immutable source URLs at the current master SHA. No codebase-memory executable, source, dependency, build, server binary or game state was changed. [Inspected commit][commit]

This is bounded source research, not in-game verification or an audit of every generator in every mod. No Gradle or game tests were needed or run. The absence statements below apply to the inspected fuel and power-conversion paths, not arbitrary mixins or external modpack patches.

### Registered Ordinary Families

`LoaderMetaTileEntities.registerCombustionGenerators` creates ordinary diesel-backed combustion generators at LV, MV and HV using `MTEDieselGenerator`. `registerGasTurbines` creates `MTEGasTurbine` at LV, MV, HV, EV and IV. These are concrete registrations, not classification inferred from display names. [Ordinary registration][ordinary-registration]

`MTEDieselGenerator` extends `MTEBasicGenerator` and selects `RecipeMaps.dieselFuels`. `MTEGasTurbine` extends the same base and selects `RecipeMaps.gasTurbineFuels`. Diesel also has a filled fuel-can value override. Neither subclass supplies an oxygen or atmosphere predicate in its fuel handling. [Diesel definition and fuel value][diesel] [Gas definition][gas]

### Ordinary Fuel Consumption And Power Buffer

`MTEBasicGenerator.onPostTick` performs fuel-to-stored-EU conversion on the server every 10 ticks while work is enabled:

- The tank branch evaluates fuel value and `consumedFluidPerOperation`, limits consumption to available fuel and free EU capacity, increases stored energy, then decreases the tank amount
- A second branch can consume a filled container or supported item fuel. It places the empty container, increases stored EU and consumes one input stack unit
- Both branches add pollution after conversion
- The active display is derived from enabled work and stored EU, not from whether fuel was burned on that tick

There is no ambient oxygen, breathable-air, dimension or pressure check in this handler. The default fluid consumption unit is one. `getFuelValue(FluidStack, boolean)` looks up a fuel record and applies its special-value energy and efficiency, rather than running ordinary machine recipe validation. `FuelBackend.findFuel` indexes only by the input fluid's name. [Basic conversion][basic-conversion] [Fuel-value methods][basic-values] [Fuel backend][fuel-backend]

The existing `isAllowedToWork` result is the tile's `mWorks` flag. `maxEUOutput` is zero when work is disabled, while stored energy is a separate buffer. Stopping new fuel conversion and disabling EU output are therefore different existing operations. The inspected code does not define which one an oxygen-loss rule should mean. [Work flag][work] [Output and storage][basic-output]

### Large And Extreme Combustion Families

Both newer and Legacy engine families are still registered under separate entries. The old `Machine_Multi_DieselEngine` and `Machine_Multi_ExtremeDieselEngine` entries construct `MTEDieselEngineLegacy` and `MTEExtremeDieselEngineLegacy`. New `LargeCombustionEngine` and `ExtremeCombustionEngine` entries construct the corresponding newer classes. A `Legacy` suffix does not establish that the registered machine is unreachable. [Legacy engine registration][legacy-registration] [New engine registration][new-registration]

The newer large engine uses `dieselFuels`. The newer extreme engine uses `extremeDieselFuels`. Each has its own `checkProcessing` implementation and directly obtains tanked fluids, looks up fuel values and depletes inputs. These methods do not go through the normal `ProcessingLogic.validateRecipe` path. They set a one-tick operation and generating result. [Large fuel handler][large-processing] [Extreme map][extreme-map] [Extreme fuel handler][extreme-processing]

The existing oxygen inputs are boosters:

- Large engine `getBooster()` returns `Materials.Oxygen`
- Extreme engine `getBooster()` returns `Materials.LiquidOxygen`
- Their handlers first consume fuel, then attempt `depleteInput(getBooster().getGas(2L * getAdditiveFactor()))` and store its result in `boostEu`
- Missing booster generally changes the engine to unboosted operation rather than rejecting the operation
- A separate `fuel_quality_too_high` failure rejects fuels whose value exceeds nominal output when not boosted
- Lubricant remains a separate periodic input requirement
- `getMaxEfficiency` returns 30000 when boosted and 10000 otherwise

The booster attempt is a tank input, not an ambient oxygen measurement. It is not an existing mandatory oxygen supply contract for ordinary combustion. The current order also means fuel can already have been consumed before a later quality or lubricant failure. This note records that order without proposing a fix. [Large constants and booster][large-booster] [Large consumption][large-processing] [Large efficiency][large-efficiency] [Extreme booster][extreme-booster] [Extreme consumption][extreme-processing] [Extreme efficiency][extreme-efficiency]

`MTEDieselEngineLegacy.checkProcessing` uses the same fuel-then-optional-booster pattern. It chooses `dieselFuels` and oxygen. `MTEExtremeDieselEngineLegacy` inherits that consumption method, changes the map to `extremeDieselFuels` and changes the booster to liquid oxygen. These are separate currently registered paths to account for when defining coverage. [Legacy large handler][legacy-processing] [Legacy extreme overrides][legacy-extreme]

No ambient oxygen or atmosphere query occurs in these inspected engine handlers. Structure definitions contain engine-intake casings and structural empty regions, but that is not an atmospheric composition measurement. This audit does not reinterpret an unobstructed intake or Minecraft air block as oxygen. [Large structure][large-structure] [Extreme structure][extreme-structure]

### Large Gas Turbines

GT also registers both `MTELargeTurbineGasLegacy` and the newer `turbines.MTELargeTurbineGas`. Both use `gasTurbineFuels`. [Legacy gas registration][legacy-gas-registration] [New gas registration][new-gas-registration]

The newer gas turbine's `fluidIntoPower` selects the first fuel fluid, looks up its value, consumes matching input fluid through `depleteInput`, and calculates output from flow and turbine efficiency. The Legacy method follows the same basic direct conversion pattern. Neither method consumes oxygen or queries ambient conditions. [New gas conversion][large-gas] [Legacy gas conversion][legacy-gas]

The newer `MTELargeTurbineBase.checkProcessing` calls `fluidIntoPower` directly and smooths changes in `lEUt` before returning a generating result. Thus zero new calculated power is not necessarily an immediate zero `lEUt` result. This is an existing turbine runtime property, not an oxygen-loss decision. It also bypasses ordinary recipe validation. [Large turbine dispatch][turbine-base]

### Actual Non-Combustion Counterexamples

The shared generator or turbine base cannot by itself classify combustion. Checked source shows these distinct paths:

| Checked machine | Actual conversion | Oxygen fact in checked path |
| --- | --- | --- |
| `MTESteamTurbine` | Inherits basic generator conversion, but assigns fuel value only to steam and consumes an efficiency-dependent steam amount | No oxidizer consumption or ambient check |
| New `MTELargeTurbineSteam` | Consumes steam and emits distilled water while calculating mechanical turbine output | No combustion input in its conversion method |
| New `MTELargeTurbinePlasma` | Consumes `plasmaFuels` and emits the depowered fluid, such as helium | Not the gas-fuel combustion map and no oxygen input |
| `MTENaquadahReactor` | Inherits the basic generator buffer conversion, but selects separate tiered Naquadah reactor fuel maps | Sharing `MTEBasicGenerator` does not make it diesel or gas combustion |
| BartWorks `MTEThoriumHighTempReactor` | Requires helium and nuclear fuel supply, consumes fuel balls and coolant, and emits hot coolant | Its runtime consumes EU and produces heat-bearing coolant rather than generating EU through the combustion handler |

[Singleblock steam][steam] [Large steam][large-steam] [Plasma conversion][plasma] [Naquadah maps][naquadah] [THTR operation][thtr]

The steam consumer is also distinct from the device that made the steam. For example, the checked bronze boiler `updateFuel` uses furnace burn time, consumes an item, adds processing energy and produces ashes. Its `getCombustionPotential` classifies burnable solids. Therefore steam turbines being non-combustion does not establish that all upstream boilers are non-combustion. This is one source-backed distinction, not a request to expand this task to all boilers. [Bronze boiler fuel path][boiler]

### Coverage Limits And Planning Facts

The checked ordinary diesel, gas and large/extreme combustion fuel handlers have no ambient oxygen gate. Tanked oxygen in the large/extreme engines is optional boosting with a fuel-quality exception, not an atmosphere API. The owner's space ban does not grant an exception for this booster. Several generator families consume fuel outside normal processing validation, and the registered Legacy variants remain concrete paths. Power buffering and turbine ramp-down are separate from new fuel consumption. These are the factual constraints relevant to planning.

Not determined here: the complete family inclusion boundary, generator shutdown versus temporary suspension, retained fuel or buffered EU policy, and absent-Galaxia behavior for generators. No changes to steam, nuclear, plasma, boiler or third-party generator gameplay are accepted by this source note.

The graph also surfaced GT++ semifluid generators and other specialized families. Their combustion coverage was not audited. IC2 reactors, every bundled generator and external mods are outside this bounded pass. No API design or implementation specification is included.

### Small HV Bootstrap Source Check

GT defines HV as tier 3 with nominal voltage 512. The following existing registrations and input/output contracts were checked. This establishes source availability, not craftability at a particular progression point or enough throughput for a factory. [Voltage table][voltage]

Ordinary solar covers already exist. `MetaGeneratedItem01.registerCovers` registers the MV cover with voltage 128, HV with 512 and EV with 2048. `CoverSolarPanel.doCoverThings` requires placement on the upper side, tracks daytime and weather, and in its generating state attempts to inject one energy packet per minimum one-tick cover update. The packet voltage is its configured voltage reduced by accumulated dirt. The owner tile must accept the injection. Dirt increases over time, and cleaning consumes a water bucket unless the player is creative. The checked code uses ordinary world daytime and weather, not distance-to-star or a Galaxia irradiance calculation. Sky access is queried in weather branches. Do not assume an uninspected orbital world provider supplies the daytime/weather state needed for generation, or that a roof alone is checked in every branch. [Solar registration][solar-registration] [Solar behavior][solar]

HV rechargeable batteries are registered with these capacities: cadmium 1200000 EU, lithium 1600000 EU and sodium 800000 EU. Their electric statistics use tier 3 and `V[3]`. Ordinary HV battery buffers exist with 1, 4, 9 and 16 inventory slots. `MTEBasicBatteryBuffer` accepts and outputs `V[mTier]`, inputs on non-front faces and outputs on its front face. Its output amperage is the number of compatible charger items counted in inventory, and input amperage is twice the chargeable-item count. The base buffer and electric item charges are storage, not new energy production. The source check does not calculate runtime, transport mass, charging logistics or crafting progression. [Battery statistics][battery-stats] [Buffer registration][buffer-registration] [Buffer input/output][buffer-io]

Ordinary steam turbines are registered at LV, MV and HV. The HV instance has tier 3, so the common enabled `maxEUOutput` is 512. Its fluid capacity is `24000 * mTier`, which is 72000 at HV. Its fuel-value function accepts steam through `GTModHandler.isAnySteam`, returns 3 for a matching fluid, and its consumption unit is `6 + mTier`, which is 9 at HV. The separate input filter rejects superheated steam. The conversion sees the fluid type and amount, not where it was produced, so normal surface-produced steam matches the same local input contract. This does not establish a transport route or sustained steam delivery rate. [Steam registration][steam-registration] [Steam input and capacity][steam] [Steam filter][steam-filter] [Basic output][basic-output]

Practical bootstrap constraints established by source are solar state and energy acceptance, finite battery charge and tier-compatible output, and steam type, tank capacity and supply. Factory demand, recipe cost, solar suitability in Galaxia space, transport and throughput remain unverified. No new solar generator, combustion workaround or gameplay viability calculation is proposed.

One graph source lookup failed with `symbol not found` for the guessed name `gregtech.common.tileentities.storage.MTEBatteryBuffer`. It was reported immediately. A graph search resolved the actual owner as `gregtech.api.metatileentity.implementations.MTEBasicBatteryBuffer`, and the correct graph outline and current remote source were inspected. This was a symbol-name error, not evidence of a broken index or backend.

[commit]: https://github.com/GTNewHorizons/GT5-Unofficial/commit/bc7a940f5e6583b5c79d049635d1586c8f4ad764
[ordinary-registration]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/loaders/preload/LoaderMetaTileEntities.java#L9118-L9158
[diesel]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/common/tileentities/generators/MTEDieselGenerator.java#L48-L102
[gas]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/common/tileentities/generators/MTEGasTurbine.java#L38-L78
[basic-conversion]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/api/metatileentity/implementations/MTEBasicGenerator.java#L203-L243
[basic-values]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/api/metatileentity/implementations/MTEBasicGenerator.java#L274-L306
[basic-output]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/api/metatileentity/implementations/MTEBasicGenerator.java#L161-L169
[fuel-backend]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/api/recipe/maps/FuelBackend.java#L95-L103
[work]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/api/metatileentity/BaseMetaTileEntity.java#L1011-L1014
[legacy-registration]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/loaders/preload/LoaderMetaTileEntities.java#L578-L587
[new-registration]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/loaders/preload/LoaderMetaTileEntities.java#L1067-L1077
[large-processing]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/common/tileentities/machines/multi/MTELargeCombustionEngine.java#L188-L294
[large-booster]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/common/tileentities/machines/multi/MTELargeCombustionEngine.java#L201-L228
[large-efficiency]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/common/tileentities/machines/multi/MTELargeCombustionEngine.java#L331-L334
[extreme-map]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/common/tileentities/machines/multi/MTEExtremeCombustionEngine.java#L168-L171
[extreme-booster]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/common/tileentities/machines/multi/MTEExtremeCombustionEngine.java#L202-L220
[extreme-processing]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/common/tileentities/machines/multi/MTEExtremeCombustionEngine.java#L316-L379
[extreme-efficiency]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/common/tileentities/machines/multi/MTEExtremeCombustionEngine.java#L227-L230
[legacy-processing]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/common/tileentities/machines/multi/MTEDieselEngineLegacy.java#L185-L291
[legacy-extreme]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/common/tileentities/machines/multi/MTEExtremeDieselEngineLegacy.java#L30-L135
[large-structure]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/common/tileentities/machines/multi/MTELargeCombustionEngine.java#L70-L97
[extreme-structure]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/common/tileentities/machines/multi/MTEExtremeCombustionEngine.java#L81-L111
[legacy-gas-registration]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/loaders/preload/LoaderMetaTileEntities.java#L491-L495
[new-gas-registration]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/loaders/preload/LoaderMetaTileEntities.java#L944-L946
[large-gas]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/common/tileentities/machines/multi/turbines/MTELargeTurbineGas.java#L108-L193
[legacy-gas]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/common/tileentities/machines/multi/MTELargeTurbineGasLegacy.java#L127-L204
[turbine-base]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/common/tileentities/machines/multi/turbines/MTELargeTurbineBase.java#L195-L251
[steam]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/common/tileentities/generators/MTESteamTurbine.java#L60-L99
[large-steam]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/common/tileentities/machines/multi/turbines/MTELargeTurbineSteam.java#L119-L171
[plasma]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/common/tileentities/machines/multi/turbines/MTELargeTurbinePlasma.java#L120-L186
[naquadah]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/common/tileentities/generators/MTENaquadahReactor.java#L72-L95
[thtr]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/bartworks/common/tileentities/multis/MTEThoriumHighTempReactor.java#L269-L336
[boiler]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/common/tileentities/boilers/MTEBoilerBronze.java#L187-L215
[voltage]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/api/enums/GTValues.java#L90-L95
[solar-registration]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/common/items/MetaGeneratedItem01.java#L4516-L4530
[solar]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/common/covers/CoverSolarPanel.java#L28-L112
[battery-stats]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/common/items/MetaGeneratedItem01.java#L5220-L5224
[buffer-registration]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/loaders/preload/LoaderMetaTileEntities.java#L8512-L8673
[buffer-io]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/api/metatileentity/implementations/MTEBasicBatteryBuffer.java#L114-L209
[steam-registration]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/loaders/preload/LoaderMetaTileEntities.java#L9160-L9170
[steam-filter]: https://github.com/GTNewHorizons/GT5-Unofficial/blob/bc7a940f5e6583b5c79d049635d1586c8f4ad764/src/main/java/gregtech/common/tileentities/generators/MTESteamTurbine.java#L218-L225
