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

# Define Automated Facility Fluid Capacity

## Question

Should Automated Facility fluid storage have finite, infrastructure-expandable capacity in Alpha?

## Established Input

[[Define Automated Facility Inventory Rules]] explicitly leaves this decision open. Unlimited fluid capacity was an earlier implementation-scope choice, not an accepted permanent gameplay rule. The facility's shared inventory and resource-preservation rules are already settled.

## Resolution

Accepted on 2026-09-17: Automated Facilities have finite fluid capacity, increased by storage modules. Each facility also has nonzero base fluid capacity before adding those modules, just as it has base item capacity. This avoids requiring storage expansion before it can accept the resources needed to get started.

Exact base capacity, module increments and tank organization remain tuning and implementation choices. The existing shared-inventory and resource-preservation rules remain in force. This abstract base capacity is not a grant of invisible storage to physical world-backed Stations.

## Provenance

Extracted from the resolved inventory note's remaining scope on 2026-09-17.
