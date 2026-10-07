---
type: wayfinder-ticket
ticket_type: grilling
status: resolved
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Observation and Research]]"
blocked_by: []
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Define Alpha Celestial Knowledge Layers

## Question

After Celestial Discovery, which environment, orbit, resource-signature, full resource-profile, and mission-planning facts become known through observation, scanning, research, or direct activity in Galaxia Alpha?

## Resolution

The first object-knowledge level provides orbital information sufficient for immediate flight planning. A later detailed satellite scan reveals the environmental facts and resource deposits without a separate research task. Atmospheric probes are outside the current scope. These are knowledge-disclosure requirements, not a claim that every object begins hidden or that the current code already implements the full contract.

## Accepted Requirements

- The 2026-09-17 opening direction starts with known Overworld resources and an already known Luna whose resources are unknown. The special opening satellite begins a scripted Luna resource survey from Overworld orbit. [[Define Alpha Observation Opening]] owns that bootstrap exception rather than a new global scan-tier system.

- For the currently designed Alpha scope, each modeled fact is either known or unknown.
- This does not commit the full Alpha milestone to binary knowledge. Additional detail may be introduced later when concrete content or other developer requirements justify it.
- The first object-knowledge level provides the orbital knowledge needed to plan a flight. Knowing that orbit permits immediate transfer planning without an additional research task.
- A completed detailed satellite scan reveals the object's environmental information, including atmosphere and relevant hazards. No separate task is required to obtain those facts in the current scope.
- Resource deposits are not revealed by discovery alone. They belong to the later satellite scan, rather than a separate new research activity.

## Implementation Evidence

Read-only inspection refreshed on 2026-09-12 at main-checkout master `7f66da49` confirmed the following source behavior. No runtime tests were run:

- Asteroids have automatic DETECTION and PROFILE passes in the same continuous prospecting process. A second scan does not require another player action.
- DETECTION changes hidden objects to discovered with unknown resources. PROFILE reveals their resource profile.
- Within a scan scope, all hidden asteroids are detected before resource profiling begins. A particular asteroid's profile is not necessarily the next completed work item after its detection.
- Environment disclosure currently happens after detection. The sidebar exposes surface and dangers before PROFILE, while asteroid ore details remain gated by PROFILE.
- Registered bodies start discovered and are not part of this asteroid scan queue. Their sidebar ore display bypasses the minor-body profile gate.
- Transfer-planner availability was not traced end to end. The first-level flight-planning rule above is accepted product intent, not a verified planner implementation claim.

Evidence anchors in the Galaxia repository:

- `src/main/java/com/gtnewhorizons/galaxia/registry/celestial/AsteroidFieldDiscoveryPolicy.java:75` and `:95`: work ordering and transitions.
- `src/main/java/com/gtnewhorizons/galaxia/client/gui/orbitalGUI/OrbitalPinnedInfoContentBuilder.java:31`, `:110`, and `:117`: environment and ore disclosure.
- `src/main/java/com/gtnewhorizons/galaxia/registry/celestial/CelestialRegistry.java:524`: registered-object defaults, currently hardcoded to discovered with unknown resources.

The environment disclosure and registered-body resource path do not yet satisfy the general detailed-scan requirement. Preserve these as implementation gaps. They do not authorize code changes during Wayfinder. Initial visible objects remain owned by Specify Alpha Opening Mission Flow.

## Out Of Scope

Atmospheric probes or additional missions to collect environmental information may be considered in a future scope. They are not a prerequisite for the current detailed satellite scan.

## Provenance

Owner decision in the Wayfinder conversation on 2026-09-10: first-level orbital knowledge permits flight planning, detailed scanning reveals environment without an additional task, and deposits are expected to appear during the later satellite scan.
