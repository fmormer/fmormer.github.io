---

layout: post
title: Integrated Seismic Workflow for Floating Offshore Wind Anchors
image: "/img/posts/morie_seismic/morie_seismic.png"
tags: [Offshore Floating Wind, Seismic Engineering, Liquefaction, Geotechnical Engineering, Suction Piles, Offshore Geohazards, Python]
---

# Celtic Sea Floating Offshore Wind – Integrated Seismic Workflow for Offshore Anchors

## Executive Summary

This study establishes the **offshore seismic and seabed degradation layer** of Morie Analytics by extending the existing geotechnical and anchor-engineering workflow toward earthquake-driven seabed transformation and post-event anchor verification.

The workflow combines:

* Response-spectrum seismic hazard definition
* Spectrum-compatible ground-motion generation
* Cyclic liquefaction screening
* Excess pore-pressure evolution
* Effective-stress degradation
* Residual seabed resistance modeling
* Post-earthquake anchor verification

within a unified offshore engineering framework.

Building directly on the outputs of:

* `morie_site`
* `morie_layout`
* `morie_soil`
* `morie_anchor`

The study demonstrates how offshore earthquake energy propagates through the seabed and ultimately modifies anchor-level engineering behavior.

Rather than treating seismic loading as a standalone structural problem, the workflow reframes the challenge as:

> Offshore seabed transformation and degradation.

The result is a reproducible framework capable of linking within the same integrated Morie ecosystem the following aspects:

* Offshore seismic hazard
* Cyclic soil degradation
* Liquefaction-driven strength loss
* Suction-anchor engineering consequences

This study represents the transition from:

> Static offshore geotechnical verification

toward:

> Dynamic offshore geohazard intelligence and degradation-aware anchor engineering.

> Site intelligence → Layout generation → Soil reconstruction → Mooring physics → Anchor verification → **Seabed degradation & seismic intelligence**

<div align="center">
  <img src="/img/posts/morie_seismic/morie_seismic.png"
       alt="Integrated offshore seismic and seabed degradation workflow for floating offshore wind anchors"
       width="1000">
</div>

*Figure 1 – Integrated offshore seismic workflow linking seismic hazard, cyclic seabed degradation and suction-anchor engineering consequences within the Morie ecosystem.*


## Project Scope

* Offshore seismic hazard definition
* Spectrum-compatible ground-motion generation
* Cyclic liquefaction screening
* Excess pore-pressure estimation
* Effective-stress degradation modeling
* Residual-strength transformation of liquefied layers
* Recomputed suction-anchor capacity and Unity Check (UC) assessment
* Post-event engineering verification

This study converts:

**Offshore seismic excitation → seabed degradation → anchor engineering consequence**.


## Engineering Context

Floating offshore wind developments increasingly move toward deeper and more geologically complex offshore environments.
Although the Celtic Sea is not a highly seismic basin, the objective of this study is not to claim seismic criticality for the site itself.

Instead, the workflow demonstrates:

> How the Morie integrated offshore engineering framework can be extended toward seismic hazard and offshore geohazard assessment.

Traditional offshore seismic workflows often separate into disconnected analyses:

* Earthquake engineering,
* Geotechnical degradation,
* Anchor verification

This study approaches the problem differently.

Rather than focusing solely on structural seismic demand, the workflow follows the transformation of the seabed itself:

```text
Earthquake source → Ground motion at seabed → Dynamic soil response → Pore-pressure generation → Effective-stress reduction → Seabed degradation → Modified anchor resistance → Updated anchor UC
```

The key engineering question therefore becomes:

> How does offshore seismic loading transform seabed resistance and anchor capacity?

This reframes seismic engineering as:

> Offshore geotechnical degradation and post-event survivability.


## Inputs and Data Sources

This study builds directly on upstream Morie Analytics outputs.

### From `morie_site`

* Bathymetry grids
* Local engineering domain
* Spatial environmental context

### From `morie_layout`

* Floating wind layout
* Shared-anchor configuration
* FOWT and anchor coordinates

### From `morie_soil`

* Layered Celtic Sea sand profiles
* Folk-7 classification framework
* Layered `profile_map` structure
* Effective stress and soil parameters

### From `morie_anchor`

* Padeye loads
* Suction-pile geometry
* VHM interaction framework
* UC verification workflow

### Additional Inputs

* Eurocode 8 response spectrum
* Seed earthquake records
* Boulanger–Idriss liquefaction screening
* Olson–Stark residual strength framework

All workflows remain tied to the same cropped Celtic Sea engineering domain used throughout the Morie ecosystem.

This preserves continuity across:

* Site characterization
* Layered soil reconstruction
* Mooring analysis
* Anchor engineering
* Offshore seismic assessment

## System Flow

Response Spectrum → Ground Motion → Liquefaction Screening → Seabed Degradation → Updated `profile_map` → Recomputed Anchor Capacity

Throughout the workflow, this architecture preserves:

* Engineering traceability
* Geotechnical continuity
* Mechanism-aware degradation
* Reproducibility of results

### Processing Workflow

1. Define offshore seismic response spectrum
2. Generate spectrum-compatible ground motion
3. Compute Cyclic Stress Ratio (CSR)
4. Estimate Cyclic Resistance Ratio (CRR)
5. Evaluate liquefaction Factor of Safety (FoS)
6. Derive excess pore-pressure ratio (`ru`)
7. Transform degraded soil layers
8. Build `profile_map_seismic`
9. Recompute suction-anchor capacity
10. Compare pre- and post-earthquake UC

This converts:

**Offshore earthquake excitation → engineering-ready degradation assessment**.

---

## Offshore Seismic Hazard Definition

The workflow begins by defining a target offshore response spectrum consistent with Eurocode 8 Type 2 seismic conditions.

<div align="center">
  <img src="/img/posts/morie_seismic/fig1_target_vs_matched_spectrum.png"
       alt="Target versus matched offshore response spectrum for the Celtic Sea seismic workflow"
       width="900">
</div>

*Figure 2 – Offshore seismic response spectrum and spectrally matched ground motion used for the Celtic Sea seismic workflow.*

The response spectrum defines the frequency-domain seismic hazard applied at seabed level.

The selected spectrum uses:

* Eurocode 8 Type 2 spectrum
* Soil Class C assumptions
* Effective seabed Peak Ground Acceleration (PGA) = 0.15·g
* 5% damping ratio

### Engineering Significance

For downstream seabed degradation analyses, this provides:

* Engineering-consistent seismic excitation,
* Offshore-compatible seismic loading,
* Reproducible hazard definition


## Spectrum-Compatible Ground Motion

Once the target spectrum is defined, a spectrum-compatible acceleration time history is generated from a seed earthquake record.

<div align="center">
  <img src="/img/posts/morie_seismic/fig2_matched_time_history.png"
       alt="Matched offshore acceleration time history and Arias intensity accumulation"
       width="1000">
</div>

*Figure 3 – Spectrum-compatible acceleration time history used for cyclic seabed loading and liquefaction screening.*

The workflow performs frequency-domain spectral matching to ensure consistency between:

* Target hazard definition,
* Realizable cyclic loading history.

The resulting signal preserves:

* Duration and cyclic accumulation effects
* Loading reversals
* Frequency content
* Arias-intensity evolution

### Engineering Significance

This step converts:

> Frequency-domain seismic hazard

into:

> Realizable cyclic seabed forcing.

A critical aspect is that:

> High-cycle low-amplitude shaking persists beyond the PGA peak.

This is particularly important for offshore liquefaction screening because cyclic pore-pressure accumulation is not controlled by PGA alone.


## Liquefaction Screening and Seabed Transformation

The core of the workflow evaluates how cyclic loading transforms seabed resistance.

<div align="center">
  <img src="/img/posts/morie_seismic/fig3a_liquefaction_screening.png"
       alt="Liquefaction screening chain for offshore layered sands"
       width="1200">
</div>

*Figure 4 – Offshore liquefaction screening chain linking effective stress, CSR, CRR, factor of safety and excess pore-pressure ratio.*

The workflow evaluates:

```text
σ'v(z) → CSR(z) → CRR(z) → FoS(z) → ru(z)
```

using:

* Seed–Idriss cyclic stress formulation
* Boulanger–Idriss liquefaction screening
* Layer-aware effective stress calculations
* Relative-density-dependent resistance estimation

### Excess Pore-Pressure Ratio

The degradation state is quantified using the excess pore-pressure ratio, `ru`.

This parameter describes how much of the initial effective vertical stress has been counteracted by earthquake-induced pore-pressure build-up.

In practical terms:

| `ru` | Interpretation |
| -------- | ---------------------- |
| `ru ≈ 0` | negligible degradation |
| `ru → 1` | liquefaction onset |

As cyclic loading accumulates, pore pressure increases and effective stress decreases. When `ru` approaches 1, the soil skeleton loses most of its effective confinement and the layer is treated as liquefied or strongly degraded.

Within the Celtic Sea demo:

* Upper loose sand approaches liquefaction conditions
* Deeper dense sand remains competent

This produces a layered degradation profile highly relevant for suction-anchor behavior.

## Effective-Stress Reduction and Residual Strength

Once liquefaction triggering is identified, degraded layers are transformed into residual-strength material states.

<div align="center">
  <img src="/img/posts/morie_seismic/fig3b_degraded_profile.png"
       alt="Effective stress and residual shear-strength transformation after liquefaction"
       width="1200">
</div>

*Figure 5 – Effective-stress collapse and constitutive transformation from drained sand behavior toward residual undrained response.*

As cyclic shaking increases pore pressure within the seabed, the soil progressively loses effective confinement.
This reduction in effective stress directly reduces the available shear resistance of the sand layers and modifies the governing anchor-capacity mechanisms.

Within the workflow:

* Loose liquefiable sands experience strong degradation
* Intermediate layers transition toward partially degraded states
* Dense deep sands remain largely competent

Rather than applying a simple reduction factor, the workflow transforms the constitutive response of the degraded layers.
The degraded profile therefore transitions from **drained Mohr-Coulomb behavior** toward **residual undrained response** through the Olson–Stark residual-strength framework.

### Engineering Significance

This step creates the degraded seabed representation used by the suction-anchor solver:

`profile_map_seismic`

The seismic problem therefore becomes modify `profile_map`→ rerun `getCapacitySuction()`→ compare `UC`


## Anchor Engineering Consequences

The degraded seabed profile is then propagated into the suction-anchor engineering workflow.

### Three-Scenario Taxonomy

The verification framework evaluates three engineering states:

| Scenario | Description                         |
| -------- | ----------------------------------- |
| A        | Baseline ULS                        |
| B        | Co-seismic pseudostatic loading     |
| C        | Post-event degraded seabed survival |

This separates **increased seismic demand** from **reduced post-liquefaction resistance**.

Scenario C does not represent the same loading condition as the baseline case. Following the seismic event, the workflow assumes a degraded seabed state combined with a 
residual operational loading condition representative of post-event survivability assessment.

This distinction is important because the governing mechanism is no longer driven solely by transient seismic demand, but by the interaction between:

- Reduced seabed resistance
- Modified anchor equilibrium
- Remaining environmental loading state

The post-event verification therefore evaluates whether the anchor system can remain operational after seabed degradation has occurred.

<div align="center">
  <img src="/img/posts/morie_seismic/fig4a_uc_three_scenarios.png"
       alt="Three-scenario anchor unity check comparison"
       width="1200">
</div>

*Figure 6 – Comparison between baseline, co-seismic and post-event anchor verification scenarios.*

### Engineering Interpretation

The workflow shows some of the most important findings:

* Seismic loading alone does not govern the design,
* Degraded seabed resistance becomes the controlling mechanism,
* Post-event survivability can require deeper embedment into competent layers.

> Seismic redesign changes the governing failure mechanism.

The revised geometry increases embedment into dense competent sand, recovering horizontal capacity despite degradation in upper layers.


## VHM Interaction Envelopes

The engineering consequences are further visualized through the evolution of the interaction envelopes.

<div align="center">
  <img src="/img/posts/morie_seismic/fig4b_capacity_envelopes.png"
       alt="MH and VH interaction envelopes for offshore seismic degradation scenarios"
       width="1400">
</div>

*Figure 7 – Evolution of MH and VH interaction envelopes under offshore seismic degradation scenarios.*

The workflow evaluates across the three seismic scenarios:

* MH interaction surfaces
* VH interaction surfaces
* Demand-point migration

### Engineering Interpretation

The results demonstrate:

* Collapse of the lateral capacity envelope in liquefied layers
* Strong sensitivity to embedment depth
* Recovery of survivability through deeper penetration into competent dense sand

The key design insight is:

> Offshore seismic survivability may be governed by minimum embedment into non-liquefiable layers rather than by static ULS conditions alone.


## Relationship with `profile_map`

One of the key concepts of this workflow is that the seismic problem can be integrated into the Morie ecosystem through modification of the layered `profile_map`.
The seismic framework therefore becomes:

Earthquake loading → liquefaction screening → degraded soil profile → updated anchor verification

Rather than an isolated seismic structural analysis. This preserves:

* Interoperability across Morie modules
* Layered geotechnical consistency,
* Engineering scalability.


## Outputs Generated

The workflow produces:

* Target response spectra
* Spectrum-compatible motions
* Liquefaction screening profiles
* Excess pore-pressure distributions
* Degraded soil profiles
* Residual-strength representations
* Updated `profile_map_seismic`
* Recomputed suction-anchor capacities
* UC comparison reports
* Interaction-envelope visualizations

These outputs are directly usable in offshore geotechnical and anchor-engineering workflows.


## Engineering Applications

The workflow supports:

* Offshore seismic screening
* Liquefaction susceptibility assessment
* Post-event anchor survivability studies
* Geohazard-informed anchor design
* Seabed degradation assessment
* Resilience-oriented offshore engineering workflows

This enables:

**Offshore Seismic Hazard → Seabed Transformation → Engineering Decision**


## Relationship to Other Morie Study Cases

This study establishes the seismic and geohazard extension of the Morie ecosystem.

### Receives from

* **morie_site** → environmental context
* **morie_layout** → floating wind geometry
* **morie_soil** → layered geotechnical framework
* **morie_anchor** → suction-anchor engineering workflow

### Feeds into

* Future offshore geohazard workflows
* Resilience-oriented anchor optimization
* Offshore risk-intelligence frameworks

It provides the transition from:

> Static offshore geotechnical verification

toward:

> Degradation-aware offshore engineering intelligence.


## Why It Matters Commercially

* Extends floating offshore wind workflows toward geohazard intelligence
* Supports early-stage seismic and liquefaction screening
* Enables degradation-aware anchor verification
* Bridges offshore earthquake engineering and geotechnics
* Preserves interoperability with integrated offshore workflows

This is where:

* Offshore geotechnics becomes degradation-aware
* Anchor engineering becomes resilience-oriented
* Seismic hazard becomes an integrated offshore design layer


## Aspects to Improve

* Fully coupled dynamic SSI formulations
* Time-dependent pore-pressure evolution
* Spatially variable `ru(x,y,z,t)` fields
* Foundation-confinement effects
* Probabilistic seismic hazard integration
* Native offshore FE coupling
* Multi-hazard seabed degradation workflows

These extensions would move the workflow toward:

> Fully integrated offshore geohazard intelligence systems.


## Design Philosophy

This study reflects the Morie Analytics approach:

* **Physics-informed**: degradation mechanisms follow established offshore geotechnical and seismic formulations.
* **Mechanism-preserving**: the workflow preserves the causal chain from seismic excitation to engineering consequence.
* **Geology-aware**: degradation depends on layered seabed behavior and soil-state transitions.
* **Engineering-ready**: degraded soil states feed directly into the anchor-capacity framework.
* **Reproducible**: all seismic, liquefaction and degradation workflows are configuration-driven.
* **Site-conditioned**: the framework remains tied to the reconstructed Celtic Sea engineering domain.

