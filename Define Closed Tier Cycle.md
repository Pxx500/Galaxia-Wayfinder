---
type: wayfinder-ticket
ticket_type: grilling
status: resolved
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Progression]]"
blocked_by: []
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Closed Tier Cycle

Resolved: 2026-07-31

## Closure Invariant

Every Ore Tier in Galaxia Alpha must satisfy a **Closed Tier Cycle**. This is a completeness invariant, not a tier-specific content specification and not a requirement to repeat one identical gameplay loop ten times.

## Required Chain

1. The player enters the tier with a defined capability supplied by the intended preceding GTNH progression.
2. That capability unlocks a concrete Galaxia activity, such as a mission, flight, logistics operation, investigation, or infrastructure objective.
3. The activity is completable without relying on a capability that belongs only to a later tier.
4. Completing it produces a defined progression result, such as a material, knowledge result, infrastructure capability, or another explicit requirement.
5. The player can apply, process, or transport that result to the place where progression consumes it.
6. The result opens the next intended GTNH or Galaxia progression step without trapping the player outside the continuing gameplay loop.

## Consequences

- Each Ore Tier needs its own later content specification naming the incoming capability, Galaxia activity, progression result, consumption point, and continuation path.
- Different tiers may satisfy the chain through different mechanics and destination roles.
- The invariant does not require every tier to repeat `rocket -> ore -> new rocket`.
- A tier fails Alpha closure if any link is absent, impossible at that point in progression, dependent on a later capability, unusable after acquisition, or a dead end.
- The current lack of tier-specific content remains Wayfinder fog to be charted into later tickets; it does not weaken the invariant.

## Related Topics

- Galaxia Alpha Charting Notes
- GTNH Ore Progression Baseline
- CONTEXT
- Galaxia Alpha Wayfinder

## Gameplay Flow

The player enters an Ore Tier with a capability from the intended preceding GTNH progression and uses it to complete a Galaxia activity. That activity must be possible without a later-tier capability and produce a defined progression result.

The player then applies, processes or transports that result to where it is consumed, opening the next intended GTNH or Galaxia step. The exact activity and result can differ between tiers.
