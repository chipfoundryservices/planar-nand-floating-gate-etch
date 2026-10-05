# Chapter 6: Control Gate Etch Chemistry — Silicide and Polysilicon in HBr/Cl₂/O₂ Systems

## Executive Summary

The control gate etch — cutting through the silicide/metal cap and the control gate polysilicon beneath it — is, of the five steps in the floating gate stack sequence, the one most directly descended from decades of conventional logic gate etch practice. This chapter develops the halogen-based (HBr/Cl₂/O₂) plasma chemistry used for this step, the specific role each gas species plays, and the profile and selectivity considerations unique to the silicide/polysilicon interface and the transition into the ONO layer beneath. Readers should treat this chapter as the chemistry foundation that Chapter 8 (floating gate polysilicon etch) modifies, rather than duplicates, when selectivity to tunnel oxide becomes the dominant design constraint.

---

## Part 1: Why HBr/Cl₂/O₂, and Not a Single Gas

### 1.1 The Role of Each Species

No single halogen gas, used alone, provides the combination of etch rate, selectivity, and profile control that advanced polysilicon/silicide etch requires. Production recipes are built from a small number of gas species, each contributing a distinct function:

| Gas | Primary Role | Mechanism |
|-----|---------------|-----------|
| **Cl₂** | Primary silicon/silicide etchant | Dissociates in plasma to reactive Cl radicals and ions; reacts with Si to form volatile SiClₓ species; etch is a combination of spontaneous chemical and ion-assisted reaction |
| **HBr** | Profile control, polysilicon selectivity to oxide | Produces Br radicals with lower spontaneous (chemical, non-ion-assisted) silicon etch rate than Cl; favors a more anisotropic, ion-driven etch mechanism, improving sidewall verticality and selectivity to oxide-based layers |
| **O₂** | Sidewall passivation | Reacts with etch byproducts and exposed silicon sidewalls to form a thin oxidized/passivated layer that resists lateral (undercutting) chemical attack, preserving vertical profile |

Production recipes typically blend these (and sometimes additional minority species, such as a noble gas like Ar for dilution/ion flux tuning, or small additions of other halogen-containing gases for fine selectivity or profile adjustment) in ratios tuned to the specific film stack, aspect ratio, and selectivity target of a given step.

### 1.2 Chemical vs. Ion-Assisted Etch Regimes

Plasma etch of silicon-based materials in halogen chemistries proceeds through two coupled mechanisms:

- **Spontaneous chemical etching:** Halogen radicals (Cl, Br) react directly with exposed silicon surfaces to form volatile halides, with a rate that depends on radical flux, surface temperature, and (for crystalline or polycrystalline silicon) exposed crystal face/grain orientation, but that proceeds even in the absence of ion bombardment
- **Ion-assisted (ion-enhanced) etching:** Energetic ion bombardment (primarily normal to the wafer surface, due to sheath acceleration) enhances the reaction rate at the point of impact well beyond the spontaneous chemical rate, and can also directly sputter material

Because spontaneous chemical etching is largely isotropic (it does not care about ion trajectory) while ion-assisted etching is strongly anisotropic (concentrated where ions land, predominantly the horizontal surfaces, not the vertical sidewalls), **the balance between these two mechanisms directly sets etch anisotropy** — a chemistry dominated by spontaneous chemical etch undercuts the mask badly (isotropic etch), while a chemistry that suppresses spontaneous etching and relies primarily on ion-assisted removal, combined with sidewall passivation (the O₂ role above) to further suppress any residual lateral chemical attack, achieves the vertical sidewalls required for a floating gate stack etch.

---

## Part 2: Silicide/Metal Cap Etch

### 2.1 Chemistry Considerations for WSix

Tungsten silicide etch in halogen-based chemistry proceeds via formation of volatile WFₓ or WClₓ/WBrₓ byproducts (depending on the specific halogen chemistry used), alongside the SiClₓ/SiBrₓ byproducts from the silicon component of the silicide. Because W and Si etch via somewhat different kinetics and byproduct volatility, achieving a uniform, residue-free silicide etch rate across the film (rather than one component etching preferentially and leaving the other as a rough, difficult-to-remove residual layer) is a specific chemistry tuning target distinct from pure polysilicon etch optimization.

### 2.2 Transition Management at the Silicide/Polysilicon Interface

The etch chemistry optimized for silicide removal is not necessarily optimal for the underlying control gate polysilicon, and production recipes frequently incorporate a deliberate chemistry step change (often called a "step 1 / step 2" or "breakthrough / main etch" transition) timed to the silicide/polysilicon interface, detected via endpoint signal (Chapter 14) or a pre-characterized time-based transition. An overly abrupt or poorly timed transition can leave silicide residue at the interface (an electrical and subsequent-etch-chemistry contamination concern) or can begin attacking polysilicon with a chemistry still tuned for silicide removal, producing a profile discontinuity exactly at the interface that is difficult to correct in later steps.

---

## Part 3: Control Gate Polysilicon Main Etch

### 3.1 Profile Objectives

The control gate polysilicon main etch, as the thickest single polysilicon layer in the stack (Chapter 2), carries disproportionate responsibility for the overall stack's profile quality: any sidewall angle error, bowing, or micro-roughness introduced here is inherited by the ONO and floating gate etch steps beneath it, which have progressively less margin to correct or compensate for upstream profile errors (Chapter 9). Production recipes for this step are typically tuned to achieve as close to 90° sidewall angle as practically achievable, with minimal bowing (a profile defect in which the sidewall is wider mid-film than at top or bottom, caused by a combination of ion scattering and chemical isotropic etch components) and minimal micro-roughness.

### 3.2 Main Etch to Soft-Landing Transition

Because the control gate polysilicon etch must stop at the ONO interface — a different material with different etch behavior — recipes typically incorporate a "main etch" step optimized purely for etch rate and bulk profile, followed by a lower-power, higher-selectivity "soft landing" or "overetch" step as the interface approaches, timed via endpoint detection (Chapter 14). This two-step (or more) approach balances overall process throughput (main etch can run aggressively since there is substantial polysilicon thickness margin before the interface) against the selectivity and damage control needed specifically near the material transition.

---

## Part 4: Profile Interactions with Pattern Density

### 4.1 Preview of Microloading

Control gate polysilicon etch rate is not uniform across regions of differing pattern density — densely packed word lines (the memory array itself) and more isolated or differently-spaced structures (peripheral circuit regions, dummy/edge structures at array boundaries) etch at measurably different rates under nominally identical plasma conditions, due to local reactant depletion and byproduct removal differences (developed fully in Chapter 12). This matters specifically to control gate etch chemistry selection because HBr-dominant, lower-chemical-component chemistries (favored for anisotropy, Part 1) tend to be more diffusion-limited and therefore more microloading-sensitive than Cl₂-dominant chemistries, creating a design tension between profile control and pattern-density uniformity that recipe development must resolve for the specific array/periphery layout of a given product.

---

## Chapter Summary

- Control gate etch chemistry combines Cl₂ (primary etchant), HBr (anisotropy/selectivity), and O₂ (sidewall passivation), with the balance between spontaneous chemical and ion-assisted etch mechanisms directly setting achievable anisotropy
- Silicide (WSix) etch requires chemistry tuning distinct from pure polysilicon etch, due to differing W and Si etch kinetics and byproduct volatility, and the silicide/polysilicon interface is typically managed via a deliberate chemistry step transition
- Control gate polysilicon main etch carries outsized responsibility for overall stack profile quality, since it is the thickest single polysilicon layer and profile errors introduced here propagate into every subsequent step with shrinking margin for correction
- A main-etch/soft-landing two-step approach balances throughput against selectivity and damage control near the ONO interface
- HBr-dominant chemistries favored for anisotropy tend to be more microloading-sensitive, creating a tension between profile control and across-pattern-density uniformity that must be resolved for each product's specific layout

## Study Questions

1. Explain why a chemistry dominated by spontaneous chemical etching produces poor anisotropy, and how O₂-based sidewall passivation helps counteract this.
2. Why does the silicide/polysilicon interface typically require a deliberate chemistry transition rather than a single continuous chemistry for the entire cap-plus-polysilicon etch?
3. Why does profile error introduced during control gate polysilicon etch have less "room to be corrected" by the time the floating gate polysilicon etch (Chapter 8) runs, compared to profile error introduced in that later step itself?
4. Why might an HBr-dominant chemistry, chosen for its anisotropy benefits, create a secondary microloading challenge that a Cl₂-dominant chemistry would not?

---

[← Chapter 5](05-hard-mask-strategy.md) · [Index](../INDEX.md) · [Next: Chapter 7 →](07-ono-interpoly-etch.md)
