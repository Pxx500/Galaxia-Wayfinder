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

# Define Remote Android Body Lifecycle

Resolved: 2026-10-18

## Question

What complete lifecycle lets a player operate a manufactured android remotely without moving their biological body or transporting its inventory?

## Accepted Direction

- Remote android operation is part of Alpha. It reduces repeated personal travel while preserving physical resource logistics and the need to establish destination infrastructure.
- A destination multiblock manufactures android bodies associated with its dock. Each android has its own inventory and body state.
- Androids are team-owned. A team may keep several androids on the same planet and team members may take control of available bodies. Each android has at most one operator, and each player controls at most one body at a time.
- The android's battery replaces food and hunger. It charges at the dock. Low charge produces a prominent warning in the center of the screen. An empty battery interrupts remote control and leaves the body inactive at its current location with its inventory, without destroying it.
- The biological body remains in a powered control and life-support capsule, which sustains it without separately supplying food or oxygen. The capsule does not grant invulnerability. Capsule destruction or loss of its required power immediately interrupts remote control and returns the player to normal operation at the capsule's location.
- Remote control requires a suitable satellite connection and reserves part of the shared communication bandwidth. Loss of that connection interrupts control.
- Active sessions keep their reserved bandwidth. New data jobs use the remaining capacity rather than displacing an operator. Loss of the connection or a reduction below the required capacity interrupts the session.
- After connection loss, the android stays inactive at its last position with its inventory. It does not automatically return or resume control when the connection recovers. Inactivity does not make it invulnerable.
- Dimension departure is forbidden regardless of the transfer mechanism. A generic transfer attempt arms permanent self-destruction before transfer. Portal contact instead starts the reversible warning described below. Completed destruction loses the android's manufacturing materials and ends control.
- Destruction drops the android's carried items locally rather than deleting them. For a dimension-transfer attempt, destruction and drops occur on the departure side before the body or its inventory can cross dimensions.
- Android destruction ends control and returns the operator to the biological body without killing the player. Voluntarily ending control also leaves the android at its current location.
- Self-destruction uses a short countdown, a non-damaging visual explosion from the android's perspective, a brief viewing interval, return to the biological body and removal of the destroyed chassis. Dimension departure is blocked as soon as self-destruction is armed. The presentation cannot move the body or its items across dimensions.
- Androids do not breathe and can operate in vacuum without oxygen. Zero-gravity operation still requires suitable EVA equipment and consumes more electrical energy. The specific equipment and energy multiplier remain to be established.
- Low pressure alone adds no android penalty. Connected bodies consume a base electrical load, with additional walking, sprinting, jumping and zero-gravity costs. Exact rates remain tuning.
- Cold exposure increases battery use for heating instead of causing biological cold damage or freezing debuffs. Androids remain subject to ordinary damage, including combat, falls, fire and lava. This specific cold rule does not grant general heat or radiation immunity.
- Health is restored by material-consuming repairs at the dock, not by natural player regeneration. Charging replenishes the battery but does not repair damage. The chassis does not passively wear out during normal operation, and random failures are not part of this balancing direction.
- An android is a remotely controlled player body, not an autonomous worker.

## Self-Destruct Presentation

Portal contact starts a warning countdown while retaining ordinary movement and blocking dimension transfer. Leaving the portal before zero cancels that warning. Staying until zero causes destruction. A generic non-portal transfer attempt remains irreversible. Logout, restart or loss of control cannot cancel an irreversibly armed destruction. Loss of capsule power or the satellite connection interrupts control immediately without restoring the armed chassis.

The visible explosion does not damage the operator, other entities or surrounding blocks. Items are settled locally once. About three seconds of countdown and two ticks of viewing time are initial tuning values, not fixed contract limits. A focused in-game check must establish that the effect is actually visible before the return.

The physical android emits one positional explosion sound. Actual damage to the biological capsule occupant warns its remote operator with a short red screen effect without damaging the android.

## Selection And Feedback

The capsule offers Change selection and Connect. Change selection opens the Star Map, replacing the previous GUI and its child windows. Right-clicking a planet lists its androids directly in the map's context menu. Selecting a body does not connect automatically. Team-owned android names persist and can be edited there.

Low and critical battery warnings appear prominently at the center of the screen. Initial thresholds of 10% and 5% remain tuning. The body returns to its associated dock and disconnects for charging. Brief boot and biological-return effects do not delay gameplay control.

## Resource Transfer Boundary

[[Require Explicit Interplanetary Logistics]] applies to androids as well as biological players and automated infrastructure. Ender Chests, Ender Tanks, AE2 and comparable mechanisms must not let remote operation bypass interplanetary item or fluid transport. Separate body inventories alone do not satisfy this requirement when a mod stores resources by the operator's UUID, name or a shared channel.

Ordinary same-destination AE2 storage, crafting and automation remain usable by androids. Quantum Ring connections must not provide interplanetary transfer. Local networks may load or unload Rocket cargo without replacing the flight.

Audit the actual transport and access paths rather than assuming a GUI restriction prevents automatic transfer. This is an accepted gameplay constraint, not a verified compatibility implementation.

[[Issue - Enforce Interplanetary Resource Transfer Restrictions]] tracks that cross-system requirement. It is required for the complete gameplay guarantee, but it is not a reason to build a second storage or logistics system inside the android feature.

## Working Introduction

EV is the provisional introduction target, using orbital electronics and a functional communication network. The destination dock must be physically established. Exact recipes and energy costs are not selected. This is an infrastructure and recipe progression target, not a player-tier permission check.

## Scope Boundary

Keep the feature focused on body manufacture, the control capsule, remote operation and shared satellite bandwidth. Modular satellites, Rocket maintenance, Gantry scheduling and a new data-processing chain are not prerequisites introduced by this decision.

The desired small integration surface is a design goal, not a verified implementation property. The accepted operator/body architecture must be validated against Minecraft and the installed mods during implementation.

## Accepted Operator And Body Architecture

One connected real player executes the currently controlled body. Account identity, team membership, permissions and account-level progression remain with the operator. Inventory, equipment, health and other physical state belong to the individual body. The capsule preserves the biological body and its belongings without requiring a second ticking player with the same profile.

A cohesive body lifecycle owner enforces exclusive control and authoritative item ownership through activation, deactivation, destruction and interrupted saves. Physical machines and GUI request those operations rather than independently coordinating state changes. This accepted architecture is not permission to copy whole-player data and is not an implementation certificate.

Extend existing team, persistence, environment and satellite capabilities rather than introducing parallel owners. Satellite reservations must reduce the same capacity used by data jobs. The research identified the existing Reaction Control System as the zero-gravity maneuvering capability. Its per-body state and electrical accounting need adjustment without adding a hidden oxygen requirement.

## Implementation Evidence Boundary

The 2026-10-18 investigation supports this architecture but does not prove running-pack compatibility. The body transition must preserve equipment and open-container contents, avoid operator death, preserve one authoritative copy of belongings through saves, and keep the capsule's required simulation and power valid.

Supported dimension-transfer paths and remote-storage integrations need concrete coverage. A listener that runs after a dimension transfer cannot satisfy the boundary. Use the actual resolved dependencies and record the tested modpack manifest when verifying compatibility, rather than treating the research's older classpath as a permanent version requirement.

## Content And Verification Boundary

Construction, charging and repair recipes for the provisional EV introduction remain to be selected. Exact costs remain tuning rather than a blocker for implementation of the accepted lifecycle. A contradiction found in the code must be raised rather than silently changing the gameplay contract.

## Not Yet Specified

The exact mapping of mod attachments to body or operator state requires implementation verification. Accepted cold handling, other damage and dock-repair rules govern the baseline. Interactions with activities that specifically require a biological body remain unspecified. Numerical battery capacity, warning thresholds, activity loads and charging rates remain tuning. No invulnerability, automatic item recovery, autonomous behavior or continued operation without a player is implied.

## Provenance

The project lead proposed remote android bodies and accepted the lifecycle rules on 2026-10-18. The separate architecture discussion supplied the approved countdown and visual-explosion presentation. The owner then approved the one-player operator/body architecture after reconciliation. The original proposal and Remote Android Body Architecture Feasibility Research are retained through Sources as reviewed provenance. Unselected research suggestions do not become requirements through that approval.

Later owner feedback in Remote Android Implementation Findings supersedes the earlier universal irreversibility, vacuum-load and biological cold-damage wording. Its selection and feedback decisions are incorporated above. Branch results remain dated source evidence, not verification of the current checkout or every supported mod integration.

## Related Topics

- Define Satellite Link Distance Quality
- Define Player Presence and Automation Tradeoffs
- Define Player Flight Interaction Model
- CONTEXT
