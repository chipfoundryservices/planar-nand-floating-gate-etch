# Chapter 14: Endpoint Detection Across Multi-Material Stack Transitions

## Executive Summary

Every chapter in Part II referenced endpoint detection as the triggering mechanism for a chemistry or bias power transition, without developing the measurement science behind it. This chapter does so: optical emission spectroscopy (OES) as the dominant in-situ endpoint technique for this stack, the specific challenge of designing a usable endpoint signal across five materially distinct transitions (some separated by only a few nanometers, as in the ONO stack, Chapter 7), and why, despite best efforts, production flows often supplement real-time endpoint detection with time-based and model-based transition triggers rather than relying on endpoint signal alone.

---

## Part 1: Optical Emission Spectroscopy Fundamentals

### 1.1 The Basic Measurement

Optical emission spectroscopy monitors light emitted by the plasma itself — specifically, characteristic emission wavelengths associated with excited-state relaxation of specific atomic or molecular species present in the plasma, whose concentration changes as the material being etched changes (because etch byproduct species change when the underlying film material changes, and because reactant species consumption rates change with the exposed material's reactivity). A sudden change in a specific wavelength's emission intensity, timed appropriately, signals a material transition — the physical basis for most "endpoint" triggers referenced in Chapters 6 through 9.

### 1.2 Signal Selection for This Specific Stack

Different material transitions in the floating gate stack produce different, and differently useful, OES signal changes:

| Transition | Representative Monitored Species (illustrative) | Signal Behavior |
|------------|-----------------------------------------------------|-------------------|
| Silicide → control gate polysilicon | W-containing byproduct species (decrease) vs. Si-containing species (relative increase) | Generally strong, clearly distinguishable signal, given substantial compositional difference |
| Control gate polysilicon → ONO (top oxide) | Si-containing species (decrease, as etch transitions from pure Si consumption to Si + O-containing byproducts) | Moderate signal strength; clear transition but less dramatic than silicide/poly |
| Within ONO (oxide → nitride → oxide) | N-containing vs. O-containing byproduct species | Weak signal strength per sub-transition, given the thin (few-nm) individual sub-layers involved, per Chapter 7 |
| ONO (bottom oxide) → floating gate polysilicon | Si-containing species (increase, oxide-dominant byproducts give way to pure Si etch byproducts) | Moderate-strong signal; clear transition, but occurring at a depth where process control stakes are highest (Chapter 8) |
| Floating gate polysilicon → tunnel oxide (the "real" endpoint) | Si-containing species (decrease, as remaining etch area shrinks to the thin oxide and surrounding silicon exposure) | Weakest, most gradual signal of the entire sequence, specifically because it must manifest gradually across a non-uniformly-clearing wafer (Chapter 8, Chapter 12), rather than as a sharp, simultaneous, wafer-wide transition |

### 1.3 Why the Final Transition Is the Hardest to Detect Well

The floating gate polysilicon-to-tunnel-oxide transition — arguably the single most consequential endpoint in the entire sequence, since it triggers the soft-landing/overetch strategy central to Chapter 8 — is also the hardest to characterize via a sharp OES signal, for two compounding reasons: the absolute change in exposed-material composition at this transition is comparatively modest (Si to Si + thin oxide, versus the much larger compositional swings at, e.g., the silicide/polysilicon transition); and, because of across-wafer non-uniformity and microloading (Chapter 12), different locations on the wafer reach this transition at different times, meaning the total OES signal (necessarily an average or aggregate over some portion of the wafer, depending on the specific optical viewport/monitoring geometry) shows a gradual, extended transition rather than a sharp step, even though any individual location's own local transition may be comparatively abrupt.

---

## Part 2: Endpoint Algorithm Design

### 2.1 Beyond Simple Threshold Crossing

Given the weak, gradual signal characteristic described in Part 1.3, naive threshold-crossing endpoint algorithms (triggering a transition the instant monitored signal intensity crosses some fixed value) are generally inadequate for the final, most consequential transition in this stack. Production endpoint algorithms instead typically combine signal derivative analysis (rate of change, rather than absolute level, often providing a more robust trigger for a gradual transition), multi-wavelength combination (using several monitored species simultaneously and combining their signals to improve robustness against noise or interference from any single wavelength), and, increasingly, model-based or statistically-trained algorithms that incorporate expected signal shape (learned from prior wafers/lots) rather than relying purely on real-time signal characteristics in isolation.

### 2.2 Endpoint as a Trigger for a Process Change, Not Just a Stop Signal

It is worth emphasizing a point implicit throughout Part II: in this multi-step stack etch, "endpoint" detection is used primarily to trigger chemistry and bias power *transitions between steps*, not merely to signal "stop the etch entirely" (which is really only the role of the final transition, into soft-landing/overetch). This means endpoint detection reliability requirements apply to every material transition in the sequence, not only the final one — an incorrectly-timed silicide-to-polysilicon transition trigger, for example, can leave silicide residue or prematurely expose polysilicon to the wrong chemistry (Chapter 6), with consequences that propagate through the rest of the sequence even though this particular transition is not the "final" endpoint.

---

## Part 3: Supplementing Real-Time Endpoint with Model-Based Triggers

### 3.1 Time-Based Sub-Step Control

As previewed in Chapter 7, some transitions (particularly within the thin ONO sub-layers) may be more reliably controlled via pre-characterized, fixed-duration sub-steps — calibrated against independently measured film thickness for the specific lot/process condition — rather than real-time endpoint detection alone, specifically because the OES signal available for those thin-layer transitions may not provide sufficient signal-to-noise ratio for robust real-time triggering.

### 3.2 Combining Real-Time and Predictive Information

Mature production endpoint strategies typically combine real-time OES-derived endpoint signal with model-based expectations (a predicted transition time window, derived from incoming film thickness metrology for that specific wafer/lot and historical process rate data), using the model-based expectation as a plausibility check or fallback trigger if the real-time signal is ambiguous or fails to cross its trigger threshold within the expected window — a combined approach that is more robust than either real-time detection or pure time-based control used in isolation, particularly for the weak-signal transitions this chapter has identified as the most challenging.

### 3.3 In-Situ Metrology Beyond OES

Some advanced production tools supplement OES with additional in-situ sensing modalities — interferometry (monitoring reflected light interference patterns, sensitive to remaining film thickness for sufficiently transparent films, useful in principle for the thin oxide-containing layers in this stack) or, less commonly in routine production but present in some advanced or research contexts, other optical or electrical in-situ diagnostics — providing additional, independent information to cross-check or supplement OES-based endpoint decisions, particularly for the hardest-to-detect transitions identified in Part 1.3.

---

## Part 4: Endpoint Detection and the Soft-Landing Strategy, Connected

### 4.1 Closing the Loop with Chapter 8

This chapter's discussion of the final, gradual, hard-to-detect floating-gate-to-tunnel-oxide transition directly explains why Chapter 8's soft-landing strategy is structured the way it is: because real-time endpoint signal for this specific transition cannot, by the physical reasoning developed in Part 1.3, provide a sharp, precisely-timed, wafer-uniform trigger, the soft-landing step is deliberately designed to be tolerant of exactly this kind of imprecise, gradual trigger — running at conditions safe enough to sustain for a genuinely uncertain duration (bounded by the overetch time budget developed in Chapter 8), rather than depending on a trigger precise enough to immediately halt the etch at the exact moment of clearing everywhere on the wafer simultaneously, which this chapter's analysis shows is not a realistic expectation for this specific material transition.

---

## Chapter Summary

- Optical emission spectroscopy monitors plasma emission at wavelengths associated with specific byproduct or reactant species, providing the primary real-time signal for triggering material-transition-driven chemistry and bias power changes throughout the stack etch sequence
- Different transitions in the stack produce signals of markedly different strength and sharpness, with the floating-gate-to-tunnel-oxide transition being both the most consequential and the hardest to detect via a sharp signal
- Endpoint algorithms for weak/gradual signals typically use derivative analysis, multi-wavelength combination, and increasingly model-based approaches, rather than simple threshold crossing
- Endpoint detection matters for every material transition in the sequence, not only the final one, since mistimed intermediate transitions propagate consequences through later steps
- Time-based sub-step control, informed by independent film thickness metrology, supplements real-time endpoint detection particularly for the thin, weak-signal ONO sub-layer transitions
- The soft-landing strategy of Chapter 8 is specifically designed to be robust to the imprecise, gradual endpoint signal this chapter shows is physically inherent to the final transition, rather than assuming a precision of detection that is not realistically achievable

## Study Questions

1. Why does the floating-gate-to-tunnel-oxide transition produce a weaker and more gradual OES signal than the silicide-to-polysilicon transition, even though both are material transitions?
2. Explain why simple threshold-crossing endpoint algorithms are generally inadequate for the thin ONO sub-layer transitions, and what alternative approaches address this limitation.
3. Why does mistimed endpoint detection at an intermediate transition (not the final one) still matter to overall stack etch outcomes?
4. How does this chapter's analysis of endpoint signal limitations directly justify the specific design of Chapter 8's soft-landing strategy?

---

[← Chapter 13](13-tunnel-oxide-damage.md) · [Index](../INDEX.md) · [Next: Chapter 15 →](15-scaling-limits-3d-transition.md)
