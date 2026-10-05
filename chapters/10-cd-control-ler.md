# Chapter 10: Critical Dimension Control & Line Edge Roughness at Sub-50nm Pitch

## Executive Summary

Critical dimension (CD) — the actual, as-manufactured width of a floating gate or control gate line — and line edge roughness (LER) — the local, high-spatial-frequency deviation of an etched sidewall from a perfectly straight line — are both metrology outputs, but this chapter treats them as what they fundamentally are: an etch uniformity and transfer-fidelity problem that becomes progressively less forgiving as pitch scales down. This chapter develops the CD budget concept, how CD bias and variation accumulate across the stack etch sequence, the physical origins of line edge roughness and its transfer from mask to final profile, and why the same absolute roughness magnitude that was negligible at relaxed pitch becomes yield- and reliability-limiting at advanced pitch.

---

## Part 1: The CD Budget Concept

### 1.1 CD as an Allocated, Finite Resource

At any given technology node, the lithographically-defined pitch sets a fixed total width available to be divided between the floating-gate-stack line itself and the space separating it from its neighbor. Device performance (drive current, coupling ratio, Chapter 4) generally benefits from a wider line; isolation and parasitic capacitance control (cell-to-cell interference, also Chapter 4) benefit from wider spacing. The as-designed CD target represents a deliberate allocation of the available pitch between these competing needs, and the **CD budget** is the acceptable variation around that target — set by how much CD deviation downstream device performance and reliability specifications can absorb before failing.

### 1.2 Where CD Bias Enters the Process

CD at the bottom of the finished stack (the floating gate's actual electrical width) is not simply inherited unchanged from the lithographic mask dimension; it accumulates bias contributions from every step between mask definition and final clear:

| Source | Typical Direction of Bias | Relevant Chapter |
|--------|------------------------------|-------------------|
| Lithographic printing (resist CD vs. mask CD) | Can bias either direction depending on exposure/focus | (Outside this book's scope; assumed as an input) |
| Photoresist trim (if used) | Deliberate CD reduction | Chapter 5 |
| Hard-mask-open etch | Can add bias via lateral (isotropic) etch component or mask faceting | Chapter 5 |
| Each subsequent stack etch step (silicide, CG poly, ONO, FG poly) | Cumulative bias from any non-ideal (non-90°) sidewall angle, since CD is measured at a specific height, and non-vertical sidewalls mean CD varies with measurement height | Chapters 6–9 |

A CD specification at the final, bottom-of-stack floating gate measurement point is therefore a specification on the *cumulative* result of this entire chain, not on any single step in isolation — which is why CD control, like the selectivity budgeting introduced in Chapter 5, must be managed end-to-end.

### 1.3 Why the Budget Shrinks Faster Than the Pitch

As pitch scales down by some factor between technology generations, the *absolute* CD variation that downstream device specifications can tolerate generally does not shrink by the same factor — much of it is set by physical and metrology limits (measurement noise floor, intrinsic plasma process fluctuation scales) that do not scale proportionally with lithographic dimensions. The result is that CD variation consumes a steadily growing *fraction* of the shrinking pitch budget at each successive node, which is the quantitative version of the "margin, not process quality, is what changes with scaling" point introduced in Chapter 4.

---

## Part 2: Line Edge Roughness — Origins

### 2.1 Mask-Transferred Roughness

Line edge roughness present in the patterned photoresist (itself arising from photon shot noise in the lithographic exposure, polymer molecular-scale resist blob size, and development process stochastics) is transferred, with some modification, into the hard mask during hard-mask-open etch, and from there into every subsequent stack etch step. Etch processes do not generally eliminate incoming roughness — they can, depending on the specific chemistry/ion-energy balance, either approximately preserve it, smooth it somewhat (via lateral/isotropic etch components that locally average out high-spatial-frequency variation), or in some unfavorable conditions, amplify it (via ion-channeling or micro-masking effects that locally protect or locally accelerate etch at specific roughness features).

### 2.2 Grain-Boundary-Correlated Roughness

As introduced in Chapter 2, polysilicon's granular microstructure means etch rate is not perfectly uniform at the length scale of individual grains, because grain boundaries present different local chemistry, strain, and defect density than grain interiors. This produces an etch-intrinsic roughness contribution, superimposed on (and not entirely separable from) the mask-transferred roughness discussed above, and it is a contribution that — unlike mask-transferred roughness — cannot be improved by better lithography; it requires either finer-grained polysilicon deposition (a materials/deposition-process lever, outside this book's direct scope but relevant context for integration engineers) or an etch chemistry less sensitive to local grain structure variation.

### 2.3 Micro-Masking

Micro-masking occurs when small particles, residue, or local regions of enhanced sidewall passivation locally protect the underlying material from etch, producing small, randomly distributed protrusions (sometimes visible in cross-section or top-down scanning electron microscope images as "grass" or isolated pillars) that are a severe, localized form of roughness rather than a smooth statistical variation. Micro-masking is frequently linked to insufficiently clean chamber conditions, residue carryover from a preceding step (Chapter 7's ONO residue discussion is directly relevant here), or excessive polymer deposition rate relative to the ion flux available to clear it uniformly.

---

## Part 3: Roughness Transfer and Amplification Through the Stack

### 3.1 Roughness Does Not Stay Constant Through Five Etch Steps

Line edge roughness present at the top of the stack (post-hard-mask-open) does not pass unchanged through the silicide, control gate, ONO, and floating gate etch steps; each step has its own roughness transfer characteristic (preserve, smooth, or amplify, per Part 2.1), and these characteristics compound. A chemistry/ion-energy combination that modestly amplifies roughness at each of five sequential steps can produce substantially worse final roughness than naive single-step characterization of any individual step would predict, which is a specific instance of this book's recurring argument that the sequence must be characterized and controlled end-to-end, not step-by-step in isolation.

### 3.2 Why LER Matters More at the Bottom of the Stack Than the Top

Roughness present at the silicide/control-gate level (top of stack) primarily affects word line resistance variation — a real concern, but one with comparatively forgiving margin. Roughness present at the floating gate level (bottom of stack) directly affects the geometric capacitances (Chapter 4) that set coupling ratio and programmed-state threshold voltage, cell by cell along a word line — meaning floating gate LER converts, with comparatively little attenuation, into the Vt distribution width that Chapter 4 established as the key capacity-limiting metric for multi-level-cell storage.

---

## Part 4: Metrology and Control

### 4.1 CD-SEM and Roughness Metrics

Critical dimension scanning electron microscopy (CD-SEM) is the primary in-line metrology tool for both CD and LER measurement, typically reporting CD as a mean value and roughness as a statistical quantity (commonly a standard deviation or 3-sigma value of edge position deviation along a measured line length, sometimes further decomposed into low-spatial-frequency "line width roughness" and high-spatial-frequency "line edge roughness" components, which can have different physical origins per Part 2 and may respond differently to process changes).

### 4.2 Advanced Nodes and the Limits of Compensation

At relaxed pitch, modest CD bias can often be compensated by adjusting the lithographic target (biasing the mask CD to pre-compensate for a known, repeatable etch bias) without addressing the underlying roughness or variation mechanism directly. This compensation strategy works only for *systematic, repeatable* bias — it does nothing for random variation (roughness, across-wafer non-uniformity) which is, by definition, not a fixed offset that can be pre-compensated. As advanced nodes make random variation an increasingly large fraction of the total CD budget (Part 1.3), this chapter's broader argument is that root-cause etch process and chemistry improvements, rather than lithographic pre-compensation, become the only effective lever remaining.

---

## Chapter Summary

- CD at the bottom of the finished floating gate stack accumulates bias contributions from lithography, trim, hard-mask-open, and every subsequent etch step, and must be budgeted end-to-end
- The absolute CD variation downstream specifications can tolerate does not shrink proportionally with pitch, so CD variation consumes a growing fraction of the available budget at each successive technology node
- Line edge roughness originates from mask-transferred lithographic stochastics, grain-boundary-correlated etch-intrinsic variation, and micro-masking, each with distinct mechanisms and distinct mitigation strategies
- Roughness transfer characteristics (preserve/smooth/amplify) compound across the five-step etch sequence, meaning single-step characterization can understate final, bottom-of-stack roughness
- Floating-gate-level roughness converts with comparatively little attenuation into Vt distribution width, directly consuming the margin multi-level-cell storage depends on
- Lithographic pre-compensation addresses only systematic CD bias, not random variation, making root-cause etch process improvement the primary lever as advanced nodes shrink the available CD budget

## Study Questions

1. Why is CD control best understood as an end-to-end, cumulative budget rather than a property of any single etch step?
2. Explain why the same absolute line edge roughness magnitude can be a non-issue at one technology node and a yield-limiting defect at a more advanced node.
3. Distinguish grain-boundary-correlated roughness from micro-masking in terms of physical origin and the process levers available to address each.
4. Why does roughness at the floating gate level have a more direct impact on Vt distribution width than roughness at the control gate/silicide level?

---

[← Chapter 9](09-rf-bias-profile-control.md) · [Index](../INDEX.md) · [Next: Chapter 11 →](11-stringers-bridging-defects.md)
