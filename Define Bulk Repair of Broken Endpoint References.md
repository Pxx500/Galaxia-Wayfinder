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

## Accepted Decision

Provide an explicit team-scoped operation that atomically replaces a broken exact Endpoint ID across every affected Vehicle Schedule. The player selects another exact endpoint or symbolic Endpoint Group. Replacement changes references, not route feasibility or an active flight's trajectory. This is accepted design, not an implemented command.

## Replacement Contract

- Destroyed/rebuilt/relocated endpoints receive new IDs. A surviving Station keeps its own identity under [[Resolve Physical Station Controller Succession]].
- No automatic same-name retargeting. Destroying a group member does not break a symbolic group reference, including an empty group that can regain compatible members.
- Alpha may use a chat command such as `/galaxia replace-endpoint <old-id> <new-id>`. Endpoint destruction identifies the old ID and should offer a clickable suggestion or autocomplete.
- Replacement may select an exact endpoint or explicit Endpoint Group. The broken reference retains its original body and endpoint kind as repair context. These default the group selection so the player usually needs only a Routing Name.
- Group selection must resolve the complete symbolic key from [[Define Transport Endpoint Identity and Registration]], including Station scope where applicable.
- Original body is a convenience default, not a restriction. An explicit body override relocates the target and is presented as rerouting. Without it, same-named groups on other bodies are excluded.
- Team scope comes from the invoking player, not an extra selector.
- Apply all affected schedule writes atomically or none. Validate only unambiguous command resolution, team authority and ability to perform that write.
- Do not reject a selected replacement for fuel, delta-v, route or vehicle compatibility, hazards, availability, cargo rules or maintenance infrastructure. Normal execution reports resulting failures. The player owns that choice.
- Renaming a group across schedules is another explicit bulk reference operation. A dedicated GUI is not required for Alpha.

## Active Flights

Update the schedule target without rewriting travel already underway. The vehicle completes travel to the original body's vicinity, not a destroyed physical dock, then evaluates travel from its actual arrival location to the replacement. Normal fuel, time, propulsion and safety rules apply. If onward travel is infeasible it waits and reports the issue.

Use [[Define Team Notification System]] for destination-change risk and any acknowledgement. No separate confirmation mechanism is selected here, and acknowledgement cannot override physics.

## Provenance And Related Decisions

Owner decision in the Wayfinder conversation on 2026-09-10.

- [[Define Transport Endpoint Identity and Registration]]
- [[Define Space Transport Dispatch Model]]
