---
type: wayfinder-ticket
ticket_type: grilling
status: open
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Observation and Research]]"
secondary_areas:
  - Area - Travel and Logistics
  - Area - Alpha Scope
blocked_by: []
claimed_by: local-wayfinder-satellite-progression
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Define Satellite Manufacturing and Deployment Progression

## Question

How should starting-world map access lead into orbital-material-based functional satellites, and which Rocket and Hammer deployment capabilities belong in Alpha?

## Accepted Direction

On 2026-09-17 the owner refined the following direction. The special opening satellite, both orbital material chains and the explicit Hammer deployment mode are accepted design intent. On 2026-10-07 the owner also resolved Hammer deployment origin and reach in [[Define Hammer Satellite Deployment Reach]]. Exact recipes and numerical balance remain open. Accepted intent is not implemented or verified behavior.

- The opening satellite is a special, easier, scripted one-off mission rather than an unrestricted normal satellite. Sending it into Overworld orbit grants the shared launch achievement. Possessing that achievement provides passive progress toward scanning Luna's resources. Initially only Overworld resources are known. Luna is already known as an object, but its resources are unknown.
- Later functional satellites use orbital SiGe crystal and specialty fluoride optical-fiber production, both required in Alpha because progression uses them. This supersedes the earlier one-chain minimum. The owner retained SiGe by approving an early low-yield sphalerite-to-germanium route under [[Define Alpha Research and Production Floor]], while the existing ABS route remains better later. Space-Grade Alloy remains an additional candidate satellite construction material.
- Only the relevant input materials need orbital production. Satellite assembly itself may happen on a planet or elsewhere. Do not add an orbital-only final satellite-crafting rule.
- The existing Rocket can gain automatic flight and control through upgraded electronics using orbital production, rather than necessarily being replaced by a new vehicle.
- Rockets can deploy satellites from a surface or carry them to another body's orbit.
- [[Define Hammer Satellite Deployment Reach]] owns the accepted atmosphere-free surface deployment, same-orbit local deployment and whole-star-system Big Hammer reach.

## Hammer Satellite Deployment Mode

When the Hammer payload slot contains a satellite, its interface exposes a `Deploy to Orbit` checkbox. Enabling it changes the destination from a receiving installation to an orbit and performs satellite deployment. This is distinct from carrying a satellite item as ordinary cargo to a receiver. The deployment operation does not require a cargo receiver at the destination orbit.

Ordinary Hammer freight still requires receiving infrastructure. Deployment origin and reach follow [[Define Hammer Satellite Deployment Reach]]. Exact deployment costs remain balance work. Final UI copy must use the normal localization system.

## Existing Contracts To Reconcile

- [[Define Alpha Observation Opening]] now uses the special opening satellite, replacing the earlier ordinary Prospecting Satellite payload without removing the successful-launch map prerequisite.
- [[Define Alpha Research and Production Floor]] now requires both orbital material chains, without selecting exact recipes.
- [[Define Alpha Transport Roles]] retains receivers for ordinary freight. The explicit deployment mode is a scoped exception, not a general receiver-free cargo route.
- Routine freight remains governed by its own endpoint and route rules. Exact satellite-deployment costs, payload form and mission accounting remain unselected.

## Opening Milestone And Team Sharing

On 2026-09-17 the owner selected a successful-launch achievement in Galaxia's planned research and achievement system as the representation of opening progress. The opening payload remains an item, without requiring a registered satellite, orbital Celestial Asset, or normal satellite worker. The intended gameplay semantics are:

- Successful deployment grants the persistent personal launch achievement to every member of the team, not just the player who launched the mission. Merely starting a launch does not complete it.
- The team receives the milestone's benefit and retains it when members leave. Every awarded member keeps their personal achievement after leaving.
- When an awarded player joins another team, the new team receives the benefit and its members receive the shared achievement. This duplication is intentional, not a unique resource transfer to prevent.
- Possessing the achievement provides passive Luna scan progress for a team whose Luna resource knowledge is incomplete. Completing the scan is an effect of the achievement, never a prerequisite for awarding it. Existing knowledge is not erased or surveyed repeatedly merely because membership changes.
- The opening payload need not appear as a managed satellite in the ordinary satellite ecosystem. It remains a real launch objective in the player's fiction, not a new satellite type with a simulated lifecycle.

The recommended responsibility split is personal achievement records for earned shared accomplishments and team research/knowledge for the durable team benefit and Luna survey. Apply the benefit on achievement completion and relevant membership changes, without repeatedly granting it or revoking it from former teams. The owner confirmed that achievements are shared with all team members. This does not by itself establish automatic transfer of every technology or blueprint.

Existing code has team celestial knowledge and team-data transfer hooks, but that does not mean personal achievement persistence or the scripted Luna survey is already implemented. Keep the new behavior with its domain owners rather than adding a fake satellite or scattered flag checks. Exact APIs and storage are implementation decisions, not a deferred implementation specification.

The owner's explicit answer resolves the sharing question in favor of all team members receiving the achievement. The earlier launcher-only recommendation is superseded.

## Accepted Opening Scan Contract

Sending the opening satellite grants the achievement to the team members. The achievement unlocks the Star Map and supplies passive Luna scan progress until the relevant celestial knowledge is complete. The achievement already exists while that scan is progressing. Scan completion reveals the result, not the launch achievement.

This is a celestial-object scan using the planetary knowledge system. It does not scan blocks, generated terrain, or physical deposits in the Minecraft world. Comparing it with local scanner output is not a gameplay choice to reopen.

## Remaining Opening Content Proposals

The owner liked the limited scripted mission and requested more detail. The following elaboration is a proposal, not a finalized contract:

- Craft an opening survey satellite from starting-world materials at the early space stage. It needs no products from the production chain it is meant to unlock.
- Launch it through the existing pre-map local-orbit deployment flow. Satellite deployment and Rocket recovery remain separate mission actions.
- Present survey progress and then publish its result through the existing team celestial-knowledge presentation. Use a tunable survey duration rather than an instant full-profile reward.
- The target and task are fixed. This opening instrument cannot be retargeted to other bodies or produce recurring prospecting-bonus data. It does not replace the later general-purpose satellite ecosystem.
- After the scan, the team's knowledge remains. No routine maintenance or continued output is required.
- Additional copies do not unlock new targets or multiply the result. A duplicate should be identified as unnecessary before launch, without requiring a new global one-item crafting limit.

This is a deliberately authored opening mission, not a new general technology-score system. Exact item names, timings and duplicate handling remain content details.

## Next Decisions

[[Design Early Orbital Production Recipe Chain]] supplies the proposed complete material, payload and control-electronics recipes. These are not accepted merely because their high-level uses are settled.

- Numerical Hammer deployment costs consistent with the accepted reach and infrastructure progression.
- Concrete orbital feedstock, processing and satellite recipes consistent with the early progression.

## Provenance

Owner's 2026-09-17 discussion of fluid storage, optional pre-Luna automation, orbital electronics and satellite deployment. This is direct planning input, not an externally imported proposal.

Owner's 2026-10-07 answers resolve the Hammer deployment origin and reach in [[Define Hammer Satellite Deployment Reach]].
