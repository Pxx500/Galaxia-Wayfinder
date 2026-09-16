---
type: source
status: reviewed
tags:
  - galaxia/alpha
  - wayfinder/source
---

# Discord Source - Galaxia Main Planning Document

Status: Reviewed and partly outdated source snapshot
Source: https://docs.google.com/document/d/1I0_qtxRzEGk6KiOuNXg74zO9CaGzLLQCIhR4LTER1zo/edit?tab=t.bsiv88fmflo6
Imported: 2026-07-31

> [!warning]
> This document mixes current ideas, outdated sections, speculative proposals, and claims that may conflict with accepted Galaxia direction. Its classification is recorded in [[Galaxia Main Planning Document Review]]; the source itself is not an accepted specification.
>
> In the live `Replacing Features` section, green means replicated, orange means replaced, and red means deprecated. The original colors were checked and recorded in the review note.
>
> Ore and resource placement in this document is not authoritative. Use the maintained GTNH Ore Sheet as the progression baseline.

## Source Snapshot

ABOUT
Galaxia
About
Galaxia is GTNH’s new planned mod that will cover all the space and space travel related content the pack needs. It adds a bunch of new mechanics, such as modular rockets, new multiblocks associated with rocket construction, launching, and part manufacture, snap together space stations (inspired by how you build bases in subnautica), and a ton of new planet surfaces and content to explore! Currently there is no planned release date due to the scope of the mod, but we’re working hard every day! 




Navigation tabs:


Rocket System   🚀⚡


Space Travelling   🔥🔍


Space Stations    🛰️📡


The Vael System (by Juniper.S)    🌏🌑


Planets and surfaces    🪨🧊


Mod aesthetics   🔩🗺️


Replacing Old Features 👵👵


Equipment ⚒️🛠️


Rocket Systems


Rocket System
To launch rockets, players need to build proper infrastructure that will handle the launch. This  infrastructure includes the: Rocket silo \ Launch pad and Module assembler


Rockets will be T1-T3 and must be built on the ground.
Spaceships will be T4-T6 (possibly up to T8) and can only be built on space stations.


Rockets and Spaceships are modular; the main parameter that determines a spacecraft tier is the rocket \ spaceship core, which allows you to attach different modules to achieve different objectives.Each rocket and spacecraft will have a payload module slot available, which will accommodate either a landing module (for the first landing on a planet) or other modules to perform other functions (delivering a functional module to a space station). For rocket construction, modules are assembled in the Module assembler multiblock, and then shipped to the Rocket silo multiblock via a gantry, where they are then placed on the rocket structure.Gantries however will not be hard to assemble on the flight to move big rocket parts from multiblock to multiblock. (The gantry looks like a monorail, along which modules attached to a trolley on top will move) Some in-dev screenshot  


The rocket core will be available for crafting as soon as you have the necessary materials for this, without prior research. Most of the main modules will also not require any additional research and will be opened as soon as new crafts or technologies are discovered within the GTNH progression. A research outpost system is proposed, which will allow you to complete certain quests on planets and receive bonuses or open certain crafts. This system can also open some unique modules. Unique research in space can also unlock specific modules. (It will be explained in detail in the chapter on space travel)


The first rocket will be available at the end of the HV, as in the standard GC progression. It will consist of a rocket core, a payload module slot, and possible slots for additional modules that will not participate directly in the flight


Basic parameters of the rocket
- Radiation (or what you might call accumulated damage)
is a zero-based scale that fills with spaceflight time. This scale is designed to determine the amount of time we can spend in space.
- Fuel this scale means how much time we can accelerate in a certain direction, it is spent on any direct movements with the main engine
- Energy, this scale determines how much we can spend on active and passive abilities that consume electricity

We also have 2 parameters that affect the minigame which are set only at the start
- Mass, a parameter denoting the total mass of all modules and fuel on a ship, can change dynamically during flight with fuel consumption, but the mass parameter does not depend on usual resources or liquids carried on a rocket/ship
- Speed ​​this parameter means the speed of ejection of the moving body into space, over time during the decrease in mass your acceleration may increase, but the basic speed parameter is not changed


The rocket tier (rocket core tier) determines the number and tier of modules you can install on the rocket to reach a particular planet. The rocket core determines the base amount of fuel and the rocket's speed. It also has its own mass parameter (Spaceships will be treated with a different logic, but similar in some sense).
The amount of radiation (durability) is always fixed, but we can change the speed of its accumulation using different modules
The amount of energy will depend on the tier of the Command module. Energy generation on any spacecraft will only be possible on spaceships; on rockets, only a battery is assumed. It is possible to install a T1 manned module on a T3 rocket if we need to reduce mass and if we don't require a large amount of energy for flight


A detailed description of the modules and minigames can be found in the space travel chapter


Liftoff:
A major issue with the current space mods in GTNH is that they were designed without the idea of the Personal Dimension, which most GTNH players use as a base as soon as it is unlockable. To fix this, rockets which take off in a personal dimension will have that dimension saved as their “overworld” configuration, so no more crash-landing in the overworld and having to find your portal. Viridis, the homeworld, will just be in code your personal dimension if you want it to be that.



Rocket System (OLD VERSION, WILL BE DEPRECATED)
To launch rockets, players need to build proper infrastructure that will handle the launch. This  infrastructure includes the: Rocket silo, Module assembler, and Fuel station.


Rockets are modular. They consist of parts such as Fuel tanks, Engines, Command modules, Payload options, and communication equipment. For rocket construction, modules are assembled in the Module assembler multiblock, and then shipped to the Rocket silo multiblock via a gantry, where they are then placed on the rocket structure.  Modules, as well as the finished rockets, will no longer be pickupable items. Gantries however will not be hard to assemble on the flight to move big rocket parts from multiblock to multiblock. (Imagine, a chain with a rocket part mounted on it, and the chain gets fed between two singleblock machines, as it moves, the rocket part travels)


Modules are gradually unlocked via rocket testing, a new mechanic to progress. This will be done in a form of tech tree, where at different game stages different launch options will be given to test new ideas, to unlock parts. Each launch in lore, gains you knowledge on the rocketry systems you're testing, and will unlock the new modules. This encourages the player to build many rocket prototypes, instead of just getting into the first rocket they build. Each starting testing rocket will be cheaper though, to ease the material cost of rocketry early game.


The first rocket will be accessible in early MV now. (being only an atmospheric flight test to extract some science), and will serve as an introduction to the module tiering and the rocketry game mechanic. Doing these very simple launches will then open the doors to the next rocket options, which will be available in 
later tiers. This is done to make the jump from starting to build rockets, to needing to be going back and forth between the moon in EV less jarring, as now many more rockets will need to be tested before your first crewed lunar flight.


Given how the new rockets are modular, there will no longer be fixed tiers for every rocket. Instead, once a rocket is built, it will be placed into a tier based on its ∆v, and that will be used to determine which planets and moons it can get to. Therefore with more advanced technology, it gets easier every time to build lower tier rockets, because you get better and better modules to work with. Ontier rockets though, will require some planning in the rocket silo multiblock where the modules are selected in order to get the correct ∆v for the mission. Estimated ∆v will be shown in the editor however, so this functions as a small simple puzzle.


  



Rockets have payload containers at the top, where crew cabins, landers, satellites, or other payloads (like space station modules) can be put.


The bottom of the rocket, booster stages, will be made using module stacking in the rocket assembler.


Rocket Modules / Upgrades:
* Pilot Modules - includes Fins, the Nose Cones, and the Control Computer (upgrades increase fuel efficiency on launch, where most fuel is used, and upgrades allow you to automate travel to planets you’ve been before at maximum calculated fuel efficiency)
* (MIGHT BE REMOVED LATER) Shields (upgrades increase the ‘durability’ of the rocket, allowing it to move through higher-tiered systems and planets. If durability is reduced to zero, the rocket will break and the player may have to find materials to patch it up enough to fly back to their base)
* Fuel Tank (upgrades increase overall fuel storage)
* Landers (upgrades increase durability of the lander itself, loses durability on landing and will drop a destroyed version of itself if durability is reduced to zero)
* Boosters (increase speed of the rocket in exchange for fuel efficiency, upgrades increase maximum speed, used mostly during launch)
* Thrusters (upgrades increase maneuverability of the rocket and fuel efficiency while doing so)
* Rocket Engines (upgrades increase the tier of allowed rocket fuel and engine stats)
* Life Control (upgrades allow for increased storage of air on the ship, allowing for longer travel)


Rocket Tiering:
T1 Rocket: HV Tier
* Targets: Theia
* Launchpad Size: 5x5
* Rocket Size: 4x9
T2 Rocket: EV Tier
* Targets: Hemateria, Anamnesis, Tenebrae
* Launchpad Size: 5x5
* Rocket Size: 4x10
T3 Rocket: IV-LuV Tier
* Targets: Asteroid Belt, Egora System
* Launchpad Size: 7x7
* Rocket Size: 6x12
T4 Rocket: LuV-ZPM Tier
* Targets: Pleura
* Launchpad Size: 7x7
* Rocket Size: 6x15
T5 Rocket: ZPM-UV Tier
* Targets: Mirage, Perihelia
* Launchpad Size: 9x9
* Rocket Size: 8x20
T6 Rocket: UHV Tier
* Targets: Ataraxia
* Launchpad Size: 9x9
* Rocket Size: 8x25


Rocket Silo multiblocks should need to be upgraded every other rocket tier.
Space travel
Space travelling:
Galaxia wants to fill the space between unique, detailed planets with equally unique, detailed space, because space cannot be invaded without space itself.
To achieve this, a new space minigame system, A Fun Playable Game (AFPG) , is being introduced.


This minigame should fill the previously missing space of travel between planets. We are confident that we can create a minigame that will not become boring with constant monotonous actions (Hello, Thaumcraft) and can provide fun for the players who will play it. The system will be created with the idea that some players do not want to immerse themselves in a minigame, so there will be possibly more resource-intensive, but less stressful ways to complete it.


To begin with, it is worth familiarizing yourself with the basic parameters and terms that will be used during a space flight or preparation for it.


we will have 3 active scales that the player will see and that will directly interact with the game

- Radiation (or what you might call accumulated damage)
is a zero-based scale that fills with spaceflight time. This scale is designed to determine the amount of time we can spend in space.
- Fuel this scale means how much time we can accelerate in a certain direction, it is spent on any direct movements with the main engine
- Energy, this scale determines how much we can spend on active and passive abilities that consume electricity

We also have 2 parameters that affect the minigame which are set only at the start
- Mass, a parameter denoting the total mass of all modules and fuel on a ship, can change dynamically during flight with fuel consumption, but the mass parameter does not depend on usual resources or liquids carried on a rocket/ship
- Speed ​​this parameter means the speed of ejection of the moving body into space, over time during the decrease in mass your acceleration may increase, but the basic speed parameter is not changed


There will be two options for launching the minigame.
Either you can launch a test flight with infinite respawn attempts. After successfully completing the test flight, you can record this flight and upload it to the rocket's flight plan. Then, board the rocket and start the countdown. The rocket will enter orbit and begin moving according to the pre-set plan (you can skip this part, as you've already completed the minigame)
In a flight simulation, you can create any route that suits you. You can fly from one planet to another, dock with a station there, refuel, then fly to another planet, land on the planet, pick up resources, take off, fly back and land, and all this in a single test flight cycle (I really wanted, and I will try to implement this, so that you could combine different flight plans and combine them, By Ya9yu)
The second option is to launch the rocket without a pre-set flight plan and launch the flight yourself, on your first try. If you're brave enough to do this, go for it.
The same flight plan can be copied to many different rockets to automate their logistics.

The minigame will be a 2D rocket game that can control its flight, accelerating in one direction or another and maintaining a constant speed. To reach a planet, you first need to accelerate in its direction, reach it, and then reduce your speed to an acceptable level, allowing you to enter orbit. Each planet will have its own gravitational field, within which the planet's gravity will act. We can use some kind of gravity assist maneuvers, but don't rely too much on them. If we slow down to the required speed within the planet's gravitational field, we'll enter orbit and be able to interact with the planet, either by building a space station, launching a satellite, or landing on the planet.

To land on a plant for the first time, you need a landing module as a payload. After landing, it's best to first build a launch pad and do whatever you want on the planet. Then, using the landing module (or launching pad), you can re-run a flight simulation upon returning to your home planet. Then, board the landing module and launch into orbit. Where you'll automatically dock with your rocket. Then, you can either fly back according to a pre-planned flight plan, or you can try your luck and courage and fly independently. Upon returning, the rocket remembers the two-way path and can continue it indefinitely as long as it has enough fuel and necessary supplies. When landing on a planet that already has a launch pad, you first choose which launch pad to land the rocket on, or you can choose (select a free one). You land on the planet with the entire rocket. You can choose not to have a landing module as a payload, but use the payload module for something else, for example, to install a storage module in it to transfer resources automatically

Now let's move on to the second part of flights to other planets, why do we need these fancy parameters like radiation or energy (we seem to have figured out the fuel issue, we spend it on acceleration or deceleration)
This is where the main limiting mechanic of the space minigame comes in, TIME

When flying to the moon, we may not have filled half the radiation scale by the time we got there, but when flying to Mard\Hemateria, we now need to think about how to protect ourselves from radiation during such a long flight, and this is where the module mechanics discussed in the previous chapter come into play.

For a flight to Mars, I'd like to introduce two main modules that can be used.


The first module is the electromagnetic shielding module. This is an active module that must be activated by pressing the active ability button during flight. It will significantly reduce any radiation affecting the ship, but it will consume energy while active. The electromagnetic shielding module is also relatively lightweight, so you get a good acceleration boost when it's attached to the ship, making reaching Mars possible using this module (remember this; there will be many other interesting things to come with this module).


The second module is the heavy radiation shielding module. It's quite expensive and weighs quite a lot, which can reduce your acceleration and make the rocket rather sluggish to control. However, it doesn't require any energy and reduces passive radiation exposure in outer space, so even at a slow speed, you can confidently reach Mars without worrying about anything other than accelerating and decelerating.


So now we can get a glimpse of what the system looks like, right?
There are active and passive abilities, which adds complexity and interest to understanding it. There are both direct methods for simply flying from one planet to another without a care as well as using active abilities, and it's also possible to perform gravity assist maneuvers (I'll shake the hand of anyone who learns to use this intentionally, not accidentally)





Space travelling (OLD VERSION, WILL BE DEPRECATED)


Once the rocket is launched, it can be piloted in two different ways: 


Manually, by guiding its ascent and orbital dynamics once in space to get where you need to go –  ( using a new 2d minigame system for planning orbital dynamics, and planning interplanetary transfers and landings ) 


Automatically, where this same 2d minigame system is used as a simulation, while still landed to plan a mission beforehand. This can be used to avoid errors in manual flight, or to automate rocket launches. Players only need to encode the trajectory once and the computer will be piloted on its own forever when the conditions are satisfied. Conditions can allow for complex item transportation, for example only start the flight when the cargo module is empty (like factorio trains and platforms)


Orbital GUI and travelling in rockets


Most, if not all space travel will be done using the Orbital GUI. (Meaning there will be no 3d representation of you when you're in deep space, only when you're docking to a space station, or landing/taking off) 


This functions essentially like a 2d minigame of orbital dynamics. Once you get to orbit (which will be done automatically for you once you launch a rocket from your ground planet) you will have automatically entered a low circular orbit around your planet. From here, you can click on your orbit line anywhere you wish, and make a maneuver. 


This is kind of like an XYZ burn direction indicator for planning where you want to go.




  

	  

	  
  

	

But here you only have X and Z to burn in, there is no Y axis as its 2d. (Y axis is purple triangle on the kerbal space program gui example)


You drag each circle to pick how far you want to go in each direction, and then the OGUI will show you a preview of what that orbit will look like, and how much deltaV it will take. Your trajectory kind of looks more and more like a stretched out oval on the GUI depending on how fast you're going. Pick where the oval is stretched to, and you get to intersect with a planet or moon. Easy enough! 


Clicking [ TIMEWARP ] now after you've decided where you want to go in your planner, will fast forward your satellite to that place, and change your orbit automatically with a small animation of it changing to be the new one you decided on, and subtract the deltaV you used up to do it from your rocket. This is fundamentally how you travel in the new system.


 If your intended orbit encounters a moon or planet, it will show how close you are intersecting to it in the future, and when you get there, you will be able to make a new node and close your orbit around the destination moon or planet. From there you can land with your remaining deltaV, if it calculates you have enough deltaV to get back. 


(somewhere in the game there will be a flowchart of how much deltaV it requires to get from each planet back to Viridis in order to do this.) This will prevent you from landing somewhere if you don't have enough fuel, unless you click [ OVERRIDE COMPUTER ]. (which is not recommended in any case, but will be included anyways for player options)




Traveling to and from stations:


Transfer of items between your current station and the planet or moon orbiting it is free, if you're returning items back to the planet from the station. Using the station's new feature, the High Accuracy Mechanised Mass Entry Rail ( HAMMER ) Railgun. Using this, shipments can be delivered to the planets via electricity only, which can easily be produced in space using solar panels. Due to the thick atmosphere though, HAMMER cannot be used on the planet's surface. (as the packages would burn up) instead, it serves as the final logistics node in space. When hammer beams down packages from the space station, you get to pick which block it lands on on earth.


Transfer of items between your current station and another station is not free. It requires a shipment satellite, which is a type of payload launched from a planet's surface that is designed specifically for shipping items between stations, cheaply. It has very high efficiency thrusters, is very light, and many can be launched from a planet at a time.  This will be a type of payload module, so it will gradually gain efficiency and speed as you tier up. 

An alternative for transporting resources between space stations would be super-large ships that can transport large quantities of resources in a single run, or even several payload modules, which would be ideal for building space stations in orbit around other stellar bodies.
Such super-large ships can only be built in orbit using a module assembler and a rocket assembler in space stations.




Space stations
Space stations:
Space stations are the primary method of storing resources in orbit, producing resources in low gravity, and facilitating shipments between planets. Once in orbit, you can dock with that planet's space stations (which act like mini factories and living quarters in space) and move your shipment of items or fluids there. 


The space station's component parts, or nodules, will be divided into two different types.
Shells empty spaces that can be used for logistics, for automating certain processes using single-unit modules, and for various other purposes
Shells can be constructed using the space station's shell, which will be made of inexpensive materials and can be stored like a regular items


Functional nodules, which are non-walkable parts of the space station and can only be interacted with via a specific interface, will need to be manufactured on a module assembler on the ground. These nodules are required to be launched manually or automatically from planetside rockets. Depending on the size of the station, multiple launches may be needed for large space assemblies. Later on, automation options for placing a “template space station” to build off of later will be available, and rockets will be able to be automatically requested from the chosen planet. 


Space stations will have a pressurization and depressurization system
In short, if a station outer block is broken and the vacuum is connected to the air inside the station, the station's operation in that nodule will cease until the damage is repaired and the room is resealed
Also, any singleblocks and other functional blocks must operate only inside the pressurized station; they will not operate outside the space station (or will operate with extremely low efficiency).

Space stations will be able to store large quantities of fluid in tanks, manufacture items in low gravity, and refuel satellites that dock to it. (Docking will be automatic for all game stages, and won't be frustrating)


To build a space station, it is necessary to launch a space station hub in a payload module into orbit and place the hub there. Shells of any size will be available for construction immediately, only resources will be required. Most functional nodes will be available for construction as soon as their production in the module assembler becomes possible. Special ones may require additional study through research outposts or space research.


The space station hub is basically a big connection point for everything else in your station, with 6 docking ports at the side to connect functional nodules, shells and rockets for docking. By default, the space station hub does not come with a built-in HAMMER nodule the (railgun package delivery system) that needs to be launched in pieces from a couple rockets from Viridis and then assembled as a multiblock from its many parts. It is quite big, and quite costly in raw materials (eg, coils, rails, and capacitors / alternate large energy storage).

Spacecraft dock with a docking port (this animation will trigger automatically once you load the space station, and click on the port you want to dock to in third person). The can then offload all their items into the space station hub's large default storage box and eject the player into the hub's main oxygen and life support room (basically the main room). On one side of the space station nodule can be installed an airlock, which will be able to allow the player to exit in a spacesuit for space walks, or for you to push your friends out there without a space suit for the memes.  (not a good idea)


If you eject yourself into the space station's hub when docked, you will have a small room you can access inside the station that will have oxygen and light (as long as power is constantly supplied) via lights on the ceiling and walls, and a co2 recycler in the wall. This makes it technically possible to be on the space station without a spacesuit, but this is not recommended


Space Station Modules:
* Hub (the central module, which is a six-sided cross with the lower part specific to the planetary attachment module and the upper part reserved for the non-removable docking port)
* Shells that consist of:
   * General Living Quarters (large empty rooms with space to place blocks and machines, square or octagon shaped. (octagons 45 degree angles would have small adjusters on the room connector parts to the next possible room, to rebind it to the 90 degree only grid))
   * Hallways (smaller, cheaper connecting modules, L shape, T shape, I shape, + shape) Windowed Variants of the hallways
   * Airlocks (for entering and exiting the Space Station)
   * Docking ports
* Functional Nodules that consist of:
   * Module Assembler (addon to the space station that allows you to craft modules right on the station that can be crafted at about ZPM tier)
   * Energy production module (an external or internal module that takes power into the system, like dollar arrays, nuclear reactor, fusion reactor)
   * Planetary attachment module (HAMMER, Space Elevator Clutch Module, Space Siphon)
   * Space multiblocks


Room and corridor modules concept: (colors are procedural) 


  



Space elevator integration:


The Space Assembler Module, Space Mining Module, and Space Pumping Module (reworking ideas are underway) are essentially the same modules, except that each module on the ground will now be tied to a specific nodule on the space station, and the bulk of the cost will be shifted from the controllers to the modules on the space station that need to be shipped and installed.


The space elevator can no longer operate without a space station. This shouldn't affect its core functions (possibly only the space pump module may change). New modules will now be added to the space station.


1) Similar to H.A.M.M.E.R. Railgun and resource reception station, which has exactly the same functionality as the space mining module
The railgun sends drones to asteroids, where they mine resources and return them to the nodule
2) Space assembler module, which is installed as a module on the space station and directly connected to the space assembler module on ground.
3) Space pumping module (WIP)


Space stations: (OLD VERSION, WILL BE DERPECATED)


Space stations are the primary method of storing resources in orbit, producing resources in low gravity, and facilitating shipments between planets. In the new module system, engines will have to be selected based on which stage of the rocket they are being used on (Atmospheric, Interplanetary, or Orbital insertions). 


As some engines will provide very high efficiency in space (think, xenon ion engines) but wont have enough thrust to get off the ground, it is more cost efficient to only use base launched rockets to get to orbit around the planet. Once in orbit, you can dock with that planet's space stations (which act like mini factories and living quarters in space) and move your shipment of items or fluids there. 


In order to build a space station, the parts required need to be launched manually or automatically from planetside rockets. Depending on the size of the station, multiple launches may be needed for large space assemblies. Later on, automation options for placing a “template space station” to build off of later will be available, and rockets will be able to be automatically requested from earth or neighboring planets. 


Space stations will be able to store large quantities of fluid in tanks, manufacture items in low gravity, and refuel satellites that dock to it. (Docking will be automatic for all game stages, and won't be frustrating)


Space stations will not be immediately unlockable. They will need their payload modules researched the same as every other module.


Another kind of satellite that could be available is a scanning satellite, which allows you to map out the terrain and prospect for ores in a region before you land on the planet, allowing for quicker setup of resource extraction. 




Platform Management and assembly:
After launching enough rockets and unlocking the space station core modules, the player can launch a space station core around Viridis (or any other unlocked planet or moon). This will create a space station structure in orbit, which can be later improved upon with further shipments. Eventually, it will be able to be a complete factory in space receiving and delivering shipments interplanetary, and gregtech machines and multiblocks will be able to be placed on and inside its corridors. 


The space station hub is basically a big connection point for everything else in your station, with 6 docking ports at the side to connect multiblocks, machines, corridors, and rockets for docking (e.g. crew capsule). By default, the space station hub does not come with a built-in HAMMER module (see Traveling to and from stations: for details on the HAMMER railgun package delivery system) That needs to be launched in pieces from a couple rockets from Viridis and then assembled as a multiblock from its many parts. It is quite big, and quite costly in raw materials (eg, coils, rails, and capacitors / alternate large energy storage).


Crew capsules dock with a docking port (this animation will trigger automatically once you load the space station, and click on the port you want to dock to in third person). The can then offload all their items into the space station hub's large default storage box and eject the player into the hub's main oxygen and life support room (basically the main room). On one side of the space station core can be installed an airlock, which will be able to allow the player to exit in a spacesuit for space walks, or for you to push your friends out there without a space suit for the memes.  (not a good idea)


The crew pod will have small solid rocket motors embedded in the bottom of it to allow for it to deorbit without an engine, and without HAMMER being installed yet. Later on, you can use HAMMER to deorbit yourself, but due to the rapid acceleration needed for the railgun to work, you take large G-force damage to your health if you go through with this option (HAMMER is meant for item / package delivery to a specific spot in your base). This still works for people though if you have high enough health, although wearing armor does not provide resistance to G-damage so keep that in mind. Some health leveling, or resistance effect is recommended. Check for something in one of the magic mods to deal with this, or just use the slow solid rocket deorbiters.


If you eject yourself into the space station's hub when docked, you will have a small room you can access inside the station that will have oxygen and light (as long as power is constantly supplied) via lights on the ceiling and walls, and a co2 recycler in the wall. This makes it technically possible to be on the space station without a spacesuit, but this is not recommended. 


Space Station Modules:
* Hub (the central module, which is a six-sided cross with the lower part specific to the planetary attachment module and the upper part reserved for the non-removable docking port)
* General Living Quarters (large empty rooms with space to place blocks and machines, square or octagon shaped. (octagons 45 degree angles would have small adjusters on the room connector parts to the next possible room, to rebind it to the 90 degree only grid))
* Hallways (smaller, cheaper connecting modules, L shape, T shape, I shape, + shape)
   * Windowed Variants of the hallways
* Airlocks (for entering and exiting the Space Station)
* Docking ports
* Module Assembler (addon to the space station that allows you to craft modules right on the station that can be crafted at about ZPM tier)
* Energy production module (an external or internal module that takes power into the system, like dollar arrays, nuclear reactor, fusion reactor)
* Planetary attachment module (HAMMER, Space Elevator Clutch Module, Space Siphon)




Room and corridor GUI modules: (colors are procedural)


  







Space elevator integration:
The Space Assembler Module, Space Mining Module, and Space Pumping Module (reworking ideas are underway) are essentially the same modules, except that each module on the ground will now be tied to a specific module on the space station, and the bulk of the cost will be shifted from the controllers to the modules on the space station that need to be shipped and installed.


The space elevator can no longer operate without a space station. This shouldn't affect its core functions (possibly only the space pump module may change). New modules will now be added to the space station.


1) H.A.M.M.E.R. Railgun and resource reception station, which has exactly the same functionality as the space mining module
The railgun sends drones to asteroids, where they mine resources, return, and return them to the module
2) Space assembler module, which is installed as a module on the space station and directly connected to the space assembler module on ground.
3) Space pumping module (WIP)



Liftoff:
A major issue with the current space mods in GTNH is that they were designed without the idea of the Personal Dimension, which most GTNH players use as a base as soon as it is unlockable. To fix this, rockets which take off in a personal dimension will have that dimension saved as their “overworld” configuration, so no more crash-landing in the overworld and having to find your portal. Viridis, the homeworld, will just be in code your personal dimension if you want it to be that.


The Vael System
          The Vael System
The new solar system and surrounding areas in Galaxia are eerily similar to our own, and yet remarkably different. Space is so much more full than we once believed it to be.


The “Overworld,” as we all call it, is merely a planet known to outsiders as “Viridis.” Its lush green fields and varied biomes are merely a microcosm of all that is out there. Below is the full scope and description of the Vael System.


* Vael, our Sun.
   * Yellow Star


* Perihelia (Mercury)
   * Distance from Earth: 8 light-minutes
   * A molten planet so close to the sun it fills up the morning sky. The entire surface is burnt into ash, rivers of lava flow so hot they turn into plasma as Vael’s gravity rips the molten rock into the planet’s burning irradiant atmosphere, turning the sky a bright shade of red at all times, and a deep maroon at night. It seems that at some point, many thousands of years ago, an ambitious civilization once tried to industrialize the planet’s mineral-rich lithology, and the aging ruins of rustic infrastructure dot the landscape, made of some mysterious, incredible material. One has to wonder what drove the former architects of this planet away.
* Tenebrae (Venus)
   * Distance from Earth: 70,000,000 km (average)
   * A volcanically active and sulfuric planet just within the habitable zone of Vael, the planet is marked by deserts of endless pyritic sand and white-hot hydrothermal lakes of something resembling water. Fumaroles and geysers dot the surface, funneling the planet’s hostile nature out of whatever edifice it can. Tenebrae’s atmosphere is incredibly acidic, with a pH of 2, so acidic and oxygen-poor that even water denatures into hydrogen, and many chemical reactions occur differently than they do on Viridis.
* Viridis (The Overworld)
   * Theia (The Moon)
      * Gravity: 0.1g. Atmosphere: 0 atm. Temperature: 130°K. 
      * Distance from Earth: 3 light-seconds, 384,400 km
      * What we once believed to be of our moon, a cold, dead, rock in the expanse of space, may have been wrong. Even upon landing on the surface, the Theia’s mercurial sheen and pale pink pearlescence suggest something more magical about this place.
* Hemateria (Mars)
   * Distance from Earth: 140,000,000 km (average)
   * The red planet is named after the rust that has taken over its surface. Hemateria once resembled Viridis, but time and possibly other forces have driven the planet into a state of extinction. I wonder if there is any evidence of ancient extraterrestrial life on this planet?
   * Anamnesis
      * Hemateria’s sole satellite is a captured asteroid from the nearby asteroid belt, appearing like every other asteroid on the surface. Anamnesis was long neglected because of this fact, but beneath the surface is a massive, abandoned spaceship, now defunct and destroyed, hiding something incredibly dangerous: the Ctenocerum, a mysterious, rapidly evolving biological substance far beyond human knowledge, and seemingly the destroyer of the former owners of the Anamnesis spaceship. Could the Ctenocerum be the secret to interstellar travel?
* The Asteroid Belt
   * The new asteroid belt, in between the orbits of Hemateria and Egora acts as the great barrier between the inner parts of the Vael system and the final frontier way out there. The asteroid belt is a treasure trove of rare resources, including the elusive Naquadah.
* Egora (Jupiter?)
   * Distance from Earth: 714,000,000 km
   * What was once believed to merely be a gas giant planet outside of the asteroid belt is actually a weakly glowing brown dwarf star, providing a weak source of light and heat to its surrounding moons.
   * Ambergris
      * The Petrified Planet, Ambergris is covered in mountains of amber and petrified wood, with valleys of dead, frozen carbon filling the spaces in between, creating a stark yet beautiful contrast. This planet was once the home to massive, atmosphere-breaching trees, that are now broken and preserved into remnants of their past self.
   * Ediacara
      * A planet with a frozen, icy surface, and a liquid ocean beneath. Scientists have long thought of Ediacara as the planet with the greatest chance of life in the Vael system, and beneath the surface, they would be correct. Life in Ediacara looks identical to the beginning of Viridis’s first life, so it is named after the period in which this occurred.
   * Mykelia
      * A planet that went undetected for centuries is hidden within the storms and dust clouds of Egora’s wind. This planet is so close to a strong heat source that advanced forms of life are able to propagate, in the case of Mykelia, the planet is fully overrun by gigantic fungi that seem to have a will of their own.
* Pleura (Saturn)
   * Distance from Earth: 1.4 billion km (average)
   * This huge spins so rapidly, massive storms form across its surface, tearing up the landscape, and launching shards of ice and crust into the stratosphere, where it all coalesces into a beautiful and dangerous ring system.
* Timeland System (Uranus and Neptune)
   * Distance from Earth: 2.2 billion km (average)
   * Two massive gas giants in the outer Vael system, planets orbiting each other, connected by a mysterious and destructive gravitational anomaly powerful enough to cause time dilations. The two planets spin around at rapid speeds, often exchanging pieces of their atmosphere with each other. 
* Ataraxia (Pluto)
   * Distance from Earth: 5 billion km (average)
   * The most distant planet in the Vael system, Ataraxia is a small, peaceful, cold planet just at the edge of the system. Nothing sits between you and the cold, vast, lonely cosmos after here, but yet the planet seems oddly peaceful, perhaps far too so. The sky is a pale, dark pink due to the atmosphere of mostly noble gases. Staring out into the abyss, you wonder what became of the civilizations behind the forges on Perihelia and the spaceship on Anamnesis.


Lore
Many hundreds of years before the players appeared on Viridis, the Vael system was occupied by a galaxy-spanning civilization known as the Celestian people. They harnessed the power of the Eternity Drive and Cosmic Circuitry to travel across the galaxy at near light speeds, but their greed left them wanting more. Despite their homeworld, Virantis, being many light-years away from Viridis, they sent one of their grandest motherships, a moon-sized device known as Anamnesis, into orbit around Viridis and send expeditions across the system to discover its planets and secrets. Perihelia became their main target, as the planet was loaded with rare and useful heavy mineral resources due to its distance to the solar center. They also became very interested in Mykelia, a planet with hyper-intelligent fungal life creating a hivemind, a sort of living planet of raw intelligence with no way to defend itself. The Celestians took a literal chunk out of the planet itself and brought it back to their spaceship to study and experiment on. Initial results were even more promising than they had hoped for. The hivemind, when exposed to the Eternity Drive, enhanced and optimized it to its greatest point, where it found a way to physically decrease the amount of distance needed to travel from point A to point B. This incredible biological power became known as the Ctenocelestian, and the Celestians spread its influence across the galaxy, opening up wormholes through a pocket dimension across many of the Celestians’ conquered systems. However, the Ctenocelestian soon began moving of its own accord, creating a host planet at the center of the wormhole dimension. From there, the Ctenocelestian suddenly gained control over most of Anamnesis, and it then became immediately clear that this was a war that the Celestians could not win. With so much of their infrastructure now reliant on the Ctenocelestian, they had no choice but to destroy the portal from their side, closing them off from their illustrious empire. Back on Anamnesis, the remaining Celestians feared that the Ctenocerum would escape and infiltrate Viridis, so they sent out a final ship to bomb and destroy the Ctenocelestian portal from their end, and ferry the ship around the dead planet Hemateria where it dislodged the planet’s existing moons, Phobos and Deimos, out of orbit, causing them to crash into the planet. Kinetic energy weapons were used to push Perihelia to a mere 0.05 AU from Vael, sentencing it to death in the hopes that the Ctenocelestian would not be able to use its technology. The final Celestian ship did its job, destroying the portal, but was fatally damaged in the process. Bits of it crashed down to Viridis, where some villages formed around the pieces of alien debris, while the majority of the ship floated endlessly through space for years until it crashed into the surface of the rogue planet Ataraxia, which had just recently been captured by the Vael system, its last message being a warning to anyone who might find Anamnesis. Over the past thousands of years, the Ctenocerum has forcefully devolved into a simple, single-celled organism in order to preserve itself and lengthen its lifespan if it were to ever be rediscovered.


OLD STUFF: DEPRECATED IN FAVOR OF STUFF ABOVE
A Potential New System:


Overview:


Galaxia has its own design of the solar system, which is somewhat analogous to our real world solar system, but with some tweaks and spicing up to make it  more fun for gameplay.


In order to make the solar system more present in players minds, we will have a new renderer for planets and moons during the night, so on clear nights you will be able to look up and see the planets, moons, and other stars above you. They’ll look similar in size to the vanilla stars mostly, but will have different colors to distinguish them from the background. We will also change the vanilla stars slightly to be more realistic. (More color variation, grouping, and small galaxies in the distance.)


The reason the solar system is being replaced is more for gameplay design. It would be odd to have a real life planet that we’ve studied suddenly be given awakened draconium ore or infinity ore. Having a custom planetary system for the home solar system fixes this, and also allows for more feature variety in Galaxia. Lots of the current new planets in the Vael star system are actually still analogous to the real planets. Calx is the moon, and it is referred to as the moon. 


The overworld's name is Viridis. Viridis means “green," "flourishing," or "blooming" in Latin. This makes more conceptual sense than calling the overworld something to do with blue (like blue marble), as technically the overworld in NH does not have oceans like Earth does. 


Viridis has two moons, but only one big noticeable one:


Calx is the most recognisable moon. It is very large in the night sky, and serves as minecrafts default moon. In essence, it functions like earth's moon did in Galacticraft. It is tidally locked to Viridis, and it has the important resources that are needed for EV on it.




Calx, the moon in the sky as you've always known it




  

	

Woah, It's Vane in the night sky! So pretty. Might need to zoom in though to spot!


  

	

The galaxy is beautiful. On clear nights, there's a lot to see! You can zoom in and see different colored stars, and even some nebulae. 




  

	

	

	

	

	

Calx’s name origin. It looks kinda like the color of metallic oxides! Maybe this hints at the presence of ores here? No idea! Go there and find out :)
	  

	

Lem is the second moon of Viridis. Lem is smaller, being only around ¼ the size of Calx. It is also very distant from Viridis, being near the edge of its orbital SOI. Lem doesn't have any interesting new resources, but it is rich in iron and silicon dioxide, and is very easy to return from. Instead, Lem serves as one of the best places in the solar system to place communication relays back to Viridis. At Lem’s lagrange points (which will just be selectable waypoints to “place” your satellite at in the 2d orbits minigame) satellites will remain in place forever, meaning you don't have to worry about the planet or moon occasionally blocking signal back to Viridis. They have slightly different orbital paths, so they don't really cover each other up.


  

Here's Lem in the sky on widescreen! Not very visible compared to Calx, the main moon, but it's still a tiny spot! It's very small and very far away. Maybe if you get a cool telescope you can take a better look?


Lem can be seen with enough searching by the naked eye in the night sky, but may not be immediately identified as a moon due to its slight pale green color, and very small size. It also orbits on a slightly different path to Calx, making it potentially not very noticeable in the sky compared to the new prettier stars at first. Whenever you unlock your orbital GUI however, Lem will be instantly visible on the orbital view as a moon. Looking up at the night sky however, only Calx will be visible as the default moon you have always seen. This specifically is not getting changed. The  moon's orbit now will however be slightly independent from the sun now! Given that the solar system now exists, and the overworld is no longer the center of the system (the star Vael is) you might occasionally be able to see the moon slightly on the horizon during the day, faintly.


Something more?


Viridis has one more secret for the players, albeit a much smaller one. Asteroids and asteroid mining will be a key resource gathering feature in Galaxia, which will be able to be automated with satellites from space stations. To serve as an introduction to this system, Viridis has its own captured asteroid. It does not have a name, and is not immediately discoverable when opening the orbital GUI for the first time, unlike Calx and Lem. Instead, Viridis’s asteroid becomes visible once you place down a telescope or big communication sensor on your viridis space station (which will inevitably happen anyways at some point). It will show up as ( ??? ) and you will be prompted to give it a custom name, and it will show up as “a small asteroid named ‘whatever you named it’ ”. 


Viridis’s asteroid is part of an optional mission in the tech progression, where you can fly a satellite to the asteroid and attach a prototype grabber to it. (This happens in the 2d orbital minigame) Completing this mission unlocks the asteroid grabbing module, which lets you in future collect small asteroid chunks. This serves as a kind of quest to unlock asteroid mining, and is very easy to complete given how close the asteroid is to Viridis compared to others, and how predictable its orbit is.


Viridis’s asteroid is sadly not very useful. It's a mix of carbon and methane ice, and can be broken off into chunks if the player wishes and be mined back to your base, but is probably more useful in space due to its large size compared to your space station for example, and how carbon, methane, and water are somewhat rare in space. It would make more sense to ship it to your station in chunks mined, and then use it in chemistry as a source of water, carbon, oxygen, and hydrogen.


The new VAEL star system (you start on viridis, the overworld)


* VAEL - Star


   * Spire                [MELTY, HOT, RESOURCE RICH] – lategame challenge


   * Icarus                [ROCKY, HOT, 0.0ATM] – venus but with flair
      * Rik


   * Hadrian        [ROCKY, SULFUROUS, 3ATM]
      * Tarv


   * Viridis                [LUSH, HABITABLE, 1ATM]         – overworld
      * Calx
      * Lem
      * Tutorial Asteroid


   * Dunia                [ROCKY, DUSTY, 0.25 ATM] – mars but with flair
      * Eta
      * Pol


   * Rogran        [ROCKY, METALIC, 0.0ATM]


   * Vane                [GAS GIANT, LIGHT BEIGE] – saturn but with flair
      * Large Rings
      * Moons


   * Orun                [GAS GIANT, LIGHT GREEN]
      * Moons


   * Merth                [GAS GIANT, MEDIUM PURPLE]
      * Moons


   * Tellumo        [GAS GIANT, MEDIUM BLUE]
      * Rings


   * Leron                [ROCKY, GEYSERS, ICY, 0.04ATM]


   * Kirth                [ROCKY, SMALL, FRACTURED]
      * Small Rings 
The old Sol star system from Galacticraft (you start on earth, the overworld)
* Sol - The Sun
   * Mercury
   * Venus
   * Earth
      * The Moon / Luna
   * Mars
      * Phobos
      * Deimos
   * Asteroid Belt
      * Ceres
   * Jupiter
      * Io
      * Europa
      * Callista
      * Ganymede
   * Saturn
      * Saturn’s Rings
      * Titan
      * Enceladus
   * Uranus
      * Titania
      * Oberon
   * Neptune
      * Triton
      * Proteus
   * Pluto
      * Eris
   * Kuiper Belt
   * Comets
extra nonsense:
To be written, I'm sleepy.
  
  



Interstellar Space
          Post-Vael Space
Travel:
Progression through the Ctenocelestian Wormhole reveals a few select locations, each with their own unique threats and resources that cause them to all be very high-tier locations.
Locations:
Eoctenus – T7, located directly within the Ctenocelestian Wormhole dimension.
        Gravity: 0.2g; Atmosphere: 0.4 atm; Temperature: 15°C
        Hazards: Extreme Ctenocelestian spore exposure, requires a more advanced version of the Wither Storm protection bauble, otherwise the Ctenocelestian will infect the player and parrot their corpse as a hostile entity which uses their equipment to fight the player if they come back for it.


Typhirus – T7, directly connected to the Ctenocelestian Wormhole.
        Lore: An offspring of Urygall was sent out through interstellar space, but met its untimely demise when it was caught in the orbit of a decaying black hole system, which drenched it in radiation, fully killing the planet.


Digita – T7, a wormhole portal connected to a defunct digital world once built inside of Virantis.
        Lore: Digita can provide a direct link to Virantis before T8, but it takes lots of effort to make it there. The simulated world exists within an AE2 digital pocket dimension, so any items can be brought in and out of the system. However, glitches and viruses have damaged the world, creating unique existential hazards. 


Miocaris – T7, a system of several gas giant planets connected to a wormhole portal.


Virantis System – T8: A small planetary system orbiting a blue supergiant, connected to the 
        Virantis – T8, located at the innermost planet of the system.
        Gravity: 1.8g; Atmosphere: 0.1 atm; Temperature: 65°C
        Hazards: Gargantuan chunks taken out of the planet have stripped the planet of most of its atmosphere.
        Lore: The former Celestian homeworld, a mix of massive, ruined cities, tall mountains, dead forests, and enormous, miles-deep cave systems leading into the molten core of the planet which leaks out through its many battle scars.


        Saigourian Belt – T8, located in the center of the system.
        Gravity: 0g; Atmosphere: 0 atm; Temperature: 70°K
        Lore: An asteroid belt between the planets of Virantis and Urygall that serves as a graveyard for thousands, possibly millions of starships destroyed in a galactic war between the two empires.


        Urygall – T8, located about 40 light minutes away from Virantis.
        Gravity: 3g; Atmosphere: 5 atm; Temperature: 10°C
        Lore: A planet comprised of the flesh of a dormant, but living organism known as the Urygan Superorganism. The planet’s surface teems with strange, alien life, and the features of the planet are formed of the flesh, blood, and organs of the superorganism. Urygall was once at war with Virantis, but went dormant after the war due to damage.


        Esperovsi – T8, a rogue planet located just outside the gravitational well of the Virantis System, 1 light-day away from the star. 
        Gravity: 5g; Atmosphere: 0.3 atm; Temperature: 1°K
        Hazards: The temperature on Esperovsi is so low that machines require special heating in order to function, and anything exposed to the atmosphere will instantly freeze. An entire war was once fought over the resources on this planet, which contains 


Septevirantis – T9, located far outside of the Ctenocelestian Wormhole’s reach in a distant star system.
        Gravity: 1.1g; Atmosphere: 1.5 atm; Temperature: 30°C
        Hazards: None
        Lore: The last bastion of the surviving Celestian civilization, planet-sized city far beyond its peak. While cities make up most of the planet, and contribute to its hazy, thick atmosphere, oceans, deserts, and a few forests still exist between the lines, though many of these are also industrialized.
Planets & Surfaces
Space worlds


New worlds to be determined, every planet from Galacticraft, Galaxyspace, and Amun-Ra will be redone or replaced and made better. Some features that were spread too thin between planets will be redone to be now part of a larger planet in feature scale. New terrain features to spice up each surface will be added!


Dungeons will not be included in galaxia, and most worlds will not have mobs. They may have plants and bacterial life, visualised as sludge blocks and plant life, but no mobs on most worlds. (Except for some! which you might need to watch out for… Keep your telescopes searching galaxia players, there might be small lifeforms on one of the planets!)


Asteroids
The Asteroid Belt is an optional but lucrative source of many materials, including Naquadah. 
Asteroid Ore: Instead of generating individual ores, asteroid cores are made up of conglomerations of the ore into a single block.


Asteroid Ore Configurations:
* Ferrous Core - Native Iron, Native Nickel, Meteoric Iron
* Vaporic Core - Native Copper, Cassiterite, Sphalerite, Galena
* Halogen Core - Halite, Sylvite, Fluorite, Caesium Iodide, Lithium Bromide
* Energetic Core - Lepidolite, Redstone, Cinnabar, Electrotine, Native Thorium
* Carbonic Core - Graphite, Diamond, Raw Silicon
* Theian Core - Bastnasite, Monazite, Meteoric Iron, Bauxite, Native Aluminium, Native Neodymium, Chromite, Ilmenite
* Hematerian Core - Uraninite, Desh*, Native Thorium, Tungstate, Scheelite, Native Plutonium
* Titanian Core - Native Titanium, Rutile, Ilmenite, Bauxite
* Auric Core - Native Gold, Native Silver, Quartz, Pyrolusite
* Metamorphic Core - Marble, Calcite, Quartzite, Lapis, Soapstone, Kyanite
* Infused Core - Aer, Ignis, Aqua, Terra, Ordo, Perditio Infused Stones
* Naquadrian Core - Naquadah, Draconium, Ardite, Enriched Naquadah
* Platlinian Core - Native Nickel, Native Platinum, Native Palladium, Native Osmium, Native Iridium
* Reenian Core - Monazite, Bastnasite, Native Neodymium, Rare Earth I, Rare Earth II, Rare Earth III
* Mysterious Core - Raw Mysterious Crystal




Progression


Progression:

Coming with Galaxia will be tiered systems, similarly to the existing tiering mechanics. Tier 1 rocket resources will be available on the Overworld, Tier 2 resources will be available in Tier 1 systems, and so on. The exception to this is the automated control computer, whose tier 1 components are only available using Tier 2 resources, and so on and so forth.


Tier 1 planets and resources will remain largely the same, as we want the Rocket to be similar in price to its Galacticraft equivalent, either more of the less valuable resources and less of the more valuable resources for crafting. The cost may change, but it won't be too difficult for the player.

The discovery of new modules and other parts will be mainly done by limiting the technological process and available resources on current tier, rather than through templates as is done in the current GC

With the research outpost system, we'll have the opportunity to create planet-specific technologies and production lines, as well as unlock unique modules if it possible and necessary


Each planet in Galaxia is unique and will contain unique technology lines and technologies, some of which can be used in Overworld, while others are exclusive to the planet. These new features aren't intended to disrupt the current tier system of the GTNH, but rather to provide a more interesting way to interact with planet-specific gameplay than simply installing a miner and killing a boss


Progressing through the Vael System
* The Moon / Theia is the only T1 planet, accessed during late HV tier. In addition to the titanium that you’ll need to progress on to Hemateria, you’ll need to collect Meteoric Iron through the processing of meteorites and tektites, which can be found on the rim of meteor craters.
* Hemateria and Anamnesis are the T2 planets, and your goal in this tier is to synthesize a material capable of taking the beatings of the asteroid belt. Tenebrae is also technically a T2 planet, but the thermal protection you’ll need to survive it is also made by the synthetic material grown from Hematerian microbes locked in the poles. Also on these planets are Tungsten, the hull material of your next ship.
* Egora’s three planets are the T3 locations. The material that you need to traverse Pleura’s rings and travel even deeper into space are a bio-alloy of the Hematerian microbial mesh and more advanced life found in these three planets. If you have the Ctenocerum already, you can begin a processing line that will allow you to skip the T3 planets, though the line must be finished in later tiers for the interstellar travel that it promises.
* Pleura, its rings, and the Asteroid Belt are the only T4 locations. Pleuran Ice, found in the cores of the comet-like bodies which orbit the planet, are the only material capable of controlling the immense solar heat of Perihelia.
* T5: Perihelia. The journey to the border of the sun blasts you with hours upon hours of unbearable heat, just to collect enough of the plasmogenic superfuel you’ll need to cross the cosmic abyss that leads to Ataraxia.
* T6: Ataraxia. The journey here is long and arduous, and for that we’ve finally provided a planet where the materials you need can just be mined. What you really get from Ataraxia is the knowledge of interstellar travel. A crashed alien spaceship has a log on its bridge showing that its course was headed for Anamnesis. If you haven’t already, you’ll need to collect some Ctenocerum of your own, and perform chemical experiments on it until it becomes unstable. From there, you’ll need to launch it in an unmanned rocket of your own, where the Ctenocerum will destroy it and fly out into the orbit of Viridis, linking the Overworld to a wormhole across the galaxy. Exploration through this wormhole requires a T7 rocket, which can be made from fusion materials in the overworld only.




THE TECHNOLOGY TREE WILL NOT BE PRESENTED IN ANY FORM!!!


Progression(OLD VERSION, WILL BE DEPRECATED)
Coming with Galaxia will be tiered systems, similarly to the existing tiering mechanics. Tier 1 rocket resources will be available on the Overworld, Tier 2 resources will be available in Tier 1 systems, and so on. The exception to this is the automated control computer, whose tier 1 components are only available using Tier 2 resources, and so on and so forth.


Tier 1 planets and resources will remain largely the same, as we want the Rocket to be similar in price to its Galacticraft equivalent.
















Module progression example, where you start with some modules at the beginning, then can selectively choose 
  



Mod Aesthetics
Mod Aesthetics:


Galaxia aims to be a lot more realistic than its predecessor 1.7.10 mods, Galacticraft, GalaxySpace, and Amun-Ra. Since the release of these mods, we’ve seen how much better spaceflight systems can be made, (in factorio, ad astra, stellaris(mc mod) and many other games) even subnautica manages to make a more realistic system than galacticraft uses for its spaceflight, and it's not even the main highlight of its gameplay. 


The new rocketry modules designed for Galaxia will be more realistic, and better fitting with Minecraft's well-put-together current style. For instance, the new minimum size command pod in the new rockets must be able to fit the average player model in its command chair. The pod will have space for small amounts of inventory (for food, supplies, and tools,) and will have a parachute and heatshield for returning to the overworld.  Rockets will be able to be upgraded as you further your tier, so it is realistic to have just one rocket during the entirety of a run. However, the rocket will also now have a durability mechanic, that you will need to repair when broken or upgrade the hull material to have a higher durability in general. Durability can be lost while entering hostile planets or crashing into celestial objects.


Parts will generally have a bit more detail in their models. Example level 1 command pod by me:


  
  
  



The Image shown above is 3x3 blocks in width and length, and 2.5 blocks tall. It fits a player comfortably in their command chair. Note, each sprite is 16x16. They look bigger, but their large size in-game makes each pixel end up being normal block size.


  



Other mods have very cool rocket textures and planet textures compared to what is currently in galacticraft. Shown here is Ad Astra, with its tier 3 rocket, and the moon, mars, earth, venus, and a purple planet shown in the background. So pretty!


Rockets aren't going to be craftable anymore as items, in any shape or form. There may be rare circumstances where a rocket part will be able to fit in your inventory as an item (eg, a parachute, its only 1x1x1 blocks wide) but the rockets themselves will need a new multiblock to be assembled, and some select early game rockets (eg, the first sounding rockets to test atmospheric flight, 1x1x3 WLH) will be multiblocks that then turn into the rocket shape. You can't pick up a full rocket as items.


Factorio has a lovely example of what the rocket assembler might look like in vibe. 
  
   


It won't be exactly like this, but the general idea is that you input modules into the multiblock, made in a separate module assembler, then it makes your rocket for you. There will be a gui terminal on the side so you can select which modules you want your rocket to be made out of and where, and then to see how many you have left to supply.


Kerbal space program also has a bunch of interesting rocket parts. These are not all of the main ones used in the game, but these are some I planned to use as references for key modules in Galaxia.




  
  
  
  
                                                  




Space station segment building will work somewhat like subnautica's base building mechanic.
  



Imagine: this in space, larger, and with space for gregtech single blocks inside, and multiblocks docked on the outside or in large rooms.


You will have tube and large room segments but these will be placed by the space station's core module, and automatically built in one burst if you have the resources. This is to stop holes from being in your space station compared to if you were building it by hand out of normal blocks, and to make the stations more regular.




  

	

This is the current design plan for the fuel tank modules. This one is made of liquid fuel and oxidiser. This tank was made by June


	



Replacing Features
Replacing Features:


As Galaxia will be replacing content from Galacticraft, GalaxySpace, and Amun-Ra, many of these mods’ mechanics will be replicated or replaced, or deprecated altogether. Features that are being replicated will be made green, features that are being replaced will be orange, and features that are being altogether deprecated will be red.


Machines:
* Cryogenic Chamber
* Oxygen Collector
* Oxygen Compressor
* Oxygen Decompressor
* Oxygen Bubble Generator (Galacticraft) - (Being replaced with a more modular oxygen ventilation system)
* Oxygen Sealer
* Oxygen Detector
* Oxygen Storage
* Energy Storage
* Galacticraft Solar Panels
* Fuel Loader
* Block Scale? - (All blocks now have a mass of one mass unit in rocket cargo, and this is not very much in gameplay)
* Cargo Loader/Unloader
* Terraformer
* Hydroponics Unit
* NASA Workbench
Features:
* Shuttle Rockets (Galacticraft)  - (being replaced with the new modular rocket system)
* Landers
* Flag
* Throwable Meteors
* Arc Lamps
* Mothership + Control + Components - (being replaced with a Warp drive ship)
* Air Lock
* Buggy
* Launchpad
* Asteroid Miner
* Parachute
* Oxygen Tanks
* Frequency Module
* Thermal Systems/Protection
* Gravity
* Artificial Gravity
* Rocket Schematics - (being replaced with the module tech tree, and testflight missions)
* Space Stations
* Glowstone Torches
* Grappler - (dash ability using a keybind works for the 0g navigation)
Items:
A few items in Galacticraft, GalaxySpace, and Amun-Ra are used in crafting recipes:
* Fluid Manipulator
* Dark Matter
* Nanite Cluster
* Nanite Control Module
* Sensor Lens
* Sensor Glasses
Resources:
Planets at different tiers contain resources helpful for further progression in GTNH, and these will be necessary to move to their required areas in Galaxia.
T1 Resources:
* Meteoric Iron
* Monazite
* Neodymium
* Bastnasite
* Bauxite
* Ilmenite
* Chromite
* Uvarovite*
T2 Resources
* Desh
* Pitchblende
* Uraninite
* Scheelite*
* Tungstate*
* Bismuth*
* Oriharukon
* Draconium
* Vinteum
* Jade
T3 Resources
* Ledox
* Callisto Ice
* Naquadah
* Quantium
* Deep Iron
* Trinium
T4 Resources
* Mithril
* Iridium*
* Plutonium 239*
* Infused Gold
* Mytryl
* Ceruclase
* Vulcanite
T5 Resources
* Osmium*
* Shadow Iron
* Tiberium
* Enriched Naquadah
* Bartimaeusnek
T6 Resources
* Neutronium
* Adamantium
* Plutonium 241*
T7 Resources
* Nether Star*
* Black Plutonium
T8 Resources
* Tartarite
T9 Resources
* Infinity Catalyst*
* Bedrockium*
* Awakened Draconium*
* Dilithium
* Mysterious Crystal*


Equipment
Equipment
Equipment will be presented in the form of two main parts: thermal protection, life support framework. For convenience players will see which equipment must be used to survive on a planet.


Thermal protection will be presented in a few tiers, some for heating and some for cooling which will depend on surface conditions.


Life support framework is a module that is equipped as an exosuit and serves as a holder for space equipment like oxygen tanks, glass helmet, protection from different sources like radiation, pressure, temperature and toxic atmosphere.


Space suit can be any armor that has space suit capabilities (already defined in-game). 
Stretch Goals
Stretch Goals:
Content to be looked at and completed after the main bulk of the Galacticraft replacement is done.


Interstellar Travel:
One entirely new facet of late-game Galaxia gameplay is the ability to explore interstellar space, traveling and interacting with far-off celestial bodies through light-speed Warp Drives, opening up an entirely new Sci-Fi realm where you can pump stellar plasma directly from stars, explore the remnants of a nebulaic supernova, and extract dark matter from the new supermassive black hole at the center of Galaxia's galaxy.


Space pumping module rework concept:
The main idea is to completely change its functionality. Now this module is responsible for searching for and delivering full-metal asteroids, comets, and fragments of destroyed planets to the space station for processing.
Some of the functionality is partially similar to meteorites from the BM but we don't order a specific meteorite using a catalyst, we search for a specific space object that meets our requirements, for example, an asteroid consisting of 99.99% platinum group metals, which does not require ore processing since it contains almost pure metals (but still requires a Platline to separate the different platinum group metals from each other).
We can also search for comets with a certain liquid gas content, which are currently obtained using pumps.
In other words, this module will have hybrid functionality for both meteorites from the BM (ordering a single asteroid with a huge amount of resources on request) and a space pump (automatically searching for the required comets with a gas/liquid composition).
Now each such module must be attached to a space tractor, which we will have to build in space station, containing a module for connecting to a space object (either drills or particularly large chains, Idk).
Therefore, to operate this module, it will be necessary not only to supply it with energy, as is currently the case, but also to provide it with the fuel necessary for the tractor (for example, helium-deuterium for a fusion engine, or nuclear fuel for a nuclear engine).
Also, one of the goals is to remove gases/liquids extracted from gas planets from the space pumping module, because now this must be done through interplanetary logistics and space stations containing space siphons, which will be buffed and redesigned




DEVELOPMENT
Galaxia Development
Important links:


Galaxia main github
Galaxia Issues Tab
Galaxia pull requests
Galaxia's tech and planning doc




Mod style or features for incorporating into galaxia:


Stellar view - Stars, night sky renderer. MIT license
Beyond earth, assets for textures - NonCommercial-ShareAlike
Galacticraft link - for referencing features
Amun-Ra link - for referencing features
