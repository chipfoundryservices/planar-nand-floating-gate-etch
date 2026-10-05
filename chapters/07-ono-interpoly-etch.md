# Chapter 7: ONO Interpoly Dielectric Etch — Breaking Through Oxide-Nitride-Oxide

## Executive Summary

The ONO breakthrough step is the chemically distinct interruption in an otherwise halogen-dominant etch sequence, and it is frequently the step where overall stack etch development effort concentrates, because it must reconcile three somewhat conflicting demands: etch oxide and nitride with controlled, predictable relative rates; avoid leaving nitride or oxide residue that contaminates the subsequent floating gate polysilicon etch; and do all of this while sitting directly above the floating gate polysilicon and, not far beneath that, the tunnel oxide whose protection is this book's central concern. This chapter develops fluorocarbon-based oxide/nitride etch chemistry, the oxide-vs-nitride selectivity control problem specific to a three-layer ONO stack, and the residue and transition management considerations that connect this chapter to Chapter 8.

---

## Part 1: Fluorocarbon Chemistry Fundamentals

### 1.1 Why Fluorocarbon, Not Halogen, Chemistry

Oxide (SiO₂) and nitride (Si₃N₄) do not etch efficiently or controllably in the Cl₂/HBr chemistry used for polysilicon and silicide (Chapter 6); their etch in plasma is instead dominated by fluorine-based chemistry, typically delivered via fluorocarbon source gases (such as CF₄, CHF₃, C₄F₈, or similar species, often in combination) rather than a simple fluorine-only gas, because fluorocarbon chemistry allows a second, crucial control mechanism not available with a simple fluorine source: **polymer-forming sidewall passivation**, developed below.

### 1.2 The Carbon-to-Fluorine Ratio and Selectivity Control

Fluorocarbon plasma chemistry generates both reactive fluorine (which chemically etches both oxide and nitride by forming volatile SiF₄, among other byproducts) and carbon-containing radical/polymer-forming species, which deposit a thin fluorocarbon polymer film on exposed surfaces during etch. This polymer deposition competes with fluorine-driven etching, and the balance between the two — controllable via the specific gas chemistry (higher carbon-to-fluorine ratio gases favor more polymer deposition) and via plasma conditions (pressure, power) — is the primary lever for oxide-to-nitride selectivity control:

- **Oxide etches via a thinner, more easily ion-sputtered polymer layer** because the oxygen in SiO₂ consumes fluorocarbon polymer-forming carbon as volatile CO/CO₂, effectively self-limiting polymer buildup on oxide surfaces
- **Nitride lacks this oxygen-consuming mechanism**, so polymer can build up more readily on nitride surfaces, more effectively blocking continued fluorine-driven etch unless ion bombardment is sufficient to continuously clear it

This asymmetry means that, by tuning gas chemistry and ion energy, a fluorocarbon process can be pushed toward oxide-selective (etches oxide faster, relatively polymer-starved on oxide, more polymer-blocked on nitride) or nitride-selective (sufficient ion energy to clear polymer from both materials, more comparable etch rates) behavior, and this tunability is exactly what the ONO stack's three-layer structure requires.

---

## Part 2: The Three-Layer Etch Problem

### 2.1 Why a Single Fixed Chemistry Is Suboptimal

A single, fixed fluorocarbon chemistry optimized for the bulk of either the oxide or the nitride layer is, by construction, not optimal for the other layer, meaning a naive single-recipe approach to the full ONO stack will etch one or more of the three layers at an undesirably slow rate (hurting throughput and increasing total ion/plasma exposure time, with associated damage risk to the layers beneath) or will fail to clear one layer's byproducts/residue cleanly before the chemistry needed for the next layer is applied.

### 2.2 Multi-Step ONO Etch Recipes

Production ONO etch recipes typically use a multi-step approach, analogous to the main-etch/soft-landing structure introduced in Chapter 6, but here driven by the need to re-tune chemistry at each of the two oxide/nitride interfaces within the ONO stack itself:

| Step | Target Layer | Chemistry Tuning Objective |
|------|--------------|------------------------------|
| **Top oxide breakthrough** | Top oxide (3–5 nm) | Fast, reliable breakthrough of a thin layer; often uses a more aggressive, lower-selectivity chemistry since there is little thickness margin at risk |
| **Nitride main etch** | Nitride (4–6 nm) | Balance etch rate against selectivity to the oxide layers above and below; sufficient ion energy to prevent excess polymer blocking |
| **Bottom oxide breakthrough** | Bottom oxide (3–5 nm) | Highest-selectivity, most controlled step in the sequence, since this interface sits directly above floating gate polysilicon, which is in turn directly above tunnel oxide |

### 2.3 Why the Bottom Oxide Step Deserves Special Attention

The bottom oxide breakthrough step is arguably the most consequential single sub-step in the entire ONO etch, not because it is intrinsically more difficult to etch than the top oxide (it is the same material, similar thickness), but because of what lies immediately beneath it: floating gate polysilicon, and not far beneath that, tunnel oxide. Any chemistry carryover, excess ion energy, or incomplete endpoint control at this specific transition risks either prematurely damaging the floating gate polysilicon surface (affecting the subsequent etch step's starting condition) or, in an overetch scenario, directly exposing tunnel oxide to a fluorocarbon chemistry it was never intended to see.

---

## Part 3: Residue Formation and Removal

### 3.1 Why ONO Etch Is Residue-Prone

Fluorocarbon chemistry's deliberate polymer-forming behavior — the same mechanism that provides selectivity control (Part 1) — also means some polymer residue formation is close to unavoidable, particularly at feature sidewalls and corners where ion bombardment (which clears polymer from horizontal surfaces) is least effective. Additionally, nitride etch byproducts can include involatile or semi-volatile nitrogen- and silicon-containing species that redeposit on sidewalls or at the base of etched features under some chemistry/pressure conditions.

### 3.2 Consequences for the Floating Gate Etch Step

Residue carried over from the ONO step onto the floating gate polysilicon surface is a direct contamination concern for Chapter 8's floating gate polysilicon etch: a residue patch can locally mask the underlying polysilicon from the subsequent etch chemistry, producing a local etch-rate deficiency that, in the worst case, leaves a floating gate polysilicon stringer or incomplete clear at that location (connecting directly to the stringer/bridging defect mechanisms of Chapter 11). Production flows frequently incorporate an in-situ or ex-situ residue removal/clean step between ONO breakthrough and floating gate polysilicon main etch specifically to manage this risk, rather than relying on the floating gate etch chemistry itself to clear ONO-step residue as a side effect.

---

## Part 4: Endpoint and Transition Timing

### 4.1 A Harder Endpoint Problem Than Single-Material Steps

Because the ONO stack contains three distinct material transitions within a combined thickness of only ~10–15 nm, endpoint detection (developed fully in Chapter 14) must resolve transitions occurring close together in time, using optical emission or other in-situ signals that may have less distinguishing signal-to-noise ratio for thin-layer transitions than for the thicker, more clearly separated transitions elsewhere in the stack (silicide-to-polysilicon, polysilicon-to-ONO). Some production approaches supplement optical endpoint with time-based sub-step control (etching each of the three ONO sub-layers for a pre-characterized duration, calibrated against film thickness measurements, rather than relying solely on real-time endpoint signal for each individual sub-layer transition).

---

## Chapter Summary

- Oxide and nitride etch via fluorocarbon chemistry, distinct from the halogen chemistry used for polysilicon and silicide, with oxide-to-nitride selectivity controlled primarily through the carbon-to-fluorine ratio and the resulting sidewall polymer passivation balance
- A single fixed fluorocarbon chemistry is generally suboptimal across all three ONO sub-layers, motivating multi-step recipes re-tuned at each oxide/nitride interface
- The bottom oxide breakthrough step deserves disproportionate process control attention because it sits directly above floating gate polysilicon and, one step further, tunnel oxide
- Fluorocarbon chemistry's polymer-forming nature makes some sidewall/corner residue formation difficult to avoid entirely, creating a direct contamination risk for the subsequent floating gate polysilicon etch step
- The ONO stack's three closely-spaced material transitions make endpoint detection more difficult than for the thicker, more clearly separated transitions elsewhere in the stack, motivating supplemental time-based sub-step control in some production flows

## Study Questions

1. Explain the role of the carbon-to-fluorine ratio in fluorocarbon chemistry, and why oxide's oxygen content gives it an inherently different polymer-passivation behavior than nitride.
2. Why is a single, fixed chemistry generally insufficient to etch all three ONO sub-layers with equally good control?
3. Why does the bottom oxide breakthrough step warrant more conservative process control than the top oxide breakthrough step, even though both are nominally the same material and similar thickness?
4. How can ONO-step residue contamination manifest as a defect mechanism (previewed here, developed in Chapter 11) in the subsequent floating gate polysilicon etch step?

---

[← Chapter 6](06-control-gate-etch-chemistry.md) · [Index](../INDEX.md) · [Next: Chapter 8 →](08-floating-gate-etch-selectivity.md)
