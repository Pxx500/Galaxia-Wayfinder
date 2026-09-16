---
type: source
status: reviewed
tags:
  - galaxia/alpha
  - wayfinder/source
---

# Voxel Room Detection Algorithms Research

Source: Primary algorithm documentation and source repositories listed below
Imported: 2026-09-13

## Source Snapshot

This note records evidence for exact enclosed-room detection in a finite 3D voxel snapshot. The working model is a graph whose vertices are traversable air voxels and whose edges join face-sharing voxels only. Let `N` be the number of voxels in the finite snapshot, `A` the traversable voxels considered by one search, `E` the corresponding 6-face edges, `C` one searched component, `R` a number of lossless row or slice runs, and `K` the number of voxels covered by those runs. For a 6-face grid, the undirected edge count is bounded by `E <= 3N`, so a graph bound of `O(V + E)` becomes linear in the voxel count when the domain is finite and the degree is fixed.

### SciPy connectivity contract

Source URL: <https://docs.scipy.org/doc/scipy/reference/generated/scipy.ndimage.generate_binary_structure.html>

Faithful source excerpt:

> `connectivity` determines which elements of the output array belong to the structure, i.e., are considered as neighbors of the central element. Elements up to a squared distance of `connectivity` from the center are considered neighbors. `connectivity` may range from 1 (no diagonal elements are neighbors) to `rank` (all elements are neighbors).

For a rank-3 array, connectivity 1 therefore gives the six face neighbors and excludes edge and corner contact. The page does not state a time or memory complexity. This is an adjacency contract, not a room-detection algorithm. Exactness is relative to the supplied structuring element.

Related API source URL: <https://docs.scipy.org/doc/scipy/reference/generated/scipy.ndimage.label.html>

Faithful source excerpt:

> Any non-zero values in `input` are counted as features and zero values are considered the background.

> A structuring element that defines feature connections.

> An integer ndarray where each unique feature in `input` has a unique label in the returned array.

This establishes the standard connected-component labeling contract. It also allows an explicit six-face structure instead of relying on a default. The page gives no asymptotic bound.

### SciPy exterior-boundary hole fill

Source URL: <https://docs.scipy.org/doc/scipy/reference/generated/scipy.ndimage.binary_fill_holes.html>

Faithful source excerpt from the Notes section:

> The algorithm used in this function consists in invading the complementary of the shapes in `input` from the outer boundary of the image, using binary dilations. Holes are not connected to the boundary and are therefore not invaded. The result is the complementary subset of the invaded region.

The parameter warning is also material:

> large-size elements make computations faster but may miss holes separated from the background by thin regions.

This is an exact boundary-reachability definition for a finite input and a chosen structuring element. A cross-shaped rank-3 structure preserves six-face semantics. A larger footprint changes the adjacency and can skip a thin wall, so it is not a safe substitute when one-voxel leaks matter. SciPy does not state a complexity bound for this operation. Its dilation implementation and stopping cost are outside the documented contract.

### Boost Graph breadth-first search

Source URL: <https://www.boost.org/doc/libs/1_84_0/libs/graph/doc/breadth_first_search.html>

Faithful source excerpts:

> BFS uses two data structures to to implement the traversal: a color marker for each vertex and a queue.

> The time complexity is `O(E + V)`.

The source defines `V` as graph vertices and `E` as graph edges. Model each known air voxel as a vertex and add an edge only for a shared face. A finite exterior shell or all voxels touching the finite box boundary can be the BFS source set. The result is exact reachability, not a heuristic. Under a fixed six-neighbor degree, one search costs `O(A + E)` and therefore `O(A)` in the worst case. The color map and queue require `O(A)` auxiliary memory in the worst case. A seed search can stop as soon as it reaches the exterior, while a sealed component may visit all `C` voxels in that component.

### cc3d 3D connected-component implementation

Primary source URL: <https://raw.githubusercontent.com/seung-lab/connected-components-3d/master/README.md>

The project documents all three common 3D connectivities:

> `connectivity = 6`  # only 4,8 (2D) and 26, 18, and 6 (3D) are allowed

Its algorithm description says that it raster scans, assigns provisional labels, records adjacent-label equivalences, and relabels in a second pass. The implementation is a two-pass connected-component labeler with union-find path compression. This is exact for the binary or multilabel input and the selected connectivity. It is not a heuristic segmentation method.

The source gives an explicit memory accounting statement:

> The union-find data structure plus the output labels means the memory consumption will be input + output + rank + equivalences. If your input labels are 32-bit, the memory usage will be 4x the input size.

The README does not claim an asymptotic time bound. Two full raster passes imply a derived `O(N)` scan cost for a fixed neighborhood, but union-find work and allocation details are implementation-dependent. The stated 10 to 20 percent and approximately 50 percent improvements for some 4 and 6-connected decision-tree cases are measurements on the author's data, not complexity guarantees.

The implementation source is separately inspectable at <https://raw.githubusercontent.com/seung-lab/connected-components-3d/master/cc3d/cc3d.hpp>. Its opening comment states:

> Implments a 3D variant of the two pass algorithim by Rosenfeld and Pflatz augmented with Union-Find and a decision tree influenced by the work of Wu et al.

> We also use a decision tree that aims to minimize the number of expensive unify operations and replaces them with simple label copies when valid.

The implementation also accepts precomputed row spans. The first raster pass reads `xstart = runs[row << 1]` and `xend = runs[(row << 1) + 1]`, then scans only that interval. The second pass uses the same run limits. This is evidence for a lossless run-limited raster optimization, not a stated span-flood-fill complexity theorem. If runs are complete, a derived cost is proportional to `R` plus `K` and the cross-run equivalence checks. The source does not state that bound.

## Algorithm comparison for Galaxia

| Method | Exactness and reachability | Initial manual Validate cost | Auxiliary memory | Leaks, pillars, and neighboring enclosures |
| --- | --- | --- | --- | --- |
| Seeded 6-face BFS | Exact graph reachability under a complete finite snapshot and explicit six-face edges | `O(C + E_C)`, derived from Boost's `O(V + E)`. Can stop on first exterior reach | `O(C)` queue and visited state in the worst case | A one-voxel tunnel is found. Diagonal contact is not a leak. Pillars and arbitrary shapes need no special cases. |
| Exterior BFS plus complement | Exact if the finite box has a proven exterior shell or boundary seed set. Unvisited traversable voxels belong to enclosed components | `O(A + E)` for the searched air domain, worst case linear in the snapshot | `O(A)` color map and queue, plus the output mask if retained | Classifies exterior versus enclosed air. Distinct enclosed rooms still need component labeling or separate seed searches. A missing wall or long narrow leak joins the exterior component and is detected. |
| Whole-grid CCL, cc3d style | Exact labeling under selected 6, 18, or 26 connectivity | Derived two-pass scan cost `O(N)` for fixed masks. The source does not state this asymptotic bound | Explicit source statement is input + output + rank + equivalences, about 4x input for 32-bit labels | Labels every component, which is useful when several rooms share a station. Do not use 26-connectivity when corners must remain sealed. |
| Run or span scanning | Exact only when runs are lossless and all six-face overlaps across adjacent rows and slices are checked | Derived cost near `O(R + K)` plus overlap checks. The cc3d source demonstrates run-limited raster passes but states no complexity | Run metadata plus labels. Exact size depends on `R` and output representation | Reduces per-voxel loop overhead in long uniform rows. It does not change global reachability, so narrow leaks and pillars still require correct overlap tests. |
| Hierarchical chunk or octree skipping | Potentially exact only with conservative uniform-node tests and explicit face connectivity at node boundaries | Could skip large proven-uniform regions, but no authoritative 3D room-flood-fill bound was verified in this pass | Tree nodes and frontier state, with size dependent on the hierarchy and obstacle surface | Useful for large cached stations. Never classify an unloaded or unknown node as empty. A node containing a possible leak must be refined. |

The local count of adjacent air voxels or neighboring room IDs is not a connectivity test. Two layouts can have the same six local counts while one contains a long face-connected tunnel to the exterior and the other is sealed. Counts also cannot distinguish a boundary to a second enclosed room from a boundary to the exterior. A component search or equivalent global reachability proof is required for arbitrary shapes.

## Galaxia-specific implications

1. Use an immutable, finite station snapshot as the algorithm input. Do not read live Minecraft world state during geometry validation.
2. Add a proven exterior shell or a boundary seed set around the cached station domain. A finite box with no exterior convention cannot distinguish an enclosed cavity from the unmodeled outside.
3. Represent unloaded chunks as `unknown`. If a possible path reaches unknown data or the snapshot edge without a proven shell, return an incomplete or indeterminate result rather than a valid room.
4. Apply six-face connectivity consistently to air traversal and to the sealing-boundary certificate. Edge and corner contact must not open a room when six-face semantics are intended.
5. A validated room can retain a certificate of the sealing blocks or faces used by the snapshot. Destruction of a known certificate member can invalidate immediately. Rebuilding still requires a new manual Validate, as requested. This is a domain invalidation optimization, not a different geometry algorithm.
6. Airlock opening belongs to the pressurization state machine. It must not mutate the geometric room component or turn a valid enclosure into an invalid one by itself.

## Evidence gaps and bounded leads

- No accessible primary source with a stated asymptotic bound for a 3D six-face run-length or span flood fill was verified here. The cc3d source only demonstrates run-limited raster passes and does not state a bound.
- No accessible primary source with a stated exact complexity for octree or hierarchical exterior flood fill was verified here. Any `O(number of tree nodes)` or surface-sensitive claim would need a precise tree model and a source.
- SciPy documents the exterior-boundary algorithm but does not state its time or memory complexity. Do not silently assign it the Boost BFS bound unless the implementation is changed to an explicit queue-based BFS.
- Candidate papers were identified but not used as evidence because full text was unavailable in this pass: <https://doi.org/10.1016/0031-3203(91)90018-z> (linear octree CCL), <https://doi.org/10.3724/SP.J.1087.2008.03150> (run-length CCL), and <https://doi.org/10.21236/ADA076130> (quadtree CCL).

[[Sources]]
