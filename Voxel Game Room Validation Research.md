---
type: source
status: reviewed
tags:
  - galaxia/alpha
  - wayfinder/source
---
# Voxel Game Room Validation Research

Source: public source repositories listed below, pinned to the commits recorded in this note
Imported: 2026-09-13

[[Sources]]

## Source Snapshot

This is source-backed research only. The observations below describe the pinned code, not current shipping behavior. The Galaxia notes are interpretation for comparison and are not architecture decisions.

### Snapshot identity

| Implementation | Source status and snapshot |
| --- | --- |
| Space Engineers | `KeenSoftwareHouse/SpaceEngineers`, archived repository, HEAD `54f2f0f3169cda687a25a438097902a43bdfa603`, commit time 2022-01-06T13:46:01Z. Repository metadata: [archived repository](https://github.com/KeenSoftwareHouse/SpaceEngineers) |
| Space Station 14 | `space-wizards/space-station-14`, public repository, HEAD `eadcd567fd8ea801cb346aaed4ff44ab42b6928c`, commit time 2026-09-12T22:31:04Z |
| Barotrauma | `FakeFishGames/Barotrauma`, public repository, HEAD `e6e95da83b1b5ca8b55ec52653c7cf6b40e30247`, commit time 2026-09-02T08:39:27Z |

## 1. Space Engineers oxygen rooms

This is the only implementation in this note that discovers arbitrary three-dimensional rooms from a cube grid. The repository is archived, so this is an historical source snapshot rather than a claim about today's game.

Primary file: [`MyGridGasSystem.cs`](https://github.com/KeenSoftwareHouse/SpaceEngineers/blob/54f2f0f3169cda687a25a438097902a43bdfa603/Sources/Sandbox.Game/Game/GameSystems/MyGridGasSystem.cs)

#### Room discovery start and finite exterior proof

Observed code:

- `MyGridGasSystem` subscribes to block-added and block-removed events. A block add sets `m_pressurizationPending`. A door state change also sets it. See [`MyGridGasSystem` constructor and event handlers, lines 269-345](https://github.com/KeenSoftwareHouse/SpaceEngineers/blob/54f2f0f3169cda687a25a438097902a43bdfa603/Sources/Sandbox.Game/Game/GameSystems/MyGridGasSystem.cs#L269-L345).
- `UpdateBeforeSimulation` starts a pressurization pass when pending. `PressurizeInitialize` computes an array for the grid extent, stores the previous arrays, clears the queue, and seeds the queue at `GridMin()`. See [`UpdateBeforeSimulation`, lines 388-445](https://github.com/KeenSoftwareHouse/SpaceEngineers/blob/54f2f0f3169cda687a25a438097902a43bdfa603/Sources/Sandbox.Game/Game/GameSystems/MyGridGasSystem.cs#L388-L445) and [`PressurizeInitialize`, lines 508-565](https://github.com/KeenSoftwareHouse/SpaceEngineers/blob/54f2f0f3169cda687a25a438097902a43bdfa603/Sources/Sandbox.Game/Game/GameSystems/MyGridGasSystem.cs#L508-L565).
- The finite search box is the cube grid min and max expanded by one cell. `GridMin()` returns `m_cubeGrid.Min - Vector3I.One`, `GridMax()` returns `m_cubeGrid.Max + Vector3I.One`, and `IsOnBounds` tests any coordinate on that shell. See [`GridMin`, `GridMax`, `IsOnBounds`, lines 1024-1071](https://github.com/KeenSoftwareHouse/SpaceEngineers/blob/54f2f0f3169cda687a25a438097902a43bdfa603/Sources/Sandbox.Game/Game/GameSystems/MyGridGasSystem.cs#L1024-L1071).
- The queue walk considers six neighbors. A neighbor outside the stored min and max is skipped. An unblocked transition that reaches the expanded shell marks the current room unpressurized and samples environmental oxygen. See [`PressurizeProcessQueue`, lines 567-674](https://github.com/KeenSoftwareHouse/SpaceEngineers/blob/54f2f0f3169cda687a25a438097902a43bdfa603/Sources/Sandbox.Game/Game/GameSystems/MyGridGasSystem.cs#L567-L674).

Small source excerpts:

> `m_queue.Enqueue(new RoomSquare(GridMin(), 0));`

> `if (IsOnBounds(current))`

> `m_cubeRoom[x, y, z].Room.IsPressurized = false;`

Interpretation: the expanded shell gives this algorithm a concrete exterior witness. A free-space component connected to the shell is outside. A component that never reaches the shell is treated as a closed room. There is no unbounded search and no need to guess whether a second room is the exterior.

#### Room and boundary representation

Observed code:

- `MyOxygenRoom` stores `IsPressurized`, `EnvironmentOxygen`, total `OxygenAmount`, `blockCount`, and a link. `MaxOxygen` is `blockCount * gridSize^3`. See [`MyOxygenRoom`, lines 30-69](https://github.com/KeenSoftwareHouse/SpaceEngineers/blob/54f2f0f3169cda687a25a438097902a43bdfa603/Sources/Sandbox.Game/Game/GameSystems/MyGridGasSystem.cs#L30-L69).
- `MyOxygenRoomLink` is an indirection shared by blocks. Its source comment says it is “Used as a pointer so that we can change rooms fast without iterating through all of the blocks.” `MyOxygenBlock` holds the link and interpolated oxygen values. See [`MyOxygenRoomLink` and `MyOxygenBlock`, lines 71-175](https://github.com/KeenSoftwareHouse/SpaceEngineers/blob/54f2f0f3169cda687a25a438097902a43bdfa603/Sources/Sandbox.Game/Game/GameSystems/MyGridGasSystem.cs#L71-L175).
- `RoomSquare` carries a position, room index, and `WasWall` flag. The flood fill uses one three-dimensional `m_cubeRoom` array plus room lists. See [`room fields, lines 214-239`](https://github.com/KeenSoftwareHouse/SpaceEngineers/blob/54f2f0f3169cda687a25a438097902a43bdfa603/Sources/Sandbox.Game/Game/GameSystems/MyGridGasSystem.cs#L214-L239) and [`RoomSquare, lines 479-491`](https://github.com/KeenSoftwareHouse/SpaceEngineers/blob/54f2f0f3169cda687a25a438097902a43bdfa603/Sources/Sandbox.Game/Game/GameSystems/MyGridGasSystem.cs#L479-L491).
- `IsPressurized(startPos, endPos)` first checks whether both positions resolve to the same block. For adjacent blocks it returns true when the start block is airtight or its face table says the direction is airtight, otherwise it checks the end block in the opposite direction. See [`IsPressurized`, lines 1073-1098](https://github.com/KeenSoftwareHouse/SpaceEngineers/blob/54f2f0f3169cda687a25a438097902a43bdfa603/Sources/Sandbox.Game/Game/GameSystems/MyGridGasSystem.cs#L1073-L1098).
- Face geometry is data-driven. The code transforms the neighbor normal and local offset by block orientation, then indexes `BlockDefinition.IsCubePressurized`. Build progress below the final model is not airtight. See [`IsPressurized(MySlimBlock...)`, lines 1100-1129](https://github.com/KeenSoftwareHouse/SpaceEngineers/blob/54f2f0f3169cda687a25a438097902a43bdfa603/Sources/Sandbox.Game/Game/GameSystems/MyGridGasSystem.cs#L1100-L1129).
- Door exceptions are state-aware. Regular and advanced doors block only when closed. Slide and hangar doors check `IsFullyClosed` and their allowed face directions. See [`IsPressurized` door branches, lines 1132-1198](https://github.com/KeenSoftwareHouse/SpaceEngineers/blob/54f2f0f3169cda687a25a438097902a43bdfa603/Sources/Sandbox.Game/Game/GameSystems/MyGridGasSystem.cs#L1132-L1198).

Interpretation: shared walls are not a separate room object. Each six-neighbor transition asks both adjacent blocks for the relevant face. A pillar or partial block can therefore seal only the directions represented by its definition. Opening a door changes passability for the pressure pass without removing the block from the grid.

#### How this compares with a uniform Minecraft-like grid

Observed code: the traversal still uses integer `Vector3I` grid positions and six unit neighbor offsets from [`m_neighbours`, lines 258-267](https://github.com/KeenSoftwareHouse/SpaceEngineers/blob/54f2f0f3169cda687a25a438097902a43bdfa603/Sources/Sandbox.Game/Game/GameSystems/MyGridGasSystem.cs#L258-L267). Room volume uses one `GridSize` cubed in [`GridCubeVolume`, lines 1018-1022](https://github.com/KeenSoftwareHouse/SpaceEngineers/blob/54f2f0f3169cda687a25a438097902a43bdfa603/Sources/Sandbox.Game/Game/GameSystems/MyGridGasSystem.cs#L1018-L1022).

The extra geometric flexibility is in each block's face data, orientation, build progress, and door state. `IsPressurized` transforms the neighbor normal and local offset before reading `IsCubePressurized`, rather than assuming every occupied cell seals all six faces. See [`IsPressurized(MySlimBlock...)`, lines 1100-1129](https://github.com/KeenSoftwareHouse/SpaceEngineers/blob/54f2f0f3169cda687a25a438097902a43bdfa603/Sources/Sandbox.Game/Game/GameSystems/MyGridGasSystem.cs#L1100-L1129).

Interpretation: this remains a unit-neighbor grid algorithm, not an arbitrary-distance geometry graph. The per-face table and dynamic doors are the parts that do not transfer directly to a uniform full-cube Minecraft model. The useful analogy is the bounded six-face traversal and exterior shell, not the game's block-definition details.

#### Block changes, grouping, and rebuild cost

Observed code:

- Block additions set `m_pressurizationPending`, attach door listeners, and increment a gas-block counter. Block removals detach door listeners and append the position to `m_deletedBlocks`. Door state changes set `m_pressurizationPending`. See [`cubeGrid_OnBlockAdded`, `cubeGrid_OnBlockRemoved`, `OnDoorStateChanged`, lines 313-342](https://github.com/KeenSoftwareHouse/SpaceEngineers/blob/54f2f0f3169cda687a25a438097902a43bdfa603/Sources/Sandbox.Game/Game/GameSystems/MyGridGasSystem.cs#L313-L342).
- If the system is not already rebuilding, `UpdateBeforeSimulation` consumes deleted positions through `RemoveBlock`. See [`UpdateBeforeSimulation`, lines 428-438](https://github.com/KeenSoftwareHouse/SpaceEngineers/blob/54f2f0f3169cda687a25a438097902a43bdfa603/Sources/Sandbox.Game/Game/GameSystems/MyGridGasSystem.cs#L428-L438).
- `RemoveBlock` chooses the largest adjacent room, folds other neighboring rooms into it, adds their oxygen and block counts, and relinks the neighboring room links. If any merged room is unpressurized, the result is unpressurized and oxygen is cleared. See [`RemoveBlock`, lines 1200-1287](https://github.com/KeenSoftwareHouse/SpaceEngineers/blob/54f2f0f3169cda687a25a438097902a43bdfa603/Sources/Sandbox.Game/Game/GameSystems/MyGridGasSystem.cs#L1200-L1287).
- A full pass preserves old room data. `PressurizePostProcess` maps old cells to new rooms and runs a separate breach-detection pass after oxygen levels are accumulated. See [`PressurizePostProcess`, lines 696-887](https://github.com/KeenSoftwareHouse/SpaceEngineers/blob/54f2f0f3169cda687a25a438097902a43bdfa603/Sources/Sandbox.Game/Game/GameSystems/MyGridGasSystem.cs#L696-L887).

Small source excerpt:

> `//Do breach detection in a separate pass to ensure that oxygen levels are correct`

Interpretation: this is a hybrid change strategy. Additions and door state changes schedule a complete room pass. A removed block is handled as a local room merge when the cached topology is available. The merge is conservative for outside exposure because an unpressurized neighboring component propagates that state to the merged result.

#### Background work and world availability

Observed code:

- When `BACKGROUND_OXYGEN` is enabled, `UpdateBeforeSimulation` initializes on the main thread and starts `Parallel.Start(BackgroundPressurizeStart, BackgroundPressurizeFinished)`. The worker processes the queued flood fill and calls the postprocess when done. See [`UpdateBeforeSimulation`, lines 390-425](https://github.com/KeenSoftwareHouse/SpaceEngineers/blob/54f2f0f3169cda687a25a438097902a43bdfa603/Sources/Sandbox.Game/Game/GameSystems/MyGridGasSystem.cs#L390-L425) and [`BackgroundPressurizeStart`, lines 441-449](https://github.com/KeenSoftwareHouse/SpaceEngineers/blob/54f2f0f3169cda687a25a438097902a43bdfa603/Sources/Sandbox.Game/Game/GameSystems/MyGridGasSystem.cs#L441-L449).
- The worker comment explicitly warns: “reading grid in realtime can clash with main thread, but process will be restarted anyway after grid change” and says not to write main-thread data. See [`BackgroundPressurizeStart`, lines 441-445](https://github.com/KeenSoftwareHouse/SpaceEngineers/blob/54f2f0f3169cda687a25a438097902a43bdfa603/Sources/Sandbox.Game/Game/GameSystems/MyGridGasSystem.cs#L441-L445).
- Grid shutdown sets `isClosing`, waits for the background task, unsubscribes events, and releases the room-link pool. See [`OnGridClosing`, lines 279-311](https://github.com/KeenSoftwareHouse/SpaceEngineers/blob/54f2f0f3169cda687a25a438097902a43bdfa603/Sources/Sandbox.Game/Game/GameSystems/MyGridGasSystem.cs#L279-L311).
- The file has no chunk-streaming or unloaded-cell state in this room algorithm. It reads the live `MyCubeGrid` and bounds the pass to that grid's min and max. No unknown or pending world cell is represented in the cited code.

Interpretation: the background pass is asynchronous, but it is not an immutable snapshot validation protocol. The source instead tolerates a concurrent grid read by restarting after a change and keeps previous room arrays until postprocess. That distinction matters when comparing it with a manual validation workflow.

## 2. Space Station 14 atmospherics

This is a current open-source two-dimensional tile analogue, not a three-dimensional voxel room solver. The cited atmos implementation does not create room IDs or run a room flood fill. It stores gas per tile and maintains an adjacency graph that excludes blocked faces.

Primary files:

- [`TileAtmosphere.cs`](https://github.com/space-wizards/space-station-14/blob/eadcd567fd8ea801cb346aaed4ff44ab42b6928c/Content.Shared/Atmos/TileAtmosphere.cs)
- [`AtmosphereSystem.GridAtmosphere.cs`](https://github.com/space-wizards/space-station-14/blob/eadcd567fd8ea801cb346aaed4ff44ab42b6928c/Content.Server/Atmos/EntitySystems/AtmosphereSystem.GridAtmosphere.cs)
- [`AtmosphereSystem.Processing.cs`](https://github.com/space-wizards/space-station-14/blob/eadcd567fd8ea801cb346aaed4ff44ab42b6928c/Content.Server/Atmos/EntitySystems/AtmosphereSystem.Processing.cs)
- [`AtmosphereSystem.Utils.cs`](https://github.com/space-wizards/space-station-14/blob/eadcd567fd8ea801cb346aaed4ff44ab42b6928c/Content.Server/Atmos/EntitySystems/AtmosphereSystem.Utils.cs)
- [`AirtightSystem.cs`](https://github.com/space-wizards/space-station-14/blob/eadcd567fd8ea801cb346aaed4ff44ab42b6928c/Content.Server/Atmos/EntitySystems/AirtightSystem.cs)

#### Boundary representation and shared tile entities

Observed code:

- `TileAtmosphere` stores cached adjacent tile references and `AdjacentBits`. Its documentation says adjacent tiles can be null when air cannot flow to them. It also stores `Space`, `Air`, `MapAtmosphere`, `NoGridTile`, and cached `AirtightData`. See [`TileAtmosphere`, lines 73-93](https://github.com/space-wizards/space-station-14/blob/eadcd567fd8ea801cb346aaed4ff44ab42b6928c/Content.Shared/Atmos/TileAtmosphere.cs#L73-L93) and [`TileAtmosphere`, lines 141-205](https://github.com/space-wizards/space-station-14/blob/eadcd567fd8ea801cb346aaed4ff44ab42b6928c/Content.Shared/Atmos/TileAtmosphere.cs#L141-L205).
- `AirtightComponent` carries initial and current blocked directions, `AirBlocked`, `FixVacuum`, and `NoAirWhenFullyAirBlocked`. See [`AirtightComponent`, lines 12-55](https://github.com/space-wizards/space-station-14/blob/eadcd567fd8ea801cb346aaed4ff44ab42b6928c/Content.Server/Atmos/Components/AirtightComponent.cs#L12-L55).
- `GetAirtightData` iterates all anchored entities on a tile, ORs the blocked direction masks for entities whose `AirBlocked` flag is true, and combines `NoAirWhenFullyBlocked` and `FixVacuum`. See [`AtmosphereSystem.Utils.GetAirtightData`, lines 88-145](https://github.com/space-wizards/space-station-14/blob/eadcd567fd8ea801cb346aaed4ff44ab42b6928c/Content.Server/Atmos/EntitySystems/AtmosphereSystem.Utils.cs#L88-L145).
- `UpdateAdjacentTiles` updates both sides of each direction. If either side blocks the shared face, both adjacency entries are cleared. Otherwise both pointers and bits are set. See [`AtmosphereSystem.GridAtmosphere.UpdateAdjacentTiles`, lines 160-224](https://github.com/space-wizards/space-station-14/blob/eadcd567fd8ea801cb346aaed4ff44ab42b6928c/Content.Server/Atmos/EntitySystems/AtmosphereSystem.GridAtmosphere.cs#L160-L224).

Small source excerpts:

> “Adjacent tiles can be null if air cannot flow to them.”

> `// Adjacency is blocked by some airtight entity.`

Interpretation: multiple walls, windows, doors, or other airtight entities sharing one tile are combined by direction masks. A shared face is open only when both tile sides agree that it is open.

#### Outside versus a closed region

Observed code:

- `UpdateTileData` treats an empty grid position as a `NoGridTile` map atmosphere tile and uses map atmosphere data. The tile is marked `MapAtmosphere` and gets an immutable map mixture. See [`ProcessRevalidate`, lines 56-105](https://github.com/space-wizards/space-station-14/blob/eadcd567fd8ea801cb346aaed4ff44ab42b6928c/Content.Server/Atmos/EntitySystems/AtmosphereSystem.Processing.cs#L56-L105) and [`UpdateTileData`, lines 169-235](https://github.com/space-wizards/space-station-14/blob/eadcd567fd8ea801cb346aaed4ff44ab42b6928c/Content.Server/Atmos/EntitySystems/AtmosphereSystem.Processing.cs#L169-L235).
- If no map atmosphere component exists, `GetDefaultMapAtmosphere` returns `GasMixture.SpaceGas` and `IsSpace = true`. See [`GetDefaultMapAtmosphere`, lines 227-235](https://github.com/space-wizards/space-station-14/blob/eadcd567fd8ea801cb346aaed4ff44ab42b6928c/Content.Server/Atmos/EntitySystems/AtmosphereSystem.GridAtmosphere.cs#L227-L235).
- `UpdateTileAir` removes a tile's air mixture when all directions are blocked and `NoAirWhenFullyAirBlocked` is true. When a newly unblocked tile has `FixVacuum`, `GridFixTileVacuum` draws a ratio from adjacent tiles. See [`UpdateTileAir`, lines 241-284](https://github.com/space-wizards/space-station-14/blob/eadcd567fd8ea801cb346aaed4ff44ab42b6928c/Content.Server/Atmos/EntitySystems/AtmosphereSystem.Processing.cs#L241-L284).

Interpretation: outside is a special immutable map or space mixture, not a discovered room. A closed region is represented by tile mixtures with no adjacency path to those map tiles. There is no finite search shell and no explicit proof object for “this is not outside” in the cited code.

#### Change grouping, invalidation, and partial processing

Observed code:

- `AirtightSystem` invalidates a grid tile when an airtight entity is anchored, re-anchored, moved, initialized, shut down, or has `AirBlocked` changed. `InvalidatePosition` forwards to the atmosphere system. See [`AirtightSystem`, lines 17-131](https://github.com/space-wizards/space-station-14/blob/eadcd567fd8ea801cb346aaed4ff44ab42b6928c/Content.Server/Atmos/EntitySystems/AirtightSystem.cs#L17-L131).
- `InvalidateTile` adds the coordinate to `GridAtmosphereComponent.InvalidatedCoords`. The API docs say invalid tiles are revalidated before other processing stages. See [`AtmosphereSystem.API.InvalidateTile`, lines 83-100](https://github.com/space-wizards/space-station-14/blob/eadcd567fd8ea801cb346aaed4ff44ab42b6928c/Content.Server/Atmos/EntitySystems/AtmosphereSystem.API.cs#L83-L100).
- `ProcessRevalidate` copies invalid coordinates into a current-run queue, updates tile data, refreshes adjacency and air, and trims disconnected off-grid map tiles. See [`ProcessRevalidate`, lines 50-105](https://github.com/space-wizards/space-station-14/blob/eadcd567fd8ea801cb346aaed4ff44ab42b6928c/Content.Server/Atmos/EntitySystems/AtmosphereSystem.Processing.cs#L50-L105) and [`TrimDisconnectedMapTiles`, lines 107-167](https://github.com/space-wizards/space-station-14/blob/eadcd567fd8ea801cb346aaed4ff44ab42b6928c/Content.Server/Atmos/EntitySystems/AtmosphereSystem.Processing.cs#L107-L167).
- Revalidation is time-sliced. `ProcessRevalidate` checks `AtmosMaxProcessTime`, returns false when the budget is exhausted, and the outer state machine marks processing paused. The next tick resumes the queued stage. See [`ProcessRevalidate`, lines 82-104](https://github.com/space-wizards/space-station-14/blob/eadcd567fd8ea801cb346aaed4ff44ab42b6928c/Content.Server/Atmos/EntitySystems/AtmosphereSystem.Processing.cs#L82-L104) and [`ProcessAtmosphere`, lines 686-729](https://github.com/space-wizards/space-station-14/blob/eadcd567fd8ea801cb346aaed4ff44ab42b6928c/Content.Server/Atmos/EntitySystems/AtmosphereSystem.Processing.cs#L686-L729).
- Grid startup invalidates every stored and map tile. Grid splits copy gas and pressure fields by matching coordinates, then invalidate both grids. See [`OnGridAtmosphereStartup` and `OnGridSplit`, lines 54-105](https://github.com/space-wizards/space-station-14/blob/eadcd567fd8ea801cb346aaed4ff44ab42b6928c/Content.Server/Atmos/EntitySystems/AtmosphereSystem.GridAtmosphere.cs#L54-L105).
- The cited room revalidation path is not an asynchronous snapshot transaction. It is a queued, budgeted update on the atmosphere processing state machine. The repository does have other parallel work, but no parallel room-discovery pass is shown here.

## 3. Barotrauma hull and gap model

This is a useful two-dimensional contrast, not a voxel solver. Rooms are rectangular `Hull` entities authored in submarine data. Walls and doors do not cause automatic room flood fill in the cited code.

Primary files:

- [`Hull.cs`](https://github.com/FakeFishGames/Barotrauma/blob/e6e95da83b1b5ca8b55ec52653c7cf6b40e30247/Barotrauma/BarotraumaShared/SharedSource/Map/Hull.cs)
- [`Gap.cs`](https://github.com/FakeFishGames/Barotrauma/blob/e6e95da83b1b5ca8b55ec52653c7cf6b40e30247/Barotrauma/BarotraumaShared/SharedSource/Map/Gap.cs)
- [`Submarine.cs`](https://github.com/FakeFishGames/Barotrauma/blob/e6e95da83b1b5ca8b55ec52653c7cf6b40e30247/Barotrauma/BarotraumaShared/SharedSource/Map/Submarine.cs)

Observed code:

- The `Hull` constructor receives a `Rectangle`, initializes oxygen to 100 percent, adds the object to the global `HullList`, and calls `Gap.UpdateHulls`. See [`Hull` constructor, lines 464-522](https://github.com/FakeFishGames/Barotrauma/blob/e6e95da83b1b5ca8b55ec52653c7cf6b40e30247/Barotrauma/BarotraumaShared/SharedSource/Map/Hull.cs#L464-L522).
- Submarine loading calls `MapEntity.LoadAll`, then finds all `Hull` objects belonging to the submarine. See [`Submarine` constructor, lines 1638-1705](https://github.com/FakeFishGames/Barotrauma/blob/e6e95da83b1b5ca8b55ec52653c7cf6b40e30247/Barotrauma/BarotraumaShared/SharedSource/Map/Submarine.cs#L1638-L1705). This is authored room loading, not geometry-derived room discovery.
- `Gap.FindHulls` probes with a one-unit tolerance beyond each side of the gap and calls `Hull.FindHullUnoptimized`. It links zero, one, or two hulls and adds the gap to each linked hull's `ConnectedGaps`. See [`FindHulls`, lines 316-369](https://github.com/FakeFishGames/Barotrauma/blob/e6e95da83b1b5ca8b55ec52653c7cf6b40e30247/Barotrauma/BarotraumaShared/SharedSource/Map/Gap.cs#L316-L369).
- `Gap.IsRoomToRoom` is true when `linkedTo.Count == 2`. `Gap.Update` branches to “gap leading from a room to outside” for one linked hull and “gap leading from a room to another” for two. See [`IsRoomToRoom` and gap state, lines 132-168](https://github.com/FakeFishGames/Barotrauma/blob/e6e95da83b1b5ca8b55ec52653c7cf6b40e30247/Barotrauma/BarotraumaShared/SharedSource/Map/Gap.cs#L132-L168) and [`Gap.Update`, lines 415-439](https://github.com/FakeFishGames/Barotrauma/blob/e6e95da83b1b5ca8b55ec52653c7cf6b40e30247/Barotrauma/BarotraumaShared/SharedSource/Map/Gap.cs#L415-L439).
- `Gap.Open` is a 0 to 1 openness value. Changes mark overlapping gaps dirty. With `open == 0`, `Gap.Update` stops flow, while the hull and gap topology remains linked. See [`Open` setter, lines 79-107](https://github.com/FakeFishGames/Barotrauma/blob/e6e95da83b1b5ca8b55ec52653c7cf6b40e30247/Barotrauma/BarotraumaShared/SharedSource/Map/Gap.cs#L79-L107) and [`Gap.Update`, lines 421-439](https://github.com/FakeFishGames/Barotrauma/blob/e6e95da83b1b5ca8b55ec52653c7cf6b40e30247/Barotrauma/BarotraumaShared/SharedSource/Map/Gap.cs#L421-L439).
- `Hull.GetConnectedHulls` recursively walks `ConnectedGaps` with a default search depth of 100 and an option to ignore closed gaps. See [`GetConnectedHulls`, lines 1108-1135](https://github.com/FakeFishGames/Barotrauma/blob/e6e95da83b1b5ca8b55ec52653c7cf6b40e30247/Barotrauma/BarotraumaShared/SharedSource/Map/Hull.cs#L1108-L1135).
- `Hull.FindHull` uses an `EntityGrid`, a 128-unit padding check around submarine borders, and rectangle containment. It does not prove exterior by flood fill. See [`FindHull`, lines 1215-1277](https://github.com/FakeFishGames/Barotrauma/blob/e6e95da83b1b5ca8b55ec52653c7cf6b40e30247/Barotrauma/BarotraumaShared/SharedSource/Map/Hull.cs#L1215-L1277).

Small source excerpts:

> `//gap leading from a room to outside`

> `//gap leading from a room to another`

Interpretation: Barotrauma makes the outside-versus-room distinction explicit at a gap edge. A door or gap can be closed for flow without changing which hulls it connects. This is a strong 2D precedent for separating geometric membership from openness, but its authored rectangles do not answer arbitrary 3D wall validation.

## Cross-implementation findings

These are comparisons of the observed code, not Galaxia decisions.

| Question | Space Engineers | Space Station 14 | Barotrauma |
| --- | --- | --- | --- |
| How discovery starts | Pending event triggers a full pass seeded from the expanded-grid corner | Invalidated tile coordinates are queued and revalidated | Authored `Hull` rectangles load, then gaps probe adjacent hulls |
| Exterior proof | Expanded one-cell shell. Reach shell means unpressurized | Immutable map or space mixture represented by `MapAtmosphere` and `NoGridTile` | Missing second hull means outside edge |
| Boundary representation | Per-block definition face table plus door state | Per-tile direction masks and bidirectional adjacency bits | Gap rectangle and `linkedTo` hull list |
| Shared walls and pillars | Both adjacent block faces can seal a transition. Partial blocks use transformed face data | All anchored airtight entities on a tile OR their masks. A shared face requires both sides open | Authored gaps decide links. No arbitrary voxel wall union in cited code |
| Door or opening change | Door event schedules a full oxygen pass. Opening changes face passability | `AirBlocked` change invalidates a tile | `Gap.Open` changes flow while links remain |
| Destruction | Deleted block positions are locally merged into the largest neighboring room. Additions trigger a full pass | Position is invalidated and revalidated before later stages | Hull and gap entities are updated when moved or rechecked |
| Rebuild grouping | Queue, previous arrays, postprocess, and breach pass | HashSet invalidations, current-run queues, trim queue, time budget | Global entity lists and per-gap updates |
| Async or partial world data | Background queue exists. It restarts after concurrent grid changes. No unloaded-cell state in cited file | Time-sliced state machine. No async room snapshot in cited path. Off-grid tiles are lazily created and trimmed | `Submarine.Loading` suppresses some spatial checks. No async room rebuild shown |

### Practical precedents relevant to the research question

- A finite exterior witness is concrete in the Space Engineers implementation. Its expanded shell is the cleanest source-backed precedent here for deciding “outside” versus “another closed room” in a bounded grid.
- Space Engineers keeps block-to-room indirection so merges do not iterate every block just to retarget room membership. Its full rebuild still carries oxygen forward through old and new cell maps.
- Space Engineers treats door state as face passability and pressure state, while block removal changes topology. Barotrauma makes the same separation explicit with `Gap.Open` versus `linkedTo` hulls.
- Space Station 14 shows a lighter alternative when persistent room IDs are unnecessary. Cache per-tile airtight masks and adjacency, invalidate only affected coordinates, and spread work over bounded ticks. It does not provide a room-level exterior proof.
- None of these sources implement a manual per-controller validation contract. None should be read as evidence for a Galaxia API or persistence choice.
