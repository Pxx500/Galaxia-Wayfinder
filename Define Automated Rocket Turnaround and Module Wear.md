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

## Question

How do module wear, failure, repair, replacement, salvage, refueling, and cargo handling form an automatable Rocket turnaround lifecycle without creating repeated manual maintenance work?

## Resolution

Rocket modules accumulate bounded statistical wear across event-based journeys. Physical Gantry-connected automation repairs the Rocket outside the Star Map, while a dummy `Perform maintenance` visit action declares where the scheduler expects servicing. A schedule safety policy checks durability through the next declared service visit with an initial 10% reserve. The precise relationship between this reserve and worst-case wear remains provisional as explained under Consolidation Caveats. The exact Gantry machine responsible for repair is separated into [[Decide Gantry Maintenance Machine Ownership]] for agreement with the other developers.

## Established Direction

- Reusable Alpha Rockets have recurring propellant and module-lifecycle costs. The opening progression may use expendable early designs as described in Specify Alpha Opening Mission Flow. This turnaround contract does not require every Rocket design to return or be reused.
- A Rocket is assembled from functional modules. When a module reaches zero durability during a mission, it loses its function and applies a module-specific failure consequence.
- Modules use persistent accumulated durability with statistically variable but bounded wear. The model is predictable in its inputs, expected value, and possible range without making every identical mission produce exactly the same damage.
- Every module receives general mission wear from flight duration and relevant environmental exposure, even when it does not perform a unique active function.
- Module definitions also contribute functional wear rules where appropriate. Engine wear may scale with burn duration and delta-v delivered, while atmospheric exposure may affect engines, thermal protection, and other exposed modules according to their own coefficients.
- Wear is not a flat identical durability subtraction applied to every module or every flight. Module durability capacity, baseline wear rate, functional coefficients, and statistical variation may differ by module type.
- The model does not invent functional module categories that do not otherwise exist. Wear rules attach to real Rocket modules and mission exposures.
- Wear remains event-based rather than simulated every tick. At departure, the journey uses its stable seed to sample total wear for each module from the bounded distribution around the estimate.
- If sampled wear would exhaust a module during the flight segment, the journey derives a failure point from the module's remaining durability and sampled total wear and stores the resulting failure event in journey data.
- Example consequences include engine failure destroying the Rocket, fuel-tank failure leaking propellant and leaving the vehicle unable to complete propulsion, or another functional module losing the capability it provides. Exact consequences belong to real module definitions.
- At departure, the planner calculates and shows one approximate expected-wear value for each relevant module for the next flight segment. The normal player-facing summary does not need a detailed probability distribution or min/max presentation.
- During transit, the vehicle exists as journey data rather than a continuously simulated Rocket entity. Stored arrival or failure events advance the vehicle state without recalculating wear every tick.
- At the next scheduled stop, a successful journey applies the already sampled durability loss.
- The persisted mission seed prevents save reloads or repeated arrival processing from rerolling the outcome.
- Wear calculation is triggered by departure and arrival state transitions. It does not run every tick.
- A Rocket may finish at an endpoint without servicing infrastructure. The planner must expose approximate expected wear across the schedule so the player can judge whether durability can cover several flight segments before returning to a servicing endpoint.
- Non-catastrophically failed modules may be restored automatically from zero durability by the physical maintenance system. Restoring from zero costs more than repairing ordinary accumulated wear; the exact material-cost model remains open.
- Maintenance is integrated into the ordinary landing-to-relaunch lifecycle rather than performed as repeated manual player work.
- Physical world machines service the Rocket item through ordinary item automation. They consume supplied maintenance materials and repair its modules without requiring the Star Map flight system to discover, command, or monitor those machines.
- Galaxia already has a physical Gantry System for creating, transporting, and installing Rocket modules through machines such as the Silo and Module Assembler. The maintenance workflow should deepen that existing module-handling ecosystem rather than introduce a parallel transport path.
- [[Research Current Gantry System]] verified that the Silo is the closest existing owner of physical Rocket turnaround, the Module Assembler is a production service, and Gantry is transport rather than a lifecycle owner.
- The current module-instance model has no durability, wear, serial identity, or repair state, and no maintenance machine exists yet.
- Gantry transport must preserve concrete worn module state and confirm handoff before maintenance can safely rely on it.
- A Rocket does not need full durability before launch. Its modules need enough remaining durability to satisfy the complete next Maintenance Cycle safety check.
- Automatic maintenance repairs modules toward full durability while suitable materials are available. With the safety policy enabled, incomplete maintenance blocks the next launch when any required module lacks enough durability for the remaining Maintenance Cycle.
- When durability is insufficient, the Rocket waits and reports the affected module through the existing warning and active-notification surfaces. The flight system does not infer which materials are missing from physical maintenance machinery.
- Routine maintenance should be an infrastructure and supply problem, not repeated manual module management. With suitable materials supplied, landing pads and docks perform the work automatically.
- The player's planning problem is whether the Rocket has enough durability to complete every flight segment before its next configured service endpoint. The player supplies maintenance resources; the endpoint performs inspection and repair automatically.
- A Rocket may be serviced after every landing or docking when the endpoint is configured and supplied for it, but schedules may deliberately span several endpoints before returning to maintenance.
- A Vehicle Schedule exposes a module-safety policy that can prevent departure when projected wear would make the current Maintenance Cycle unsafe.
- When this policy blocks departure, the Rocket remains on its current scheduled action, retries through the normal bounded retry lifecycle, and maintains one active notification describing the affected module or modules. It does not discard or advance the schedule.
- A Maintenance Cycle is delimited by scheduled visits containing `Perform maintenance`. The declaration identifies the planning boundary without observing or confirming a physical repair. Before departure, current durability must cover the remaining travel to the next declared service visit.
- At an intermediate stop, the safety policy validates only the remaining flight segments leading to the already selected service stop. It does not rotate the loop and require the Rocket to survive another copy of flight segments it has already completed.
- A scheduled visit block may explicitly declare that maintenance is expected during that landing, docking, or other stationary endpoint interaction. This declaration identifies the next service stop used by the scheduler; merely passing through the same endpoint does not implicitly end the Maintenance Cycle.
- `Perform maintenance` is a visit action nested inside that specific visit block, alongside actions such as unloading or loading. It is not its own top-level route block and does not make maintenance a global property of the celestial object or endpoint.
- `Perform maintenance` is a planning boundary, not a remote command sent to a physical maintenance machine.
- `Perform maintenance` has no repair, replacement, salvage, inventory, or completion logic of its own. It is only a dummy schedule declaration used to delimit durability planning.
- Each visit block targets either one concrete Transport Endpoint or an Endpoint Group on one celestial object. Maintenance expected during one visit applies to whichever endpoint actually receives that visit; it does not imply that unrelated endpoints on the same celestial object can service the Rocket.
- The Star Map trusts the player's declaration that servicing is expected at that stop. It does not need confirmation from the physical machine and does not infer maintenance infrastructure from the world.
- Before departure after a declared maintenance stop, the scheduler reads the Rocket's current module durability and validates the next complete Maintenance Cycle. If the physical machine did not repair the Rocket sufficiently, departure remains blocked and the active notification explains the durability shortfall.
- Provisional safety formulation: evaluate the worst allowed cumulative wear roll for every module across the complete Maintenance Cycle and require at least 10% remaining durability on the worst module.
- The accepted purpose of the initial 10% reserve is protection against statistical variance. Whether to combine it with worst-case wear or use another bounded guarantee requires confirmation. Do not claim that a particular implementation guarantees survival before its wear bounds are established.
- `Require safe durability until next service` is enabled by default on every new Vehicle Schedule.
- With the policy enabled, a schedule must contain a reachable later visit with `Perform maintenance`. Otherwise the configuration cannot begin its next Maintenance Cycle and reports the missing maintenance boundary.
- The player may explicitly disable the policy for a deliberately risky, experimental, or one-way schedule. Disabling it removes the preventive durability block but retains a red warning describing the possible module failure.
- A safe Maintenance Cycle does not add a persistent safety panel or extra status text to the schedule.
- When a planned trajectory is unsafe because of module durability, the existing trajectory-warning surface reports the affected module and a plain reason such as the module being too damaged for the trajectory.
- The warning does not need to expose exact durability arithmetic. Detailed current durability and maintenance values belong in the relevant Rocket or module inspection GUI.
- This ticket does not invent a new warning placement. Maintenance safety reuses the same warning presentation used by other trajectory hazards and feasibility problems.

## Related Topics

- [[Define Alpha Transport Roles]]
- [[Define Vehicle Capability and Route Requirements]]
- [[Define Space Transport Dispatch Model]]
- [[Define Team Notification System]]
- [[Explore Automated Reusable Rocket Staging]]
- [[Decide Gantry Maintenance Machine Ownership]]

## Consolidation Caveats

The durable requirement is predictable bounded wear, a service declaration, and a launch safety margin. The existing note specifies worst-case wear plus a 10% floor. The visible owner discussion motivates 10% as protection against bad rolls but does not establish that exact double-conservative calculation. Preserve it as a provisional safety formulation requiring confirmation, not a proven guarantee of the final distribution.

Departure sampling and derived mid-flight failure timing are a candidate realization. The owner explicitly requested estimates before departure and event-based updates rather than per-tick simulation. Confirm the sampling and failure timing contract when implementing real module consequences.

Gantry implementation statements above come from Research Current Gantry System at its recorded revision. They are not a fresh inventory of current code.

## Current Implementation Boundary

Read-only inspection on 2026-09-12 found definition, placement, and radial data in `src/main/java/com/gtnewhorizons/galaxia/registry/rocketmodules/rocket/blueprint/RocketPartInstance.java:7`, without wear or durability state in the inspected instance and serialization. The existing Rocket part model therefore does not certify module wear, maintenance-cycle forecasting, or automatic repair. The repair-machine ownership decision remains with Decide Gantry Maintenance Machine Ownership.
