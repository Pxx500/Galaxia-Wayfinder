---
type: source
status: unreviewed
tags:
  - galaxia/alpha
  - wayfinder/source
---

# Discord Source - Crater Nodes Proposal

Source status: unreviewed Discord research
Imported: 2026-07-31
Original document: [Google Docs](https://docs.google.com/document/d/1SW-HysWHLHMK6a7ABwUkXO3V97SE-lSTLvot05xoYOA/edit?tab=t.0)

> This file preserves a proposal authored by another developer. The project owner has not endorsed its claims or design. Do not treat this material as an accepted specification or integrate it into the Wayfinder until it is reviewed with the project owner.

## Imported Content

Crater Nodes
Crater Nodes


What is this feature:

Impact craters are large craters formed by meteor impacts, these are NOT the volcanic craters we currently have as magma biomes, as those are caused by volcanic activity. 

Impact craters are vaguely circular biomes, generated with a carver after initial generation to allow it to dig into the landscape and the surrounding biomes.


Each impact crater has its own resource node for the whole biome, the resource is randomised between a few resources for the moon, (iron, gold, nickel etc).


To extract the resource from the node, you need a basic space drill. These are functionally similar to miners from Satisfactory, you simply put it down anywhere in the biome, provide it power and it starts generating resources at a fixed rate. Each node has a high but limited amount of the given resource.


Nodes have a density rating that provide small modifiers to the drill, a denser node is slower to extract from but has a higher amount to extract, a weaker, less dense node can be extracted faster but has less to extract. These are small buffs/debuffs - around ~25% at most. Density is 50-150 with 100 being default.


These resources can be refined into their major element and used to supply a resource chain or sent to other locations using Galaxia’s logistics system.


They also have secondary resources that can be extracted from the ore and used in making a material that can be used for progression through Galaxia (Space-Grade Alloy).


Refining these resources into their major element is NOT how you create Space-Grade Alloy, refining them that way is a separate bidirectional process. More details in the Space-Grade Alloy tab.


Using Space-Grade Alloy, you will be able to upgrade the drill to extract a good bit more from the node and extract from higher densities faster.


Additionally, there is a second form of miner, the fracking rig. The fracking rig “pumps” a fluid into the ground to extract more resources from a node than a normal drill can, the amount of ore left in the node is irrelevant to the fracking rig.


Used fracking fluid (called [Ore] Solution) recovers the fracking fluid at a 1:1 ratio when processed correctly. However the more you have fracked a node, the rig requires more fluid to create the same amount of solution.


Initially the rig can be used in a closed loop for a bit, and eventually it starts to increase the amount of fluid used at a slightly exponential scale.


Used fracking fluid is processed into a much higher yield of the secondary resource, with a slightly higher yield of the base element, however the processing of the fluid is more complex than the ore.


Density also affects the fracking rig, a less dense node will start at (for example) 10mb/t of fluid in, and 10mb/t of fluid out, whereas a denser node starts at 15 mb/t in and 15 mb/t out, costing more fluid as a base, but having a higher output to match.


Why should this feature exist:

This feature was designed to add a system that allows you to generate metals for material lines, the moon needs a progression of a sort but it’s pretty barren and still just “the moon”. This opens up ways to make the player want to create automation lines rather than just getting some of a resource and making the needed material. By introducing a mechanic that produces a lot of resources, we can make lines that consume a lot of resources.


It introduces an interesting set of constraints and variables depending on where you land on the moon, the craters are relatively rare and so most people will choose to work with what they have. E.g spawning near a thin (not dense) iron node may make you use a standard miner and use a mix of both the iron and secondary resource to create whatever important material you need from the moon, if you spawn near a dense gold node you might instead use a fracking rig and use just the secondary resource for progression.


Rigs can be used as part of interplanetary infrastructure if connected to the Galaxia logistics system. An automated outpost can be used to generate the fluid for fracking and sent over to the rig location to generate the primary or secondary resource from the node, and that can then be sent to another place that needs those resources.


This also creates a reason to have one central “outpost” on the moon, as the first planet in Galaxia, having a central base of operations simplifies the objectives of the player to only considering what things are around them.


What considerations were made in the design of this feature:

The fracking rig requires exponentially more input, as having infinite resources in EV is hard to balance (also it’s more interesting this way)


The basic drill can be upgraded to allow easy scaling of your existing outpost once it’s been finished and not need to go setup everything on another node once it runs out.


Satisfactory was a large part of the inspiration for the design of this, the spawn locations and therefore what mining nodes you have surrounding you are a large part of how it can make different runs feel unique.


A lot of this is based in reality! Impact craters are mined in real life for resources sometimes (see Sudbury Basin in Ontario for a major one). Fracking is used in real life to extract mineral solutions (not just hydrocarbons!). Also needing more and more fluid the more you frack a node makes an amount of intuitive sense (the bigger you make the hole by fracking it, the more fluid is needed to reach the same pressure), density is also somewhat intuitive for both miners.


How will this feature appear visibly:


Impact craters were described before, but the basic drill would be relatively small, maybe a little smaller than the GTNH mining drill, in the “immersive engineering” style that we want for our multiblocks. The fracking rig would be larger, and have a large “hydraulic pump” thing with a pumping animation in the middle, and have the design around the pump inspired by actual fracking rigs.




Technical details and more:


Each impact crater has its own singular node, these are stored in a hashmap with the key being based on the noise that is used to generate the crater biomes themselves, so the miner checks if its in a crater biome, then finds or generates the respective node into the hash map and references that.




There are 3 crater material types of equal rarity


Fe-Pt
9 parts “Unrefined Wüstite”, 1 part “Impure Asteroidal Platinum”


Au-Co
7 parts “Rough Asteroidal Gold” , 3 parts “Natural Asteroidal Cobalt”


Al-Sc
“Unprocessed Scandium-Rich Bauxite” (10 Al2O3:2 Sc)




Basic Space Drill stats:




Fe-Pt


9 Unrefined Wüstite and 1 Impure Asteroidal Platinum every 50 seconds
40 seconds at minimum (50) density
60 seconds at maximum (150) density


12000 total resources, almost exactly a week of drilling (10800 Unrefined Wüstite and 1200 Impure Asteroidal Platinum)
9000 total at 50 density
15000 total at 150 density

Au-Co


7 Rough Asteroidal Gold and 3 Natural Asteroidal Cobalt every 40 seconds
30 seconds at 50 density
45 seconds at 150 density


10500 total resources, about 5 days of drilling (8400 Rough Asteroidal Gold and 3600 Natural Asteroidal Cobalt)
9660 total at 50 density
14700 total at 150 density








Al-Sc


12 Unprocessed Scandium-Rich Bauxite every 70 seconds
40 seconds at 50 density
90 seconds at 150 density


12000 total resources, about 8 days of drilling
10000 total at 50 density
14000 total at 150 density




Improved Space Drill stats (only the changes):




Fe-Pt


55 seconds at 150 density


16000 total resources
13000 total at 50 density
18000 total at 150 density

Au-Co


40 seconds at 150 density


12600 total resources
10500 total at 50 density
16800 total at 150 density


Al-Sc


80 seconds at 150 density


13500 total resources
11500 total at 50 density
15500 total at 150 density
























Fracking Rig stats:




All resources share the same stats


100mb in/out every 10 seconds
50mb in/out at 50 density
150mb in/out at 150 density


It takes 14 days of straight runtime to reach double consumption, but about 8 hours to stop being a perfect closed loop.


The base of the power decreases greatly after 48 hours, making the first 48 hours have a much stronger curve than afterwards.


More specifics on the formula here.




Processing lines:


Al-Sc Line, based on the Bayer process and selective scandium extraction, distinct from GT bauxite processing in many ways. Simple but low yield in comparison to the other (currently unfinished) lines. 




Iron and aluminium are present as oxides.
Platinum is present as PMP.


UNFINISHED INFO:


Converting iron into the raw material is 1:1 but converts to an oxide
Converting gold into the raw material is 2:1
Converting dirty alumina into alumina is 2:1
Platinum can be converted to PMP at a 10% chance per part
Cobalt when turned into the raw material is 2:1
Scandium when turned into the raw material is 2:1


Space-Grade Alloy
Space-Grade Alloy is a secondary but necessary-to-explain part of Impact Craters and their respective drill system.


Space-Grade Alloy is a material that can’t be created in-atmosphere, it (and its components) must be created in the vacuum of space to ensure the material’s stability in space.


It’s an alloy formed of 2 materials, the intention is that you use any kind of space drill to produce the base resources for the alloy on the moon, and process them into Space-Grade Alloy.


Space-Grade Alloy is created at an extremely poor ratio compared to the respective “ore” input. This encourages the player to automate the creation of it on-planet as opposed to building a station and manually creating the alloy there, while still allowing that as an option (though very expensive logistics-wise).


There are 3 kinds of Space-Grade Alloy, all with separate textures but named identically. They are completely interchangeable in recipes but separated by metadata in code.


(some data sourced from here)


Each crater type has its own alloy formed from the two materials that it consists of: 


The Aluminium-Scandium alloy is a bit simpler to process than the other two, being only a simplified Bayer process + Scandium extraction, but has lower yields. Al-Sc alloys are real alloys that are used in aerospace. Both Al oxides and Sc can be found in real asteroids.


The Gold-Cobalt alloy requires significantly more cobalt than gold, but has good yield. Gold and Cobalt are both found in asteroids (cobalt moreso but we bend reality).


The Iron-Platinum alloy is a more advanced process than either alloy, however it has good yield, and makes a fluid that can be easily recycled into a small amount of PMP. Iron and platinum are found in abundance in asteroids compared to earth’s crust
Al-Sc Line
Step 1:


1 Unprocessed Scandium-Rich Bauxite -> 
Macerator = 
1 Crushed Scandium-Rich Bauxite


Step 2:


2 Crushed Scandium-Rich Bauxite AND 
2 Sodium Hydroxide Dust ->
Vacuum-Rated Pressure Chamber new = 
1 Dirty Scandium-Alumina Mixture


OR


2 Crushed Scandium-Rich Bauxite AND
2 Scandium-Rich Slag AND
4 Sodium Hydroxide Dust ->
Vacuum-Rated Pressure Chamber = 
2 Dirty Scandium-Alumina Mixture


Step 3:


6 Dirty Scandium-Alumina Mixture ->
Sifter =
5 Dirty Alumina AND
8 Low-Scandium Red Mud


Step 4:


(source)


8 Low-Scandium Red Mud AND
1000mb of Diluted Nitric Acid (HNO3) ->
Chemical Reactor =
2 Iron (III) Oxide Dust (Fe2O3) AND
12 Sodium Hydroxide Dust AND
1000mb of Leached Scandium Solution












Step 5:


1000mb of Leached Scandium Solution ->
Sifter =
1 Poor Scandium Dust AND
1000mb of Diluted Nitric Acid




Step 6:


20 Dirty Alumina AND
4 Poor Scandium Dust ->
EBF (not in-atmosphere) =
1 Space-Grade Alloy AND
24 Scandium-Rich Slag 




Shitty mockup:


  

Fracking Rig Formula
Where x = number of cycles, and d = density
Raw LaTeX:
y=\left(\left(d-1\right)+\left(83\cdot\min\left(\max\left(x-17280,0\right),1\right)\right)\right)+\left(\left(1.0003\cdot\left(\max\left(\min\left(17280-x,1\right),0\right)\right)\right)+\left(1.0000375\cdot\left(\min\left(\max\left(x-17280,0\right),1\right)\right)\right)\right)^{\left(\max\left(x-2500,\ 0\right)\right)}
  
The actual simplified version is:
