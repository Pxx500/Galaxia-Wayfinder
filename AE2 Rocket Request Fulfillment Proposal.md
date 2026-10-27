---
type: source
status: unreviewed
tags:
  - galaxia/alpha
  - wayfinder/source
---

# AE2 Rocket Request Fulfillment Proposal

Source: Owner conversation on 2026-10-21 about rocket automation, AE2 and destination refueling
Imported: 2026-10-21

## Source Snapshot

The owner proposed adding AE2 integration to the rocket silo. A rocket could enable a `fulfill requests` mode. When a resource is requested within the solar system and exists in the attached AE2 storage, the rocket loads it, delivers it to the requesting landing pad and returns.

The owner requires return fuel, with a possible exception when the destination silo can provide fuel. They explicitly raised the unresolved question of how to identify that silo when arrival is at a landing pad, and noted that these details complicate the design.

Read-only context found that the rocket-missions branch already stores an explicitly selected service silo on a pad endpoint. The selection validates the same team/body and a reachable gantry connection. This is an existing service association, not proof that automatic destination refueling or AE2 request fulfillment is implemented.

Existing logistics signals and the vehicle-owned schedule executor are relevant owners to reuse. This source does not approve a second executor or a separate logistics ledger. The owner subsequently resolved the return-fuel policy below.


### Owner Clarification, 2026-10-21

The owner explicitly chose a departure-time presence check for destination refueling. If the rocket relies on refueling at the destination, check only that the servicing silo contains some compatible fuel when the mission departs. Do not compare its quantity with the amount required for refueling or the return flight. Do not reserve or lock that stock. Insufficient fuel or stock consumed before arrival is the player's logistics responsibility. This latest clarification supersedes the earlier quantity-aware departure check and the agent's recommendation to require onboard fuel for both directions or a destination reservation in the first version.

[[Sources]]
