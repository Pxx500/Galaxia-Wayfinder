---
type: wayfinder-ticket
ticket_type: grilling
status: resolved
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Travel and Logistics]]"
secondary_areas:
  - Area - Automation and Infrastructure
blocked_by: []
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Define Bulk Repair of Broken Endpoint References

## Question

How can a player replace one removed or relocated Transport Endpoint across every affected Vehicle Schedule without editing many vehicles individually or allowing unsafe automatic retargeting?

## Resolution

Alpha provides an explicit team-scoped chat operation that atomically replaces one schedule target across every affected Vehicle Schedule. The replacement may be another exact Endpoint ID or a symbolic Endpoint Group, using the old target's Celestial Object as a convenience default with an optional explicit override for relocation. The operation performs only the checks required to resolve and apply the player's command. It does not judge route feasibility, vehicle compatibility, hazards, services, or whether the resulting schedules will work.

## Established Direction

- Destroying a standalone physical endpoint controller removes its backing asset and breaks its exact references. Destroying an individual Station endpoint breaks that endpoint's exact identity, not automatically the owning Station ID. Station-controller succession follows [[Resolve Physical Station Controller Succession]].
- Rebuilding or relocating the endpoint creates a new Endpoint ID. A machine within a surviving Physical Station retains that Station's routing scope rather than creating a new Station asset.
- The player identifies the old target and explicitly selects a replacement exact endpoint or Endpoint Group. The operation applies that replacement across all affected team Vehicle Schedules without requiring individual vehicle edits.
- Replacement is explicit. The system does not silently select another same-named endpoint.
- Bulk repair applies to broken exact Endpoint ID references. Destroying one member of a still-populated Endpoint Group does not break schedules targeting that group.
- The initial Alpha interface may be a chat command such as `/galaxia replace-endpoint <old-id> <new-id>` rather than a dedicated GUI.
- Destroying an endpoint should identify the destroyed Endpoint ID, explain that exact references are now broken, and expose a clickable command suggestion or autocomplete where practical.
- The command replaces the old exact reference across every affected Vehicle Schedule in its authorized team scope. It does not infer a replacement from Routing Name.
- An exact Endpoint ID reference may be replaced either with another exact Endpoint ID or with an explicitly selected Endpoint Group.
- A broken exact reference retains the destroyed endpoint's original Celestial Object and endpoint kind as repair context.
- When replacing that exact reference with an Endpoint Group, the group selector inherits the original Celestial Object and compatible endpoint kind. The player only needs to select or enter the Routing Name within that scope.
- The inherited Celestial Object is a convenience default rather than a restriction. The player may explicitly select a different Celestial Object when the replacement intentionally relocates a destination such as the team's main base.
- Without that explicit override, same-named groups on other celestial objects are not candidates and do not create ambiguity.
- Replacing a target across celestial objects is presented as rerouting because it changes the actual journeys in every affected Vehicle Schedule.
- The command operates inside the invoking player's team scope, so team identity does not need to be entered as another player-facing selector.
- Bulk replacement is atomic. It either writes the requested target to every affected Vehicle Schedule or changes none of them if the operation itself cannot be completed.
- Validation is limited to resolving the command unambiguously, checking authority to modify the affected team schedules, and confirming that the atomic write can be performed.
- The system does not reject a replacement because of vehicle compatibility, route feasibility, fuel, delta-v, hazards, endpoint availability, cargo configuration, or maintenance infrastructure. The player owns that decision, and ordinary schedule execution reports any resulting failure.
- A dedicated bulk-repair GUI may replace or supplement the command later if real usage shows that the command is insufficient.
- A symbolic Endpoint Group reference does not break when its last member is destroyed. It remains unavailable and automatically resumes if a compatible endpoint recreates the same group key.
- Renaming one endpoint only changes its group membership. Renaming an Endpoint Group across existing schedules is a separate explicit bulk reference operation and may also use a chat command in Alpha.

## Related Topics

- [[Define Transport Endpoint Identity and Registration]]
- [[Define Space Transport Dispatch Model]]
- [[Define Team Notification System]]

## Replacement During an Active Flight

Bulk replacement updates the schedule target without rewriting a flight already in progress. The vehicle completes travel to the original destination object's vicinity. It then recalculates travel from that actual arrival location to the replacement endpoint, using normal time, fuel, propulsion, and safety requirements.

If the vehicle cannot perform the new journey, it waits and reports the problem. Replacing a reference does not make an infeasible journey executable and does not teleport the vehicle or cargo.

Destination changes and the risk that a vehicle is unprepared for the additional journey belong to the general team notification system. Any acknowledgement behavior is deferred with that system's presentation and event policies. Do not create a separate route-change confirmation mechanism or make its detailed interface a blocker here. Acknowledgement cannot override physical flight feasibility.

Owner decision in the Wayfinder conversation on 2026-09-10. The flight completes to a valid arrival location near the original object before recalculation, not to a destroyed physical dock.
