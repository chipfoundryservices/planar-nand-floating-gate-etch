# Planar NAND Floating Gate Etch — Chapter Index

## Navigation & Quick Reference

---

## Front Matter

| Section | Status | Overview |
|---------|--------|----------|
| [README.md](README.md) | ✓ | Book overview, audience, scope, and file organization |
| [PREFACE.md](PREFACE.md) | ✓ | Why floating gate etch is an etch problem first, intellectual framework |

---

## Part I: Floating Gate Fundamentals

### The Cell, Its Materials, and Its Integration Scheme

| Chapter | File | Status | Key Topics |
|---------|------|--------|-----------|
| **1** | [01-nand-cell-context.md](chapters/01-nand-cell-context.md) | ✓ | Planar NAND array architecture, string/block/page organization, floating gate cell role, industrial context and production history |
| **2** | [02-stack-materials.md](chapters/02-stack-materials.md) | ✓ | Tunnel oxide, floating gate polysilicon, ONO interpoly dielectric, control gate polysilicon, silicide cap — material properties and why each exists |
| **3** | [03-sa-fg-sti-integration.md](chapters/03-sa-fg-sti-integration.md) | ✓ | Self-aligned floating gate (SA-FG) flow, STI trench formation using the FG stack as hard mask, gap-fill constraints, coupling to FG height/profile |
| **4** | [04-charge-retention-physics.md](chapters/04-charge-retention-physics.md) | ✓ | Floating gate charge storage physics, coupling ratio, threshold voltage window, retention/endurance mechanisms, how etch quality maps to device reliability |

---

## Part II: Stack Etch Process Design

### Engineering the Multi-Material Etch Sequence

| Chapter | File | Status | Key Topics |
|---------|------|--------|-----------|
| **5** | [05-hard-mask-strategy.md](chapters/05-hard-mask-strategy.md) | ✓ | Hard mask material selection (oxide, nitride, amorphous carbon), multi-layer mask stacks, mask selectivity requirements across the full FG stack etch |
| **6** | [06-control-gate-etch-chemistry.md](chapters/06-control-gate-etch-chemistry.md) | ✓ | Silicide (WSix) etch chemistry, control gate polysilicon etch in HBr/Cl₂/O₂ systems, profile control at the silicide/poly interface |
| **7** | [07-ono-interpoly-etch.md](chapters/07-ono-interpoly-etch.md) | ✓ | Oxide-nitride-oxide breakthrough chemistry, fluorocarbon chemistries for oxide/nitride, residue formation and removal, transition to floating gate poly |
| **8** | [08-floating-gate-etch-selectivity.md](chapters/08-floating-gate-etch-selectivity.md) | ✓ | Floating gate polysilicon etch chemistry, selectivity to tunnel oxide, soft-landing strategies, endpoint-triggered chemistry switching |
| **9** | [09-rf-bias-profile-control.md](chapters/09-rf-bias-profile-control.md) | ✓ | RF bias power strategy across material transitions, ion energy management near tunnel oxide, sidewall angle control through the full stack |

---

## Part III: Process Phenomena & Defect Control

### Physics of Failure Modes and Their Mitigation

| Chapter | File | Status | Key Topics |
|---------|------|--------|-----------|
| **10** | [10-cd-control-ler.md](chapters/10-cd-control-ler.md) | ✓ | Critical dimension control through the stack, line edge/width roughness transfer from mask to final profile, metrology approaches |
| **11** | [11-stringers-bridging-defects.md](chapters/11-stringers-bridging-defects.md) | ✓ | Polysilicon stringer formation at topography steps, gate footing, floating-gate-to-floating-gate bridging, root causes and mitigation strategies |
| **12** | [12-microloading-aspect-ratio.md](chapters/12-microloading-aspect-ratio.md) | ✓ | Microloading in dense vs. isolated word line arrays, aspect ratio dependent etch (ARDE) in the FG/STI trench geometry, compensation strategies |
| **13** | [13-tunnel-oxide-damage.md](chapters/13-tunnel-oxide-damage.md) | ✓ | Plasma-induced charging damage, antenna effects, trap generation in tunnel oxide, correlating etch conditions to retention/endurance degradation |
| **14** | [14-endpoint-detection.md](chapters/14-endpoint-detection.md) | ✓ | Optical emission spectroscopy across material transitions, endpoint signal design for silicide/poly/ONO/poly stack, soft-landing endpoint strategies |

---

## Part IV: Production Integration & Scaling Limits

### From Manufacturing Reality to Architectural Transition

| Chapter | File | Status | Key Topics |
|---------|------|--------|-----------|
| **15** | [15-scaling-limits-3d-transition.md](chapters/15-scaling-limits-3d-transition.md) | ✓ | Word line/bit line pitch scaling history, physical and electrical limits reached at advanced nodes, cell-to-cell interference, the transition to 3D NAND |
| **16** | [16-post-etch-clean-yield.md](chapters/16-post-etch-clean-yield.md) | ✓ | Post-etch clean chemistry and residue removal, inspection strategies for stack etch defects, yield learning loop and feedback to recipe development |

---

## Status Legend

| Symbol | Meaning |
|--------|---------|
| ✓ | Complete and published |
| 🔨 | In development |
| 📋 | Outline ready, writing in progress |
| 🚩 | Not yet started |

---

## Reading Recommendations

### For Process Engineers
**Optimal path:** Preface → Part I (Ch 1–4) → Part II (Ch 5–9) → Part III (Ch 10–14)

This path builds the full etch-sequence logic before addressing failure modes, matching how a process engineer would actually develop a recipe.

### For Integration Engineers
**Optimal path:** Preface → Ch 1, 3 → Ch 12 → Part IV (Ch 15–16)

This path emphasizes the SA-FG/STI coupling and its downstream scaling and yield consequences.

### For Device & Reliability Engineers
**Optimal path:** Ch 1, 4 → Ch 13 → Ch 15 → Ch 16

This path connects etch conditions most directly to retention, endurance, and field reliability outcomes.

### For Readers Focused on the 3D NAND Transition
**Optimal path:** Ch 1 → Ch 10–12 → Ch 15

This path establishes what scaling broke before explaining why the industry moved to a vertical architecture.

### Complete Reading (Recommended for Deep Understanding)
**Front to back:** Read in order, Part I → Part II → Part III → Part IV.

This provides the most rigorous foundation, since later chapters assume the stack-by-stack and defect-mechanism logic built earlier.

---

## Relationship to Sibling Volumes in This Series

- **Polysilicon gate etch (logic devices):** single-material gate etch fundamentals that this book extends into a multi-material stack context
- **3D NAND process volumes** (slit etch, memory hole etch, high-aspect-ratio ONO stack etch): the vertical successor architecture; Chapter 15 is the explicit bridge
- **Shallow trench isolation etch:** general-purpose STI processing; this book covers STI only as co-defined with the floating gate in the SA-FG flow

---

## How to Use This Index

1. **Start here** if you're new to the book — pick your reading path based on your role
2. **Reference this** while reading chapters to understand where each chapter fits in the larger narrative
3. **Quick lookup** when you need specific topics (use the Key Topics column)
4. **Status tracking** to see which chapters are complete

---

**Development Phase:** Complete (16 of 16 chapters)
