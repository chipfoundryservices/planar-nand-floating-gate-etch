# Chapter 3: Self-Aligned Floating Gate (SA-FG) Integration & STI Interaction

## Executive Summary

Shallow trench isolation (STI) separates adjacent NAND strings electrically, just as it separates any two adjacent transistors in conventional CMOS. But in planar NAND's dominant production integration scheme — self-aligned floating gate (SA-FG) — the floating gate stack and the STI trench are not independently patterned and etched modules. The floating gate film stack itself is used as the hard mask that defines the STI trench, and the resulting trench fill geometry in turn constrains the floating gate's allowable height, sidewall profile, and corner shape. This chapter develops that coupling in detail: why the self-aligned approach replaced earlier, non-self-aligned flows; how the process sequence actually interleaves FG stack etch and STI etch/fill steps; and why, as a direct consequence, no floating gate etch engineer in an SA-FG flow can treat their process as a standalone module optimized purely against FG-specific metrics.

---

## Part 1: Why Self-Alignment Replaced Earlier Approaches

### 1.1 The Non-Self-Aligned (Conventional) Alternative

In an earlier, non-self-aligned floating gate flow, STI trenches are etched and filled *before* the floating gate stack is deposited and patterned. The floating gate is then patterned with its own independent lithography step, aligned to the already-existing STI pattern using conventional overlay techniques. This approach is conceptually simpler — each module (STI, then floating gate) can be developed and qualified largely independently — but it has a specific, scaling-limiting weakness: the floating gate pattern must be deliberately sized and positioned with enough margin to tolerate realistic overlay error relative to the STI pattern beneath it. As minimum feature size shrinks, the *absolute* overlay error budget (determined by lithography tool capability) shrinks much more slowly than the feature size itself, so overlay margin consumes a rapidly growing fraction of the available cell pitch. By the sub-100nm generations, this overlay margin tax became large enough that an alternative was needed.

### 1.2 The Self-Aligned Solution

The self-aligned floating gate (SA-FG) flow removes the independent floating-gate-to-STI overlay step entirely, by using the *same* patterned hard mask / floating gate stack to define both the floating gate cut and the STI trench. In broad outline:

1. Tunnel oxide is grown, and floating gate polysilicon plus a hard mask are deposited as blanket films (ONO and control gate are **not** yet present at this stage)
2. The hard mask and floating gate polysilicon are patterned and etched to define the **active area / STI pattern** — this etch cuts through the floating gate polysilicon and tunnel oxide and continues into the silicon substrate, forming the STI trench, using the floating-gate-stack hard mask as the trench etch mask
3. The STI trench is filled with a gap-fill dielectric (commonly a flowable or high-density-plasma CVD oxide) and planarized (typically via chemical mechanical planarization, CMP)
4. The gap-fill oxide is recessed (etched back) to expose the upper portion of the floating gate polysilicon sidewalls, which is what allows the floating-gate-to-control-gate coupling capacitance (Chapter 4) to form along those sidewalls, not just across the top surface
5. ONO interpoly dielectric and control gate polysilicon (plus silicide cap) are deposited as blanket films over the now-topographically-structured surface
6. A **second** lithography and etch step defines the word line direction — cutting through control gate, ONO, and (critically) separating the floating gate into individual, electrically isolated islands along the word line

Because the floating gate's *position* relative to the STI trench edge is set by the same mask/etch step that *defines* the STI trench (step 2), there is no independent overlay error between the two — the floating gate is, by construction, self-aligned to the active area. This is the origin of the "self-aligned floating gate" name, and it is why this chapter cannot be deferred to a generic STI etch discussion: **the floating gate etch module described in this book's Part II is, in the SA-FG flow, split across two separate etch steps (step 2 and step 6 above), with a trench fill and recess operation happening in between.**

---

## Part 2: The Active-Area Etch (Step 2) as a Floating-Gate-Stack Etch

### 2.1 What Is Actually Being Cut

The active-area/STI etch in an SA-FG flow is, in material terms, nearly identical to the top portion of the floating gate stack etch described in Chapter 1: hard mask, then floating gate polysilicon, then tunnel oxide, and finally into the silicon substrate to the target STI trench depth (commonly several hundred nanometers, depending on isolation and fill requirements). This means the selectivity and damage concerns usually associated with "floating gate etch" — particularly tunnel oxide sensitivity — are already present in this first etch step, well before the control gate or ONO layers even exist on the wafer.

### 2.2 STI Trench Profile Requirements

The STI trench etched in this step must simultaneously satisfy requirements driven by both isolation physics and gap-fill process capability:

| Requirement | Reason |
|-------------|--------|
| **Sidewall angle near-vertical, slightly tapered (e.g., 85–89° from horizontal)** | Fully vertical sidewalls are difficult to gap-fill void-free at high aspect ratio; slight taper (wider at top) eases fill, but excessive taper wastes array area and degrades isolation at a given pitch |
| **Smooth sidewall, minimal micro-trenching at the trench base** | Micro-trenching (a common RIE lag/reflection artifact, Chapter 12) locally deepens the trench corner and creates stress concentration and fill voids at that location |
| **Corner rounding at the top of the trench (active area corner)** | A sharp top corner concentrates electric field during subsequent device operation and can nucleate a parasitic leakage path or a localized "corner device" with anomalously low threshold voltage, degrading the uniformity the array depends on |
| **Minimal silicon substrate damage/roughness at the trench sidewall and bottom** | Damage here is not adjacent to the memory cell's electrical path in the same way tunnel oxide damage is, but excessive substrate damage can still affect junction leakage and isolation leakage currents |

Because this etch is also, simultaneously, cutting through the floating gate polysilicon and tunnel oxide at the *top* of the trench, the chemistry must transition cleanly from a polysilicon/oxide etch regime into a silicon trench etch regime within a single continuous process — a materially different integration challenge than the control-gate-side etch (step 6), which never touches bulk silicon at all.

---

## Part 3: Gap Fill, CMP, and Recess — The STI Steps That Constrain the Floating Gate

### 3.1 Why Recess Depth Matters to Floating Gate Geometry

After gap fill and CMP planarize the STI oxide level with (or slightly above) the top of the floating-gate-stack hard mask, the fill oxide is deliberately etched back ("recessed") to expose some fraction of the floating gate polysilicon's sidewall height before ONO and control gate deposition. This recess depth is one of the most consequential dimensions in the entire cell, because it directly sets how much of the floating gate's sidewall area becomes available for floating-gate-to-control-gate capacitive coupling (Chapter 4) — the control gate "wraps" down along the exposed floating gate sidewall in a well-formed cell, and the exposed sidewall area adds directly to the coupling capacitance beyond what the top-surface-only capacitance alone would provide.

### 3.2 The Coupling Created Between Modules

This creates a specific, concrete coupling between the floating gate etch module and the STI module that this book's framing insists on making explicit:

- If floating gate polysilicon height (set in the Chapter 1/8 etch step) is increased to raise available sidewall coupling area, the STI trench depth and gap-fill aspect ratio inherited from step 2 are affected, because the hard mask and floating gate stack together determine trench etch depth reference and aspect ratio during gap fill
- If STI recess depth (an STI-module process parameter) is increased to expose more floating gate sidewall, the floating gate must have sufficient total height to still leave an adequate, well-controlled remaining sidewall height beneath the exposed region, or mechanical stability and subsequent control-gate-to-floating-gate electrical uniformity suffers
- If floating gate sidewall angle from the active-area etch (step 2) is not well controlled, the exposed sidewall area after recess (and therefore coupling ratio) varies cell-to-cell even at constant nominal recess depth and floating gate height, because the *effective* exposed area depends on the actual sidewall geometry, not just the two depth parameters

A floating gate process engineer and an STI process engineer who each optimize their own module's metrics (floating gate CD and profile uniformity; trench fill void-free yield) without coordinating on this shared geometry can each report excellent standalone process control while the combined, integrated coupling ratio distribution across the array is unacceptably wide. This is a recurring theme in self-aligned integration schemes generally, and it is why integration engineers (one of this book's stated audiences) need the material in this chapter even if they never directly own either etch recipe.

---

## Part 4: The Word-Line-Direction Etch (Step 6) Revisited

### 4.1 What This Step Does Not Have to Worry About

By the time the word-line-direction etch (step 6 in Part 1's sequence) runs, the floating gate's position and base geometry relative to the STI trench have already been fixed by the earlier self-aligned step. This etch's job is narrower: cut through silicide/control gate/ONO, and finally separate the floating gate polysilicon along the word line direction into individual islands — without needing to re-engage with the STI trench or bulk silicon substrate at all, because the floating gate islands in this direction are bounded above the (already-filled and planarized) STI oxide, not by cutting new trenches into silicon.

### 4.2 What It Does Have to Worry About, Because of Step 2

Because step 2 already defined the floating gate's position, height, and partial sidewall profile, the word-line-direction etch inherits those characteristics as fixed boundary conditions. Any systematic bias in floating-gate height, sidewall taper, or corner shape from the active-area etch shows up in the word-line-direction etch as a variation in local topography that the etch chemistry must handle uniformly regardless of whether it originated upstream. This is one concrete reason endpoint detection strategy (Chapter 14) for the word-line-direction etch must be robust to some inherited variability rather than assuming a perfectly uniform starting film stack, which would be a reasonable assumption for a true single-material blanket-film etch but is not a safe assumption here.

---

## Part 5: Why This Chapter Precedes the Process Chemistry Chapters

Parts II through IV of this book largely treat the floating gate etch sequence as occurring against a single, continuous film stack (the framing introduced in Chapter 1, for pedagogical clarity). This chapter exists specifically to correct that simplification before it causes confusion: in the dominant SA-FG production flow, the sequence is actually split across two separate lithography/etch events with a full STI module (deposition, fill, CMP, recess) interleaved between them. Readers should carry the following mapping forward into later chapters:

| This Book's Framing (Chapters 1, 5–9) | SA-FG Production Reality |
|----------------------------------------|----------------------------|
| "Hard mask open" (Chapter 5) | Occurs twice — once for the active-area/FG/STI etch, once for the word-line-direction etch |
| "Floating gate polysilicon etch" (Chapter 8) | Occurs in the active-area etch (step 2), cutting the full floating gate film prior to control gate deposition |
| "Control gate / silicide etch" (Chapter 6) and "ONO breakthrough" (Chapter 7) | Occur only in the word-line-direction etch (step 6), after control gate and ONO have been deposited over the already-structured floating gate/STI topography |
| "Endpoint detection across the full stack" (Chapter 14) | Must be understood as two separate endpoint problems, corresponding to the two separate etch steps, not one continuous signal |

Later chapters will generally use the simplified single-sequence framing for clarity when discussing a specific chemistry or defect mechanism in isolation, but the reader should mentally re-insert this chapter's two-step, STI-interleaved reality whenever reasoning about full-flow integration, cycle time, or cross-module yield coupling.

---

## Chapter Summary

- Self-aligned floating gate (SA-FG) integration eliminates an independent floating-gate-to-STI overlay step by using the floating gate stack itself as the STI trench hard mask
- This splits the "floating gate etch" conceptually described in Chapter 1 into two physically separate etch events (active-area/STI etch, and word-line-direction etch), with a full STI gap-fill/CMP/recess module interleaved between them
- STI recess depth and floating gate sidewall geometry jointly determine the exposed sidewall area available for floating-gate-to-control-gate coupling, creating a cross-module dependency that neither module's standalone metrics capture
- Floating gate and STI process engineers who optimize only their own module's local metrics can produce excellent standalone results while still generating an unacceptably wide integrated coupling ratio distribution
- Later chapters' simplified single-sequence framing of the floating gate etch should be mentally mapped back onto this chapter's two-step SA-FG reality when reasoning about full-flow integration

## Study Questions

1. Why does shrinking minimum feature size make lithographic overlay error a proportionally larger problem, and how does self-alignment address this specific issue?
2. In the SA-FG flow, which etch step is responsible for setting floating gate height and base sidewall profile, and which is responsible for the final word-line-direction isolation cut?
3. Explain how STI recess depth and floating gate sidewall taper can interact to produce coupling ratio variation even when each parameter is individually well-controlled.
4. Why might an integration engineer need to understand both the floating gate etch module and the STI gap-fill/recess module, even if they do not personally develop either recipe?

---

[← Chapter 2](02-stack-materials.md) · [Index](../INDEX.md) · [Next: Chapter 4 →](04-charge-retention-physics.md)
