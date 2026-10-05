# Chapter 8: Floating Gate Polysilicon Etch & Selectivity to Tunnel Oxide

## Executive Summary

Every chapter so far has pointed toward this one: the floating gate polysilicon etch is the step where the entire stack's accumulated profile, residue, and chemistry history finally meets the one material this book treats as inviolable — tunnel oxide. This chapter develops the specific chemistry and process strategy used to etch floating gate polysilicon with maximum achievable selectivity to the oxide beneath it, the "soft landing" concept that extends selectivity management into the final moments of the etch, and the way endpoint detection and overetch time budgeting must be designed around a tunnel oxide that simply cannot absorb the kind of margin available in earlier steps.

---

## Part 1: Why This Step Differs from Control Gate Polysilicon Etch

### 1.1 Same Material, Different Constraint

Floating gate polysilicon and control gate polysilicon (Chapter 6) are chemically similar materials — both are CVD-deposited, doped polysilicon — and a chemistry capable of etching one is, in a basic sense, capable of etching the other. The chapters are separated not because the material etch chemistry is fundamentally different, but because the **constraint governing chemistry selection** is fundamentally different: control gate etch is optimized primarily for profile, rate, and silicide-transition management, with a comparatively generous selectivity requirement to the ONO beneath it; floating gate etch must additionally achieve very high selectivity to a tunnel oxide with, as established in Chapter 2, essentially zero thickness margin to spare.

### 1.2 The Selectivity Requirement, Quantified Illustratively

If tunnel oxide is 7 nm thick and the process must tolerate even generous across-wafer floating gate thickness non-uniformity (say, equivalent to ±10 nm of polysilicon in local overetch time) without consuming more than, illustratively, 1 nm of tunnel oxide at the most aggressively overetched location, the required floating-gate-to-tunnel-oxide etch selectivity is on the order of:

$$\text{Selectivity} \approx \frac{10 \text{ nm overetch margin (polysilicon)}}{1 \text{ nm tolerable oxide loss}} = 10:1 \text{ (minimum, illustrative)}$$

Real production requirements are generally more demanding than this illustrative figure once realistic across-wafer and lot-to-lot variation, plus the cumulative damage effects developed in Chapter 13 (which matter even without measurable oxide thickness loss), are accounted for — selectivity targets in the range of 20:1 to 50:1 or higher are representative of what advanced floating gate etch chemistries aim to achieve, though the specific figure for any given production process depends on its measured non-uniformity and the retention margin available at that technology node.

---

## Part 2: Chemistry Strategy for High Selectivity

### 2.1 HBr-Dominant, Low Chemical-Component Chemistry

Floating gate polysilicon main etch typically favors HBr as the dominant halogen species (over Cl₂), for the same anisotropy-related reason introduced in Chapter 6, but with the added benefit that HBr-based chemistry also tends to offer inherently better polysilicon-to-oxide selectivity than Cl₂-dominant chemistry, because Cl₂'s higher spontaneous chemical reactivity with silicon does not discriminate as strongly against oxide as HBr's more ion-assisted-dominant mechanism does. This is a specific instance of a general pattern in this book: a chemistry choice made for profile/anisotropy reasons in Chapter 6 turns out to also serve the selectivity requirement that becomes dominant in this chapter.

### 2.2 The Role of Oxygen Addition

Small, carefully controlled oxygen addition to the HBr-based chemistry serves a dual role here, more consequential than in the control gate etch step: it enhances sidewall passivation (as in Chapter 6) while also contributing to a thin surface oxidation effect on exposed oxide surfaces (the tunnel oxide, once exposed) that further suppresses the oxide etch rate, reinforcing selectivity precisely where it matters most. Oxygen concentration in this step is tuned more conservatively (and characterized more extensively) than in the control gate step, because both insufficient and excessive oxygen can degrade the selectivity/profile balance in ways that are costly to discover late in process development.

### 2.3 Low Ion Energy as a Selectivity and Damage Lever

Because oxide etches via a mechanism more dependent on ion-assisted bombardment (relative to polysilicon's greater spontaneous chemical etch component under HBr-dominant chemistry), reducing ion energy — via lower RF bias power — simultaneously improves polysilicon-to-oxide etch selectivity and reduces the plasma-induced damage mechanisms developed in Chapter 13. This dual benefit is why floating gate etch, and especially its final overetch/soft-landing sub-step, is typically run at markedly lower bias power than the control gate main etch, even though this sacrifices some etch rate and process throughput — a tradeoff this book argues is correctly made in favor of selectivity and damage control, given the retention consequences established in Chapter 4.

---

## Part 3: Soft Landing and Overetch Strategy

### 3.1 Why a Single-Rate Etch to Endpoint Is Insufficient

Across-wafer and die-to-die polysilicon thickness and local etch rate variation (Chapter 12) mean that a single, uniform etch time calculated from a nominal film thickness and a nominal etch rate will, at some wafer locations, clear polysilicon earlier than at others. If the entire etch runs at main-etch conditions (optimized for throughput, not maximum selectivity) until a global endpoint signal is detected, locations that cleared early are left exposed to main-etch conditions — including its comparatively higher ion energy — for longer than locations that cleared late, directly creating the non-uniform tunnel oxide damage and thinning this book is centrally concerned with.

### 3.2 The Soft-Landing Concept

Production floating gate etch recipes address this with a deliberate chemistry and power step-down — a "soft landing" — triggered before complete clearing, timed via endpoint signal onset (Chapter 14) or a pre-characterized time offset from the main etch. The soft-landing step runs at substantially reduced ion energy and often a modified gas chemistry further favoring oxide selectivity, specifically to absorb the across-wafer non-uniformity in polysilicon clearing time without concentrating high-energy ion exposure on the earliest-clearing locations.

### 3.3 Overetch Time Budgeting

The overetch time (total soft-landing duration beyond the point where polysilicon is nominally expected to clear everywhere) is a deliberately engineered parameter, not simply "as short as possible" or "as long as a comfortable safety margin allows" — it must be long enough to ensure the latest-clearing locations (set by the measured non-uniformity distribution, not the nominal average) are fully cleared, since any residual, unetched floating gate polysilicon connecting adjacent cells is an immediate electrical bridging defect (Chapter 11), which is generally judged a more severe and less tolerable outcome than a modest, uniform amount of soft-landing-stage tunnel oxide exposure. This asymmetry — bridging defects being worse than oxide exposure, up to a point — is why soft-landing chemistry is engineered for very high selectivity specifically: it allows overetch time to be generously budgeted against the non-uniformity distribution without unacceptable cumulative oxide damage.

---

## Part 4: What Happens at the Channel, Not Just the Gate

### 4.1 Exposed Channel Regions Between Cells

Once floating gate polysilicon clears in the spaces between adjacent cells (during the active-area/STI etch, Chapter 3, for the lateral direction; or between adjacent word lines, for the longitudinal direction in the word-line-direction etch), the etch chemistry is, for a brief period, exposed directly to tunnel oxide (and, if overetch continues past that point, to the silicon substrate/channel beneath it) in those cleared regions, even while polysilicon in the still-active cell regions has not yet fully cleared. This is precisely the condition the soft-landing strategy (Part 3) is designed to manage, and it is why endpoint signal design (Chapter 14) must account for a transition that occurs gradually, pattern-density-dependent location by location, rather than as a single, sharp, wafer-wide event.

### 4.2 Channel/Substrate Sensitivity

Where overetch does proceed far enough to expose silicon substrate directly (at locations between cells where tunnel oxide itself has also locally cleared, intentionally or as a process margin consideration specific to the integration scheme), substrate damage and dopant profile disturbance become a secondary concern layered on top of the tunnel-oxide-focused selectivity discussion above — relevant primarily to junction leakage and isolation behavior rather than to the floating gate cell's own retention physics, but still part of the overall process window this chapter's chemistry choices must satisfy.

---

## Chapter Summary

- Floating gate polysilicon etch chemistry is similar in material terms to control gate etch chemistry, but is governed by a fundamentally tighter selectivity constraint, since tunnel oxide has essentially no thickness margin to spare
- HBr-dominant, low-ion-energy chemistry serves both the selectivity requirement and the damage-minimization requirement simultaneously, at a deliberate cost to etch rate and throughput
- A single-rate etch to global endpoint is insufficient given realistic across-wafer non-uniformity; production recipes use a deliberate soft-landing step at reduced ion energy and modified chemistry to absorb this non-uniformity
- Overetch time is engineered against the measured non-uniformity distribution's slowest-clearing locations, accepting modest, uniform, well-controlled oxide exposure as preferable to any location with residual, bridging-capable polysilicon
- Endpoint and soft-landing strategy must account for the gradual, pattern-density-dependent nature of polysilicon clearing across a real wafer, not a single sharp wafer-wide transition

## Study Questions

1. Why can the same basic polysilicon etch chemistry used for control gate etch (Chapter 6) be insufficient for floating gate etch, even though the target material is chemically the same?
2. Walk through the illustrative selectivity calculation in Part 1 and explain what each term in it represents physically.
3. Why does the soft-landing concept specifically address across-wafer non-uniformity, rather than simply running the entire etch at lower, "safer" ion energy from the start?
4. Why is a small, uniform amount of tunnel oxide exposure during soft-landing generally judged preferable to any risk of residual, bridging-capable floating gate polysilicon?

---

[← Chapter 7](07-ono-interpoly-etch.md) · [Index](../INDEX.md) · [Next: Chapter 9 →](09-rf-bias-profile-control.md)
