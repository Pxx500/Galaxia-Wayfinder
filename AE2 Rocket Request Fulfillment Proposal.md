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

A proposed silo `fulfill requests` mode would load resources from attached AE2 storage, deliver them to a requesting landing pad within the star system and return.

The mission requires return fuel unless it relies on refueling at the destination. Identifying the servicing silo for a landing-pad destination remains an integration question.

Read-only context found that the rocket-missions branch already stores an explicitly selected service silo on a pad endpoint. The selection validates the same team/body and a reachable gantry connection. This is an existing service association, not proof that automatic destination refueling or AE2 request fulfillment is implemented.

Reuse existing logistics signals and the vehicle-owned schedule executor, not a second executor or separate ledger. The fulfillment mode remains a proposal, with the following refueling clarification recorded separately.


### Recorded Refueling Decision, 2026-10-21

For a mission relying on destination refueling, departure checks only that the servicing silo contains some compatible fuel. It does not check the quantity or reserve stock. Insufficient fuel or stock consumed before arrival is the player's logistics responsibility. This explicit decision replaces the earlier quantity-aware or reserved-stock proposals, without approving the entire fulfillment mode.

[[Sources]]
