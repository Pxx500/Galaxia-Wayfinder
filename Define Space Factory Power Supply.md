---
type: wayfinder-ticket
ticket_type: grilling
status: open
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Automation and Infrastructure]]"
secondary_areas:
  - Area - Alpha Scope
blocked_by: []
claimed_by: wayfinder
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Define Space Factory Power Supply

## Question

What practical power options support early orbital and lunar production, and may wireless energy transfer replace transporting or generating power at the destination?

## Established Inputs

- [[Define Celestial Capability Rules]] owns the combustion prohibition and solar-resource model. Oxygenated Station rooms do not provide a combustion exception.
- [[Design Early Orbital Production Recipe Chain]] records transported ordinary GT batteries and a suitable Battery Buffer as the provisional bootstrap. Actual energy demand and transport capacity still need verification.
- Space Grade Solar Panel remains a recipe-component item. The selected physical generator is a separate panel-block array with a Solar Energy Dynamo adapter. Existing GT wiring and energy consumers remain the baseline.
- Sustained non-combustion supply remains open. Resolving it is independent of redesigning Rocket missions or android bodies.

## Accepted Direction

- Solar output varies with the actual celestial environment. Farther orbits receive less solar energy than nearer ones under the shared illumination model. A productive near-star installation is a valid potential strategy. Cheap early cross-dimension energy export must not remove its logistics and progression costs. Late export possibilities belong to [[Define Late Interplanetary Network Access]].
- Wireless EU transfer between planets is prohibited under the explicit-logistics policy. Generate energy locally or transport suitable energy stores or generator inputs physically.
- Solar, nuclear reactors and radioisotope thermoelectric generators are the selected families to investigate for space power. This does not approve every existing machine, recipe or performance value in those families.
- Ground manufacture provides the same solar hardware at a deliberately very high material cost, sufficient to bootstrap orbital solar production but uneconomical for large expansion. Microgravity-derived SiGe and fluoride materials make later manufacture substantially cheaper. Ordinary silicon with very poor yield is the candidate ground route. The illustrative 90% silicon loss is not an accepted recipe quantity.
- Manufacturing advantage and generation advantage are separate. Even efficiently manufactured orbital panels should retain substantial upfront cost compared with non-passive generation. This is a balance direction, not an approved cost ratio.
- Do not interpret the space restrictions as a blanket ban on nuclear reactors or every generator. Evaluate the actual generating process and required supporting infrastructure. Existing combustion restrictions remain in force.

## Remaining Decisions

### Orbital Solar Walls And Radiators

The owner supports directional solar arrays that can form vertical walls in an orbital dimension, together with exposed radiators serving a modular Computer. The intended loop uses locally generated solar EU and regenerated chilled coolant to process satellite data from other celestial bodies. Computer placement is not restricted to orbit.

The Space Grade Solar Panel remains a recipe-component item used to manufacture placeable panel blocks. The array and its adapter are separate equipment, not a conversion of that item into an existing GT solar cover. Recipes and electrical ratings remain open.

The orbital convention in [[Define Celestial Capability Rules]] is accepted: the parent planet appears below the player, the Sun stays to the side in a fixed horizontal direction, and there are no periodic planetary eclipses. Microgravity remains unchanged. The visible sky, solar collection and radiator exposure must use the same direction. This supports vertical solar walls without tracking equipment. Exact cardinal direction and local shading checks remain open.

Solar collecting faces work best facing the Sun. Radiator placement should minimize direct solar exposure. The owner described a perpendicular arrangement and explicitly rejected interpreting this as merely turning the radiator's front away from the Sun. Exact face-orientation and placement checks remain open.

The selected coolant loop is closed. [[Define Data Processor Machine Topology]] owns the radiator multiblock and its environment-temperature-dependent throughput. Space is a 100% reference, not a ceiling, and sufficiently cold atmospheric locations may perform better. A powered chiller restores the same coolant under conditions unsuitable for passive operation. Any circulation EU cost, numerical capacity, placement checks, shadow handling and thermal thresholds remain open.

An orbit near the Sun can provide strong solar power without granting unlimited cooling. Radiators still need suitable placement and exposure. Do not implement a blanket planetary radiator ban. A location that really satisfies the same thermal requirements should remain eligible.

NASA's thermal-control overview describes external spacecraft heat rejection through radiation and the importance of absorbed solar heat, surface properties and view to the heat sink. It motivates the design, not the selected coolant temperature or a universal space-cooling multiplier: [Thermal Control](https://www.nasa.gov/smallsat-institute/sst-soa/thermal-control/).

Orbital illumination evidence checked on 2026-10-22: [ESA's orbit overview](https://www.esa.int/Enabling_Support/Space_Transportation/Types_of_orbits) distinguishes geostationary and Sun-synchronous orbits, including dawn-dusk configurations. Polar or Sun-synchronous placement alone does not establish perpetual sunlight. [NOAA's GOES eclipse information](https://www.ospo.noaa.gov/operations/goes/eclipse.html) records seasonal Earth-shadow intervals of up to 72 minutes per day for geostationary satellites. These facts informed the accepted simplified convention rather than mandate a real-orbit simulation.

### Proposed Power Roles, Awaiting Approval

The expensive ground-manufacturing route and efficient microgravity-fed route are accepted above. They do not introduce separate weak and strong panel grades based on manufacturing location.

Transported batteries bootstrap the first workshop. Solar rewards suitable illumination and investment in panel production. Nuclear is the candidate for dense sustained factory demand. RTGs are candidates for modest remote loads where avoiding frequent supply is valuable. These roles require checking existing GT machinery, feedstock access and full supply costs. They do not certify generator availability or select EU/t.

Approve or revise these roles together, then compare complete equipment and recipe packages against actual factory loads.

- Select concrete solar recipes and complete bootstrap supply routes without requiring orbital products for the ground-manufactured starter equipment.
- Define the role and availability of solar, nuclear and RTG options after inspecting existing GT machinery.

### Accepted Solar Array And Adapter

One array occupies a bounded panel plane plus one rear adapter, provisionally named Solar Energy Dynamo. Tiered collectors increase the supported area. The initial collector covers 5 by 5 panels. Proposed higher areas are 9 by 9 and 11 by 11, not finalized tier assignments or recipes. The adapter faces the collection direction. Its immediately adjacent block in that direction is the central panel, and its coverage extends symmetrically along the plane according to its tier. Multiple arrays may form a larger installation, with a separate adapter and cable connection behind each section.

Incomplete arrays work. Only panels connected to the adapter through a continuous panel path within its tier-bounded plane contribute. A panel isolated in a corner contributes nothing. A connected corner can contribute through intervening panels and does not need direct adjacency to the adapter itself. The central panel is the entry point. A path outside the bounded area does not connect an otherwise isolated panel inside it. Face-adjacent panel connections are the proposed concrete interpretation, rather than diagonal-only contact.

Panel blocks and the adapter automatically align on placement from the environment, not the player's look direction. In an orbital dimension they face the fixed horizontal Sun, forming a vertical panel plane. On a planetary surface they face upward, with the adapter below the central panel and a horizontal panel plane above it. The surface upward convention does not require continuous Sun tracking.

The adapter collects and exports the array's energy. It is not a large central power-controller structure and is unrelated to the Computer's controller. Panel ownership where coverage overlaps, recipes and electrical ratings remain open.

Panel blocks are passive ordinary blocks, not independent ticking machines or energy-network endpoints. They do not generate or store EU themselves and should not require per-panel tile entities. The collector is the ticking generator and electrical endpoint for its connected panels. Placement and removal notifications do not imply panel ticking. Larger collector coverage reduces the number of active generators and cable connections needed for the same panel area, rather than increasing each panel's intrinsic efficiency.

Prefer existing GT structure-check and update mechanisms where suitable. Cache the connected panel set and refresh it on relevant structural changes and initialization, not by repeatedly scanning the world every generation tick. Connectivity checks cover at most the collector's bounded area, such as 25, 81 or 121 positions for the discussed sizes. Reading cached panel capacity to calculate current environmental output is separate from rediscovering the structure. Verify update coverage for passive panel blocks before claiming that GT integration handles all changes. Keep rendering and exposure checks from reintroducing per-panel per-tick work. These are design constraints, not measured performance gains.

Overlapping collectors must not generate multiple copies of the same panel's output. The exact ownership or placement rule remains open and must preserve the passive-block design. No rewrite of existing GT solar generators is authorized by this new array design.

The adapter provides no accumulated energy storage. At most one tick of current generation may be held for transfer, and unused output must not accumulate into a later burst. Without a connected accepting electrical network, potential output is not banked. Demand below available output leaves the remainder unused. Across all output connections combined, export in one tick must not exceed that tick's available generation. A 1000 EU/t array delivering no more than 1000 EU/t is illustrative, not selected output tuning.

Any implementation buffer must preserve this behavior rather than stack previously unused generation on top of the next tick's output. Voltage, amperage, fractional output and the relationship between environmental yield and adapter rating still need an explicit GT-compatible contract.

The adapter offers current generation to the ordinary energy network and accounts for the portion actually accepted. If generation is 1000 EU/t and demand is 2000 EU/t, only the available 1000 EU/t can be supplied. If generation is 2000 EU/t and demand is 1000 EU/t, only the accepted energy is transferred and the remainder is not stored. These are idealized source-side examples before cable losses and packet granularity, not a replacement electrical protocol. The earlier recommendation of tiered adapters with intentional excess-generation clipping was not approved by this clarification.

The owner explicitly selected native GT electrical behavior as the integration contract. The descriptions above express player-visible intent, not a required push/pull implementation or arbitrary exact-size energy packets. Use GT's voltage, amperage, demand acceptance, cable losses and overload rules. Do not introduce a parallel electricity model or bypass cable limits to reproduce the illustrative EU/t examples literally. Choose packet representation through implementation research while preserving current-generation availability, demand-limited accepted output and no accumulated burst storage. Any substantive compromise to those gameplay requirements needs a new decision. Collector tiers are selected for supported panel area, not as approval of the earlier artificial output-clipping proposal. Electrical tier mapping remains open.

#### Checked GT Integration Evidence

At GT5 revision 6eac02935d42b3ab13d341e4fe090b4403e15f60, MTEMultiBlockBase.checkStructure uses a structure-change flag or a forced check. onMachineBlockUpdate schedules a delayed check through onPostTick, with an initialization check as well. This supports reusing the update lifecycle rather than adding continuous geometry polling, but does not prove that arbitrary new panel blocks already notify the collector.

IEnergyConnected.Util.emitEnergyToNetwork offers voltage and amperage through injectEnergyUnits and returns accepted amperage. MTECable.transferElectricity uses consumer demand, and PowerNodes.processNodeInject records the amperage actually accepted. The checked path is emission-driven with demand-aware acceptance, not a pure consumer-pull protocol.

PowerNodePath.applyVoltage can burn an overvolted cable before amperage acceptance. PowerNodePath.addAmps tracks actual transferred amperage and an overload accumulator. Therefore low accepted EU/t is not a guarantee of cable safety under excessive voltage. Preserve native electrical behavior rather than treating EU/t alone as voltage and current. Exact solar packet sizing remains open.

### Accepted Directional Shadow Update Design

Preserve the accepted fixed horizontal orbital Sun if a practical shadow implementation is feasible. The owner permits reconsidering an overhead Sun only as a last resort after investigating performance, not as a selected change. Fixed orbital illumination removes time-of-day changes from solar yield, but does not make vanilla vertical skylight represent horizontal visibility.

On 2026-10-23, the owner selected coarse-to-fine, change-driven shadow updates with batching and a shared processing budget. The direction uses a finite forward obstruction-check distance. The discussed 16 and 32 blocks remain alternatives to measure, not a selected constant. Orbital dimensions may eventually contain generated rocks or asteroids, so ungenerated orbital space must not be assumed permanently empty. This replaces the global horizontal obstruction-index proposal as the primary design.

Maintain a chunk-keyed collector registry for local candidate discovery. A relevant block change records the chunk as dirty and expands a bounding box of changed coordinates within that chunk. Repeated changes update one pending entry rather than immediately scanning panels. Store minimum and maximum X, Y and Z, not every changed block. A conservative box may include unchanged space and trigger extra checks, but must not omit actual changed positions. Use dimension-qualified coordinates and remove stale collector registrations through lifecycle handling.

Process dirty chunks by finding candidate collectors and intersecting each changed bounding box with the collector's bounded sunlight-check volume. The volume starts in front of the panel plane, not at the rear adapter, extends by the selected shadow distance, and spans the collector's two in-plane half-widths. For a 5 by 5 array, those half-widths are two blocks. All three coordinate intervals must overlap. Reject on the first disjoint interval before reading world blocks. Testing depth first is a reasonable implementation choice, not a requirement or the main performance gain. A positive intersection only schedules a visibility check, it does not prove that an opaque blocker or an installed panel is present.

Deduplicate collectors in the work queue. Budget both candidate enumeration and actual visibility checks across ticks, using a shared system-wide work limit rather than an independent budget per collector. Checks must be resumable so a large bulk edit does not force all affected arrays to scan in one tick. Empty queues do no geometry work. Do not replace this with synchronized periodic rescans of all unchanged arrays. Generation reads cached exposure and current environmental yield separately from geometry discovery.

Changes arriving while queued work is running must remain represented, rather than being lost when a dirty entry is cleared. A completed check must not be treated as current if relevant newer changes were not considered. Provisional behavior during delayed validation remains to be confirmed: retain a running collector's last validated exposure, while a new collector waits for its first result. No precise latency guarantee or benchmark has been established.

Remaining implementation evidence includes a reliable mutation/opacity-change hook that covers bulk tools such as Matter Manipulator, chunk load/unload and startup initialization. World-access block-update notifications alone are not established as complete: the checked World.markAndNotifyBlock path is conditional on flags and chunk state. Unloaded portions of the bounded check volume must not silently become clear space. Do not force-load an unlimited ray or build a global shadow map for this local rule. Select the unloaded-state policy and opaque-block rule during feasibility review. An overhead Sun remains a last-resort redesign, not approved behavior.

Checked source evidence: GT5 MTESolarGenerator refreshes weather, daylight and vertical sky exposure every 100 ticks and on its first tick. World.canBlockSeeTheSky delegates to Chunk.canBlockSeeTheSky, a comparison with the stored column height map. World.setLightValue dispatches IWorldAccess.markBlockForRenderUpdate, whose vanilla WorldManager implementation is empty. This is a generic lighting/render notification, not a horizontal solar-occlusion event. A lateral obstruction can leave vanilla skylight unchanged. CoverSolarPanel has different behavior and does not require sky visibility in its clear-weather daytime branch, so it is not a general roof-occlusion reference.

### Solar Yield Calibration

[[Define Celestial Capability Rules]] owns the common daylight-Overworld reference. Surface Overworld daylight is 100% and night is 0%. Calculate other environments from source distance, atmospheric effects and illumination rather than hardcoding a percentage for each dimension. Overworld orbit should have a substantial instantaneous advantage as well as continuous illumination. The owner's 200% or 300% examples are calibration candidates, not selected multipliers. A constant orbital multiplier alone is not the intended environmental model.

The yield calculation is distinct from manufacturing cost. Higher output on a suitable orbit does not imply that panel manufacture itself requires that exact orbit. Exact attenuation, distance scaling, shading and electrical conversion remain tuning and implementation work.

## Evidence Needed After The Direction Is Selected

Compare existing GT non-combustion options against the intended introduction stage, available inputs and actual production demand. Assess the complete supply route, including any upstream combustion, instead of assuming a turbine alone supplies a viable factory. Derive implementation details when execution begins.
