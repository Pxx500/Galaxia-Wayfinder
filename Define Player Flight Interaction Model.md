---
type: wayfinder-ticket
ticket_type: grilling
status: resolved
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Travel and Logistics]]"
blocked_by: []
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Define Player Flight Interaction Model

## Question

What does the player actively do during a physical flight in Alpha: use an abstracted trip, manually fly a route, create and reuse a recorded flight plan, or use a deliberate combination of these interactions?

## Resolution

Alpha uses planned, time-based, event-driven travel rather than active piloting. A player configures and confirms the mission, then remains attached to the In-Transit Vehicle for the full journey while using the Star Map as the transit screen. The player may continue browsing and managing other team systems but cannot act in either physical world or alter the active journey segment. Vehicle Schedules provide reusable logistics intent, while each departure calculates a fresh trajectory. The recorded-flight minigame and separate pre-recorded Flight Plan system from the source document are rejected.

## Established Input

- The reviewed main planning document proposes a two-dimensional active flight sequence and reusable pre-recorded flight plans.
- That proposal is not accepted merely because it appears in the source.
- This ticket defines player interaction, not vehicle eligibility or route-cost mathematics.

## Accepted Requirements

- Alpha does not require active steering, thrust control, or a two-dimensional flight minigame during Rocket or Spaceship transfers.
- The player actively selects the vehicle and destination, plans the route, reviews duration, delta-v, propellant use, and warnings, then confirms departure.
- After departure, the vehicle becomes an In-Transit Vehicle and completes the selected journey through time-based event transitions rather than continuous player control.
- A player aboard a crewed mission remains assigned to that journey for its full transfer duration. Crewed travel does not skip or shorten the mission timer.
- Journey progression is independent of whether the player remains connected. Logging out does not cancel, pause, or reroll the mission.
- When the player reconnects, they return to the still-active transit state or to the completed arrival state if the journey finished while they were offline.
- The Star Map is the Alpha transit screen for an onboard player. Alpha does not create a physical Rocket or Spaceship interior solely to occupy the player during travel.
- The player's current vehicle is clearly marked on the Star Map together with its active route, progress, remaining time, and destination.
- The player remains in the Star Map transit screen until arrival or logout and cannot return to either physical world while the journey is active.
- During transit, the player may browse the Star Map, inspect celestial objects, vehicles, endpoints, and notifications, and manage other team vehicles or schedules.
- The player cannot alter or cancel the currently executing journey segment. Actions that require physical presence remain unavailable until arrival.
- A manual flight is a mission directly dispatched by a player rather than a manually piloted trajectory.
- Reusable travel intent belongs to Vehicle Schedule. Alpha does not record a successfully piloted trajectory or upload it as a separate Flight Plan.
- Alpha does not create, persist, copy, upload, or attach any separate Flight Plan artifact. Reusable transport intent belongs to Vehicle Schedule, and the active transfer retains the journey state needed to complete it. This statement does not restrict unrelated persistence or mandate an additional named Journey abstraction.
- A Vehicle Schedule stores endpoint visits and actions rather than frozen trajectory geometry. Each departure recalculates the route, duration, delta-v, propellant use, and warnings for the current celestial and vehicle state.
- Required progression and logistics never depend on active piloting. A future optional flight interaction would be a separate expansion rather than part of the Alpha contract.

## Related Topics

- Galaxia Main Planning Document Review
- Define Alpha Transport Roles
- Define Vehicle Capability and Route Requirements
- Define Flight Progression Balance Invariants

## Arrival at Non-Physical Facilities

A crewed vehicle may visit an eligible Automated Facility without creating physical player access to that facility. During the stop, the player stays aboard and remains in the Star Map view. The vehicle can perform its stop actions and continue its journey. The player can disembark only at a destination providing a physical player-accessible space.

Before departure, the mission warns the player when the destination does not allow disembarkation. This is not a blanket ban on crewed traffic to Automated Stations or asteroid Outposts.

Owner accepted this behavior in the Wayfinder conversation on 2026-09-10.

## Current Implementation Boundary

Read-only inspection on 2026-09-12 found fixed upward acceleration, a speed cap, and altitude-bound removal in `src/main/java/com/gtnewhorizons/galaxia/registry/rocketmodules/rocket/entities/EntityRocket.java:128`. This is not implementation of a persistent Star Map journey, passenger interaction, or offline transit continuation. Accepted player-flight behavior remains design rather than a certified current feature.
