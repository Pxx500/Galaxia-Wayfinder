---
type: glossary
status: active
tags:
  - galaxia/alpha
  - wayfinder/context
---

# Galaxia

Galaxia is GTNH's space-progression hub. Its player-facing systems connect technological tiers through exploration, spaceflight, off-world activity, and rewards that advance the wider modpack progression.

## Language

**Technology Knowledge**:
A team's acquired knowledge that can be required to produce particular parts or use particular recipes. It is separate from knowledge of celestial objects and from a Rocket's assembly design.
_Avoid_: Rocket Blueprint, Celestial Discovery

**Technology Blueprint**:
A physical item that a player consumes to grant its associated Technology Knowledge to their current team. In the initial Alpha flow it is crafted from materials unlocked through the relevant planetary progression.
_Avoid_: Rocket Blueprint, reusable recipe catalyst

**Rocket Blueprint**:
A reusable design describing the parts and arrangement of a Rocket, used to automate production of matching Rockets. It is not a technology unlock or proof of research.
_Avoid_: Technology blueprint, research unlock

**Celestial Asset**:
A persistent team-owned object placed on, around, or otherwise associated with a Celestial Object. It provides durable identity and Star Map representation for abstract facilities and for physical machines that require a backing asset.
_Avoid_: Restricting Celestial Asset to abstract facilities only, treating the physical block coordinates as the durable Star Map identity

**Facility Insertion Filter**:
A rule that decides whether new units of a resource may be inserted into an Automated Facility's abstract inventory. It does not hide existing resources, prevent extraction, or govern reconstruction.
_Avoid_: Admission filter, inventory visibility filter, extraction filter

**Galaxia Alpha**:
The first playable product milestone in which a player can traverse every included Galaxia tier gate without blockers and continue through the wider GTNH progression. Every included mechanic participates in a closed gameplay chain.
_Avoid_: Prototype, demo

**Progression Hub**:
Galaxia's role in connecting successive GTNH technology tiers through off-world objectives and rewards rather than operating as a separate campaign.
_Avoid_: Standalone campaign

**Celestial Progression Cycle**:
The repeating progression pattern in which a technology tier enables an off-world mission and completing that mission provides the material, knowledge, or capability needed to enter a later tier.
_Avoid_: Planet ladder

**Closed Tier Cycle**:
The completeness invariant for one Ore Tier: intended prior progression unlocks a completable Galaxia activity whose usable result advances the player through the next intended Tier Gate without trapping progression. The activity and result may differ by tier.
_Avoid_: Repeated rocket-and-ore loop

**Progression-Bearing Destination**:
A celestial destination whose activity or result supplies at least one required link in a Closed Tier Cycle. It may be mandatory or one member of an alternative route group.
_Avoid_: Required planet

**Galacticraft-Equivalent Destination**:
A retained Alpha destination without a Galaxia-specific gameplay loop that receives a minimal Galaxia-owned implementation based on its Galacticraft counterpart. It provides complete travel, environment, required ore access, extraction, return, and progression continuation and may be deepened later.
_Avoid_: Dummy destination, Star Map placeholder, original Galacticraft runtime

**Tier Destination Portfolio**:
The destinations, capabilities, activities, rewards, and prerequisites available within one Ore Tier from which the player can construct a Valid Tier Route.
_Avoid_: One planet per tier, planet checklist

**Valid Tier Route**:
A player-chosen sequence of accessible activities and destinations that satisfies a Tier Gate without relying on a later capability or creating a Progression Bypass.
_Avoid_: Canonical route, prescribed itinerary

**Progression Ecosystem**:
The interacting destination capabilities, resources, activities, prerequisites, and Tier Gates whose authored rules let players construct their own valid routes while preserving the intended broad progression order.
_Avoid_: Planet quest chain, fixed campaign route

**Persistent Tier Infrastructure**:
A durable surface, orbital, automated, logistics, or other celestial asset whose continuing capability participates in a Closed Tier Cycle beyond a one-time visit or deployment.
_Avoid_: Mandatory planet base, temporary mission equipment

**Construction Site**:
An incomplete celestial asset that receives the materials required to become its finished operational form. Creating it is distinct from satisfying its construction requirements.
_Avoid_: Completed asset, tier-locked build button

**Destination-Dependent Production**:
Production whose available process, inputs, outputs, or operating conditions depend on authored physical or environmental properties of its celestial location.
_Avoid_: Dimension-agnostic production

**Tier Gate**:
A Galaxia-controlled requirement that must be satisfied before the player can enter a later GTNH technology tier. In the current Alpha model, research or capability requirements may contribute to reaching a gate but do not replace its progression material.
_Avoid_: Planet reward

**Ore-Backed Tier Gate**:
A Tier Gate whose primary non-substitutable requirement is acquiring and processing the intended off-world progression material. Research, knowledge, or data may precede or accompany that requirement without replacing it.
_Avoid_: Research-only tier, data-only tier, mandatory Composite Tier Gate

**Progression Bypass**:
An outcome that satisfies a later Tier Gate without completing the intended prerequisite progression. Merely detecting or reaching a later destination is not a bypass unless the resulting knowledge, resource, or capability advances the gated progression.
_Avoid_: Early discovery, difficult alternative route

**Celestial Discovery**:
Team knowledge that a celestial object exists, with orbital information sufficient for flight planning. It does not imply a visit or knowledge of its environment and resources.
_Avoid_: Visit, resource scan

**Star Map Object**:
A persistent celestial entity used for orbital structure, discovery, planning, infrastructure, or other gameplay. It does not necessarily own a dimension or appear as matching physical terrain inside a shared dimension.
_Avoid_: Dimension, world instance

**Star Map Actionability**:
The completeness invariant that every retained Star Map Object has a meaningful Gameplay Representation and at least one object-appropriate interaction derived from its celestial nature. Physical travel and a dedicated dimension are not required.
_Avoid_: Decorative object, empty context menu, inert placeholder

**Gameplay Representation**:
The interaction model through which a Star Map Object or celestial region participates in play, such as a direct dimension, a Regional Dimension, Star Map-managed infrastructure, or an explicitly contextual role.
_Avoid_: Dimension requirement

**Regional Dimension**:
A player-accessible dimension representing a celestial region rather than a single Star Map Object. Its procedurally generated local bodies are gameplay terrain and need not be physical incarnations of persistent objects shown in that region on the Star Map.
_Avoid_: One dimension per object, persistent asteroid instance

**Persistent Asteroid**:
A stable Star Map Object inside an asteroid belt that can receive remote infrastructure and eligible vehicle traffic but cannot be visited physically by the player. It is distinct from local asteroid terrain generated inside the belt's Regional Dimension.
_Avoid_: Belt terrain asteroid, player destination

**Belt Coordinate**:
A selectable point on an asteroid belt's Star Map band that maps to physical coordinates in its Regional Dimension.
_Avoid_: Persistent Asteroid

**Belt Beacon**:
A player-placed block inside an asteroid-belt Regional Dimension that maintains a repeatable Star Map coordinate marker. After block destruction, the marker remains until a member of its team explicitly deletes it.
_Avoid_: Persistent Asteroid, temporary landing point

**Resource Knowledge**:
The team's information about resources associated with a celestial object. It is independent of Celestial Discovery, so a known object may still have unknown resources or only partial resource information.
_Avoid_: Object discovery

**Star Map Activation**:
The team milestone established by deploying its first Prospecting Satellite into the starting world's orbit, making the Star Map available. Activation exposes developer-authored initial object knowledge without itself granting detailed scans.
_Avoid_: Celestial Discovery, universal discovery

**Ore Tier**:
A group of destinations that share the same stage of access in the GTNH ore progression, represented by a common destination color in the maintained Ore Sheet.
_Avoid_: Planet color

**Highlighted First Occurrence**:
A colored ore-placement mark identifying where an ore vein first becomes available along a progression route. It is evidence that the vein may matter to progression, but it is not by itself proof that the vein is a Tier Gate.
_Avoid_: Mandatory ore

**Capability Parity**:
Coverage of the essential player capabilities offered by Galacticraft and the selected addon baseline, implemented through Galaxia's own mechanics and content rather than copied feature-for-feature.
_Avoid_: Literal feature parity, one-to-one parity

**Orphaned Mechanic**:
A mechanic whose inputs, player decisions, consequences, or downstream progression do not connect into a complete gameplay chain, leaving it as a dead end or isolated activity.
_Avoid_: Standalone feature

**Interplanetary Logistics**:
The explicit movement of players, items, and fluids between celestial destinations through Galaxia travel and cargo systems, without teleportation shortcuts.
_Avoid_: Teleportation network

**Hammer**:
A Galaxia electromagnetic cargo launcher whose ordinary deliveries require sending and receiving infrastructure, with shot feasibility governed by route and environment. Its explicit satellite-deployment mode targets an orbit instead of a cargo receiver.
_Avoid_: Teleporter, player transport, unrestricted direct surface-to-surface logistics

**Gas Siphon**:
An orbital extraction module for a Gas Giant, using the body's atmosphere data without a surface dimension. It is distinct from ordinary atmospheric gas collection on solid worlds.
_Avoid_: Generic atmospheric collector, terrestrial atmosphere pump

**Solid Surface**:
An authored property identifying stable terrain on a Celestial Object. It does not itself guarantee a player-accessible dimension, usable resources, or every form of surface infrastructure.
_Avoid_: Separate `canLand`, `canMine`, `canBuildOutpost`, or `canPlaceSilo` flags

**Solar Resource Modifier**:
The authored Celestial Object coefficient applied to baseline solar availability for balance and exceptional local conditions. It contributes to the player-visible Daylight Solar Intensity and Average Solar Yield.
_Avoid_: `goodForSolar` flag, dimension-render brightness as production output

**Daylight Solar Intensity**:
The instantaneous solar output available while illuminated, normalized so Overworld daylight is `1.0x`.
_Avoid_: Full-cycle average yield

**Average Solar Yield**:
The long-term solar output across the local light and dark cycle, normalized so a complete Overworld cycle is `1.0x`. Light and dark duration remain separate because equal averages can require different storage.
_Avoid_: Instantaneous daylight output

**Environmental Properties**:
The shared operational facts derived for a Celestial Asset from its associated Celestial Object, Asset Environments, and installed protections or modules. Gameplay systems read relevant properties instead of owning copied celestial data or machine-specific location flags.
_Avoid_: Per-machine copies of gravity, atmosphere, radiation, temperature, or solar facts

**Raw Prospecting Data**:
A non-item network stream describing its originating Celestial Object, pooled across that object's Prospecting Satellites. It is transient input rather than a durable survey stockpile.
_Avoid_: Physical data item, originless prospecting data, permanent survey stockpile

**Processed Prospecting Data**:
The processed network result describing the same origin as its Raw Prospecting Data. Sustained return throughput contributes to that origin's prospecting bonus.
_Avoid_: Transferable planet-neutral bonus, cross-object prospecting data

**Data Processor**:
A player-built, expandable multiblock that uses EU to process typed network data, with capacity determined by its structural computing sections and their tiers. Each installation has its own job settings and a configurable throughput-versus-energy-efficiency tradeoff.
_Avoid_: Assumed singleton global processor, assumed per-machine topology, Prospecting-only processor stack, unlimited computation, consumable processor per job

**Automated Facility**:
A Star Map-managed Celestial Asset without direct physical player access. Automated Outposts and Automated Stations are its two placement forms.
_Avoid_: Player base, generic station

**Automated Facility Inventory**:
The single shared item inventory available to every module installed in one Automated Facility. Facility modules do not require internal item routing or separate per-module inventories.
_Avoid_: Physical pipes inside an Automated Facility, per-module item logistics

**Automated Outpost**:
An Automated Facility anchored directly to a Celestial Object through a valid Body Environment. Its available operations derive from local object properties and may include extraction from the object. A minor-asteroid Outpost operates in zero gravity and may provide a Dock without becoming a Station.
_Avoid_: Automated Station

**Automated Station**:
An Automated Facility occupying an Eligible Orbit and operating in a Space Environment. It cannot mine the underlying object's terrain and may serve eligible space-transport routes.
_Avoid_: Automated Outpost

**Space Environment**:
The vacuum and negligible local gravity conditions used for space operations in gameplay, available at both orbital Stations and suitable low-gravity asteroid Outposts. Production may require either condition independently, so absence of atmosphere does not imply microgravity.
_Avoid_: Treating Space Environment as proof that the associated object has an orbit

**Eligible Orbit**:
An orbit usable for Station placement under the associated Celestial Object's physical conditions. The numerical eligibility criterion remains unresolved.
_Avoid_: `canCreateStation` flag, local space beside a low-gravity asteroid

**Body Environment**:
The local conditions of an asset anchored directly to a Celestial Object. A body-associated asset does not necessarily have a player-accessible physical dimension.
_Avoid_: Assuming every body anchor is a conventional planetary surface

**Surface Environment**:
A Body Environment on an authored Solid Surface. It exposes the asset to surface conditions such as atmosphere, terrain, and local illumination cycles.
_Avoid_: Space Environment, body anchor without a Solid Surface

**Atmospheric Gas Collection**:
Physical-dimension extraction of gases from an authored atmosphere above a solid world. It shares atmosphere composition and pressure data with Gas Siphon but uses a separate access method and machine contract.
_Avoid_: Gas Siphon, finite planetary atmosphere reservoir

**Physical Station**:
A player-accessible station built as physical infrastructure. Planetary orbital Stations share their planet's orbital dimension, including Stations owned by different teams, and are distinct from Star Map-managed Automated Stations.
_Avoid_: Automated Station, Automated Facility

**Main Station Controller**:
The controller currently responsible for a Physical Station. Its connected construction defines the active fragment, while disconnected fragments retain Station membership without Station-provided functionality.
_Avoid_: Treating chunk unload as controller destruction, electing an independent main controller in every disconnected fragment

**Physical Station Room**:
A space within a Physical Station whose enclosing geometry is identified through validation, with one shared environmental state and operating cost regardless of how many controllers serve it. Geometric validity is distinct from the current ability to maintain pressure through its airlock connections.
_Avoid_: One duplicate room per controller, using Station identity as Room identity, equating an open airlock with invalid room geometry

**Room Validation**:
The check that establishes a Physical Station Room's enclosing geometry and whether that geometry meets the room's structural requirements.
_Avoid_: Treating validation as a measurement of current pressure or as proof of Station-wide device connectivity

**Spaceship**:
A reusable player and cargo vehicle for routes without atmospheric ascent or escape from a significant gravity well. It trades slow travel and high initial cost for high capacity and low unit cost.
_Avoid_: Rocket

**Rocket**:
A high-acceleration spaceflight vehicle capable of carrying a route from a planetary surface through its atmosphere and gravity well. It may also fly space-to-space routes, but does so less efficiently than a Spaceship.
_Avoid_: Spaceship

**One-Way Mission**:
A mission whose current vehicle and available infrastructure support arrival but not the required return journey. Later refueling or construction may make a return possible.
_Avoid_: Impossible mission, permanently inaccessible return

**Burn Feasibility**:
Whether a vehicle in its current state can perform a required maneuver within that maneuver's propulsion and timing constraints. It is a per-maneuver result, not a vehicle tier.
_Avoid_: Vehicle speed tier, one global burn flag

**Vehicle Schedule**:
An ordered linear itinerary owned by one Rocket or Spaceship, containing travel and visits with their own actions. It may run once or repeat.
_Avoid_: Flight Plan when referring to logistics actions rather than trajectory geometry

**Travel Block**:
One flight segment between two visits in a Vehicle Schedule.
_Avoid_: A frozen trajectory or a separate Flight Plan artifact

**Route Delta-V Budget**:
A player-selected upper limit on the propulsive delta-v expenditure of one scheduled Travel Block.
_Avoid_: Expected consumption, fuel-volume cap, tank capacity, guaranteed departure availability

**Flight Priority**:
The player's choice to favor fuel efficiency or speed when selecting eligible routes for a Travel Block.
_Avoid_: Permission to exceed a delta-v budget or bypass maneuver feasibility

**Transport Endpoint**:
A prepared, addressable logistics location such as a particular Rocket Pad, Silo, Dock, or eligible Automated Facility. It has a stable identity distinct from its name and associated Celestial Object.
_Avoid_: Treating an entire planet as the final destination when a specific endpoint is required

**Unprepared Landing**:
A manual player or cargo Rocket arrival at a stable physical site selected without a prepared Transport Endpoint. Its coordinates are resolved before departure and it is not an automated Vehicle Schedule target.
_Avoid_: Transport Endpoint, automated destination

**Landing Site Reservation**:
A temporary claim on the resolved footprint of an accepted Unprepared Landing mission. Pending reservations and physically occupied Rocket footprints prevent later scans from selecting overlapping sites.
_Avoid_: Full traffic-control system, permanent land claim

**Endpoint ID**:
The immutable identity of one Transport Endpoint used by exact references. It is never reused after destruction and remains separate from any player-editable Routing Name.
_Avoid_: Display name as identity, reusing a destroyed endpoint's ID

**Routing Name**:
The mutable player-facing name used to find and intentionally group compatible Transport Endpoints within their routing scope. Physical Station machines are scoped to their owning Station, while standalone endpoints are scoped to their Celestial Object. It does not replace Endpoint ID.
_Avoid_: Endpoint ID, globally unique machine name

**Endpoint Group**:
A symbolic routing target grouping compatible team endpoints with the same Routing Name and landing or docking kind within one routing scope. That scope is the owning Physical Station for its machines or the Celestial Object for standalone endpoints. A group can remain empty and become available again when matching endpoints are built.
_Avoid_: Using the shared name as an endpoint's identity, grouping endpoints across celestial objects

**Team-Owned Transport Endpoint**:
A Transport Endpoint belonging to a team rather than following its original builder. A team merge transfers ownership, while a member leaving an established team does not take its infrastructure.
_Avoid_: Letting a departing member take established team infrastructure

**Singleton Team**:
The ordinary team ownership container for a solo player. It has one member and can merge into another team.
_Avoid_: Teamless player as the normal post-login state, personal asset owner parallel to team ownership

**Visit Block**:
One occurrence of a vehicle at a Transport Endpoint or Endpoint Group inside a Vehicle Schedule. It contains the actions configured for that visit, which may differ from actions at another visit to the same target.
_Avoid_: Planet Block, global endpoint actions

**Perform Maintenance**:
A declaration inside one Visit Block that physical servicing is expected there. It marks a Maintenance Cycle boundary without commanding or observing repair.
_Avoid_: Implicitly discovered maintenance, remote maintenance command, repair implementation

**Active Notification**:
A team notification representing one condition that remains active while its source maintains it. It clears when the condition ends or its maintenance expires.
_Avoid_: Emitting a new notification for every retry or tick

**Rocket Turnaround**:
The automatable lifecycle between a Rocket's arrival and its next launch. A landing pad or service endpoint may inspect persistent module durability, consume supplied repair or replacement resources, refuel, handle cargo, and return the vehicle to launch-ready state without repeated manual player work.
_Avoid_: Making routine Rocket reuse depend on manual module replacement

**Maintenance Cycle**:
The ordered travel between scheduled visits declaring Perform Maintenance, or the remaining travel to the next such visit. Its boundaries express expected servicing, not confirmation that a machine actually repaired the vehicle.
_Avoid_: Full loop, round trip

**In-Transit Vehicle**:
A Rocket or Spaceship represented by persistent flight data while traveling between departure and arrival, rather than by a continuously simulated world entity.
_Avoid_: Per-tick vehicle simulation when departure and arrival calculations provide the required behavior

**Cargo Instruction**:
An item or bulk-fluid transfer intention belonging to a vehicle visit or endpoint service, identifying direction, resource, and quantity or target. Fluid freight is distinct from propulsion supplies.
_Avoid_: Requiring the vehicle to duplicate the dock's cargo configuration

## Orbital Production Vocabulary

**SiGe Blend**:
The unrefined silicon-germanium processing mixture that requires impurity-removal treatment before becoming crystal-growth feedstock.
_Avoid_: Ready-to-melt SiGe, wafer-grade SiGe

**SiGe Seed**:
A small SiGe crystal used to initiate further monocrystal growth. Seeds can be obtained by splitting a SiGe Monocrystal or remelted as crystal-growth feedstock.
_Avoid_: Reusable recipe catalyst, pure-germanium seed

**Poly SiGe**:
The polycrystalline SiGe output of powder processing, usable only as material for remelting. It is not the crystal used for wafers or seed multiplication.
_Avoid_: Returned powder, wafer-grade SiGe

**SiGe Monocrystal**:
A single-crystal SiGe product used either for electronic wafers or for additional SiGe Seeds.
_Avoid_: Pure-germanium monocrystal, Poly SiGe

**Space Grade Solar Panel**:
A manufactured photovoltaic component using SiGe solar cells and fluoride glass, used to craft Galaxia solar generators of different tiers.
_Avoid_: Existing GT solar cover, finished tiered generator

## Crater Vocabulary

Crater extraction and alloy terms reflect the owner's 2026-09-16 decisions. Size-class and richness tuning remain part of the earlier working proposal.

**Crater Deposit**:
A resource deposit associated with one generated crater feature, independent of biome or chunk boundaries. Its extractors share a finite ordinary-mining reserve and a subsequent unlimited fracking stage with progressively increasing fluid cost.
_Avoid_: Per-chunk deposit, independent reserve per extractor

**Crater Extractor**:
A machine that mines a Crater Deposit's initial ore reserve and then switches to fracking when the required fluid is supplied. This is a working domain name, not a finalized machine name.
_Avoid_: Assuming separate ordinary-drill and fracking-rig machines

**Space-Grade Alloy**:
A low-tech, mass-produced bulk material for space equipment and infrastructure, produced only in an atmosphere-free environment. Different feedstock recipes yield the same item rather than distinct material-origin variants.
_Avoid_: Per-feedstock ingot variants, the material gate between successive technology tiers

**Fracking Fluid**:
The extraction medium supplied to a Crater Extractor after ordinary mining is exhausted. Processing its enriched output recovers only part of this fluid, requiring ongoing replacement production.

**Enriched Fracking Fluid**:
The resource-bearing fluid produced by crater fracking and processed downstream to obtain resources and recover part of the extraction medium.

**Fracking Fluid Family**:
A shared family of fluid variants used by the crater-processing chain. Each subtype has a distinct registered fluid identity so recipe processing and browsing can distinguish it.
_Avoid_: One Fluid ID distinguished only by NBT

**Crater Size Class**:
An authored `Small`, `Medium`, or `Large` category defined by a mean diameter and standard deviation. Classes may overlap, so a crater's realized diameter does not uniquely identify the class that generated it.
_Avoid_: Hard size interval, diameter-derived class

**Crater Material Profile**:
An authored crater-deposit composition with an independent generation weight for each Crater Size Class. A zero weight makes the material profile unavailable under that Size Class.
_Avoid_: One global resource table for every crater size

**Crater Richness**:
The reserve multiplier derived from a crater's realized diameter relative to its originating Crater Size Class and moderated by the selected Crater Material Profile's authored size response.
_Avoid_: Material composition, independent unbounded random bonus
