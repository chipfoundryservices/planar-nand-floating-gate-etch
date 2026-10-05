# Chapter 5: Hard Mask Strategy for Multi-Layer Floating Gate Stacks

## Executive Summary

A hard mask's job sounds simple — survive the etch long enough to protect what is beneath it, in the pattern photolithography defined. For a floating gate stack spanning silicide, two polysilicon layers, and an ONO dielectric, "survive the etch" means surviving five distinct process chemistries in sequence, each with different mask erosion behavior, without losing so much thickness or so much critical dimension that the pattern transferred to the bottom of the stack no longer matches the pattern intended at the top. This chapter develops hard mask material selection, multi-layer mask strategies, and the selectivity budget that must be planned across the entire etch sequence — not optimized chemistry by chemistry in isolation.

---

## Part 1: Why Photoresist Alone Is Insufficient

### 1.1 The Thickness and Selectivity Problem

Photoresist is consumed during plasma etch at a rate that depends on chemistry, ion energy, and photoresist formulation, typically expressed as an etch selectivity ratio (target film etch rate divided by photoresist etch rate). For a single-layer etch (etch through one material, stop on another), adequate photoresist selectivity and starting thickness is usually achievable directly. For a stack etch spanning silicide, two polysilicon layers, and ONO — potentially 200–350 nm of total film thickness depending on generation — the cumulative photoresist consumption across all steps, combined with the comparatively aggressive thinning rates fluorocarbon-based ONO chemistries can exhibit on organic photoresist, frequently exceeds what a lithographically-achievable photoresist thickness (itself bounded by depth-of-focus and resolution requirements at advanced pitch) can supply.

### 1.2 The Resolution Problem

Separately, and often more restrictively at advanced nodes, achievable photoresist thickness is bounded from above by lithographic resolution requirements — thick resist degrades depth of focus and CD control at fine pitch. This means the photoresist thickness available for a given technology node's minimum feature size may be set by lithography constraints entirely independent of what the etch sequence would ideally want for its own selectivity and erosion budget. A hard mask exists specifically to decouple these two constraints: a thin, lithographically-compatible photoresist pattern is transferred into a separate hard mask material with better, chemistry-appropriate etch selectivity, and it is the hard mask — not the photoresist — that survives the subsequent, more demanding stack etch steps.

---

## Part 2: Hard Mask Material Options

### 2.1 Deposited Oxide Hard Mask

A deposited silicon oxide (commonly via plasma-enhanced CVD) hard mask offers good selectivity against halogen-based polysilicon and silicide etch chemistries (Chapter 6), since oxide etches comparatively slowly in HBr/Cl₂-dominant plasmas. It offers markedly *worse* selectivity during the ONO breakthrough step (Chapter 7), however, because that step's fluorocarbon-based chemistry is specifically designed to etch oxide (and nitride) efficiently — an oxide hard mask is chemically similar to part of the stack it is meant to protect against during that specific step. This mismatch is a central reason single-material oxide hard masks are frequently inadequate for the full floating gate sequence on their own.

### 2.2 Deposited Nitride Hard Mask

Silicon nitride hard masks offer the converse tradeoff: generally good resistance to halogen-based polysilicon/silicide chemistries, but, like oxide, nitride is also a target material during ONO breakthrough, producing the same fundamental mismatch, since the ONO stack itself contains nitride.

### 2.3 Amorphous Carbon Hard Mask

Amorphous carbon (sometimes called advanced patterning film or similar trade names depending on supplier) hard masks offer a materially different approach: a carbon-based film that etches via oxygen-dominant chemistry, distinct from both the halogen chemistry used for polysilicon/silicide and the fluorocarbon chemistry used for oxide/nitride. Because its removal mechanism is orthogonal to both of the stack's main etch chemistries, amorphous carbon can offer good selectivity across the *entire* sequence — good resistance in both the halogen and fluorocarbon regimes — at the cost of requiring its own dedicated deposition and patterning integration (typically via a thin oxide or nitride "cap" hard mask used to transfer the lithographic pattern into the carbon layer first, since carbon's optical properties and inorganic hard mask compatibility often make direct resist-on-carbon patterning less straightforward than resist-on-oxide or resist-on-nitride).

### 2.4 Multi-Layer Hard Mask Stacks

In practice, advanced-node floating gate processes frequently use a multi-layer hard mask stack rather than any single material — for example, a thin oxide or nitride "cap" layer (itself patterned by photoresist) on top of a thicker amorphous carbon layer, which in turn is the mask that survives the bulk of the stack etch. This is directly analogous to the overall floating gate stack problem this book addresses: a multi-material sandwich chosen so that no single material has to simultaneously satisfy every etch chemistry's selectivity requirement.

| Hard Mask Option | Good Selectivity Against | Poor/Marginal Selectivity Against | Typical Role |
|-------------------|----------------------------|--------------------------------------|---------------|
| **Deposited oxide** | Halogen (poly/silicide) chemistries | Fluorocarbon (ONO) chemistries | Cap layer for carbon hard mask, or sole mask at relaxed pitch |
| **Deposited nitride** | Halogen (poly/silicide) chemistries | Fluorocarbon (ONO) chemistries; also chemically similar to ONO's nitride layer | Cap layer alternative to oxide |
| **Amorphous carbon** | Both halogen and fluorocarbon chemistries (oxygen-based removal is orthogonal to both) | Oxygen-containing chemistry steps, if any are used elsewhere in the flow | Primary bulk mask for the full stack sequence at advanced nodes |

---

## Part 3: Selectivity Budgeting Across the Full Sequence

### 3.1 Why Chemistry-by-Chemistry Optimization Is Insufficient

A hard mask selectivity ratio measured against a single chemistry in isolation does not predict whether the mask survives the full sequence, because mask thickness consumed in step 1 is not available in step 5 — erosion is cumulative. A hard mask strategy must be budgeted end-to-end: starting mask thickness (bounded by what can be lithographically patterned and by hard-mask-open etch time, Part 4 below) must exceed the sum of thickness consumed across every subsequent step, with margin for process variation, or late-in-sequence steps (typically floating gate polysilicon etch and the soft-landing overetch, Chapter 8) will erode through the mask and begin attacking whatever underlying film or topography is exposed — frequently in a spatially non-uniform way correlated with pattern density (Chapter 12), making the resulting damage harder to detect and characterize than a uniform, predictable mask failure would be.

### 3.2 Illustrative Selectivity Budget

The following table illustrates (with representative, non-manufacturer-specific figures) how a cumulative mask erosion budget might be planned across the sequence for an amorphous carbon primary hard mask:

| Etch Step | Approx. Film Thickness Etched | Illustrative Mask:Film Selectivity | Illustrative Mask Consumed |
|-----------|-------------------------------|--------------------------------------|------------------------------|
| Silicide/metal cap etch | 60 nm | 3:1 | 20 nm |
| Control gate polysilicon etch | 80 nm | 4:1 | 20 nm |
| ONO breakthrough | 12 nm (oxide-equivalent) | 2:1 | 6 nm |
| Floating gate polysilicon etch + soft landing | 80 nm | 3.5:1 | ~25 nm |
| **Cumulative mask consumption** | — | — | **~71 nm** |

A hard mask starting thickness must exceed this cumulative figure with margin (commonly 20–40% additional, to accommodate across-wafer and lot-to-lot process variation), meaning a starting amorphous carbon thickness on the order of 90–100 nm would be a reasonable illustrative target for this particular sequence. This exercise — summing consumption across every step rather than evaluating each step's selectivity independently — is the core discipline this chapter argues for.

---

## Part 4: Hard Mask Open and Mask-to-Pattern Fidelity

### 4.1 The First Etch Step Is Also a Mask Step

The hard-mask-open etch — transferring the photoresist pattern into the hard mask material itself — is, from the hard mask's perspective, the step that establishes its final CD and sidewall profile before any of the "real" stack etch steps begin. Any CD bias, footing, or profile error introduced during hard-mask-open propagates through every subsequent step as a fixed boundary condition; this etch step receives disproportionate process control attention relative to its apparent simplicity (patterning a single material) precisely because of this propagation effect.

### 4.2 Photoresist Trim and the Mask CD Relationship

Many advanced-node flows deliberately trim (laterally etch) the photoresist pattern isotropically before hard-mask-open, in order to achieve a final mask CD smaller than the photoresist's own lithographically-printed CD — a technique used to extend an existing lithography tool's effective resolution. This trim step, while not part of the "floating gate stack etch" in a narrow sense, directly sets the mask CD that every subsequent step (Chapters 6–9) will transfer downward, and its own uniformity and repeatability requirements are at least as demanding as the stack etch steps that follow it.

---

## Chapter Summary

- Photoresist alone is generally insufficient to survive the full floating gate stack etch sequence, due to both cumulative selectivity limits and lithography-driven resist thickness constraints
- Oxide and nitride hard masks offer good selectivity against halogen-based polysilicon/silicide chemistry but poor selectivity during ONO breakthrough, since ONO itself contains oxide and nitride
- Amorphous carbon hard masks offer selectivity across both the halogen and fluorocarbon chemistry regimes by using an orthogonal (oxygen-based) removal mechanism, at the cost of additional integration complexity
- Multi-layer hard mask stacks (thin oxide/nitride cap over bulk carbon) are a common advanced-node solution, directly analogous to the overall multi-material floating gate stack problem this book addresses
- Mask selectivity must be budgeted cumulatively across the entire etch sequence, not evaluated chemistry-by-chemistry in isolation, because erosion from early steps directly reduces margin available for later, more damage-sensitive steps
- Hard-mask-open CD and profile become a fixed boundary condition for every subsequent etch step, making this nominally simple first step disproportionately important to overall stack etch outcomes

## Study Questions

1. Why does an oxide or nitride hard mask face a specific selectivity challenge during the ONO breakthrough step that it does not face during the polysilicon or silicide etch steps?
2. Walk through the illustrative selectivity budget in Part 3 and explain why planning mask thickness against only the final (floating gate polysilicon) etch step would be insufficient.
3. Why does a photoresist trim step performed before any "stack etch" chemistry has run still meaningfully affect the final floating gate CD at the bottom of the stack?
4. What specific property of amorphous carbon hard masks makes them attractive for a stack spanning both halogen-etched and fluorocarbon-etched materials?

---

[← Chapter 4](04-charge-retention-physics.md) · [Index](../INDEX.md) · [Next: Chapter 6 →](06-control-gate-etch-chemistry.md)
