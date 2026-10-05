# Planar NAND Floating Gate Etch

## Multi-Layer Stack Plasma Etch, Self-Aligned Floating Gate Integration, and the Scaling Limits of 2D Charge-Trap-Free Flash Memory

**ChipFoundryServices Technical Series**

---

## Overview

*Planar NAND Floating Gate Etch* is a comprehensive technical treatment of the plasma etch processes that define the floating gate (FG) memory cell in planar (two-dimensional) NAND flash memory — the dominant non-volatile memory architecture from the mid-1990s through the early-2010s, and still the conceptual foundation for every 3D NAND cell etched today.

Unlike a single-material gate etch, the floating gate stack is a multi-layer sandwich — control gate polysilicon, tungsten silicide or metal, an oxide-nitride-oxide (ONO) interpoly dielectric, floating gate polysilicon, and tunnel oxide — and the etch must cut cleanly through all of them in one continuous process while leaving the delicate tunnel oxide beneath electrically undamaged. This book treats that requirement as the organizing constraint of the entire discipline:

- **Multi-Material Stack Etch:** Continuous breakthrough across silicide, polysilicon, and ONO layers without accumulating profile error
- **Self-Aligned Integration:** How the floating gate etch interlocks with shallow trench isolation (STI) formation in the self-aligned floating gate (SA-FG) process flow
- **Charge Retention as an Etch Metric:** Why etch-induced damage to the tunnel oxide and inter-cell bridging defects are read out, years later, as bit failures — not as etch defects
- **Aggressive Pitch Scaling:** Word line and bit line pitch scaling from >1µm generations down to sub-20nm, and the physical limits that scaling exposed
- **The Transition to 3D:** Why, after roughly two decades of aggressive planar scaling, the industry abandoned lateral scaling of the floating gate cell entirely in favor of vertically stacking the same basic charge-storage physics

---

## Audience

This book is designed for:
- **Process Engineers** developing or troubleshooting floating gate stack etch recipes
- **Integration Engineers** managing the interaction between FG etch, STI fill, and self-aligned flows
- **Device/Reliability Engineers** tracing bit-failure and retention-loss mechanisms back to etch root causes
- **Equipment Engineers** designing or specifying chambers for multi-material, high-selectivity stack etch
- **Memory Architects** seeking the physical scaling history that motivated the move to 3D NAND
- **Students and Researchers** studying the evolution of non-volatile memory manufacturing technology

---

## Table of Contents

### Front Matter
- **Preface:** The Floating Gate as an Etch Problem, Not Just a Device Problem

### Part I: Floating Gate Fundamentals (Chapters 1–4)
1. Planar NAND Architecture & the Floating Gate Cell
2. Floating Gate Stack Materials: Tunnel Oxide, Polysilicon, ONO, and Control Gate
3. Self-Aligned Floating Gate (SA-FG) Integration & STI Interaction
4. Charge Storage Physics & Why Etch Profile Determines Retention

### Part II: Stack Etch Process Design (Chapters 5–9)
5. Hard Mask Strategy for Multi-Layer Floating Gate Stacks
6. Control Gate Etch Chemistry: Silicide and Polysilicon in HBr/Cl₂/O₂ Systems
7. ONO Interpoly Dielectric Etch: Breaking Through Oxide-Nitride-Oxide
8. Floating Gate Polysilicon Etch & Selectivity to Tunnel Oxide
9. RF Bias Control & Profile Engineering Across Stack Material Transitions

### Part III: Process Phenomena & Defect Control (Chapters 10–14)
10. Critical Dimension Control & Line Edge Roughness at Sub-50nm Pitch
11. Polysilicon Stringers, Footing, and Floating Gate Bridging Defects
12. Microloading & Aspect Ratio Effects in Dense Word Line Arrays
13. Tunnel Oxide Damage Mechanisms & Plasma-Induced Charging
14. Endpoint Detection Across Multi-Material Stack Transitions

### Part IV: Production Integration & Scaling Limits (Chapters 15–16)
15. Cell Scaling Limits: Why Planar NAND Transitioned to 3D NAND
16. Post-Etch Clean, Inspection, and Yield Learning for Floating Gate Arrays

---

## File Organization

```
planar-nand-floating-gate-etch/
├── README.md                          (this file)
├── PREFACE.md                         (Foundational Philosophy & Context)
├── INDEX.md                           (Chapter Index & Navigation)
├── .gitignore
└── chapters/
    ├── 01-nand-cell-context.md
    ├── 02-stack-materials.md
    ├── 03-sa-fg-sti-integration.md
    ├── 04-charge-retention-physics.md
    ├── 05-hard-mask-strategy.md
    ├── 06-control-gate-etch-chemistry.md
    ├── 07-ono-interpoly-etch.md
    ├── 08-floating-gate-etch-selectivity.md
    ├── 09-rf-bias-profile-control.md
    ├── 10-cd-control-ler.md
    ├── 11-stringers-bridging-defects.md
    ├── 12-microloading-aspect-ratio.md
    ├── 13-tunnel-oxide-damage.md
    ├── 14-endpoint-detection.md
    ├── 15-scaling-limits-3d-transition.md
    └── 16-post-etch-clean-yield.md
```

This book is scoped intentionally to *chapters only* — no appendices or asset directories are declared unless and until they are actually populated, so the table of contents above always matches what is committed to the repository.

---

## Key Technical Themes

### 1. **The Stack Is the Problem**
A floating gate etch is not one etch — it is four or five etches (silicide, control gate poly, ONO, floating gate poly, sometimes a tunnel-oxide-proximal touch-up) that must behave as one continuous process. Each material transition is a place where profile, selectivity, and residue chemistry can go wrong, and errors compound downward toward the tunnel oxide.

### 2. **Self-Alignment Couples Etch to Isolation**
In the self-aligned floating gate flow, the floating gate etch and the STI trench etch are not independent unit processes — the floating gate film stack itself becomes the hard mask for STI trench formation, and STI gap-fill geometry constrains the floating gate's allowable height and sidewall angle. Changes made for etch-rate or defectivity reasons in one module ripple into the other.

### 3. **Retention Is a Downstream Readout of Etch Damage**
Floating gate charge retention is measured in years, under bias and temperature stress, long after the wafer has left the fab. Plasma-induced damage to the tunnel oxide — charging damage, trap generation, thinning at the gate edge — does not fail a wafer-level electrical test; it fails a retention bake or, worse, a return from the field. This book treats retention modeling as inseparable from etch process development.

### 4. **Scaling Exposed Physics, Not Just Lithography Limits**
As word line pitch scaled below ~30nm, failure modes that were statistically invisible at relaxed pitch (polysilicon stringers, floating-gate-to-floating-gate bridging, cell-to-cell interference) became yield-limiting. This book traces how etch process windows narrowed generation over generation until lateral scaling of the planar cell no longer made physical sense.

### 5. **Planar NAND Is the Ancestor of 3D NAND**
Every charge-storage, coupling-ratio, and interference concept developed for the planar floating gate cell reappears in 3D NAND — reoriented from a lateral array to a vertical channel. Chapter 15 treats the planar-to-3D transition not as an ending but as a coordinate transformation of the same underlying physics.

---

## Constraints & Scope

### In Scope
- Planar (2D), discrete floating gate NAND cells (SLC/MLC/TLC generations)
- Polysilicon/polysilicon floating gate–control gate stacks with ONO interpoly dielectric
- Tungsten silicide (WSix) and polycide control gate structures
- Self-aligned floating gate (SA-FG) and self-aligned STI (SA-STI) integration schemes
- Technology nodes from >1µm generations through sub-20nm planar NAND (pre-3D NAND transition)
- Capacitively and inductively coupled plasma etch systems used for gate stack definition

### Out of Scope
- 3D NAND vertical channel, memory hole, and slit etch processes (covered in sibling volumes)
- Charge-trap (SONOS/TANOS) floating-gate-free memory architectures
- Generic single-material polysilicon gate etch for logic devices (covered in the polysilicon etch volume of this series)
- Generic shallow trench isolation etch outside the self-aligned floating gate context
- Back-end-of-line, bit line contact, and peripheral CMOS process modules

---

## Relationship to Sibling Volumes

This book shares a technical series with other ChipFoundryServices etch volumes. In particular:
- **Polysilicon gate etch:** covers single-material polysilicon gate definition for logic; this book extends that foundation to the multi-material floating gate stack and its self-aligned isolation interaction
- **3D NAND process volumes** (slit etch, memory hole etch, high-aspect-ratio oxide/nitride stack etch): cover the vertical successor architecture; Chapter 15 of this book is the explicit bridge between the two
- **Shallow trench isolation etch:** covers STI as a general-purpose isolation module; this book covers STI only insofar as it is co-defined with the floating gate in the SA-FG flow

This volume does not duplicate the detailed content of those sibling books and defers to them for topics outside its stated scope.

---

## Development Status

**Status:** Complete (16 of 16 chapters)

**Version:** 1.0

---

## Attribution & License

This book is authored by **ChipFoundryServices** and distributed under the **Creative Commons Attribution 4.0 International (CC-BY-4.0)** license.

**Academic citations welcome.** Please cite as:

> ChipFoundryServices. (2026). *Planar NAND Floating Gate Etch — Multi-Layer Stack Plasma Etch, Self-Aligned Floating Gate Integration, and the Scaling Limits of 2D Charge-Trap-Free Flash Memory*. GitHub. https://github.com/chipfoundryservices/planar-nand-floating-gate-etch

---

[Begin Reading →](PREFACE.md)
