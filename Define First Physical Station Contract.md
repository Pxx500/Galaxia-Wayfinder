---
type: wayfinder-ticket
ticket_type: grilling
status: open
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Automation and Infrastructure]]"
secondary_areas:
  - Area - Observation and Research
blocked_by:
  - "[[Define Alpha Celestial Knowledge Layers]]"
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Define First Physical Station Contract

## Question

What minimum player-accessible capability makes at least one Physical Station necessary after the first Moon activity and before the first Mars mission, without hardcoding the station's orbit?

## Established Input

- A Physical Station and an Automated Station are separate entities.
- Alpha must require at least one player-accessible Physical Station.
- `Overworld -> Moon -> Physical Station -> Mars` is a provisional ordering.
- The station's location must emerge from eligible locations and required capabilities rather than a destination-specific placement rule.
- The first Moon mission must not require orbital assembly, refuelling, or similarly complex station logistics.
- Observation, telescopes, and research are candidates, but no exact capability or output is accepted yet.
- The Star Map's `Create Station` action must not imply that a physical Station can be created remotely. It should eventually link to a localized `How to build a station` guide explaining controller-first construction.
- Physical Stations are created through their controller and do not participate in planned asset construction. They have no asset-level construction inventory. Their items and fluids remain in physical inventories connected through the Station graph.

## Accepted Direction

The production floor and this Station contract are coordinated peer decisions. The accepted one-chain minimum does not require closing the entire production-floor ticket before discussing the Station's role. Recipe feasibility and concrete route validation remain evidence needed before final placement in progression.

The first Physical Station should primarily support production that benefits from or requires orbital conditions. It may have several useful roles at once. The concrete process and material remain undecided and must have a defensible environmental reason rather than an arbitrary station-only recipe condition.

## Orbital Production Candidates and Economic Role

Orbital processing may offer a more favorable recipe for the same product that can also be manufactured on a surface. A better usable yield from expensive feedstock can justify the capital and transport cost of the Station. Absolute orbital exclusivity is not required for every process. This does not weaken the separately accepted environmental vacuum requirement for Space-Grade Alloy.

The owner explicitly welcomed two concrete candidates:

- Silicon-germanium crystal growth for optics or electronics, inspired by more uniform growth in microgravity.
- Specialty fluoride optical fiber drawing, inspired by reduced unwanted crystallization in microgravity.

These are retained design candidates, not finalized recipes or confirmed early-tier material availability. Do not infer that all semiconductor manufacturing requires orbit, guarantee commercial superiority, or invent quality variants solely to represent improved yield. Ingredients, products, placement in progression, and numerical benefits require later content and balance work.

[[Define Alpha Research and Production Floor]] sets one complete orbital production chain as the current Alpha minimum, with more chains planned later. Both candidates remain available, but neither is selected by that scope decision. Its production machinery baseline applies here: use existing GT machinery unless a concrete process requirement justifies a custom machine. This is not an unresolved choice between two equally default approaches.

Primary-source findings are preserved in [[Orbital Manufacturing Research]]. The cited NASA reports describe orbital benefits, not physical impossibility of terrestrial production. No quantitative advantage over lunar gravity was established.

Owner accepted the better-recipe direction and expressed strong interest in both candidates in the Wayfinder conversation on 2026-09-10. The separate requirement that a first Physical Station be necessary for progression remains unresolved by an efficiency benefit alone.

## Material Progression Boundary

The owner supports Galaxia adding its own progression and infrastructure materials. Materials may participate in unlocking Automated Facilities, but this does not establish a mandatory dependency on output from a Physical Station specifically.

The owner recalled Space-Grade Alloy as a planned material whose feedstock comes from Luna and whose production requires a vacuum environment. The later accepted item identity, production environment and bulk-material role are owned by [[Review Crater Nodes Proposal]]. Do not describe the finished alloy itself as naturally mined ore or use it as the material gate between technology tiers. Exact feedstock recipes remain open.

Vacuum production is an environmental requirement, not a Station-only requirement. This material therefore does not by itself justify a mandatory orbital manufacturing step when the same required conditions are available on Luna. The exact first-Station production process and progression necessity remain open. Galaxia-specific materials need not remain exclusively useful inside Galaxia.

The owner subsequently confirmed that this vacuum requirement is a location/environment condition. A vacuum chamber constructed on Overworld does not satisfy it in the current scope. Luna and eligible orbital environments can satisfy it. This is a deliberate gameplay abstraction, not a claim that artificial vacuum is physically impossible.

Owner clarification in the Wayfinder conversation on 2026-09-10. The proposed fixed chain from first Physical Station output to first Automated Facility was not accepted as mandatory.

## Candidate Transport Role

The owner proposed orbital refueling as another possible reason to build infrastructure. An early vehicle might lack the fuel capability to complete a surface-to-destination journey directly, but be able to reach orbit, refuel there, and continue using the same vehicle.

This is an exploratory progression option, not an accepted mandatory refueling gate or a fixed destination assignment. The example of refueling before Luna does not yet supersede the earlier simple-first-Luna mission or the provisional Luna, Station, Mars order. If that option is selected, those earlier requirements must be revisited explicitly.

The candidate concerns a refueling stop, not a new multistage Rocket or booster-recovery system. Station placement and route feasibility should still follow environmental and vehicle capabilities rather than a hardcoded requirement to visit a particular station.

## Orbital Construction Bootstrap

The first physical orbital construction location is established by delivering a crafted kit aboard a Rocket. Station Starter Kit is a working item name, not final product copy. Its recipe consumes a modest collection of construction blocks rather than granting a free orbital structure.

An explicit kit-deployment mission places a small starter structure made from Station blocks, a Station controller, a chest containing additional Station building blocks, and a prepared Rocket landing location, potentially a preconfigured Landing Pad. The owner illustrated this with a 5-by-5 floor, a central controller, and one stack of spare blocks. Those dimensions and quantities are examples, not fixed balance or layout requirements. The final layout must accommodate the Rocket landing infrastructure.

The kit recipe includes the materials deployed into the structure and the supplied building stock. It does not generate free building materials. The starter provides a basis for player expansion, not completed production, refueling, or other advanced services.

Deployment is an explicit mission action. Merely carrying the kit as cargo does not construct a Station. Kits can be transported and stored at an existing location for later deployment elsewhere. An uncrewed Rocket can execute the deployment action.

The controller-first rule governs the deployed structure's Station registration. The kit places the initial controller rather than bypassing that rule. Ordinary controller lifetime and endpoint identity rules still apply.

Owner acceptance in the Wayfinder conversation: craft a Station Starter Kit from construction blocks and deliver it to orbit to establish the initial station structure. The item name and exact recipe were illustrative.

## Shared Orbital Space and Initial Placement

The current gameplay model assumes a geostationary Station orbit with continuous full sunlight. Do not add periodic planet-shadow outages or an orbital day/night production cycle in this scope. Solar intensity still follows the accepted celestial solar rules. The full-sun assumption is a gameplay simplification, not a claim that real geostationary orbits cannot experience eclipses.

- Each planet's orbital space is one shared physical dimension. Physical Stations belonging to different teams may occupy that same dimension. Do not create a separate private dimension for every Station or team.
- When deploying a new Station, the team may select coordinates or request a randomly selected location.
- Placement checks the selected location against existing Stations. Different-team Stations must remain at least a minimum separation apart. The owner gave 1,000 blocks as an initial illustrative distance, not a fixed balance constant.
- Stations belonging to the same team may be placed closer together. The player receives a visible warning about potential overlap and owns the consequences of choosing nearby sites.
- Minimum separation is measured horizontally between Station controllers using X/Z coordinates, ignoring height. This prevents bypassing the initial separation by deploying directly above another team's controller. The rule applies when deploying a new Station, not to later manual expansion of an existing structure.
- This is separation between initial Station locations, not a permanent guarantee of empty space between later-expanded structures. Permission to place same-team Stations nearby does not permit overwriting existing world blocks or inventories.

### Occupied Deployment Positions

Before placing the first block, check only the positions the kit intends to write. If any required position is occupied, do not begin deployment and do not consume the kit. This does not require discovering the bounds of surrounding Stations or continuously scanning the world.

The Rocket remains near the destination object with its kit intact, reports the occupied deployment site through the general notification system, and waits for the player to select another location. Waiting consumes no fuel and causes no durability loss under the common vehicle waiting rule.

No automatic replacement-site search, platform shifting, or partial construction rollback is required by this contract. The prior random-location choice is an explicitly requested placement mode, not an automatic response to a failed deployment.

Owner accepted this bounded occupancy check and waiting behavior in the Wayfinder conversation on 2026-09-10. Blind overwriting after a warning was discussed but not selected.

Owner accepted the shared orbital dimension and team-sensitive placement separation in the Wayfinder conversation on 2026-09-10.

## Provenance

Owner direction in the Wayfinder conversation on 2026-09-10: accept orbital production as the primary role and retain additional roles, including intermediate refueling, as possible complementary constraints. Refueling before Luna was explicitly an example rather than a final decision.

## Related Topics

- Audit Galaxia Concept Map
- Define Alpha Celestial Knowledge Layers
- Define Alpha Research and Production Floor
- Area - Automation and Infrastructure
- Area - Observation and Research
