---
layout: post
title: Shared Anchor Load Resolution & Capacity Verification – Celtic Sea
image: "/img/posts/morie_anchor/morie_anchor2.png"
tags: [Offshore Floating Wind, Anchors, Suction Piles, Shared Anchors, Geotechnical Engineering, Python]
---

# Celtic Sea Floating Offshore Wind – Shared Anchor Load Resolution & Capacity Verification

## Executive Summary

This study establishes the **anchor verification layer** of Morie Analytics by transforming **mooring-derived loads into capacity-verified anchor designs**.

Starting from the mooring response generated in `morie_mooring`, the workflow identifies the governing event, extracts **concomitant loads** across all contributing lines, transfers those loads through **embedded chain mechanics**, resolves the full **shared-anchor load state**, and verifies suction pile capacity under combined loading.

A central objective of the workflow is to avoid simplified anchor checks based on isolated peak line tensions. Instead, the methodology reconstructs the **true simultaneous load condition** acting at the anchor during the governing event, preserving traceability from dynamic mooring response to geotechnical verification.

This module represents the point where **mooring-system mechanics and local soil conditions are combined into capacity-verified anchor design decisions**.

The result is a **reproducible anchor design framework** that connects system-level response, load transfer, vector resolution, torsional effects, and layered-soil capacity assessment into a structured engineering workflow.

Site intelligence → Layout generation → Soil reconstruction → Mooring physics → **Anchor verification** → Cable optimization


## Project Scope

- Governing event identification from mooring response  
- Concomitant multi-line load extraction  
- Embedded chain load transfer from mudline to padeye  
- Shared-anchor load resolution into resultant demand  
- Torsional load evaluation due to padeye eccentricity and misalignment  
- Layered-soil suction pile capacity assessment  
- VH and VHM interaction verification  
- Utilization-based anchor acceptability check  

This workflow transforms:

**Mooring Loads → Anchor Demand → Capacity Verification**


## Engineering Context

Floating offshore wind farms increasingly adopt **shared-anchor configurations**, where multiple mooring lines connect to a single anchor.

This reduces:

- Anchor count  
- Installation cost  
- Seabed footprint  

However, it introduces a more complex design problem:

- Multi-directional loading  
- Vertical uplift contributions  
- Torsional effects  
- Soil–structure interaction  

The critical point is:

**The anchor design state is not defined by isolated maxima, but by the simultaneous load combination acting during the governing event.**

This workflow resolves that by computing the **true concomitant anchor load state**, ensuring consistency between:

- Mooring response  
- Load transfer  
- Geotechnical verification  


## Inputs and Data Sources

### From `morie_mooring`

- Padeye or mudline loads (Ha, Va, θ)  
- Time series of mooring response  
- Governing event definition  
- Concomitant load states  

### From `morie_layout`

- Shared-anchor topology  
- Floater-anchor connectivity  
- Anchor coordinates  

### From `morie_site`

- Bathymetry context  
- Spatial domain  

### From `morie_soil`

- Layered soil profile (`profile_map`)  
- Soil parameters governing resistance  

### Additional Inputs

- Chain properties and embedment parameters  
- Suction pile geometry  
- Capacity model settings  


## Quantitative Scope & Processing Metrics

- Multiple shared anchors evaluated  
- 1–3 lines contributing per anchor  
- Governing event extracted from full time series  
- Load components resolved: horizontal, vertical, torsional  
- Capacity domains checked: VH and VHM  


## Technical Architecture

The workflow integrates:

- Mooring load processing  
- Event detection  
- Load transfer mechanics  
- Vector resolution  
- Capacity verification  

### System Flow

Mooring Time Series → Critical Event → Concomitant Loads → Load Transfer → Anchor Resolution → Capacity Check


## Processing Workflow

1. Load mooring results  
2. Identify governing event  
3. Extract concomitant loads  
4. Transfer loads to padeye  
5. Resolve shared-anchor load state  
6. Compute torsional demand  
7. Evaluate suction pile capacity  
8. Verify load–capacity interaction  


## Anchor System Topology

<div align="center">
  <img src="/img/posts/morie_anchor/2dfarm_shared.png" 
       alt="Floating wind farm layout showing shared-anchor configurations with multiple mooring lines connected to common anchor points" 
       width="500">
</div>
*Figure 1 – Shared-anchor configurations across the floating wind farm.*

<div align="center">
  <img src="/img/posts/morie_anchor/shared_anchor_floaters.png" 
       alt="Mooring connectivity diagram showing multiple floating turbines linked to shared anchors through mooring lines" 
       width="500">
</div>
*Figure 2 – Multiple mooring lines connected to shared anchors.*

### Engineering Interpretation

Shared anchors form a **coupled load network**, where:

- Multiple lines contribute simultaneously  
- Load directions differ  
- Vector combination governs demand  


## Critical Event & Concomitant Loads

<div align="center">
  <img src="/img/posts/morie_anchor/mooring_loads.png" 
       alt="Mooring tension time series showing dynamic load variation and peak response used to define governing load case" 
       width="700">
</div>
*Figure 3 – Mooring tension time series.*

The governing event can be represented as:

**T_design = T_mean + 3.8·σ**

<div align="center">
  <img src="/img/posts/morie_anchor/concomitant_loads.png" 
       alt="Concomitant mooring loads extracted at peak event showing simultaneous loading conditions across multiple lines" 
       width="700">
</div>
*Figure 4 – Concomitant loads at peak event.*

### Engineering Interpretation

The anchor must be checked against **simultaneous load conditions**, not independent maxima.

## Anchor-Level Soil Profile (fowt1b)

The selected anchor **fowt1b** is exported with its fully reconstructed soil profile in a structured format (`profile_map`), directly usable in downstream anchor capacity models.

This structure represents the **final engineering output** of the soil reconstruction workflow.

### Profile Structure

```python
profile_map = {
    'layers': [
        {
            'type': 'sand',
            'z_top': stick-up_length,
            'z_bottom': Z1 + stick-up_length,
            'gamma_top': 9.0,
            'gamma_bot': 10.0,
            'phi_top': 30.0,
            'phi_bot': 32.0,
            'Dr_top': 60.0,
            'Dr_bot': 75.0},
        {
            'type': 'sand',
            'z_top': Z1 + stick-up_length,
            'z_bot': Z2 + stick-up_length,
            'gamma_top': 10.0,
            'gamma_bot': 11.0,
            'phi_top': 32.0,
            'phi_bot': 37.0,
            'Dr_top': 75.0,
            'Dr_bot': 85.0},
        {
            'type': 'sand',
            'z_top': Z2 + stick-up_length,
            'z_bot': Zmax + stick-up_length,
            'gamma_top': 11.0,
            'gamma_bot': 12.0,
            'phi_top': 37.0,
            'phi_bot': 40.0,
            'Dr_top': 85.0,
            'Dr_bot': 95.0}]}```


## Load Transfer to Padeye

<div align="center">
  <img src="/img/posts/morie_anchor/anchor_inverse_catenary.png" 
       alt="Inverse catenary representation of embedded mooring chain showing load transfer from mudline to padeye within seabed" 
       width="700">
</div>
*Figure 5 – Inverse catenary load transfer.*

<div align="center">
  <img src="/img/posts/morie_anchor/load_transfer.png" 
       alt="Transformation of mooring loads from mudline to padeye including horizontal and vertical load components" 
       width="700">
</div>
*Figure 6 – Load transformation from mudline to padeye.*

### Engineering Interpretation

- Loads evolve along embedded chain  
- Soil properties influence transfer  
- Padeye loads govern anchor design  


## Shared Anchor Load Resolution

<div align="center">
  <img src="/img/posts/morie_anchor/shared_anchor_planview.png" 
       alt="Plan view of shared anchor showing resolved horizontal load vectors from multiple mooring lines" 
       width="500">
</div>
*Figure 7 – Load vectors acting on a shared anchor.*

Load resolution:

`Hx = Ha*cos(ψ)`  
`Hy = Ha*sin(ψ)`  

`H_total = √(Hx² + Hy²)`  
`V_total = ΣVa`  

### Engineering Interpretation

Multiple lines are combined into a **single 3D load state**.


## Torsional Load Evaluation

`T_i = Ha,i*r_lug*sin(ψ_lug)`  
`T_total = Σ|T_i|`

<div align="center">
  <img src="/img/posts/morie_anchor/shared_anchor.png" 
       alt="System-level view of shared anchor interaction showing multiple line load contributions and resulting load state" 
       width="600">
</div>
*Figure 8 – Shared-anchor interaction.*

### Engineering Interpretation

Torsion arises from:

- Load misalignment  
- Padeye eccentricity  
- Multi-line interaction  


## Suction Pile Capacity Model

<div align="center">
  <img src="/img/posts/morie_anchor/suction_plot.png" 
       alt="Suction pile geometry showing diameter, embedded length, and padeye position used for anchor capacity evaluation" 
       width="600">
</div>
*Figure 9 – Suction pile geometry.*

Vertical capacity:

`V_max = min(V1, V2, V3)`

<div align="center">
  <img src="/img/posts/morie_anchor/anchor_failure_modes.png" 
       alt="Suction pile failure mechanisms including uplift, sliding, and rotational modes under combined loading" 
       width="600">
</div>
*Figure 10 – Failure mechanisms.*

### Engineering Interpretation

Capacity depends on:

- Geometry  
- Load combination  
- Layered soil profile  


## Load–Capacity Interaction

<div align="center">
  <img src="/img/posts/morie_anchor/capacity_ellipsoid.png" 
       alt="VHM interaction surface representing combined vertical, horizontal, and moment capacity of suction pile anchor" 
       width="600">
</div>
*Figure 11 – VHM interaction surface.*

<div align="center">
  <img src="/img/posts/morie_anchor/capacity_envelope.png" 
       alt="VH capacity envelope showing allowable combinations of vertical and horizontal loads for suction pile design" 
       width="600">
</div>
*Figure 12 – VH capacity envelope.*

### Engineering Interpretation

Defines **admissible load combinations** and anchor utilization.

---

## Outputs Generated

- Concomitant load states  
- Padeye loads  
- Resultant anchor loads (H, V, T)  
- Capacity envelopes  
- Utilization factors  


## Engineering Applications

- Shared-anchor verification  
- Anchor sizing  
- Geotechnical design decisions  
- Floating wind optimization  

**System Response → Anchor Demand → Geotechnical Verification**


## Relationship to Other Morie Study Cases

This study is the **geotechnical verification layer** of the Morie Analytics workflow.

### Receives from

- **morie_site** → bathymetry context  
- **morie_layout** → geometry and topology  
- **morie_soil** → layered soil profile and load-transfer environment  
- **morie_mooring** → design-driving loads  

### Completes

The anchor branch of the system workflow.

It provides the **geotechnical transition from anchor demand to capacity-verified design**.  


## Why It Matters Commercially

- Validates shared-anchor strategies  
- Reduces overdesign  
- Links physics to cost  
- Ensures geotechnical feasibility  

This is where:

- Layout efficiency is validated  
- Anchor cost is determined  
- System design becomes real  


## Aspects to Improve

- Soil–mooring static vs dynamic decoupling loads  
- Probabilistic loads  
- Optimization loops  


## Design Philosophy

This study reflects Morie Analytics principles:

- Physics-based  
- Modular  
- Traceable  
- Scalable  


## How to Run

1. Place datasets in `celtic_sea_share/`  
2. Install dependencies:

- `numpy`  
- `matplotlib`
- `famodel`  
 
3. Execute:

```bash
python morie_anchor.py