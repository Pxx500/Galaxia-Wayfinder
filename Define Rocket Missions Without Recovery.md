---
type: wayfinder-ticket
ticket_type: grilling
status: resolved
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Travel and Logistics]]"
secondary_areas:
  - Area - Observation and Research
blocked_by: []
claimed_by: null
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Define Rocket Missions Without Recovery

## Question

How does a Rocket mission without a recovery ending finish, and how does the player know its consequence before launch?

## Resolution

On 2026-10-07 the owner accepted missions that end without recovering the Rocket. The mission planner shows a warning that the Rocket will disappear after completing the mission. Such a plan remains launchable if its scheduled actions are feasible with the available fuel.

After the final scheduled action completes, the mission ends with the Rocket lost. Remove it from the active fleet together with its installed modules and any remaining cargo. Successfully deployed payloads and the opening launch achievement remain credited. This is a consequence of the planned mission ending, not a special first-launch destruction rule.

An occupied pad for a planned feasible recovery remains a waiting case. The Rocket travels to the destination and waits there for docking capacity. Temporary unavailability does not turn that mission into intentional loss.

[[Specify Alpha Opening Mission Flow]] owns the early progression and concrete mission-action examples. [[Define Space Transport Dispatch Model]] owns schedule execution. Exact warning copy and presentation belong to implementation and follow localization requirements.

## Provenance

Direct owner confirmation in the Wayfinder conversation on 2026-10-07. The owner accepted terminal Rocket loss and specified that a plan without a recovery ending shows a warning that the Rocket disappears after the mission.
