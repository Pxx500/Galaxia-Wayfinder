---
type: source
status: reviewed
tags:
  - galaxia/alpha
  - wayfinder/source
---

# Discord Source - Galaxia Dev Notes

Source status: reviewed historical developer notes
Imported: 2026-07-31
Original document: [Google Docs](https://docs.google.com/document/d/1kyRDNYa4DpgGRy6Sq5Y77DPSezG7nJh97so4hAIrfco/edit?tab=t.62cu26l6xf9d)

> This file preserves historical Galaxia developer notes and may be outdated. Its classification is recorded in [[Galaxia Dev Notes Research]]; the source itself is not an accepted specification.

## Imported Content

MAIN INFORMATION
THIS DOCUMENT WAS CREATED TO DESCRIBE DEV’S IDEAS AND CONCEPTS TO OTHERS AND AVOID 10001 TXT DOCUMENTS


To describe an idea, create a new tab in this document and give it a descriptive name
Space flight （Ya9yu and Four's idea)
The concept of an AFPG that will include arcade space flights with various dangers and opportunities


To start, we will have 3 active scales that the player will see and that will directly interact with the game

- Radiation (or what you might call accumulated damage)
is a zero-based scale that fills with spaceflight time. This scale is designed to determine the amount of time we can spend in space.
- Fuel this scale means how much time we can accelerate in a certain direction, it is spent on any direct movements with the main engine
- Energy, this scale determines how much we can spend on active and passive abilities that consume electricity

We also have 2 parameters that affect the minigame which are set only at the start
- Mass, a parameter denoting the total mass of all modules and fuel on a ship, can change dynamically during flight with fuel consumption, but the mass parameter does not depend on usual resources or liquids carried on a rocket/ship
- Speed ​​this parameter means the speed of ejection of the moving body into space, over time during the decrease in mass your acceleration may increase, but the basic speed parameter is not changed


Rocket Modules (Skorched)
PROPOSAL - ROCKET SYSTEMS:


Core Rocket


This is effectively a 'super module', it provides the general shape of the rocket/ship, and how many modules are available to that rocket.
It also determines which dimensions you can go to, such as T1 -> Theia, T2 -> Hemataria + moons etc. etc.
Module


These are "additions" to the core rocket. There are multiple types of modules, but each core rocket will have a designated amount all added in the same way, and they are as follows:


 Structural Modules: 
These are modules that are effectively required for entry to certain planets. Radiation shielding, Temperature shielding, Pressure Shielding etc. all fit into this category. Within this category, it subdivides to:


* Enforced Modules - These modules are REQUIRED for the rocket, and have module slots designated to them. This is generally things such as fuel tanks, engines etc. This would mean that there is still player choice in things like the engine / fuel used, but the rocket is still tiered


* Passive Modules - More expensive modules that passively provide bonuses but at a resource cost, used for things such as shielding


* Active Modules - Cheaper, but require constant source of electricity to maintain bonuses. Have the general same purpose as passive modules


Functional Modules:
These are modules that provide some other functionality beyond simply getting to a planet. Examples would include (but not limited to)
 - Thrust Modules - Decrease the time taken for the rocket to reach atmosphere (QOL)
 - Processing Modules - Ore processing steps taken on any ore resources in the internal storage (Similar to how the miner multi pre-macerates)
 - Fluid Storage Modules - Effectively just large tanks attached to the rocket to make an earlier way of transporting bulk fluids from other dimensions
 - Item Storage Modules - Self explanatory, but allow storage of items based on module size etc.


THIS is the core place to be creative as a dev team, the entire viability of having modular rockets as part of our identity will come down to the execution of modules


EXAMPLES:
TIER 1 ROCKET


TIER 1 ROCKET CORE
├─ Structural Modules
│  ├─ Enforced Modules
│  │  ├─ Fuel Tank Slot 1
│  │  └─ Engine Slot 1
│  └─ Customisable Modules
│        └─ NO AVAILABLE MODULE SLOTS
├─ Functional Modules
     └─ NO AVAILABLE MODULE SLOTS




TIER 2 ROCKET
TIER 2 ROCKET CORE
├─ Structural Modules
│  ├─ Enforced Modules
│  │  ├─ Fuel Tank Slot 1
│  │  ├─ Fuel Tank Slot 2
│  │  ├─ Engine Slot 1
│  │  └─ Engine Slot 2
│  └─ Customisable Modules
│       └─ Custom Slot 1 (Rad Shield etc.)
└─ Functional Modules/
     └─ Custom Slot 1 (Storage Module etc.


As can be seen in these examples, the core enforced modules are designated to be of one specific type, whereas the custom slots allow any of that type to be inserted
________________




Module Assembler


This is the primary method for creating both the modules, and the core rocket, across all tiers. Higher tier rockets will be unlocked using Research Notes (or some similar system) that allows the player to create T2+ rocket cores and modules


Silo/Launch Pad


This is the multi responsible for rocket launching. It takes the created modules (including the core rocket) from a linked module assembler, and allows the player to build the rocket, play whatever minigame we decide on, and launch on that path. It is also (potentially) where landing rockets will go.


Overview


The Tiered Core Rocket determines what planets can be accessed at a fundamental level.
>NOTE: This does not mean that a T2 rocket core just immediately allows a player to safely travel to Hemataria, you still need appropriate shielding etc.


The Structural Modules give the player the correct rocket to access planets, whether it being the shielding required, or some other requirement. The Enforced structural modules are designated to be of ONE specific module type (engine etc.)


The Functional Modules are entirely excess to requirements, and give the player the biggest amount of freedom, where as you unlock more modules (particularly in higher tier spaceships) you can customise your rocket to be as you intend






Gantry System (Skorched)
PROPOSAL - GANTRY SYSTEM:


As of the time of writing, the current working system for the gantry is as follows:


With a Silo TE and an Assembler TE both placed, shift right click the assembler with a linking tool to set it as a master point, and right click on silos to set as linked silos.


My proposal is to expand on this to make a fully fledged system.

For the purposes of this proposal, any reference to a ‘TOOL’ should be assumed to be the linking tool.
Initial Linking
I have only one suggested change for the initial linking of 2 multis - DO NOT require direct line of sight between the two linked modules. The underlying reasoning will be clearer after reading this proposal


Structural Changes
Included in the multiblock structure is a required single TileEntity, a gantry door controller. This controller will designate the positioning of the door within the multi, and will be the point from which gantry animations begin/terminate. This must be placed in the centre of one of the sides of the multi (will be clearer once we have a design of said multis)


Gantry Linking
Instead of the linking tool being used on multis, the tool is linked more directly on the gantry door blocks. This will then internally set the offset required for the animation starting within the main controller of the multi


When two gantry doors are linked, it is initially assumed to be a fully linear, line of sight check. Once this is set up, the user can right click non-gantry blocks with the tool, and it will add “spline” points. These points will work to direct the desired path of the gantry to make a fully customisable gantry path. This path must still be fully clear of any blocks or the transfer will fail (TBD what this actually means). The path must also follow an exact block line (similar to minecarts in vanilla), so there are no diagonal paths or curved paths.


Code Implementation
For the gantry path, it seems logical to use some version of a LinkedList style traversal. The code will effectively just transfer a module from start -> point A, then point A -> point B -> … point X -> end. Each of these transfers then isolates the check of clear blocks, allowing smaller updates, as changing the path only changes the checks on the 2 new segments created.


Animation
Though the math eludes me at the minute, there is a lot of potential for an immersive animation loop. Going round corners retains inertia of the module, causing a ‘swing’ out effect.


This swing out can be dependant on mass to further add to the realistic animation
Alpha checklist (Vortex)
Alpha Release Must-have List:


Gt integration
* recipes for: 
   * singleblock machines
   * multiblock machines
   * casings
   * rocket modules
   * rocket parts
* decide how much microcrafting we need to keep it logistics challenge
* GT ore generation
* create processing line for moon (most likely simpler titanium setup)
* add fuel line / choose CBD (if choose CBD remove the quest for 64 cells) 
* discuss balancing of recipes with GTNH devs
* Add GTNH teams integration for starmap and research outpost
Mechanics
* Redo airlocks to be more clean (discussed with sbancuz)
* Redo gantries to be node-powered and make them more clear to use and render
* basic satellite handling for wireless connection
* Add automation for rocket launches similar to factorio trains
* Research outpost:
   * discuss the exact mechanics and UX
   * create proper research tree/whatever research type we choose
   * create all researches up to mars flight (last research unlocks mars)
* Decide which machines we need to make for alpha
* Add visible tanks and gear on player
* Finish dynamic plumes by chloe
* Add returnable rocket parts (was discussed on 16th may meeting)
* Make rockets consume fuel
* Gralpling hook???(no, not yet (wait i actually added it))
* Add the combined fuel tank/engine combos (orbitals)
QOL & UX
* Add in-game info about how to use of starmap (in the starmap itself)
* Remove dismounting for rockets (at least make it take 1-3 seconds)
* Create a mini-doc for mechanics explanations
Design
* create all leftover modules’ models (currently lander, storage, rider modules, maybe some others)
* decide whether we are using models or blocks for galaxia only multis
* create proper structures for multis
   * Hammer Target
   * Hammer Cannon (just the base)
* create GUI for:
   * module assembler
   * rocket silo
   * oxygen collector
   * oxygen filler
   * oxygen pylon
* add/redo textures to:
   * Moon Anorthosite
   * Rocket Silo
   * Module Assembler
   * Gantry Terminal
   * Gantry shafts
   * oxygen collector
   * oxygen filler
   * oxygen pylon
   * AirLock Door
   * AirLock Casing
   * AirLock Controller
   * Station Controller
   * Small Oxygen Tank
   * Medium Oxygen Tank
   * Large Oxygen Tank
   * Creative Oxygen Tank
   * Oxygen Mask (not merged)
   * Reaction Control System
   * Wither Protection (not merged)
   * High Pressure Shielding
   * Low Pressure Shielding
   * Galactic Map
   * Teleporter
   * Trophy Block
   * Oxygenator (not added mechanically yet)
   * Air purifier (not added mechanically yet)
   * Heating coil
   * Cooling coil
   * Space station maintenance hatch
   * Space station plugs (lots of dynamo hatches)
   * Casings/Glass/Scaffolds for space station
   * kinetic tether (both rope and itself)
* SKY
   * milky way overlay
   * special stars (maybe, not sure needed)
   * nebulas
   * other galaxies
Stations (Sbancuz)
Proposal - Stations


With the nerf to ender chests, quantum rings, etc. physical stations will be the decentralized hub for all space logistics systems. They will integrate with the starmap with the objective to automate resource deliveries. In addition to the logistic network stations will also provide modules for specialized, optimal lines for resource automation.


The station will also offer protection from environmental effects for the player and all the machines (single blocks or multiblocks) and, as such, will have to be built with appropriate materials to function correctly
Structure
A physical station will be composed of different modules, each created by their respective controller. A module will accept any shape so long as it is either enclosed or simply connected to the controller. Each module will be able to interact with specific multiblocks that will become part of the station itself
Station parts
* Station room - This is an enclosed room with nothing special in it, all the normal machines will work fine as long as the station protects against environmental hazards. Since air is a very limited resource here, any usage of a muffler hatch will amplify the oxygen usage dramatically depending on the speed and tier of the recipe (or they won’t work all together) 
* Main station room - Same as the normal room, but it holds the main controller that is tied to the station (in the starmap) and can control every room
* The docks - This is an open “room” that can interface with logistics multiblocks for handling deliveries and rocket launches
   * Hammer target - a multiblock that can request and receive packages from the starmap
   * Hammer cannon - a multiblock that can provide and send packages to the starmap
   * (TBD) Automated rocket assembly and logistics
   * (TBD) Integration with ME requests
* (TBD) The power room - An enclosed space that will hold any non-polluting generator and all the batteries to provide energy to the station. Energy in the spaceship will be used for life support systems and will be delivered “wirelessly” via plugs in the walls to all the multiblocks integrated in the core station building (eg. rooms and attachments like the hammer cannons). Note that this courtesy is not reserved for any other machine, but each room can embed a couple of special hatches into the structure to act as plugs into the centralized power. 
* (TBD) The hydroponics room - Integration with cropsNH and bees that will provide new optimal environments for them
Tiering system
The station won’t have tiers, the attached multiblocks however will get the voltage tier from a special hatch that can draw power from the station
Structure blocks
The external shell of the station has to be built with special blocks that can protect from various environmental effects (extreme heat, extreme cold, radiation, etc..). There will be different blocks for making space stations depending on these factors.
Special lines (To be discussed) 
The space station should also be the place where to put special processing lines or multiblocks that can effectively take advantage of environmental factors, for example a better freezer that boosts the colder the environment is.


Zero gravity should allow some special processing line.


Highly radioactive environments could enrich processing lines like the naquadah line for example


Research station integration
In there is a very clear view of the stars and planets, and as such it would be a perfect place to put an observatory to gather information about your solar system (and maybe more)


Satellites


These are for spreading the ae2 network in some way
AutomatedFacility
Automated Facility Systems
Automated Outposts
Automated outposts serve as an abstraction for locations that players cannot or do not need to visit in person. These outposts would be primarily located on minor celestial bodies, such as small asteroids or high-radiation zones, which do not possess a dim (or just don’t have to).
Interaction with these outposts occurs exclusively through the Starmap. This system allows for the inclusion of numerous minor worlds and asteroid types without the bloat of adding numerous boring dimensions.
Minor Asteroid Properties
The system would require adding small, non-visitable asteroids with randomized statistics generated within predefined bounds (or static, but where’s the fun in that). These statistics determine the ores that can be mined (or maybe some other systems that can be implemented later like crafting in the coldness of space or microgravity).
Outpost Modules and Upkeep
Outposts are built and upgraded via the Starmap using specialized hardware launched from a primary station or planet. Module types:
• Power Modules (solar, nuclear, fusion, maybe something else like RTG)
• Resource Modules (mining, fluid drilling, tiered)
• Production Modules (something assembler like, ore processing for cheaper resource transfers 64 raw ore -> 16 -> 1 so each railcannon shot is worth even more with each processing step)
• Logistics Modules (hammer can have a throughput of one stack per 10sec or however much is chosen so adding multiple or upgrading could also be an option)
Stations would also need some kind of upkeep (as opposed to manual ones) for each station/module. Required resources should be tiered with the module tier to keep the cost relevant.
Logistics and Item Transfer
Automated outposts cannot use standard inventory transfers and must rely on automated ships or railgun systems. (we blocking AE2 with that one 🔥)
• Standard HAMMER: Is sufficient for intra-system transfers, such as moving items between a moon and its parent gas giant.
• Interplanetary Railcannons (BIG HAMMER or whatever name is chosen): Transfers between different planetary systems require a larger, high-tech version of the HAMMER.
• Receiving Cargo: Direct delivery to a planet's surface is restricted; players must have a station in orbit to receive cargo before it can be dropped to the surface via standard HAMMER units.


Progression Roadmap
1. Chemical fuel rockets for manual exploration and initial resource gathering.
2. Establishment of normal space stations.
3. Ion thruster spaceships for more efficient travel (or maybe only for places with low thrust requirements?).
4. Advanced: Deployment of Automated Outposts to hostile or distant celestial bodies for that sweet resource extraction.
5. Construction of Interplanetary Railcannons to link all orbital stations into a unified, high-speed logistics network.
Integration
Players utilize predefined modules for construction to prioritize logistical speed over flexibility.
Outposts function in tandem with manual stations to eliminate repetitive setup on minor celestial bodies.
This level of abstraction enables the massive industrial scaling necessary for late-game progression.
The stations could serve as a significant resource sink and a long-term investment in automated growth.
System Requirements
The Vael System must be updated to include asteroid belts, small moons, and individual asteroids to provide locations for these automated nodes. 
The HAMMER railgun system requires full automation to support the automatic requesting and sending of resources between different orbital stations (no micro from the player except setting up new functionality). 
Planetary integration with logistics systems like AE2 is essential for managing planetary resource transfers (AE2 to a multiblock that can supply orbital stations with resources requested by the stations in the star system). 
The outpost management interface needs to be well integrated into the starmap GUIs for remote operation.
