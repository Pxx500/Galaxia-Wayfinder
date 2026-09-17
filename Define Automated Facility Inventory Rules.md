---
type: wayfinder-ticket
ticket_type: grilling
status: resolved
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Automation and Infrastructure]]"
blocked_by: []
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Define Automated Facility Inventory Rules

## Question

Which inventory, resource-preservation, and shared-state rules must remain true for Automated Facilities independently of their internal implementation?

## Resolution

Automated Facilities own abstract shared inventory. Physical Stations retain world-backed inventory and routing. Their different inventory models must not change resource accounting or team authority.

## Accepted Requirements

- A Facility Insertion Filter applies to new insertion. It does not hide stored resources, prevent extraction, or discard resources when saved state is restored.
- Physical Station attachment filters govern routing for insertion, extraction, and usable free space. They do not hide already stored contents. They are not the same rule as an Automated Facility insertion filter.
- Transfers change storage by exactly the amount actually accepted or extracted, never more than requested.
- Item storage capacity derives from the facility and its effective storage modules. Controlled removal of capacity cannot leave stored items above the resulting capacity.
- Unexpected over-capacity state preserves resources. Extraction remains possible, while new insertion waits until capacity permits it.
- Deconstruction refunds that cannot yet be inserted remain pending and retry as space becomes available. They survive saving and loading.
- Inventory bounds are logistics thresholds, not hard storage restrictions. They do not independently block production or direct transfers. An inverted lower and upper bound is rejected without partial changes, and clearing one bound preserves the other.
- Restoring inventory does not replay insertion filters against already owned resources. A rejected state restoration does not partially replace live contents.
- The server owns resource-affecting changes. Rejected or unauthorized edits have no gameplay effects and do not disclose another team's private assets.
- Accepted visible changes reach all eligible team members, not only the player who made the edit. Repeated or delayed state delivery must not duplicate resources or replace newer state with older state.
- Reconnect and team changes clear obsolete client-visible state. Stored and displayed overlapping facts must agree after a successful load or synchronization.

## Scope

The archived architecture effort left fluid capacity unlimited for that effort. It did not establish a permanent Alpha fluid-capacity balance rule. [[Define Automated Facility Fluid Capacity]] now owns that open product question. This does not prescribe inventory classes, state codecs, network framing, or synchronization algorithms.

## Provenance

These requirements were extracted from the approved August architecture decisions and the completed physical inventory-filter correction during the owner-authorized cleanup on 2026-09-11. No new gameplay behavior was approved by the cleanup, and current implementation was not reverified.

The original records are recoverable from the external archive `D:/ObsidianVaults/Galaxia Consolidation Backups/Galaxia-before-engineering-cleanup-20260911.zip`.
