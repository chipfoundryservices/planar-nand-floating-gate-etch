# Chapter 1: Planar NAND Architecture & the Floating Gate Cell

## Executive Summary

Before any etch chemistry can be discussed sensibly, the thing being etched must be understood in context: what it is, why it is shaped the way it is, and what failure actually means for it. This chapter establishes that context. We examine why NAND's string-based array architecture exists (and how it differs from NOR flash), how the floating gate cell sits inside that architecture, and why — across roughly two decades of production history — the quality of a single plasma etch step became one of the primary levers determining whether a given technology node could be manufactured profitably at all. The chapter closes with a production-history overview that the rest of the book will refer back to repeatedly: as word line pitch fell from micron-scale to sub-20nm, the etch process window available to the floating gate stack etch did not merely get tighter — it eventually stopped existing, which is the physical reason the industry moved to 3D NAND rather than a simple business preference.

---

## Part 1: NAND in the Memory Hierarchy

### 1.1 Why Flash Memory Exists

Non-volatile memory — memory that retains its state without applied power — has always traded off against the much faster, much more expensive volatile memory (SRAM, DRAM) that computers use for active working memory. Flash memory occupies the price/performance/non-volatility point that makes it suitable for long-term storage: slower to write than DRAM, far cheaper per bit, and durable without power for years.

Two flash architectures emerged in the late 1980s, both based on the floating gate transistor but organized at the array level in fundamentally different ways:

| Property | NOR Flash | NAND Flash |
|----------|-----------|------------|
| **Cell arrangement** | Parallel, each cell independently addressable | Cells connected in series ("strings") of 16–128+ |
| **Read access** | Random access, byte-level | Page-level, sequential within a block |
| **Write/erase granularity** | Byte/word programmable, block erase | Page programmable, block erase |
| **Cell size (relative)** | Larger (2 contacts per cell) | Smaller (shared contacts across string) | 
| **Primary use case** | Code execution (XIP), small data | Mass storage (SSDs, USB, memory cards) |
| **Introduced** | Intel, 1988 | Toshiba, 1987 (announced), production mid-1990s |

NAND's series-connected string architecture is the source of both its principal advantage and its principal etch engineering challenge. Because adjacent cells in a string share a single active area strip and are separated only by the gate stack itself (no isolation contact between them), NAND achieves a theoretical cell size of 4F² (where F is the minimum lithographic feature size) — dramatically smaller than NOR's cell size, which requires a contact for every cell or every two cells. This density advantage is what made NAND the technology of mass storage. It is also what makes floating-gate-to-floating-gate etch defects (Chapter 11) catastrophic rather than merely undesirable: there is no isolation contact to absorb a bridging defect between neighboring cells.

### 1.2 String, Block, and Page Organization

A NAND array is organized hierarchically:

- **Cell:** A single floating gate transistor, storing one or more bits depending on the number of distinguishable threshold voltage (Vt) states programmed (SLC: 1 bit/cell, 2 states; MLC: 2 bits/cell, 4 states; TLC: 3 bits/cell, 8 states; QLC: 4 bits/cell, 16 states)
- **String:** A series connection of 16, 32, 64, or (in later generations) 128+ cells between a bit line select transistor and a source select transistor
- **Page:** The set of cells sharing a single word line within a block; the unit of program and read operations
- **Block:** The set of strings sharing the same bit lines, spanning all word lines in that physical region; the unit of erase operations

This hierarchy matters to the etch engineer for a specific reason: the floating gate etch is performed once, across the entire array, defining every cell in every string in every block simultaneously. There is no opportunity to correct a systematic etch bias after the fact on a per-cell or per-block basis — whatever profile, CD, and damage characteristics the etch produces are baked into millions (per die) to billions (per wafer) of cells uniformly. A 2% systematic CD bias is not 2% of cells failing; absent sufficient process margin, it can be a hard yield or reliability cliff affecting the entire array simultaneously.

### 1.3 Why "Planar" and What It Contrasts With

"Planar" NAND describes every NAND generation in which the floating gate cell is built as a conventional, laterally-scaled transistor on a bulk or SOI silicon surface — the channel, floating gate, and control gate are stacked vertically within a single lithographically-defined cell footprint, and density scaling comes entirely from shrinking that footprint generation over generation (the classic Dennard-style scaling path). This contrasts with **3D NAND**, introduced commercially starting in 2013 (Samsung's first V-NAND generation), in which the cell count per unit area is increased not by shrinking the lateral cell footprint further, but by stacking cells vertically in a channel that threads through dozens to hundreds of stacked conductive layers.

This book is exclusively about the planar architecture — the floating-gate-over-channel cell built via lateral lithographic scaling — because:
1. It was the dominant NAND architecture for roughly two decades (circa 1995–2013 in volume production, with some planar derivatives persisting later at mature nodes)
2. Its etch challenges are qualitatively different from 3D NAND's (high-aspect-ratio vertical channel etch, charge-trap film stacks) even though both are "NAND flash"
3. Understanding *why* planar scaling stopped making sense (Chapter 15) requires first understanding, in detail, what planar scaling actually did to the etch process window — which is the purpose of Parts II and III of this book

---

## Part 2: The Floating Gate Cell

### 2.1 Basic Cell Structure

A planar floating gate NAND cell, in cross-section along the word line (gate) direction, consists of the following stack, from the silicon substrate upward:

| Layer | Typical Thickness (advanced planar node) | Function |
|-------|------------------------------------------|----------|
| **Tunnel oxide** | 6–9 nm | Allows Fowler-Nordheim tunneling for program/erase; must block charge leakage during retention |
| **Floating gate (FG) polysilicon** | 60–100 nm | Charge storage node; fully electrically isolated conductor |
| **Interpoly dielectric (ONO)** | 10–15 nm (oxide equivalent) | Blocks charge leakage from FG to CG; sets coupling ratio |
| **Control gate (CG) polysilicon** | 60–100 nm | Word line conductor; capacitively couples programming voltage to FG |
| **Silicide/metal cap (WSix or similar)** | 50–100 nm | Reduces word line sheet resistance for array-level RC delay |
| **Hard mask (oxide/nitride/carbon)** | Process-dependent | Pattern transfer layer; typically consumed or partially consumed during etch |

The floating gate is the defining feature: unlike the control gate, it has **no electrical contact to anything** — not to a word line driver, not to a bit line, not to any other structure. It is a fully isolated conductor whose only electrical interaction with the rest of the device is capacitive (to the channel below, through tunnel oxide; and to the control gate above, through the ONO interpoly dielectric). Charge placed on this isolated conductor — electrons, during a program operation — remains there, modulating the threshold voltage of the transistor, for as long as the surrounding dielectrics successfully prevent it from leaking away. Chapter 4 develops this charge storage physics and its coupling ratio dependence in detail; it is previewed here because it explains why the etch process (Part II) is held to such a demanding standard: **any etch-induced leakage path around or through the tunnel oxide or ONO dielectric is a direct, irreversible threat to the core function of the device.**

### 2.2 Why Floating Gate, Specifically

Floating gate is not the only way to build a non-volatile charge-storage cell. The competing approach, charge-trap memory (silicon-oxide-nitride-oxide-silicon, SONOS, and its variants), stores charge in discrete traps within a nitride layer rather than on a continuous conductive floating gate. Both approaches reached volume production, but for different roles:

- **Floating gate** dominated planar NAND because a continuous conductive storage node gives a larger, more easily sensed threshold voltage shift per stored electron, and because the technology built on decades of floating-gate EEPROM manufacturing experience predating NAND itself
- **Charge-trap (SONOS/TANOS)** found use in some NOR and embedded applications, and became the default storage mechanism for 3D NAND, because distributing charge across discrete traps makes the cell inherently tolerant of a single localized leakage path (a pinhole defect in a floating gate's surrounding oxide can discharge the entire node; the same defect in a charge-trap layer only discharges the traps in its immediate vicinity)

This book is specifically about floating gate etch because the conductive, continuous nature of the floating gate is precisely what makes its etch definition — cutting a continuous polysilicon film into millions of fully isolated, identically-sized islands, each electrically perfect — such a demanding manufacturing problem. A charge-trap film, by contrast, does not need to be etched into isolated islands at all in some 3D NAND integration schemes; the nitride layer can remain continuous, because charge mobility within the trap layer is low enough that lateral charge spreading between cells is not a first-order concern. Floating gate NAND has no such luxury — electrical isolation between adjacent floating gates **is** the etch's job, not an inherent material property making the etch forgiving.

### 2.3 Coupling Ratio: A Preview

The control gate does not sit directly on the channel — it sits on top of the floating gate, which sits on top of the channel. Voltage applied to the control gate therefore does not appear in full on the floating gate; it is attenuated by a capacitive voltage divider formed between the control-gate-to-floating-gate capacitance (through ONO) and the floating-gate-to-channel capacitance (through tunnel oxide), plus parasitic capacitances to neighboring cells. This divider ratio is the **coupling ratio**, conventionally defined as:

$$\alpha_G = \frac{C_{ONO}}{C_{ONO} + C_{tunnel} + C_{parasitic}}$$

A higher coupling ratio means more of the control gate voltage reaches the floating gate, which means lower control gate voltages are needed to achieve a given program/erase electric field across the tunnel oxide. Coupling ratio is primarily a *geometric* quantity — it depends on the surface area and spacing of the floating gate relative to the control gate above and the neighboring cells beside it — which means **the etched shape of the floating gate directly sets the coupling ratio**, and therefore directly sets the required program/erase voltages, and therefore directly affects peripheral circuit design, power consumption, and reliability margin. Chapter 4 develops this relationship quantitatively. It is introduced here to make a general point that recurs throughout this book: in floating gate NAND, **etch geometry is not merely a yield concern — it is a first-order device design parameter**, to a degree that has no equivalent in most other semiconductor etch applications.

---

## Part 3: Why the Etch Defines the Cell

### 3.1 The Stack as Manufactured vs. the Stack as Modeled

Device physics textbooks draw the floating gate cell as an idealized rectangular cross-section: perfectly vertical sidewalls, perfectly flat interfaces, uniform film thicknesses. The etched reality looks different in ways that matter:

- Sidewalls are never perfectly vertical; some taper or bow is inevitable, and it directly changes the effective capacitor areas that set the coupling ratio
- Corner rounding at the top and bottom of the floating gate concentrates electric field, affecting both program/erase uniformity and long-term dielectric reliability at those corners
- Residual polymer or incomplete removal of etch byproducts at the base of the stack can leave resistive or leaky paths exactly where the tunnel oxide needs to be pristine
- Line edge roughness transferred from the patterning stack through the etch becomes threshold voltage variation from cell to cell, directly consuming the Vt margin that multi-level-cell (MLC/TLC/QLC) storage schemes depend on

None of this is a minor footnote to device physics — it *is* the device physics, as actually realized in silicon. This book's organizing premise is that a floating gate cell's real-world behavior (retention, endurance, Vt distribution width, inter-cell interference) is substantially determined by etch process decisions, and that treating etch as a downstream "manufacturing detail" disconnected from device design is a category error that the industry's own production history repeatedly punished.

### 3.2 A First Look at the Etch Sequence

The floating gate stack etch, developed in full in Part II, proceeds roughly as follows (illustrative sequence; specific chemistries and the reasoning behind each step are developed chapter by chapter):

1. **Hard mask open:** Pattern transfer from photoresist into a more etch-resistant hard mask material (Chapter 5)
2. **Silicide/metal cap etch:** Breaking through the WSix or metal conductor (Chapter 6)
3. **Control gate polysilicon etch:** Cutting through the control gate, typically the thickest single polysilicon layer in the stack (Chapter 6)
4. **ONO breakthrough:** Etching the oxide-nitride-oxide interpoly dielectric, chemically the most different step in the sequence (Chapter 7)
5. **Floating gate polysilicon etch:** Cutting through the floating gate with a chemistry tuned for maximum selectivity to the tunnel oxide beneath (Chapter 8)
6. **Soft landing / overetch:** A final, gentler process step intended to clear residual floating gate material at cell edges without meaningfully consuming tunnel oxide or damaging the channel (Chapter 8, Chapter 9)

Each of these six steps must be optimized individually and then integrated so that the cumulative profile, CD, and damage outcome meets device specification — not just at the end of development, but repeatably, across every wafer, for the entire production lifetime of the node. That integration problem is the subject of this book.

---

## Part 4: Production History and Technology Node Context

The following table summarizes representative planar NAND technology node generations, illustrating the scaling trajectory that Parts II through IV of this book trace in etch-specific detail. Values are representative/illustrative of publicly reported industry trends rather than any single manufacturer's exact specifications.

| Era (approximate) | Representative Half-Pitch | Bits/Cell | Notable Etch-Relevant Characteristics |
|--------------------|---------------------------|-----------|----------------------------------------|
| Mid-1990s | >400 nm | 1 (SLC) | Generous etch margin; stack etch largely inherited from EEPROM/logic poly etch practice |
| Early 2000s | 130–180 nm | 1–2 (SLC/MLC) | ONO interpoly dielectric etch becomes a distinct, optimized process step |
| Mid-2000s | 50–90 nm | 2 (MLC) | Self-aligned floating gate (SA-FG) integration becomes standard; FG/STI coupling (Chapter 3) becomes a first-order concern |
| Late 2000s | 30–50 nm | 2–3 (MLC/TLC) | Microloading and ARDE effects (Chapter 12) become yield-relevant; stringer control (Chapter 11) becomes a dedicated process module |
| Early 2010s | 15–25 nm | 2–3 (MLC/TLC) | Cell-to-cell interference and tunnel oxide damage margins (Chapters 4, 13) approach physical limits; industry-wide transition to 3D NAND begins |

By the early 2010s, essentially every major NAND manufacturer had announced or shipped a 3D NAND roadmap, even while continuing planar production at trailing nodes for cost-sensitive applications. Chapter 15 returns to this table and explains, mechanism by mechanism, which specific etch-and-device physics limits were responsible for each step of this trajectory — and why no incremental etch process improvement was sufficient to extend it further.

---

## Chapter Summary

- NAND's series-string architecture gives it a density advantage over NOR flash, at the cost of making floating-gate-to-floating-gate isolation — an etch responsibility — electrically critical
- The floating gate is a fully isolated conductor; its only interactions with the rest of the device are capacitive, through the tunnel oxide below and the ONO interpoly dielectric above
- Floating gate etch geometry directly sets the coupling ratio, making etch output a first-order device design parameter rather than a downstream manufacturing detail
- The floating gate stack etch is a sequence of distinct, chemically different steps (silicide, polysilicon, ONO, polysilicon again) that must be integrated as one continuous, repeatable process
- Across roughly two decades of planar scaling, the etch process window narrowed generation over generation until it motivated the industry-wide transition to 3D NAND — the subject this book builds toward in Chapter 15

## Study Questions

1. Why does NAND's series-string architecture make floating-gate-to-floating-gate bridging defects more consequential than an equivalent defect would be in a NOR array?
2. Explain, in your own words, why coupling ratio is primarily a geometric (etch-dependent) quantity rather than a materials quantity.
3. A process engineer proposes optimizing the control gate polysilicon etch step purely for maximum etch rate, independent of the ONO and floating gate etch steps that follow it. What risks does this chapter's framing suggest such an approach creates?
4. Why is "planar" NAND etch fundamentally a different engineering problem from 3D NAND vertical channel etch, even though both store charge using closely related physics?

---

[← Preface](../PREFACE.md) · [Index](../INDEX.md) · [Next: Chapter 2 →](02-stack-materials.md)
