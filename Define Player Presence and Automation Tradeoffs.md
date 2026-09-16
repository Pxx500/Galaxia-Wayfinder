---
type: wayfinder-ticket
ticket_type: grilling
status: resolved
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Automation and Infrastructure]]"
secondary_areas:
  - Area - Destinations
blocked_by: []
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Define Player Presence and Automation Tradeoffs

Resolved: 2026-07-31

## Question

How do individual Galaxia activities determine whether physical player presence is required or automation is available, and what trade-offs prevent automation from becoming a cost-free replacement for active play?

## Confirmed Direction

- Player presence is an activity-level rule, not a universal requirement for an entire Ore Tier or destination.
- Some activities are intrinsically player-bound because their intended interaction is the gameplay. A planned biological destination illustrates this direction: the player physically explores, gathers flora, encounters fauna, and performs field research that cannot be delegated to an Automated Facility. Its exact content remains unspecified because the originating developer's design has not yet been reviewed.
- Other activities, including standard extraction, may become automatable after the required technology is unlocked.
- Automated Facilities are not available from the beginning of Galaxia progression. Define Automated Facility Introduction sets EV as the working introduction target, reached through construction prerequisites rather than a player-tier check. This does not prohibit ordinary physical-machine automation during MV or HV.
- A manual route spends player time, attention, travel effort, and risk to produce its result.
- An automated route saves player time and attention but must impose other meaningful costs, constraints, or risks.
- Candidate automation costs include construction capital, module-specific recurring upkeep, supply logistics, energy, throughput limits, and shutdown when required inputs are not delivered.
- Alternatives do not need identical numerical strength. They must present understandable advantages and disadvantages so the player has a reason to choose according to preference and circumstances.
- Automation is part of the Progression Ecosystem rather than a strictly superior replacement for player activity.

## Upkeep Contract

Define Automated Facility Upkeep Behavior owns the accepted resource-upkeep contract: actual work incurs upkeep, and missing supplies temporarily stop only the affected module with its warning. Mere existence or idle time does not incur resource upkeep.

Resource choices, accounting cadence, buffering, and numerical balance remain module-specific follow-ups. Do not treat old per-minute or per-hour examples as accepted tuning or add another global shutdown rule here.

## Terminology Resolution

The current domain glossary distinguishes:

- **Automated Outpost:** body- or surface-anchored and potentially capable of mining;
- **Automated Station:** orbital and unable to mine the underlying body;
- **Automated Facility:** the umbrella term covering both placement forms.

The project owner uses `Automated Station` and `Automated Outpost` interchangeably in casual dictated discussion until placement or a concrete capability becomes material. Ambiguous casual usage must therefore be normalized to the umbrella term `Automated Facility` rather than treated as a change to the strict domain definitions.

In the extraction example that surfaced this ambiguity, the intended general concept was an Automated Facility and the specific extracting placement was an Automated Outpost. The orbital Automated Station remains unable to mine the underlying body.

## Accepted Terminology Rule

- Use **Automated Facility** when the user is speaking generally or casually.
- Use **Automated Outpost** only when body- or surface-anchored placement or its local capabilities matter.
- Use **Automated Station** only when orbital placement or its orbital capabilities matter.
- Do not infer a new station or outpost capability from one casual dictated use of the wrong specific term.
- If the distinction changes a consequential decision and the intended placement cannot be inferred from context, ask one focused clarification.
- The extracting asset in the current example is an Automated Outpost. An Automated Station may later support it through orbital capabilities such as energy, processing, data, storage, or transport, but does not directly mine the body.

## Fog Exposed

- Exact automation unlock tier and prerequisite technology.
- Which activity families are player-bound, automatable, or support both strategies.
- Formal costs and benefits of manual and automated strategies.
- Module upkeep inputs, consumption cadence, buffers, starvation behavior, and recovery.
- How players compare manual and automated options before committing resources.
- The biological destination's actual research loop and progression role.

## Related Topics

- Define Tier Destination Portfolio
- Require Persistent Tier Infrastructure
- Galaxia Alpha Charting Notes
- CONTEXT
- Galaxia Alpha Wayfinder
