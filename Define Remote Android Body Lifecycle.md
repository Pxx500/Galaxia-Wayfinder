---
type: wayfinder-ticket
ticket_type: grilling
status: resolved
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Automation and Infrastructure]]"
secondary_areas:
  - Area - Observation and Research
  - Area - Alpha Scope
blocked_by: []
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Remote Android Body Lifecycle

Resolved: 2026-10-18

## Bodies and Control

Remote android operation is part of Alpha. It reduces repeated personal travel while preserving physical resource logistics and the need to establish destination infrastructure. A destination multiblock manufactures bodies associated with its dock. Each has its own inventory and physical state. Androids are team-owned, several may exist on one planet, and team members may control available bodies. Each android has at most one operator, and each player controls at most one body. Androids are not autonomous workers.

The biological body remains in a powered control and life-support capsule, sustained without separate food or oxygen. It is not invulnerable. Destruction or loss of required capsule power immediately returns the player to normal operation at the capsule. Voluntarily ending control leaves the android at its current location.

## Connection and Battery

Remote control requires a suitable satellite connection and reserves shared communication bandwidth. Active sessions retain their reservation, leaving the rest for new data jobs. Connection loss or capacity dropping below the requirement interrupts control. The android stays inactive at its last position with its inventory, without automatic return or reconnection, and remains vulnerable to damage.

The battery replaces food and hunger and charges at the dock. Low charge produces a prominent center-screen warning. An empty battery interrupts control and leaves the body inactive with its inventory rather than destroying it.

## Environment and Repair

Androids do not breathe and can operate in vacuum without oxygen or a low-pressure penalty. Zero gravity requires suitable EVA equipment and additional electrical energy. Equipment and multiplier remain open. Connected bodies have a base electrical load and additional walking, sprinting, jumping and zero-gravity costs. Rates remain tuning.

Cold increases battery use for heating instead of causing biological cold damage or freezing debuffs. Androids still take ordinary damage, including combat, falls, fire and lava. This does not grant general heat or radiation immunity. Material-consuming dock repairs restore health, while charging only replenishes the battery. There is no natural regeneration, passive chassis wear or random failure in this direction.

## Dimension Restrictions and Destruction

Dimension departure is forbidden by every transfer mechanism. A generic transfer attempt arms irreversible self-destruction before transfer. Portal contact instead starts the reversible warning below. Destruction loses the manufacturing materials, drops carried items locally and returns the operator to the biological body without killing the player. For transfer attempts, destruction and drops occur on the departure side before the body or inventory crosses dimensions.

Self-destruction blocks departure as soon as it is armed. It uses a short countdown, a non-damaging visual explosion from the android's perspective, a brief viewing interval, return to the biological body and removal of the chassis. The presentation cannot transfer the body or items.

## Self-Destruct Presentation

Portal contact starts a warning countdown while retaining ordinary movement and blocking dimension transfer. Leaving the portal before zero cancels that warning. Staying until zero causes destruction. A generic non-portal transfer attempt remains irreversible. Logout, restart or loss of control cannot cancel an irreversibly armed destruction. Loss of capsule power or the satellite connection interrupts control immediately without restoring the armed chassis.

The visible explosion does not damage the operator, other entities or surrounding blocks. Items are settled locally once. About three seconds of countdown and two ticks of viewing time are initial tuning values, not fixed contract limits. A focused in-game check must establish that the effect is actually visible before the return.

The physical android emits one positional explosion sound. Actual damage to the biological capsule occupant warns its remote operator with a short red screen effect without damaging the android.

## Selection And Feedback

The capsule offers Change selection and Connect. Change selection opens the Star Map, replacing the previous GUI and its child windows. Right-clicking a planet lists its androids directly in the map's context menu. Selecting a body does not connect automatically. Team-owned android names persist and can be edited there.

Low and critical battery warnings appear prominently at the center of the screen. Initial thresholds of 10% and 5% remain tuning. The body returns to its associated dock and disconnects for charging. Whether this means player-directed return or automatic movement is unresolved alongside the rule that interruption leaves it at its current location. Brief boot and biological-return effects do not delay gameplay control.

### Presentation Details

- The Star Map context list opens at the clicked planet and closes when clicking outside. Renaming owns its input without the map dismissing the list.
- Android boot uses the ClankOS SYSTEM ONLINE presentation. The accepted short timings are 0.85 s for boot and 0.65 s for biological return, without delaying gameplay control.
- Android control shows blue circuit accents extending from both screen edges. Biological projections retain the operator's skin and a body-name label. Standard cape display is suppressed during android control and restored on return.
- Self-destruct uses the ROGUE ANDROID DETECTED alarm. Portal warnings explain that leaving cancels the countdown rather than claiming irreversibility.
- Connection loss produces one localized message. Reserved bandwidth does not consume satellites, and disabled satellite assets remain visible even though they supply no usable capacity.

Source: direct gameplay and presentation feedback, 2026-10-18. Rendering and compatibility observations from that session are historical, not a guarantee for every cosmetic mod.

## Resource Transfer Boundary

[[Require Explicit Interplanetary Logistics]] applies to androids as well as biological players and automated infrastructure. Ender Chests, Ender Tanks, AE2 and comparable mechanisms must not let remote operation bypass interplanetary item or fluid transport. Separate body inventories alone do not satisfy this requirement when a mod stores resources by the operator's UUID, name or a shared channel.

Ordinary same-destination AE2 storage, crafting and automation remain usable by androids. Quantum Ring connections must not provide interplanetary transfer. Local networks may load or unload Rocket cargo without replacing the flight.

Audit the actual transport and access paths rather than assuming a GUI restriction prevents automatic transfer. This is an accepted gameplay constraint, not a verified compatibility implementation.

[[Issue - Enforce Interplanetary Resource Transfer Restrictions]] tracks that cross-system requirement. It is required for the complete gameplay guarantee, but it is not a reason to build a second storage or logistics system inside the android feature.

## Dock Access And Manufacturing Feedback

- An inactive android must not lock the dock entrance. The occupied control capsule retains protective locking.
- Both installations need a standing-height entrance and interior, with two clear air blocks.
- Manufacturing shows an android outline filling from feet to head with progress. An arrow may supplement it but is not the main visualization.
- Supplied materials determine which chassis the dock manufactures.
- Entering or leaving the correct station position shows charging-port connection feedback near the bottom of the screen. Port connection is distinct from energy entering an actively controlled body. Active-body or shared-dock charging is not selected.

Source: android implementation feedback, 2026-10-18 to 2026-10-21.

## Chassis And Power

The selected chassis tiers are EV, LuV and UV, two GT tiers apart. Use orbital electronics and a functional communication network, with the destination dock physically established. Material quantities should make the upgrades substantial rather than cheap copies. Exact production recipes remain open. Tiers describe manufacture and infrastructure, not a player-tier permission check.

Use existing GT batteries, not android-specific Power Cores or recursively crafted batteries. Both dock and control capsule use native GT Energy Hatches. Laboratory recipes and free power are not production content.

The recorded native-battery proposal uses the following components. Capacities were checked against local GT5 5.09.54.64, not every final-pack configuration. Charging rates remain proposed tuning.

| Chassis | Native battery candidate | Checked capacity | Proposed charging rate |
| --- | --- | ---: | ---: |
| EV | Small Sunnarium Battery | 6,400,000 EU | 1,024 EU/t |
| LuV | Large Sunnarium Battery | 102,400,000 EU | 16,384 EU/t |
| UV | Large Naquadria Battery | 1,638,400,000 EU | 262,144 EU/t |

The accepted EV operating proposal is 128 EU/t idle, plus 64 EU/t walking or 192 EU/t sprinting, 640 EU per jump, 128 EU/t heating and 128 EU/t in zero gravity. Recorded scaling is four times EV operating costs at LuV and sixteen times at UV. These are working balance settings, subject to testing.

Source: chassis and native-battery decisions, 2026-10-21 to 2026-10-22.

### Remaining Content Questions

- Inventory capacity and compatibility: preserve the player inventory, restrict selected slots, or change its size only after checking affected mods.
- Tier-specific statistics, substantial recipe bills and the source of any initial battery charge.
- Repair material selection and health restored. A six-material choice restoring two hearts was an illustrative proposal, not an accepted algorithm.

## Scope Boundary

Keep the feature focused on body manufacture, the control capsule, remote operation and shared satellite bandwidth. Modular satellites, Rocket maintenance, Gantry scheduling and a new data-processing chain are not prerequisites introduced by this decision.

The small integration surface is a design goal. Validate the operator/body architecture against Minecraft and installed mods during implementation.

## Accepted Operator And Body Architecture

One connected real player executes the currently controlled body. Account identity, team membership, permissions and account-level progression remain with the operator. Inventory, equipment, health and other physical state belong to the individual body. The capsule preserves the biological body and its belongings without requiring a second ticking player with the same profile.

A cohesive body lifecycle owner enforces exclusive control and authoritative item ownership through activation, deactivation, destruction and interrupted saves. Physical machines and GUI request those operations rather than independently coordinating state changes. Do not copy whole-player data.

Extend existing team, persistence, environment and satellite capabilities rather than introducing parallel owners. Satellite reservations must reduce the same capacity used by data jobs. The research identified the existing Reaction Control System as the zero-gravity maneuvering capability. Its per-body state and electrical accounting need adjustment without adding a hidden oxygen requirement.

## Implementation Evidence Boundary

The 2026-10-18 investigation supports this architecture but does not prove running-pack compatibility. The body transition must preserve equipment and open-container contents, avoid operator death, preserve one authoritative copy of belongings through saves, and keep the capsule's required simulation and power valid.

Supported dimension-transfer paths and remote-storage integrations need concrete coverage. A listener that runs after a dimension transfer cannot satisfy the boundary. Use the actual resolved dependencies and record the tested modpack manifest when verifying compatibility, rather than treating the research's older classpath as a permanent version requirement.

## Not Yet Specified

Construction and repair recipes remain to be selected. Working power settings and battery candidates above need final-pack and balance checks. Warning thresholds and charging rates remain tuning. The mapping of mod attachments to body or operator state needs verification. Interactions with activities requiring a biological body remain unspecified. No invulnerability, automatic item recovery or continued operation without a player is implied.

## Provenance

The lifecycle and one-player operator/body architecture were accepted on 2026-10-18. Direct gameplay feedback that day refined portal retreat, cold-energy use, low-pressure behavior and presentation. Later dock, tier and native-battery decisions are dated in their sections. The original proposal and feasibility research remain in Sources.

## Related Topics

- Define Satellite Link Distance Quality
- Define Player Presence and Automation Tradeoffs
- Define Player Flight Interaction Model
- CONTEXT

## Gameplay Flow

The player establishes a destination dock and communication network, then enters a powered capsule and selects a team-owned android through the Star Map. They control that body with its own inventory and battery while their biological body remains in the capsule. The dock charges and repairs androids, and the shared satellite connection reserves bandwidth for the session.

Connection loss or an empty battery ends control and leaves the android inactive at its last position with its inventory. Losing capsule power also ends control and returns the operator to the biological body. Dock return for charging remains unresolved as described above. Androids cannot leave their dimension. Portal contact warns before destruction and can be cancelled by leaving, while other transfer attempts arm irreversible destruction. Destruction drops carried items on the departure side.
