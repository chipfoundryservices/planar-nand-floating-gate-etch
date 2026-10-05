# Chapter 11: Polysilicon Stringers, Footing, and Floating Gate Bridging Defects

## Executive Summary

This chapter examines the specific failure mode this book has previewed repeatedly since Chapter 1: residual, unintended electrical connections between structures that must be isolated. Stringers, footing-related residue, and direct floating-gate-to-floating-gate bridging are related but mechanistically distinct defect categories, and this chapter develops each one's root cause, why NAND's series-string architecture makes them disproportionately consequential (as established in Chapter 1), and the specific process mitigation strategies — both preventive (chemistry, hard mask, topography management) and detective (inspection) — that production flows use to control them.

---

## Part 1: Why Topography Creates Stringers

### 1.1 The Basic Mechanism

A polysilicon stringer is a thin, unintentionally-remaining ribbon or filament of polysilicon left behind after an etch process that was intended to clear that polysilicon completely. Stringers most commonly form at locations where the film being etched has to conform to underlying topography — a step, a sidewall, a corner — because, at such a location, the *effective* film thickness seen by a directional (anisotropic) etch is greater along the sloped or vertical surface than it is on a flat surface, even though the as-deposited film thickness (measured perpendicular to the local surface) may be nominally uniform everywhere.

### 1.2 Why Anisotropic Etch Makes This Worse, Not Better

This might seem paradoxical: anisotropic etch is generally desirable for CD and profile control (Chapter 9), yet it is specifically the directionality of anisotropic etch that creates the stringer problem. An ion-driven, vertically-directional etch removes material fastest where it travels the shortest vertical path to clear; at a topographic step, the sidewall of that step presents a surface roughly parallel to the etch direction, meaning vertically-incident ions do not efficiently clear material along that sidewall, regardless of how thin the film is when measured perpendicular to the sidewall itself. A more isotropic (chemically-dominant) etch would clear such locations more completely, precisely because it is not direction-dependent — but at the cost of the undercut and CD loss that anisotropic etch exists to prevent (Chapter 6, Chapter 9). Stringer control is therefore a direct consequence of the same anisotropy that profile control requires, not an independent, unrelated problem.

### 1.3 Where Stringers Form in This Book's Specific Stack

Given the SA-FG integration flow developed in Chapter 3, the most topographically significant step in the floating gate cell's fabrication is the STI recess (exposing floating gate sidewall above the recessed gap-fill oxide) — this step creates exactly the kind of sidewall/step topography described above, onto which the subsequently-deposited control gate polysilicon and silicide conform. The word-line-direction etch (Chapter 3, Part 4) that separates the floating gate into individual cells must then clear control gate (and, where the floating gate itself is also being cut, floating gate) polysilicon across this non-planar topography, making this specific etch step a primary stringer risk location in the overall flow.

---

## Part 2: Footing and Its Residue Consequences

### 2.1 Relationship to the Profile Defect of Chapter 9

Footing, introduced in Chapter 9 as a profile defect (sidewall flare near the base of an etched feature), has a direct defectivity consequence beyond pure geometry: a footed profile locally increases the effective film thickness an anisotropic etch must clear at that specific location, for the same fundamental reason topographic steps cause stringers (Part 1.2) — a flared, non-vertical sidewall segment presents more effective path length to a vertically-incident ion than a straight vertical sidewall does. Footing and stringers are therefore mechanistically linked: a process prone to footing at a given interface is, for the same underlying reason, prone to leaving residual material (a localized stringer-like residue) at that same interface if overetch time is insufficient to fully compensate.

### 2.2 Footing at the Floating-Gate/Tunnel-Oxide Interface, Specifically

Because footing at this specific interface (previewed in Chapter 9) occurs at the bottom of the entire stack etch sequence, any resulting residue risk is particularly dangerous: it occurs at the step with the least remaining selectivity margin (Chapter 8), meaning the overetch time increase that would most directly address a footing-related residue risk is in direct tension with the tunnel-oxide protection goal that same overetch step is also responsible for. This specific interaction — where the fix for one defect risk (residue) directly increases exposure to another (tunnel oxide damage) — is a recurring structural tension in floating gate etch process development, not a one-off coincidence.

---

## Part 3: Floating-Gate-to-Floating-Gate Bridging

### 3.1 Direct Bridging vs. Stringer-Mediated Bridging

Floating-gate-to-floating-gate bridging describes any electrical connection between two cells' floating gates that should be isolated, which can occur via at least two distinct mechanisms: **direct bridging**, in which the etch simply fails to fully separate two adjacent floating gates at some location (an incomplete clear of the gap between them, generally due to insufficient CD/spacing margin combined with some combination of CD bias, LER, or local etch rate deficiency, Chapter 10); and **stringer-mediated bridging**, in which a topography-induced stringer (Part 1) of control gate or floating gate material happens to physically connect two cells that are otherwise properly separated at the main, planar portion of their geometry.

### 3.2 Why This Defect Is Categorically Worse Than Most Others in This Book

As established in Chapter 1, NAND's series-string architecture provides no isolation contact between adjacent floating gates to absorb a bridging defect — unlike many other semiconductor defect categories, where a localized short might be isolated by a fuse, redundancy scheme, or simply affect a single transistor's performance without catastrophically affecting its neighbors, a floating-gate-to-floating-gate bridge directly couples two cells' stored charge, generally producing an immediate, severe electrical malfunction in both affected cells (and potentially corrupting read/program operations on the shared string more broadly, depending on the specific bridge location and resistance). This is why, as established in Chapter 8, production soft-landing and overetch strategies are deliberately biased toward accepting modest, controlled tunnel oxide exposure risk in preference to any residual bridging risk — the asymmetry in defect severity, not merely a notional "safety margin" preference, drives this specific process tradeoff.

### 3.3 Spacing Margin and the CD Budget Connection

Direct bridging risk connects directly to the CD budget framework developed in Chapter 10: because spacing between adjacent floating gates is the complement of floating gate CD within the fixed pitch budget, any CD bias or variation that widens the floating gate necessarily narrows the spacing, and sufficiently narrowed spacing — combined with any incomplete etch clearing in that narrowed gap — directly produces a bridging defect. This means CD control (Chapter 10) is not merely a device-performance concern but a direct defectivity concern specifically because of the bridging failure mode developed in this section.

---

## Part 4: Mitigation Strategies

### 4.1 Preventive Strategies

| Strategy | Mechanism |
|----------|-----------|
| **Topography minimization** | Reducing step height (e.g., optimizing STI recess depth, Chapter 3, to the minimum consistent with coupling ratio requirements) directly reduces the effective-thickness-at-sidewall problem underlying stringer formation |
| **Chemistry/ion-energy tuning for sidewall clearing** | A modest increase in isotropic (chemical) etch component, carefully balanced against the CD/profile cost (Chapter 9), can improve sidewall clearing at topographic steps without unacceptably degrading overall profile |
| **Overetch time, appropriately budgeted** | As developed in Chapter 8, sufficient overetch time, informed by the measured non-uniformity and topography-specific clearing-time distribution (not just planar-region clearing time), directly reduces residual stringer risk |
| **CD/spacing margin in design and lithography** | Allocating adequate nominal spacing margin in the CD budget (Chapter 10) directly reduces sensitivity of bridging risk to a given level of etch variation |

### 4.2 Detective Strategies

Stringers and bridging defects are generally difficult to detect via standard top-down inspection, because a thin stringer at the base of a topographic step, or a resistive (rather than fully conductive) bridge, may not produce a strong enough top-down imaging signal to distinguish reliably from normal process variation. Production flows typically rely on a combination of cross-sectional inspection (destructive, used for process characterization and periodic monitoring rather than 100% production screening), electrical test (which can detect the *consequence* of a bridging defect — an anomalous read/program behavior on an affected string — without necessarily localizing or characterizing the physical defect itself), and, increasingly, advanced non-destructive inspection techniques capable of detecting subtle topography-correlated residue signatures.

---

## Chapter Summary

- Stringers form because anisotropic (directional) etch clears material inefficiently at topographic steps and sidewalls, where effective film thickness along the ion trajectory exceeds the as-deposited film thickness
- Footing and stringer-related residue are mechanistically linked, both arising from non-vertical sidewall geometry presenting excess effective thickness to a directional etch
- Footing at the floating-gate/tunnel-oxide interface creates a specific structural tension: the overetch increase that addresses footing-related residue risk directly increases tunnel oxide exposure risk
- Floating-gate-to-floating-gate bridging is categorically more severe than most defect categories in semiconductor manufacturing generally, because NAND's series-string architecture provides no isolation contact to absorb it
- CD control (Chapter 10) is directly connected to bridging risk, since floating gate CD and inter-cell spacing are complementary within a fixed pitch budget
- Mitigation combines topography minimization, chemistry/ion-energy tuning, carefully budgeted overetch time, and adequate design-stage spacing margin, supported by a combination of destructive cross-sectional inspection and electrical test for detection

## Study Questions

1. Explain why anisotropic etch, generally desirable for profile control, is specifically what makes stringer formation at topographic steps difficult to avoid.
2. Why are footing and stringer-related residue described as mechanistically linked rather than as two unrelated defect categories?
3. Why does this book argue that floating-gate-to-floating-gate bridging deserves categorically more conservative process bias (toward tunnel oxide exposure risk) than most other defect categories would warrant?
4. How does the CD budget framework from Chapter 10 directly determine bridging defect sensitivity to a given level of etch process variation?

---

[← Chapter 10](10-cd-control-ler.md) · [Index](../INDEX.md) · [Next: Chapter 12 →](12-microloading-aspect-ratio.md)
