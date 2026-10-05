# Chapter 4: Charge Storage Physics & Why Etch Profile Determines Retention

## Executive Summary

This chapter develops the device physics of the floating gate cell in enough quantitative detail to make a single point precisely: retention, endurance, and threshold voltage distribution width — the metrics that actually determine whether a floating gate NAND product succeeds in the market — are not independent of etch process outcomes. They are, in large part, *etch* outcomes, expressed through a device physics vocabulary. This chapter develops coupling ratio quantitatively, connects it to programming and retention behavior, and establishes the specific etch-controlled geometric and damage parameters that Part III's defect-mechanism chapters will repeatedly trace back to.

---

## Part 1: Coupling Ratio, Developed Quantitatively

### 1.1 The Capacitive Divider

Chapter 1 introduced coupling ratio conceptually. Here it is developed as the capacitive divider it physically is. The floating gate's potential, $V_{FG}$, in response to a control gate voltage $V_{CG}$ (with other terminals held at fixed reference potentials, for simplicity) is:

$$V_{FG} = \alpha_G \cdot V_{CG} + \text{(terms from channel, source, drain coupling)}$$

where the gate coupling ratio is:

$$\alpha_G = \frac{C_{ONO}}{C_{ONO} + C_{tunnel} + C_{FG,parasitic}}$$

$C_{ONO}$ is the capacitance between control gate and floating gate (through the ONO interpoly dielectric, including both the top-surface area and any exposed sidewall area from STI recess, Chapter 3); $C_{tunnel}$ is the capacitance between floating gate and channel (through tunnel oxide); $C_{FG,parasitic}$ lumps floating-gate-to-floating-gate (neighboring cell) and floating-gate-to-substrate parasitic terms.

### 1.2 Why Higher Coupling Ratio Is Desirable, Within Limits

A higher $\alpha_G$ means a larger fraction of any applied control gate voltage reaches the floating gate, which means a lower absolute $V_{CG}$ is needed to establish a given tunnel-oxide electric field for programming or erase. This matters because:

- Lower required programming voltage reduces stress on peripheral high-voltage transistors and charge pump circuitry, which has its own area, reliability, and power consumption cost
- Lower required voltage swing, for a fixed oxide reliability budget (oxide wearout is strongly field-dependent), extends achievable program/erase cycle endurance

Coupling ratio cannot simply be maximized without limit, however, because raising $C_{ONO}$ relative to $C_{tunnel}$ generally requires either thinning the ONO dielectric (which directly increases floating-gate-to-control-gate leakage, the opposite of what ONO exists to prevent) or increasing the geometric overlap/sidewall area between floating gate and control gate (which, per Chapter 3, is set by floating gate height and STI recess depth, and trades directly against cell pitch and parasitic capacitance to neighboring cells). Coupling ratio design is therefore a genuine optimization under competing constraints, not a simple "more is better" target — and the etched geometry of the floating gate is the primary lever by which that optimization is realized in silicon.

### 1.3 Etch's Specific Levers on Coupling Ratio

| Etch-Controlled Parameter | Effect on Coupling Ratio | Relevant Chapter |
|----------------------------|---------------------------|-------------------|
| **Floating gate height** | Sets available sidewall area for $C_{ONO}$ after STI recess | Chapter 3, Chapter 8 |
| **Floating gate sidewall angle/taper** | Determines actual exposed sidewall area at a given recess depth and nominal height | Chapter 3, Chapter 9 |
| **Top corner rounding** | Affects local field concentration and effective capacitor edge geometry | Chapter 9, Chapter 11 |
| **CD uniformity (floating gate width)** | Sets $C_{tunnel}$ footprint area directly; CD variation is coupling ratio variation | Chapter 10 |
| **ONO thickness post-etch (if thinned during breakthrough)** | Directly changes $C_{ONO}$ | Chapter 7 |

This table is the quantitative version of the claim made repeatedly in this book: coupling ratio distribution across an array — which shows up to a device engineer as program/erase voltage variation and, ultimately, threshold voltage distribution width — is substantially an etch uniformity metric wearing a device-physics name.

---

## Part 2: Programming, Erase, and the Threshold Voltage Window

### 2.1 Fowler-Nordheim Tunneling

Both programming (electron injection onto the floating gate) and erase (electron removal from the floating gate) in most planar NAND designs are accomplished via Fowler-Nordheim (FN) tunneling through the tunnel oxide, with current density given approximately by:

$$J_{FN} = A \cdot E_{ox}^2 \cdot \exp\left(-\frac{B}{E_{ox}}\right)$$

where $E_{ox}$ is the electric field across the tunnel oxide and $A$, $B$ are material-dependent constants. The strong (exponential) field dependence means program/erase speed is extremely sensitive to the actual field realized across the tunnel oxide for a given applied voltage — which, per Part 1, depends on coupling ratio, and therefore on etched geometry. A cell with coupling ratio below its design target requires a higher control gate voltage (or longer pulse duration) to achieve the same programming result as a nominal cell; across an array, coupling ratio variation directly becomes programming speed and programmed-state threshold voltage variation.

### 2.2 The Threshold Voltage Window and Multi-Level Cell Storage

A floating gate cell's usable information capacity depends on how many distinguishable threshold voltage (Vt) states can be reliably programmed and read within the device's total Vt window (bounded below by erase-state Vt and above by the maximum programmable Vt consistent with read voltage and reliability limits). Each additional bit per cell (SLC → MLC → TLC → QLC) halves the nominal Vt margin available between adjacent states, which directly means each state's Vt distribution must be tighter for a higher-bit-density cell to maintain the same read error rate.

This is the device-level reason that etch-induced CD variation, profile variation, and coupling ratio variation — individually tolerable at SLC or early MLC generations — become yield- and reliability-limiting as bit density per cell increases. **The etch process does not become worse at TLC/QLC generations; the margin available to absorb its native variability shrinks**, which is a distinct and important distinction developed further in Chapter 10.

---

## Part 3: Retention — Charge Loss Over Time

### 3.1 Retention Mechanisms

Stored charge on the floating gate is lost over time through several physical mechanisms, each with a different sensitivity to etch-induced damage:

- **Intrinsic (undamaged) leakage:** Even a perfect tunnel oxide and ONO stack has some baseline leakage current at operating field and temperature; this sets the theoretical maximum retention time for a defect-free cell and is not an etch-controllable quantity
- **Trap-assisted tunneling (TAT):** Defects (traps) within the tunnel oxide or at its interfaces provide intermediate energy states that assist charge transport, increasing leakage current well above the intrinsic baseline; trap density is directly affected by plasma-induced damage (Chapter 13) during floating gate etch
- **Stress-induced leakage current (SILC):** Traps generated by *previous* program/erase cycling (not necessarily by the original etch) create additional, cycling-history-dependent leakage paths; cells with higher as-etched baseline trap density are more susceptible to SILC growth with cycling, coupling the etch-induced damage question to the endurance question
- **Localized/pinhole leakage:** A physical defect (void, residual contamination, incomplete breakthrough residue) creating a discrete high-conductance leakage path at a specific point on the floating gate; because the floating gate is a single continuous conductor, such a defect can discharge the *entire* node even if it is spatially tiny, which is the device-level consequence of the "no isolation contact" property discussed in Chapter 1

### 3.2 Retention as a Statistical, Not Deterministic, Specification

Retention specifications (commonly stated as some multi-year duration under specified temperature and cycling conditions) are inherently statistical — they describe a target failure rate across a population of cells, not a guarantee for every individual cell. This matters to etch process development because an etch defect mechanism that affects even a small fraction of cells (parts per million or lower) can still violate a retention specification stated in terms of acceptable failure rate across a multi-gigabit or multi-terabit array, long before that same defect rate would be visible as a wafer-level electrical test yield loss. This is why retention and endurance qualification (typically involving extended bake and cycling tests, sometimes with accelerated conditions and extrapolation) is treated as a distinct, later-stage gate in process development, separate from and in addition to standard wafer-level electrical test — and why etch process changes that pass wafer-level test can still fail retention qualification weeks or months later.

### 3.3 Endurance and Cumulative Damage

Endurance (the number of program/erase cycles a cell can sustain before failing to meet its specification) is degraded by the same trap-generation mechanisms that threaten retention, but cumulatively, over many cycles rather than as a single-event concern. A cell with higher as-manufactured (etch-induced) trap density starts its cycling life with less margin before cumulative, cycling-induced trap density crosses a failure threshold; this is why floating gate etch damage mitigation (Chapter 13) is evaluated not only against day-one retention metrics but against endurance-cycled retention metrics, which are more sensitive and more representative of real product use.

---

## Part 4: Cell-to-Cell Interference

### 4.1 The Parasitic Capacitance Problem

As cell pitch scales down, the parasitic capacitance term $C_{FG,parasitic}$ in the coupling ratio equation (Part 1) — specifically, the floating-gate-to-neighboring-floating-gate component — grows as a fraction of the total capacitance, because parallel-plate-like parasitic capacitance between adjacent floating gates scales inversely with the shrinking spacing between them while the "useful" capacitances ($C_{ONO}$, $C_{tunnel}$) scale with shrinking area. This produces **cell-to-cell interference**: the threshold voltage read from a given cell shifts measurably depending on the programmed state of its neighbors, because a neighboring floating gate's stored charge capacitively couples into the cell being read.

### 4.2 Why This Is Also an Etch Story

Cell-to-cell interference magnitude depends on the actual, as-etched spacing and sidewall geometry between neighboring floating gates — not merely the nominal lithographic pitch. Etch-induced CD bias, sidewall bowing, or non-uniform spacing (Chapter 10, Chapter 12) directly changes the realized parasitic capacitance, meaning two arrays patterned with identical lithography but etched with different profile control can exhibit measurably different interference behavior. This is one of the specific mechanisms (previewed in Chapter 1 and developed fully in Chapter 15) by which etch process window narrowing with scaling became a genuine physical barrier to further lateral scaling, rather than merely a yield/cost concern that could in principle be engineered around indefinitely.

---

## Chapter Summary

- Coupling ratio is a capacitive divider whose value is set primarily by etched geometry: floating gate height, sidewall angle, corner shape, and CD, not primarily by material properties alone
- Fowler-Nordheim tunneling's strong field dependence means coupling ratio variation translates directly into programming speed and programmed-state Vt variation across an array
- Multi-level cell storage (MLC/TLC/QLC) does not require a "better" etch process than SLC — it requires the same etch-induced variability to be absorbed within a proportionally shrinking Vt margin
- Retention and endurance depend on trap density and localized defect rates that are directly influenced by plasma-induced damage during floating gate etch, and are evaluated statistically across very large cell populations
- Cell-to-cell interference, driven by parasitic capacitance between neighboring floating gates, depends on as-etched spacing and profile, not merely on nominal lithographic pitch, and is one of the physical mechanisms underlying the scaling limits developed in Chapter 15

## Study Questions

1. Write the coupling ratio equation and identify which terms are primarily etch-controlled versus primarily materials-controlled.
2. Why does Fowler-Nordheim tunneling's exponential field dependence make coupling ratio variation especially consequential for programming uniformity?
3. Explain why a fixed etch-induced trap density becomes more problematic for a TLC/QLC design than for an SLC design at the same technology node.
4. Why can a localized, spatially tiny etch defect (a pinhole or residue path) discharge an entire floating gate, when a similarly tiny defect in a charge-trap memory might only affect a small fraction of the stored charge?

---

[← Chapter 3](03-sa-fg-sti-integration.md) · [Index](../INDEX.md) · [Next: Chapter 5 →](05-hard-mask-strategy.md)
