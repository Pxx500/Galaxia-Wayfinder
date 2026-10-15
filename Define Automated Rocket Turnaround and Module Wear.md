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

# Define Automated Rocket Turnaround and Module Wear

## Accepted Decision

Rocket modules accumulate persistent, statistically variable but bounded wear. Routine repair is physical, supplied automation in the existing Gantry ecosystem, not repeated manual work or a Star Map maintenance controller. Schedules declare service visits and check durability to the next service. This is accepted design, not implemented module durability or repair machinery.

## Wear And Failure

- Each real module has its own durability capacity, baseline rate, functional coefficients and bounded variation. General wear reflects flight duration and relevant exposure even when the module performs no unique active function. Engine use may depend on burn duration and delivered delta-v. Atmospheric exposure affects relevant modules under their own coefficients.
- Show one approximate expected-wear value per relevant module before departure, plus schedule-wide expected wear for planning several legs between services. A detailed probability distribution is not required in the normal summary.
- During transit the vehicle is journey data, not a continuously simulated entity. Wear and failure advance through flight events rather than per-tick damage.
- At zero durability the module loses its function and applies its own failure consequence. Examples include engine failure destroying the Rocket or tank failure leaking propellant and preventing completion. Consequences must belong to actual module definitions.
- Persist outcomes so reloads and repeated arrival processing cannot reroll wear or apply it twice.
- Non-catastrophically failed modules can be restored automatically from zero, at greater material cost than ordinary repair. Exact costs remain open.
- Reuse depends on recovery and mission conditions. This contract does not require every early Rocket to return.

## Physical Servicing

Physical machines repair the Rocket item through ordinary item automation using supplied maintenance materials. The flight system neither discovers nor commands those machines and does not infer their missing materials. Module transport must preserve concrete worn state and confirm handoff.

Maintenance deepens the existing Silo, Module Assembler and Gantry ecosystem. [[Research Current Gantry System]] identifies the Silo as the closest turnaround owner, the Module Assembler as production and Gantry as transport. [[Decide Gantry Maintenance Machine Ownership]] owns the unresolved choice of repair machine.

Repair proceeds toward full durability while materials are available. Full durability is not required to launch, but the next Maintenance Cycle must pass the configured safety policy. An endpoint without service infrastructure may still be a valid stop.

## Schedule Safety

- `Perform maintenance` is a dummy visit action, nested alongside load/unload actions in a particular Visit Block. It is a planning boundary, not a repair, replacement, salvage, inventory command or completion detector.
- A Maintenance Cycle ends at the next reachable visit declaring that action. Merely passing the endpoint does not end the cycle. The declaration applies to whichever exact endpoint or group member serves that visit, not every endpoint on the body.
- The Star Map trusts the player's service declaration. At the next departure it reads actual durability. If servicing did not repair enough, the Rocket remains blocked.
- `Require safe durability until next service` is enabled by default on new schedules. With it enabled, a reachable later maintenance declaration is required to begin a cycle.
- Check the remaining legs through that service visit. At an intermediate stop do not rotate the loop and count already completed legs again.
- Insufficient durability keeps the current action, retries through the scheduler's bounded lifecycle and maintains one active notification naming affected modules. It does not advance or discard the schedule.
- A player may disable the policy for risky, experimental or one-way missions. Preventive blocking is removed, but a red warning retains the possible failure.
- Safe cycles need no extra persistent panel. Unsafe trajectories use the existing trajectory-warning surface with plain module-specific reasons. Detailed arithmetic belongs in Rocket/module inspection.

## Provisional Formulation And Open Questions

The initial reserve is 10%, intended to protect against statistical variance. The recorded candidate checks worst allowed cumulative wear across the cycle and requires at least 10% durability remaining on the worst module. Whether both protections should apply together remains unresolved. Bounded wear does not certify that exact survival guarantee.

Departure sampling of total per-module wear from a stable journey seed, deriving and persisting a mid-flight failure point when it exceeds remaining durability, then applying the stored loss on successful arrival is a candidate realization. Event-based updates and preflight estimates are accepted. Exact sampling/failure timing requires confirmation with module consequences.

Open choices are the repair machine, material costs including zero-durability restoration, module coefficients/distributions and precise reserve calculation.

## Implementation Evidence And Provenance

Read-only inspection on 2026-09-12 found definition, placement and radial data but no durability/wear serialization in `registry/rocketmodules/rocket/blueprint/RocketPartInstance.java:7`, under `src/main/java/com/gtnewhorizons/galaxia/`. The Gantry research is dated evidence, not a current code inventory.

Owner discussions establish bounded wear, event-based simulation, physical automation, service declarations and a default safety policy. The 10% reserve's exact relationship to worst-case wear was not settled.

## Related Decisions

- [[Define Alpha Transport Roles]]
- [[Define Vehicle Capability and Route Requirements]]
- [[Define Space Transport Dispatch Model]]
- [[Define Team Notification System]]
- [[Explore Automated Reusable Rocket Staging]]
