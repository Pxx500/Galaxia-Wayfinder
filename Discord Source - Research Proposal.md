---
type: source
status: reviewed
tags:
  - galaxia/alpha
  - wayfinder/source
---

# Discord Source - Research Proposal

Source status: reviewed developer proposal
Imported: 2026-07-31
Original document: [Google Docs](https://docs.google.com/document/d/1wZDwmi78wMBlzFNc08W2tMrgyYfpygY0DEIyXy-Rqvo/edit?tab=t.0)

> This file preserves a proposal authored by another developer. Its classification is recorded in [[Galaxia Research Proposal Research]]; the source itself is not an accepted specification.

## Imported Content

Research


What is this feature:


Research is a system that gates progression on planets and introduces a unique and interesting way of interacting with planets.


Research is quantified as a “point” number, from 0 to 400 points. At 100 points, you unlock the ability to do everything progression-wise on a planet (given you have the resources to do it).


Any further research has milestones every 50 points that gives you a bonus to planet-specific things. This could be higher power generation from a generator, or faster processing times for a machine. This does NOT give you access to alternative production lines, those will be inherent as part of the 100 point reward. There is no gameplay reward for the final 400 point milestone, to disincentivise looking for “that one randomly generated thing I can’t find to get the final boost”.


Points are gained by interacting with the planet. These “Research Objectives” will be similar to modern vanilla Minecraft advancements. A Research Objective are as simple as: finding and mining a crystal underground, stepping in quicksand, visiting a structure, visiting a biome, interacting with flora, growing flora. 

On each planet, there will be a lot of little interactions that exist, that are mostly environmental and don’t have a progression reason to interact with them. Things like these are what makes the vanilla overworld (especially in modern minecraft) feel so full compared to other modded dimensions that feel relatively empty.


Simpler objectives are classified as “Simple” and reward 2 points each, “Moderate” objectives reward 5 points each, and “Remarkable” objectives reward 10 or more points depending on the exact objective.


Moderate objective consist of things such as: using a scanner item on three separate small craters, mining a certain amount of an ore, sifting through dust until you get a special item, visiting all biomes, almost drown in quicksand, bring flora to a space station, bring flora to the overworld and grow it.


Remarkable objectives require time and/or resource investment, and reward you accordingly: build a satellite and transmit data from orbit for 30 points, use an existing or new telescope in L2 anywhere to study the planet (can be done BEFORE first landing on the planet) for 25 points, assemble a rover and drive it 2000 blocks for 15 points, drive a rover into quicksand for 10 points, create a space station that is human survivable for 30 points, take a radiation measurement from a space station for 10 points.


These are just a small sample of random things I came up with over a few minutes, there are 100s of potential ideas for little interactions to be had on each planet. The Minecraft Advancement page is a good place to look for inspiration, mainly the adventure section and below.


Why should this feature exist:


This feature gives the player a reason to interact with random things on planets, the more a player interacts with a planet, the more real and deep it feels. This is how the overworld in modern vanilla Minecraft feels as wide as it does, and the vanilla advancements aim to do the same thing, incentivise the player to interact with the world and its features and give them challenges to complete.


Research Objectives are a minimally obstructive way to encourage the player to explore. There aren’t any guide rails on what you have to do, you can choose to do only “Remarkable” objectives if you wish, or do no Remarkable objectives at all.

They only require you to do 25% of the available points to get to the more “GTNH” style things like making material lines. This also means even if you spawn near very few things to do, you can still reach the point threshold.


This also gives planetary exploration an element of replayability and “roguelike” mechanics, in one Galaxia run you might land in a certain biome and do 15 simple objectives in it, in another run you might land in a different biome and instead do a different set of 10 simple objectives there and do 2 Remarkable objectives you didn’t do last time.


What considerations were made in the design of this feature:


Minimal buffs are given for getting over 100 points so that only those who actually enjoy exploring and doing “Research Objectives” will do them, and still receive a reward of some kind, rather than more than 100 points being “the meta”.


As mentioned earlier, there is no gameplay reward for 400 points, maybe some small visual or trophy, but trying to find randomly generated things and getting unlucky can be very frustrating. With the sheer volume of simple objectives, completing everything is going to be tedious (and bad for server storage!) and is only intended to be done by completionists who enjoy doing that in particular.


Satisfactory was of course a big inspiration, I like the collectible rewards for the most part, and this aims to improve and expand upon the idea in a way that fits better in Minecraft and GTNH. I think locking production lines behind a high enough research milestone would not feel the best for GTNH, Satisfactory hard drives do this and I think it works okay for it, albeit it does have a few issues, and I think it instead being a less impactful buff will feel better for the general GTNH playerbase.


Likewise, Satisfactory instead uses combat as its method of making finding these “buffs” interesting and fun. I personally am not the biggest fan of that, and also don’t think it would fit as well into GTNH.


The Research Objectives are designed to be very similar to Minecraft Advancements in a lot of ways. They both give a reason and structure to interacting with the dimensions, and I personally really like the way Minecraft Advancements are done. I think they give a good way of interacting with such a wide sandbox.
Stardew Valley (SDV) is another thing I took inspiration from! In SDV the game has a “final goal” of repairing the Community Center. The Community Center has a few rooms that each have a few bundles. Every bundle requires a few items, some items are specific, and some not, allowing you to contribute any of a type of item to the bundle. Each room unlocks something new in the town that helps you grow your farm. SDV uses this to make the player interact with systems they otherwise might not. E.G foraging, this is looking around the town for specific items that grow randomly on the ground rather than on your farm.


Part of my vision for Research Objectives is inspired by the way SDV makes it all come together. In SDV you don’t usually GO foraging for your Community Center, you simply collect anything you see while walking in between places. The design is done in a way that incentivises doing things, but tries to make it so that you can group these things together. E.G going to the mountain to fish for a specific fish, and along the way you forage for some things and dig some archaeology nodes. This makes “objectives” feel less like chores and far more fluid and interesting. It introduces a meta-game of trying to find the most “objectives” that can be chained one into another to optimize your time.


Also randomisers and finding checks is a lot of the inspiration but I’ve explained enough to get the point across I think lol.


How will this feature appear visibly:


In whatever map view there is for Galaxia, clicking on a planet will also show its research points. Building a Research Station on the planet will give you a page (kind of like minecraft advancements) that allows you to look at all the objectives for the respective planet.
