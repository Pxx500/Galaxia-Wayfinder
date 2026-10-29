---
type: wayfinder-ticket
ticket_type: grilling
status: open
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Automation and Infrastructure]]"
secondary_areas:
  - Area - Alpha Scope
blocked_by: []
claimed_by: wayfinder
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Space Factory Power

Space factories need local generation or physically transported energy and inputs, with solar output determined by their celestial environment.

## Power Sources

Wireless EU transfer between planets is prohibited under [[Require Explicit Interplanetary Logistics]]. Transported ordinary GT batteries and a suitable Battery Buffer are the provisional first-workshop bootstrap. Actual demand and transport capacity remain to be verified.

Solar, nuclear reactors and radioisotope thermoelectric generators are selected families for investigation, not blanket approval of every existing machine, recipe or performance value. Combustion remains prohibited under [[Define Celestial Capability Rules]], including in oxygenated Station rooms. Assess the complete supply route and infrastructure, not just the generator.

Proposed roles are solar for suitable illumination and panel-production investment, nuclear for dense sustained demand, and RTGs for modest remote loads with infrequent supply. These roles and concrete GT machinery remain open. Late interplanetary energy export belongs to [[Define Late Interplanetary Network Access]].

## Solar Manufacture And Yield

The Space Grade Solar Panel is a recipe component. Placeable panel blocks and their Solar Energy Dynamo adapter are separate equipment. Ground manufacture produces the same hardware at deliberately high material cost, enough to bootstrap orbital manufacture but uneconomical for large expansion. Microgravity-derived SiGe and fluoride materials make later manufacture substantially cheaper. Poor-yield ordinary silicon is a candidate ground route, not an approved recipe. There are no separate panel grades based on manufacturing location.

Manufacturing and generation are separate advantages. Orbital panels should still have substantial upfront cost relative to non-passive generation, but no cost ratio is selected. Solar output varies with distance, atmospheric effects and illumination under [[Define Celestial Capability Rules]]. Overworld daylight is the 100% reference and night is 0%. Orbit should have a substantial instantaneous advantage and continuous illumination. The 200% and 300% examples are candidates, not selected multipliers. Exact scaling and electrical conversion remain open.

## Solar Arrays

An array consists of a bounded panel plane and one rear adapter. The initial collector supports a 5 by 5 plane. Higher 9 by 9 and 11 by 11 areas are proposed, with tier assignments and recipes open. Larger installations can use multiple arrays, each with its own adapter and cable connection.

The adapter faces the collection direction and the immediately adjacent panel is the central entry point. Incomplete arrays work. Only panels connected to that entry through a continuous path inside the bounded plane contribute. An isolated corner does not contribute, while a corner connected through other panels does. A path outside the boundary cannot connect panels inside it. Face-adjacent connections are proposed, not finalized. Overlapping collectors must not count a panel twice, but the ownership rule is open.

Panels and adapter align from the environment rather than the player's view. In orbit they face the fixed horizontal Sun, forming a vertical wall. On a planetary surface they face upward, with the adapter below the central panel. Surface panels do not require continuous tracking.

Panels are passive blocks, not independently ticking generators, storage or network endpoints. The collector generates and exports power for its connected panels. Cache the connected set and refresh it on relevant structure changes and initialization rather than rediscovering it every generation tick. Existing GT structure-update mechanisms are preferred where suitable, but their coverage for new passive blocks needs verification. Rendering and exposure checks must not reintroduce per-panel per-tick work.

Coverage extends symmetrically from the central panel along both axes of the plane. A 5 by 5 array extends two blocks in each direction. The shadow-check volume uses this footprint and extends forward from the panel plane, not from the adapter.

## Electrical Output

The adapter offers current generation to the ordinary GT energy network. Unused output is not stored for later ticks or accumulated into a burst. At most one tick of current generation may be held for transfer, and total export across connections in a tick cannot exceed that generation. Accepted output depends on demand.

Native GT voltage, amperage, cable losses and overload behavior apply. Low accepted EU/t does not guarantee safety from excessive voltage. Collector tiers select panel area, not an approved artificial output-clipping scheme. Electrical tier mapping, packet representation, fractional output and adapter ratings remain open.

GT5 source inspection at revision `6eac02935d42b3ab13d341e4fe090b4403e15f60` found demand-aware energy emission and structure checks driven by updates and initialization. It did not establish that arbitrary new panel blocks notify the collector.

## Sunlight And Cooling

In orbit the parent planet appears below, the Sun remains in a fixed horizontal direction and periodic planetary eclipses do not occur. The sky, solar collection and radiator exposure use the same direction. Exact cardinal direction and local shading checks remain open. Panels work best facing the Sun. Radiators should minimize direct solar exposure, with a perpendicular arrangement intended. Exact face and placement checks remain open.

The Computer's coolant loop is closed. Its radiator rejects heat according to environmental temperature, with space as a reference rather than a maximum. A powered chiller restores coolant when passive cooling is unsuitable. A near-Sun orbit can offer strong solar power without unlimited cooling. There is no blanket planetary radiator ban. [[Define Data Processor Machine Topology]] owns the cooling equipment and thermal choices.

The simplified orbital convention is a gameplay decision, not a claim that real orbits always stay sunlit. [ESA's orbit overview](https://www.esa.int/Enabling_Support/Space_Transportation/Types_of_orbits), [NOAA's GOES eclipse information](https://www.ospo.noaa.gov/operations/goes/eclipse.html) and [NASA's thermal-control overview](https://www.nasa.gov/smallsat-institute/sst-soa/thermal-control/) informed the direction.

The perpendicular radiator arrangement does not mean merely turning its front away from the Sun.

## Shadow Updates

The accepted direction is coarse-to-fine, change-driven shadow updates with batching and a shared processing budget. Use a finite forward obstruction distance. The discussed 16 and 32 blocks are alternatives to measure, not selected constants. Generated orbital objects cannot be assumed permanently absent.

A dimension-qualified, chunk-keyed collector registry finds local candidates. Block changes mark a chunk dirty and expand a bounding box, coalescing repeated changes. Candidate collectors are checked against a bounded sunlight volume in front of their panel plane. An intersection schedules a visibility check, not proof of an obstruction. Deduplicate queued collectors and budget candidate discovery and visibility checks across ticks. Work must be resumable, and changes arriving during processing must not be lost or mistaken for a validated result. Unchanged arrays do not need periodic geometry rescans.

The proposed delayed-validation behavior retains a running collector's last validated exposure and makes a new collector wait for its first result. It is not yet confirmed. Mutation and opacity hooks, bulk edits, startup, chunk load and unload, unloaded check volumes, the opacity rule and latency remain open. Do not force-load an unlimited ray or assume unloaded space is clear. An overhead Sun is a last-resort reconsideration if the fixed direction proves impractical, not the selected design.

Checked vanilla vertical skylight uses a column height map and cannot by itself establish horizontal visibility. The checked block-update path is conditional, so complete mutation coverage is not established. No performance gain or latency has been measured.

## Open Decisions

- Select solar recipes, electrical ratings and a complete starter supply route that does not require orbital products.
- Evaluate solar, nuclear and RTG equipment against actual loads and complete supply costs.
- Resolve panel overlap, connection interpretation, shading distance, update coverage and unloaded-state behavior.
- Calibrate environmental yield and radiator exposure and thermal thresholds.

## Gameplay Flow

Players can carry batteries to bootstrap a first workshop, then build a more sustained local supply. Ground-made solar hardware can start orbital production, although its high material cost makes large expansion expensive. Production using microgravity-derived materials makes further panels cheaper, while the same hardware still responds to the local environment.

In orbit, players assemble panel walls facing the fixed Sun and connect each section through an adapter to ordinary GT wiring. Connected panels contribute even when the array is incomplete. The adapter supplies only current generation, so unused power does not accumulate for a later burst. A nearby Computer can use that power while its radiator rejects heat away from the Sun, or use a powered chiller where passive cooling is unsuitable.
