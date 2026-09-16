---
type: wayfinder-ticket
ticket_type: grilling
status: blocked
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

## Owner Proposal Pending Designer Reconciliation

The following is the owner's working crater proposal. It has not been reconciled with Chloe's design. Keep its concepts and requirements as proposal material while this ticket remains blocked. The conversation already contains later Chloe replies, so the blocker is clarification and reconciliation, not a claim that no reply was received.

## Working Proposal

- Each impact crater owns one finite Crater Deposit, even when its footprint crosses chunk boundaries.
- Every eligible extractor inside the crater draws from the same remaining reserve.
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
- Additional extractors increase aggregate throughput but never increase the deposit's total reserve. Their practical constraints are physical space, machine capital, energy, processing capacity, logistics, and faster progression into more expensive depletion steps.
- Every extraction operation receives a unique position in the deposit's global depletion sequence. Concurrent extractors cannot all consume the same cheaper depletion step.
- Depletion-dependent inputs such as fracking fluid are calculated from the operation's assigned global depletion position, not from a drill-local counter or an independently cached deposit snapshot.
- Drills do not require peer-to-peer coordination; they coordinate by claiming work from the shared Crater Deposit authority.
- At operation start, an extractor determines its depletion-dependent cost and reserves the corresponding deposit portion as one indivisible domain action. The next extractor therefore observes the next depletion position even if the first operation has not completed.
- This is a sequencing invariant, not a requirement for multithreaded execution, locks, or a particular technical synchronization mechanism. Sequential server-tick execution is sufficient when the cost calculation and reservation occur together.
- The claimed deposit portion is permanently deducted when the operation starts; the system does not roll it back into the crater.
- The started operation persistently records the claimed material batch, its depletion-dependent cost, and its progress. Resuming that same operation never claims or deducts the batch again.
- Successful completion produces output from the operation's recorded batch and does not mutate Crater Deposit depletion a second time.
- Normal interruption such as loss of power or chunk unloading pauses the persisted machine operation. Destroying or explicitly discarding the in-progress operation loses its already claimed deposit portion and consumed inputs.
- This bounded loss is an accepted simplification because a single operation consumes only a small fraction of a crater's total reserve.
- The concrete builder API, persistence layout, and spatial-index data structure are not Wayfinder decisions.

## Still Open

- Reconcile the owner's proposal with Chloe and the other responsible developer. Recorded replies discuss different generation and progression assumptions. Confirm the extraction-pool and fracking-cost contract without assuming that the existing proposal has their agreement.
- Standard deviation for each Size Class.
- Standard drilling, enhanced recovery, processing-consumable, and exhaustion behavior.
