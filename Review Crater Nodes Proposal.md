---
type: wayfinder-ticket
ticket_type: grilling
status: resolved
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Alpha Scope]]"
secondary_areas:
  - Area - Destinations
source_file: "Discord Source - Crater Nodes Proposal.md"
blocked_by: []
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Review Crater Nodes Proposal

## Question

Does the isolated Crater Nodes Proposal define a current destination mechanic for Alpha, a later optional system, or an obsolete direction, and what complete gameplay chain would justify retaining it?

## Owner-Led Design

On 2026-09-16 the owner reopened this topic and authorized making the remaining decisions directly rather than waiting for the other developers. External designer feedback is no longer a prerequisite. This does not imply their endorsement or automatically approve every detail of either proposal.

The following preserves the owner's working crater proposal. Its differences from the original source remain explicit until resolved in discussion. Previously recorded choices should not be re-asked merely because the coordination blocker was removed.

## Accepted Crater Direction

Owner decisions on 2026-09-16 supersede conflicting parts of the original source and the earlier working proposal below.

- Add one crater-extraction machine with two operating modes rather than separate ordinary-drill and fracking-rig machines. The final machine name is not selected.
- The machine first performs ordinary mining against the crater's initial ore reserve. After that reserve is exhausted, it switches to fracking when the required fluid is supplied. Exhaustion is not bypassed merely by supplying fluid early. Without that fluid it cannot continue the fracking stage.
- Any number of extraction machines may operate on one crater. They share the crater's resource state rather than receiving independent reserves.
- Craters support a general authored deposit system, not only the three material profiles from Chloe's proposal.
- Titanium remains a separate material-processing chain and may occur in a crater. The crater feature does not require changing GTNH's titanium production chain.
- Craters are world-generation features. Their identity and extraction membership do not depend on creating a Crater biome.
- After the finite ordinary reserve is exhausted, fracking can continue indefinitely. Its fluid input per operation increases with successive fracking operations on that crater.
- The fluid-cost curve should rise gradually enough to make continued operation useful, but eventually make supplying the old site inconvenient enough that the player wants to develop a new location. There is no selected numerical curve, operation count or time threshold.
- Fracking history belongs to the crater's shared state. Several machines advance the same history rather than each starting a cheaper independent sequence.
- Fracking consumes fracking fluid and produces a resource-enriched fluid, not the ordinary-mining item output directly. Downstream processing extracts resources and recovers part of the fracking fluid for reuse. Losses require ongoing production of replacement fluid, so the chain is not a closed loop. Exact processing steps, fluid identities and recovery ratios remain undecided.
- Enriched fluid is processed in ordinary GregTech machines through their normal recipe maps. This does not select particular machines or chemical recipes yet.

## Accepted Fluid Representation

On 2026-09-16 the owner accepted one fluid family with a separate registered Fluid ID for each subtype. Variants may share definitions and behavior rather than requiring separate handwritten implementations.

This replaces the tentative single-ID subtype representation. The purpose is to distinguish variants through normal GT recipe matching and NEI browsing without relying on NBT-only identity. It does not select a universal input-fluid recipe or exact chemical variants. Verify the integration against the actual dependency versions during implementation.

## Accepted Space-Grade Alloy Direction

- Space-Grade Alloy is one canonical item, independent of which feedstock recipe produced it. Do not preserve origin as separate metadata or NBT variants.
- Different feedstock recipes produce that same item. Three recipes were the owner's example, not a permanent cap on the general deposit system.
- Production is allowed only in an atmosphere-free environment. The existing environment requirement is not satisfied merely by an artificial vacuum chamber on an atmospheric world.
- Its role is low-tech, mass-produced bulk material for space equipment and infrastructure. It is not the material that distinguishes or gates successive technology tiers. Recipes still require the appropriate other progression materials.
- This supersedes the source's proposal for three distinct, ore-dictionary-interchangeable ingots. It does not mean that every space recipe must consume this alloy or select exact compositions and yields.

## Accepted Scanner Direction

On 2026-09-16 the owner selected reuse of existing GregTech ore scanners, extending their prospecting/minimap integration to crater deposits rather than introducing a separate Galaxia scanner machine.

- To identify a crater, the scanner must be used inside that crater's geometric footprint. Its biome is not the detection criterion.
- The crater is already visible as a terrain feature, so the player can locate it and enter it before scanning.
- Scanning identifies the crater deposit and exposes its resource composition, remaining ordinary-mining reserve, fracking state and current fluid consumption per operation through the minimap integration.
- These fields were accepted on 2026-09-16. The owner subsequently assigned map-record storage and refresh behavior to the existing scanner/map integration rather than a separate Galaxia policy. The proposed scan-time-only snapshot rule was not accepted. Research the existing integration's ownership and extension requirements before selecting how crater data reaches it.
- This selects the desired integration, not a claim that GregTech already recognizes Galaxia crater deposits. No new requirement that scanning unlocks extraction follows from this decision.

## Historical Scanner Proposal

Chloe's 2026-08-02 messages describe a local investment: moving to scan another area would require investing again. The stated goal was to encourage players to work with the crater they found instead of repeatedly searching for a better one. She also answered that the player would know what the crater contains beforehand.

The supplied conversation did not establish what additional information the scanner reveals, its cost, whether extraction is blocked before scanning, or its physical form. The owner's later GregTech-scanner direction supersedes an assumed new local scanner installation. Do not import the original investment-gate proposal as an accepted requirement.

## Earlier Working Proposal

The earlier generation and shared-accounting proposal is retained for context. Its finite reserve formula applies to ordinary mining, not a cap on the subsequently accepted unlimited fracking stage.

- Each impact crater owns one shared Crater Deposit, even when its footprint crosses chunk boundaries. Its ordinary-mining reserve is finite. Fracking then continues without a reserve cap, at increasing fluid cost.
- Every eligible extractor inside the crater uses that same deposit state.
- Crater membership is defined by the crater's geometric footprint rather than by chunk ownership.
- The crater system indexes each crater under every chunk intersected by its footprint. This chunk index only narrows the lookup to candidate Crater IDs; an exact footprint-containment check determines whether the machine is inside a candidate crater.
- A machine performs this spatial lookup once when it first binds to a crater, then persistently remembers the resolved Crater ID. Normal extraction does not repeat the geometric check.
- For a circular footprint, exact containment is equivalent to comparing squared horizontal distance from the crater center with the squared crater radius. A later non-circular footprint may replace that test without changing the candidate-index or machine-binding model.
- Craters use three authored Size Classes: `Small`, `Medium`, and `Large`.
- Each destination defines an independent occurrence weight for every Crater Size Class.
- Each Size Class defines a mean diameter and standard deviation rather than a fixed diameter or hard size interval.
- Diameter is sampled from the class's normal distribution. The three distributions may overlap, so physical diameter does not uniquely identify the originating Size Class.
- The working Moon means are approximately one chunk for `Small`, three chunks for `Medium`, and eight chunks for `Large`; their standard deviations remain tuning values.
- Each Crater Material Profile defines an independent generation weight for every Size Class.
- A weight of `0` makes that material profile ineligible for the named Size Class; positive weights are selected proportionally among the eligible profiles.
- Generation first selects a Size Class from the destination's class weights, then samples its physical diameter, and finally selects a Crater Material Profile from that class's material weights.
- Realized diameter is a result of the selected Size Class and never reclassifies the crater or changes which material-weight table it uses.
- Every Crater Deposit has Richness derived from two inputs: its realized diameter relative to the mean of its originating Size Class, and an authored size-response value on its Crater Material Profile.
- The material size response may dampen or amplify the size-derived change so rare materials do not inherit the same reserve growth as bulk materials.
- As a working example, a crater receiving a `+50%` size-derived change with a material size response of `0.1` receives only `+5%` Richness from size.
- An illustrative, replaceable Richness calculation discussed with the owner is:
  - `baseReserve = sizeClassBaseReserve * materialReserveMultiplier`
  - `sizeChange = actualDiameter / classMeanDiameter - 1`
  - `richnessChange = sizeChange * materialSizeResponse`
  - `richnessMultiplier = 1 + richnessChange`
  - `totalReserve = baseReserve * richnessMultiplier`
- `sizeClassBaseReserve` defines the average reserve scale of the selected Size Class.
- `materialReserveMultiplier` belongs to the selected Crater Material Profile and controls that material's baseline abundance before size-derived Richness is applied.
- `materialSizeResponse` separately controls how strongly that material reacts to above- or below-mean realized diameter.
- `materialSizeResponse` may be positive, zero, or negative. A negative value reverses the size relationship: above-mean diameter reduces Richness while below-mean diameter increases it.
- Authored values must keep `richnessMultiplier` positive for valid generated craters.
- The formula is intentionally replaceable balance policy and may evolve without changing Crater Deposit identity, generation order, or extraction ownership.
- Multiple extractors may operate inside one crater, but the Crater Deposit remains the single authority for remaining reserve, cumulative depletion, and depletion-dependent extraction cost.
- A crater imposes no artificial limit on the number of installed or simultaneously active extractors.
- Additional extractors increase aggregate throughput but do not duplicate any defined crater reserve. Their practical constraints are physical space, machine capital, energy, processing capacity, logistics, and any accepted depletion-dependent costs.
- Fracking operations receive successive positions in the crater's shared fracking history. Concurrent extractors cannot all consume the same cheaper operation step.
- Fracking fluid cost follows that shared operation history, not a drill-local counter or a fresh history created when a machine is replaced.
- Drills do not require peer-to-peer coordination; they coordinate by claiming work from the shared Crater Deposit authority.
- At operation start, ordinary mining claims its finite resource batch. Fracking instead claims the next shared cost step. The next extractor observes the updated state even if the first operation has not completed.
- This is a sequencing invariant, not a requirement for multithreaded execution, locks, or a particular technical synchronization mechanism. Sequential server-tick execution is sufficient when the cost calculation and reservation occur together.
- For ordinary mining, the claimed deposit portion is permanently deducted when the operation starts. The system does not roll it back into the crater.
- The started operation persistently records the claimed material batch, its depletion-dependent cost, and its progress. Resuming that same operation never claims or deducts the batch again.
- Successful completion produces output from the recorded operation and does not debit its reserve or cost step a second time.
- Normal interruption such as loss of power or chunk unloading pauses the persisted machine operation. Destroying or explicitly discarding the in-progress operation loses its already claimed deposit portion and consumed inputs.
- This bounded loss is an accepted simplification because a single operation consumes only a small fraction of a crater's total reserve.
- The concrete builder API, persistence layout, and spatial-index data structure are not Wayfinder decisions.

## Resolution

Crater extraction is retained as an Alpha gameplay chain under the owner's revised design. One extractor uses a shared finite reserve, then unlimited fracking with progressively increasing fluid cost. Enriched-fluid processing uses normal GT recipe maps and recovers only part of the input fluid. Registered fluid variants have distinct IDs within one family. Existing scanners and map integration expose crater composition and extraction state. Space-Grade Alloy remains one vacuum-produced bulk-material item rather than a tier gate.

This resolves the proposal review, not implementation or numerical balancing. Conflicting source proposals are superseded only where explicitly stated above. Earlier working generation values remain provisional.

## Remaining Content And Integration Work

- The concrete enriched-fluid processing chain, required fracking fluids and partial recovery ratios.
- Verify the accepted registered-fluid variants with normal GT recipe maps and subtype-specific NEI browsing in the target dependency versions.
- The scanner/map integration's existing data ownership and extension requirements. This is an integration investigation, not another gameplay vote on map refresh policy.
- Standard deviation for each Size Class.
- Concrete deposit profiles, output forms, processing recipes and fracking consumables. Exact quantities and generation tuning remain balance work.

The one-machine transition, unlimited fracking with increasing fluid cost, enriched-fluid output with partial fluid recovery, canonical alloy item and scanner information are settled. Do not reopen them while choosing processing recipes and numerical balance. The separately resolved Data Processor design is owned by [[Define Data Processor Machine Topology]].
