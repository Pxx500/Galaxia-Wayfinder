---
type: source
status: reviewed
tags:
  - galaxia/alpha
  - wayfinder/source
---

# Station Construction Pathfinding Research

Source: first-party algorithm papers and author-maintained reference implementations, with the Galaxia station construction contract as the problem context
Imported: 2026-09-13

[[Sources]]

## Source Snapshot

### Problem context

The station construction graph has one vertex per traversable construction block and an edge for each face-adjacent move. That gives at most six neighbors per vertex. A witness starts at the main controller and joins every functional device. When adding a device, the route may end at any marked block in the existing connected witness. Only a path-membership marker is retained in runtime construction data, not persisted to disk. Removing a marked block invalidates the witness and causes a complete rebuild, so persistent parent pointers and dynamic tree repair are not required.

The important distinction is between the next route and the whole witness. A shortest route to the current witness is a local objective. The union of all selected routes is only a heuristic witness. It is not a minimum Steiner tree or a minimum spanning tree requirement.

### 1. Amit Patel, Heuristics

URL: https://theory.stanford.edu/~amitp/GameProgramming/Heuristics.html

This is an author-maintained explanation of A* heuristics. Relevant excerpts:

> “The heuristic function `h(n)` tells A* an estimate of the minimum cost from any vertex `n` to the goal.”

> “If `h(n)` is always lower than (or equal to) the cost of moving from `n` to the goal, then A* is guaranteed to find a shortest path.”

> “If you want to search for any of several goals, construct a heuristic `h'(x)` that is the minimum of `h1(x), h2(x), h3(x), ...` where `h1, h2, h3` are heuristics to each of the nearby spots.”

> “If you want to search for paths to all of several goals, your best option may be Dijkstra’s Algorithm with early exit when you find all the goals.”

Application to a six-neighbor unit-cost grid:

* For target set `T`, use `h(v) = min(distance_lower_bound(v, t) for t in T)`. The Manhattan lower bound for one target is `|dx| + |dy| + |dz|`. It is admissible and consistent when every face move costs one. The pointwise minimum of these per-target bounds remains admissible.
* A direct implementation that scans every marked block for every heuristic call costs `O(|T|)` per expanded node. This is an inference from the formula, not a free property of A*. A target index, a conservative bounding-box lower bound, or a different search direction can reduce that overhead, but each option needs its own correctness and update analysis.
* A* with a binary heap has a worst-case search cost of `O((N_r + E_r) log N_r)` and `O(N_r)` search memory, where `N_r` and `E_r` are the vertices and edges examined in the reachable search region. With degree at most six, `E_r <= 6N_r`, so this is `O(N_r log N_r)`. The usual worst case still expands essentially the whole reachable component.
* This formulation optimizes one new route to any current witness block. Repeating it for `k` devices can cost `O(kN_r log N_r)` in a worst-case rebuild. It does not optimize the total number of marked blocks.

### 2. Red Blob Games, multi-source BFS and weighted search

Multi-source BFS: https://www.redblobgames.com/pathfinding/distance-to-any/

The page explicitly generalizes the method beyond square grids:

> “Running Breadth First Search with multiple start points can do some cool things.”

> “The ideas here are a modification of the algorithm presented there. Note that even though the demos on this page use a square grid, none of these algorithms is limited to only square grids, or even to grids.”

Its source setup and expansion are:

```text
frontier = Queue()
cost_so_far = dict()
for location in start:
    frontier.put(location)
    cost_so_far[location] = 0
while not frontier.empty():
    current = frontier.get()
    for next in current.neighbors():
        if next not in cost_so_far:
            cost_so_far[next] = cost_so_far[current] + 1
            frontier.put(next)
```

For this station, put every marked witness block in `start`, and stop when the new device anchor is dequeued or first discovered. Because the construction graph is undirected, this reverse wave is exactly a shortest path to any marked block. Store transient predecessors while searching, trace the route, set the one-bit markers, and discard the predecessor map.

With `N_r` examined vertices and `E_r` examined edges, BFS costs `O(N_r + E_r)` time and `O(N_r + |T|)` memory. The six-neighbor bound makes both linear in `N_r` for a bounded search region. A successful search can stop when the wave reaches the new device. A disconnected device or a failed search may require exhausting its entire reachable component. A U-shaped corridor can therefore approach full-component work even though the Manhattan distance is small. No algorithm here promises to avoid whole-component exploration in arbitrary mazes.

The companion implementation page is https://www.redblobgames.com/pathfinding/a-star/implementation.html. It shows the weighted extension and warns:

> “once we add movement costs it’s possible to visit a location again, with a better `cost_so_far`.”

It implements Dijkstra with a priority queue and a decrease-in-cost check. A multi-source version initializes every target with distance zero and exits when the source is settled. With a binary heap its conventional bound is `O((N_r + E_r) log N_r)` time and `O(N_r)` memory. This is the appropriate exact variant if construction moves have positive nonuniform costs.

For a complete rebuild, one BFS from the main controller can compute a shortest-path tree to every reachable functional device. Tracing and unioning those parent paths gives one connected witness in `O(N + E)` time for the component if each trace stops at an already marked path. Repeatedly retracing common ancestors would lose that bound. This optimizes each device’s distance to the controller, not the total marker count and not necessarily the next-device-to-current-witness heuristic. Sequential multi-source searches can favor shorter attachments to already selected branches at the cost of more searches.

### 3. Harabor and Grastien, Online Graph Pruning for Pathfinding on Grid Maps

AAAI landing page: https://ojs.aaai.org/index.php/AAAI/article/view/7994

Open PDF: https://ojs.aaai.org/index.php/AAAI/article/download/7994/7853

The paper states:

> “Pathfinding in uniform-cost grid environments is a problem commonly found in application areas such as robotics and video games.”

> “The state-of-the-art is dominated by hierarchical pathfinding algorithms which are fast and have small memory overheads but usually return suboptimal paths.”

> “Our algorithm can be described as a macro operator which identifies and selectively expands only certain nodes in a grid map which we call jump points.”

> “Jump point pruning is fast, requires no preprocessing and introduces no memory overheads.”

Its notation fixes the domain used by the proof:

> “We work with undirected uniform-cost grid maps. Each node has <= 8 neighbours and is either traversable or not.”

The paper reports that jump points can speed up A* “by an order of magnitude and more” on its benchmarks. That is an empirical result, not an asymptotic worst-case bound. The paper also lists extending jump points to other grids, including hexagons, as future work. It gives no 3D six-neighbor proof or implementation.

Implications for station construction:

* Standard JPS assumes uniform edge costs, a static undirected grid, and directional path symmetry. The published rules are for a two-dimensional eight-neighbor setting with straight and diagonal moves, not a six-neighbor 3D graph.
* JPS can skip long symmetric runs in open space. A sparse solid-wall station has narrow corridors, wall-adjacent movement, and frequent forced turns. In those areas many cells become jump points, so the gain can approach ordinary A* while the 3D pruning rules remain an additional implementation surface.
* The no-preprocessing property is attractive when a marked-block removal triggers a rebuild. It does not remove the need to benchmark open rooms, one-block corridors, U-shaped detours, and disconnected fragments. The safe worst-case assumption remains `Theta(N_r)` expanded cells and `O(N_r)` search memory.
* A 3D JPS variant should be treated as an experiment requiring a proof or focused regression tests. This source set is not evidence to select it for production.

### 4. HPA* reference implementation and preprocessing tradeoff

University of Alberta pathfinding page: https://www.cs.ualberta.ca/~games/pathfind/

Reference implementation archive: https://www.cs.ualberta.ca/~games/pathfind/hpa.tgz

The University of Alberta page exposes “Download HPA*”. The archive is a first-party reference implementation. Its `HPA/abstiling.cpp` has `computeClusterPaths()`, which loops over clusters and calls each cluster’s internal path computation. Its `HPA/htiling.cpp` has a `// building hierarchy` phase that runs A* searches between entrance nodes and adds hierarchical edges, followed by a `// hierarchical search` phase that searches the abstract graph and refines each abstract edge at lower levels.

The code gives a useful cost model, although it does not state a general theorem. Let `C` be the cluster count, `b_c` the number of entrances in cluster `c`, and `S_c` the cost of one local search in that cluster. The entrance-pair preprocessing is approximately `O(sum_c b_c^2 S_c)` in the reference structure. An abstract query then costs `O((A + E_A) log A)` for `A` abstract nodes and `E_A` abstract edges, plus local refinement work. These are implementation-derived bounds, not claims made by the source.

HPA* is therefore useful only when preprocessing can be amortized over many route queries on unchanged topology. A station rebuild can amortize it if one hierarchy serves many devices. Frequent construction edits or a small station can make direct BFS or A* cheaper and easier to reason about. Portal abstraction can also return a longer path, which is acceptable only if the witness requirement remains heuristic shortness rather than exact shortest total length. Any 3D hierarchy would need face portals along all three axes and explicit handling for narrow U-shaped passages.

## Comparison for the station contract

| Method | Next route to any marked block | Whole witness rebuild | Preprocess and memory | 3D six-neighbor fit |
| --- | --- | --- | --- | --- |
| A* with `min` Manhattan heuristic | Exact shortest route if the set heuristic is admissible. Naive set scan adds `O(|T|)` per expansion. | Repeat per device, or use one controller-rooted tree as a simpler approximation. | No preprocess. `O(N_r)` search memory. | Direct and easy for unit costs. |
| Multi-source BFS | Exact shortest route to the target set. Stops when the source is reached. | One controller-rooted flood can serve all reachable devices, then parent paths are unioned. | No preprocess. `O(N_r + E_r)` time and `O(N_r)` memory. | Direct. Six neighbors are just the neighbor iterator. |
| Multi-source Dijkstra | Exact weighted shortest route to the target set. | Same whole-rebuild pattern with positive movement costs. | No preprocess. `O((N_r + E_r) log N_r)` with a binary heap. | Direct if costs are explicit. |
| HPA* | Fast abstract route after preprocessing, often near-optimal rather than exact. | Potentially amortizes one hierarchy across many devices. | Entrance and intra-cluster data consume extra memory. Rebuild or invalidate after topology edits. | Conceptually general, but the cited implementation is 2D and needs a real 3D design. |
| Standard JPS | Exact on its published domain, with strong empirical speedups on symmetric uniform grids. | No preprocess, but 3D rules are unverified. | Low extra memory. | Not established. Sparse corridors may erase its benefit. |

## Findings and gaps

1. For unit-cost construction, BFS is a simple exact next-route search for the accepted “attach to any marked block” rule. It can start at the new device and stop on reaching any marked block, using constant-time marker membership checks. Alternatively, reverse multi-source BFS seeds the existing witness, but initialization costs at least `O(|T|)`. Which direction visits fewer blocks depends on the layout and the number of queries. Neither needs a full target-set scan at every expansion.
2. A* is a good alternative when a cheap admissible lower bound is useful and the implementation wants goal-directed expansion. The minimum-of-target heuristic is valid, but a naive `O(|T|)` target scan must be counted.
3. A complete rebuild can use one transient controller-rooted BFS or Dijkstra and then mark the union of parent paths for all functional devices. Sequential target-set searches better express “nearest existing witness” but can cost one search per device. Neither construction is a minimum-total-length Steiner solution.
4. Do not promise that any method avoids whole-component exploration. Disconnected targets and U-shaped or maze-like corridors can force that work to prove failure or reach a distant route.
5. HPA* is a conditional optimization for large stations or many queries per unchanged topology. It adds portal data and invalidation complexity, and its preprocessing must be amortized.
6. The cited JPS paper does not establish a 3D six-neighbor variant. Treat 3D JPS as an optional benchmarked experiment, not as a source-backed default.

Open implementation questions are the maximum construction volume, whether all moves are unit cost, the exact device-to-block anchor rule, deterministic tie-breaking, and how unloaded chunks participate in a rebuild. Those choices determine whether direct BFS, Dijkstra, or A* is the right default and whether hierarchy preprocessing can pay back its cost.
