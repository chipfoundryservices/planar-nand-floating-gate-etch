# Chapter 9: RF Bias Control & Profile Engineering Across Stack Material Transitions

## Executive Summary

Earlier chapters developed chemistry step by step, material by material. This chapter develops the complementary axis: RF bias power (and, more generally, ion energy) as a continuously adjustable control variable that must be deliberately re-tuned across the sequence, not held constant, and the profile engineering consequences — bowing, tapering, notching, footing — of getting that re-tuning wrong at any single transition. It closes the loop on Part II by treating the floating gate etch sequence as a single, continuously-managed ion energy trajectory rather than five independently-optimized steps bolted together.

---

## Part 1: RF Bias Power and Ion Energy

### 1.1 The Basic Relationship

In the capacitively or inductively coupled plasma systems typically used for gate stack etch, RF bias power applied to the wafer electrode (distinct from source power, which primarily controls plasma density/ion flux in many tool architectures) determines the DC self-bias voltage that develops across the sheath at the wafer surface, which in turn determines the energy with which ions are accelerated into the wafer. Higher bias power produces higher ion energy; this is the single most direct lever process engineers have for trading off etch rate, anisotropy, selectivity, and damage against each other within a given chemistry.

### 1.2 Why Ion Energy Cannot Be Fixed for the Whole Sequence

Each step in the floating gate stack etch sequence has a different optimal point on the ion-energy tradeoff curve:

| Step | Ion Energy Priority | Reasoning |
|------|------------------------|-----------|
| **Silicide/metal cap etch** (Ch. 6) | Moderate-high | Throughput matters; no proximal damage-sensitive layer yet |
| **Control gate polysilicon main etch** (Ch. 6) | Moderate-high | Profile/anisotropy dominant concern; some margin before ONO |
| **ONO breakthrough** (Ch. 7) | Moderate, step-dependent | Must balance polymer-clearing (needs some ion energy) against approaching floating gate/tunnel oxide proximity in the final bottom-oxide sub-step |
| **Floating gate polysilicon main etch** (Ch. 8) | Reduced relative to control gate | Selectivity to tunnel oxide becomes a first-order concern even before full clearing |
| **Soft landing / overetch** (Ch. 8) | Lowest in the sequence | Tunnel oxide protection and damage minimization dominate; throughput is secondarily important here |

A single, fixed ion energy applied across this entire sequence is, by this table, guaranteed to be wrong for at least some steps — either too low for efficient silicide/polysilicon removal early in the sequence, or too high for safe floating gate/tunnel oxide proximity late in the sequence. Production recipes therefore step bias power down through the sequence, broadly tracking the priorities in this table, in coordination with the chemistry transitions developed in Chapters 6–8.

---

## Part 2: Profile Defects from Ion Energy Mismanagement

### 2.1 Bowing

Bowing — a sidewall profile defect in which the etched feature is wider at some intermediate depth than at either the top or bottom — arises from a combination of ion scattering (ions reflecting off sidewalls at glancing incidence and striking slightly below their nominal vertical trajectory) and a chemical isotropic etch component that is locally strongest where ion-assisted passivation clearing is weakest. Excessive bias power, or an imbalance between ion energy and the passivation chemistry's polymer deposition rate (Chapter 6, Chapter 7), tends to worsen bowing by increasing the chemical isotropic component relative to directional ion-assisted removal at mid-sidewall locations.

### 2.2 Footing (Notching)

Footing describes a profile defect at the base of an etched feature, where the sidewall flares outward just above the underlying interface, commonly caused by ion deflection off the underlying material's surface (particularly at an interface between a conductor and an insulator, where charging effects can locally deflect ion trajectories, a specific case of the plasma-induced charging mechanism developed further in Chapter 13) or by reduced ion-assisted passivation clearing efficiency very close to an etch-stop interface. Footing at the floating-gate/tunnel-oxide interface is a specific concern this book returns to repeatedly, because a footed profile at that location locally reduces the margin between the floating gate's lower sidewall edge and lateral extent, which can affect both coupling capacitance uniformity (Chapter 4) and tunnel oxide proximity at the most vulnerable part of the profile.

### 2.3 Corner Rounding

Top-corner rounding (a gradual, convex rounding of the normally sharp 90° corner at the top of an etched feature, where the sidewall meets the original, unetched top surface or remaining hard mask edge) results from preferential mask erosion and ion scattering effects concentrated at that corner. Some controlled corner rounding is often deliberately engineered (rather than merely tolerated) at the top of the floating gate, because a sharp top corner otherwise concentrates electric field during device operation in ways that can degrade long-term ONO reliability at that specific location — this is one of relatively few instances in this book where a "profile defect" in the purely geometric sense is actually a desired, intentionally-tuned outcome.

---

## Part 3: Managing Ion Energy Transitions in Practice

### 3.1 Stepped vs. Ramped Bias Power

Production recipes can implement bias power transitions between steps either as discrete steps (an abrupt change in bias power setpoint, synchronized with a chemistry change or endpoint-triggered transition) or as a continuous ramp (bias power gradually decreasing over some transition window). Stepped transitions are simpler to characterize and reproduce but can introduce a brief period immediately after the step where plasma and sheath conditions are transiently out of equilibrium with the commanded setpoint (a settling time, generally short — on the order of plasma/sheath response timescales — but not zero); ramped transitions avoid this transient at the cost of a more complex recipe and calibration burden. Most production floating gate etch recipes favor stepped transitions synchronized tightly to endpoint-detected material transitions, accepting the brief settling transient as a known, characterized, and acceptable cost.

### 3.2 Pulsed Bias and Advanced Control Schemes

More advanced bias power delivery schemes — pulsed RF bias, in which bias power is modulated on and off (or between high and low states) at a frequency much faster than the overall etch step duration — offer an additional control dimension: by adjusting pulse duty cycle and frequency, the time-averaged ion energy delivered to the wafer can be tuned somewhat independently of the instantaneous (on-state) ion energy, which can allow, for example, sufficient instantaneous ion energy to maintain effective sidewall passivation clearing while still achieving a lower time-averaged energy (and correspondingly reduced cumulative damage) than continuous-wave bias at an equivalent etch rate. Such schemes add both capability and recipe/hardware complexity, and their adoption in floating gate etch specifically reflects the industry's increasing willingness, at advanced nodes, to accept additional process complexity in exchange for the tighter damage and profile control that increasingly tight device margins (Chapter 4, Chapter 10) demanded.

---

## Part 4: Profile as an Integrated, End-to-End Outcome

### 4.1 Why This Chapter Concludes Part II

Chapters 5 through 8 each developed a specific etch step's chemistry and selectivity logic largely in isolation, which is a necessary simplification for exposition but not how the process actually behaves: ion energy, chemistry, and profile at any given step interact with the accumulated geometric and surface-condition state left by every step before it. This chapter's purpose is to make explicit what the preceding four chapters' individual-step framing could obscure: the floating gate stack etch should be engineered, validated, and controlled as a single, continuously-managed sequence — profile at the bottom of the stack is not merely "whatever the floating gate etch step, considered alone, produces" but the cumulative, compounded result of every ion energy, chemistry, and selectivity decision made from hard-mask-open onward.

---

## Chapter Summary

- RF bias power directly sets ion energy, which must be deliberately re-tuned (generally stepped downward) across the five-step sequence rather than held constant, since each step's optimal tradeoff point differs
- Bowing, footing, and corner rounding are the principal profile defects arising from ion energy and chemistry mismanagement at specific points in the sequence, each with distinct mechanisms and distinct consequences for the finished cell
- Footing at the floating-gate/tunnel-oxide interface is a specific, recurring concern connecting this chapter to coupling ratio uniformity (Chapter 4) and tunnel oxide damage (Chapter 13)
- Some corner rounding at the top of the floating gate is deliberately engineered, not merely tolerated, for long-term ONO reliability reasons
- Advanced bias delivery schemes (pulsed RF bias) offer an additional control dimension for decoupling time-averaged ion energy (damage-relevant) from instantaneous ion energy (passivation-clearing-relevant)
- The floating gate stack etch should be understood and engineered as one continuously-managed sequence, not as five independently-optimized unit processes

## Study Questions

1. Why is a single, fixed ion energy setpoint guaranteed to be suboptimal for at least some steps in the floating gate stack etch sequence?
2. Explain the mechanistic difference between bowing and footing as profile defects, and why footing at the tunnel oxide interface is of particular concern in this book's framing.
3. Why might deliberately engineered top-corner rounding be a desirable outcome rather than a defect to be eliminated?
4. What specific control capability does pulsed RF bias add beyond what continuous-wave bias power adjustment alone provides?

---

[← Chapter 8](08-floating-gate-etch-selectivity.md) · [Index](../INDEX.md) · [Next: Chapter 10 →](10-cd-control-ler.md)
