---
layout: post
title: Shared Anchor Load Resolution & Capacity Verification 
image: "/img/posts/morie_anchor/morie_anchor2.png"
tags: [Offshore Floating Wind, Anchors, Suction Piles, Shared Anchors, Geotechnical Engineering, Python]
---

# Celtic Sea Floating Offshore Wind – Shared Anchor Load Resolution & Capacity Verification

## Executive Summary

This study establishes the **geotechnical verification layer** of Morie Analytics by transforming **mooring-derived loads into capacity-verified anchor designs**.

The workflow identifies the governing event, extracts concomitant loads, transfers them through embedded chain mechanics, resolves shared-anchor demand, and verifies suction pile capacity.

The result is a **reproducible framework** connecting system response, load transfer, and geotechnical resistance.

This module represents the point where **mooring demand and soil resistance are combined into verified design decisions**.

> Site intelligence → Layout generation → Soil reconstruction → Mooring physics → **Anchor verification** → Cable optimization


## Project Scope

- Governing event identification  
- Concomitant load extraction  
- Load transfer to padeye  
- Shared-anchor resolution  
- Torsional evaluation  
- Capacity verification  

This study converts **mooring loads into geotechnically verified anchor design**.


## Engineering Context

Shared anchors reduce cost but introduce:

- Multi-directional loading  
- Vertical uplift  
- Torsional effects  
- Soil–structure interaction  

The key principle is:

**Design must be based on simultaneous load conditions, not isolated maxima.**

This workflow ensures a **consistent transition from system mechanics to geotechnical verification**.  


## Inputs and Data Sources

This study builds directly on upstream Morie Analytics outputs:

### From `morie_site`

- Bathymetry context 

### From `morie_layout`

- Shared-anchor topology  
- Connectivity  
- Anchor coordinates  

### From `morie_soil`

- Layered soil profile  
- Soil parameters  

### From `morie_mooring`

- Padeye or mudline loads  
- Time series response  
- Governing event  
- Concomitant load states  


### Additional Inputs

- Chain properties  
- Suction pile geometry  
- Capacity model parameters  

This provides the **load and resistance inputs required for anchor verification**.


## Technical Architecture

The workflow is implemented in Python using:

- `numpy`, `scipy` → numerical operations  
- `matplotlib` → visualization  
- `famodel` → system definition and data handling  
- `RAFT` → dynamic response input  
- `getTransferLoad` → embedded chain load transfer  
- `getCapacitySuction` → suction pile capacity model  

Core modules:

- system initialization → project setup and soil loading  
- RAFT interface → dynamic response simulation  
- event detection → governing load case identification  
- time-series reconstruction → PSD-to-time-domain conversion  
- concomitant extraction → simultaneous multi-line load definition  
- load transfer → mudline-to-padeye force transformation  
- vector resolution → shared-anchor load combination  
- torsion evaluation → lug-induced torque computation  
- capacity verification → suction pile response assessment   

### System Flow

Mooring Response → Critical Event → Load Transfer → Anchor Resolution → Capacity Check

The architecture ensures **traceability from system loads to geotechnical verification**.


## Processing Workflow

1. Load mooring results  
2. Identify governing event  
3. Extract concomitant loads  
4. Transfer loads to padeye  
5. Resolve shared-anchor load state  
6. Compute torsional demand  
7. Evaluate suction pile capacity  
8. Verify load–capacity interaction  

This converts **mooring loads into capacity-verified anchor design**.


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

`T_design = T_mean + 3.8·σ`

Note here that the standard deviation was increased to match the maximum load in the context of a limited time series.

<div align="center">
  <img src="/img/posts/morie_anchor/concomitant_loads.png" 
       alt="Concomitant mooring loads extracted at peak event showing simultaneous loading conditions across multiple lines" 
       width="700">
</div>
*Figure 4 – Concomitant loads at peak event.*

### Engineering Interpretation

The anchor must be checked against **simultaneous load conditions**, not independent maxima.


## Load Extraction

Loads are extracted at the **mudline connection point** are derived at the **padeye connection point**:

- Horizontal → Ha  
- Vertical → Va  
- Direction → θa  

### Link with Soil Reconstruction

The transformation from mudline loads to padeye loads depends on:

- Soil friction angle (φ)  
- Relative density (Dr)  
- Embedded line behavior  

These parameters are provided by **morie_soil**, establishing a direct coupling between:

- Mooring response  
- Soil-dependent load transfer 

## Anchor-Level Soil Profile (fowt1b)

The selected anchor **fowt1b** is exported with its fully reconstructed soil profile in a structured format (`profile_map`), directly usable in downstream anchor capacity models.

This structure represents the **final engineering output** of the soil and it was generated in the previous study case **morie_soil**.

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
            'Dr_bot': 95.0}]}
```

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


## Outputs Generated

- Concomitant load states  
- Padeye loads
- Shared-anchor load evaluation 
- Resultant anchor loads (H, V, T)  
- Anchor sizing and verification    
- Capacity envelopes  
- Utilization factors  


## Engineering Applications

The outputs support:

- Shared-anchor verification  
- Anchor sizing  
- Geotechnical design decisions  
- Floating wind optimization  

This enables:

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

Shared-anchor strategies only create value if they remain geotechnically feasible.

- Validates shared-anchor concepts  
- Reduces unnecessary overdesign  
- Links system loads to foundation cost  
- Ensures geotechnical feasibility  

This is where:

- Layout efficiency is validated  
- Anchor cost is determined  
- System design becomes physically viable   


## Aspects to Improve

- Soil–mooring static vs dynamic decoupling loads  
- Probabilistic loads  
- Optimization anchor design loops  


## Design Philosophy

This study reflects the Morie Analytics approach:

- Physics-informed  
- Modular  
- Traceable  
- Engineering-focused  
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
```