---
layout: post
title: Shared Anchor Load Resolution & Capacity Verification 
image: "/img/posts/morie_anchor/morie_anchor.png"
tags: [Offshore Floating Wind, Anchors, Suction Piles, Shared Anchors, Geotechnical Engineering, Python]
---

# Celtic Sea Floating Offshore Wind – Shared Anchor Load Resolution & Capacity Verification

## Executive Summary

This study establishes the **geotechnical verification layer** of Morie Analytics by transforming **mooring-derived loads into capacity-assessed anchor evaluation**.

The workflow identifies the governing event, extracts concomitant loads, transfers them through embedded chain mechanics to main padeye elevation, resolves shared-anchor demand and verifies suction pile capacity.

The result is a **reproducible framework** connecting system response, load transfer and geotechnical resistance.

This module represents the point where **mooring demand and soil resistance are combined into preliminary geotechnical design assessment**.

> Site intelligence → Layout generation → Soil reconstruction → Mooring physics → **Anchor verification** → Cable optimization


## Project Scope

- Governing event identification  
- Concomitant load extraction  
- Load transfer from mudline to main padeye  
- Shared-anchor load resolution  
- Capacity verification  

This study converts **mooring loads into geotechnically assessed anchor design**.


## Engineering Context

Shared anchors reduce cost but introduce:

- Multi-directional loading  
- Accumulation of vertical uplift and torsional effects
- Complex soil–structure interaction  

The key principle is:

**Design must be based on simultaneous load conditions, not isolated maxima.**

This workflow ensures a **consistent transition from system mechanics to geotechnical verification**.  


## Inputs and Data Sources

This study builds directly on upstream Morie Analytics outputs:

### From `morie_site`

- Bathymetry and soil classification grids
- Lease boundary definitions

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
- Coupled capacity model parameters  

This provides the **load and resistance inputs required for anchor verification**.


## System Flow

Mooring Response → Critical Event → Load Transfer → Anchor Resolution → Capacity Check

The architecture ensures **traceability from system loads to geotechnical verification**.

### Processing Workflow

1. Load mooring results  
2. Identify governing event  
3. Extract concomitant loads  
4. Transfer loads to padeye  
5. Resolve shared-anchor load state  
6. Compute torsional demand  
7. Evaluate suction pile capacity  
8. Verify load–capacity interaction  

This converts **mooring loads into capacity-assessed anchor design**.


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


<div align="center">
  <img src="/img/posts/morie_anchor/concomitant_loads.png" 
       alt="Concomitant mooring loads extracted at peak event showing simultaneous loading conditions across multiple lines" 
       width="700">
</div>
*Figure 4 – Concomitant loads at peak event.*

### Engineering Interpretation

The anchor must be checked against **simultaneous load conditions**, not independent maxima.


## Load Extraction

Loads are extracted at the **mudline elevation point** and transferred to the embedded **padeye connection point** through inverse catenary mechanics:

- Horizontal → Ha  
- Vertical → Va  
- Direction → θa  

### Link with Soil Reconstruction

The transformation from mudline loads to padeye loads on sandy soils depends on:

- Soil friction angle (φ)  
- Relative density (Dr)  
- Embedded line behavior  

These parameters are provided by `morie_soil`, establishing a direct coupling between:

- Mooring response  
- Soil-dependent load transfer 

## Anchor-Level Soil Profile (fowt1b)

The selected anchor **fowt1b** is exported with its fully reconstructed soil profile in a structured format (`profile_map`), directly usable in downstream anchor capacity models.

This structure represents the **final engineering output** of the soil and it was generated in the previous study case `morie_soil`.


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

- Loads evolve along embedded chain, reducing the tension and increasing the angle with the horizontal plane  
- Chain and soil properties influence transfer  
- Padeye loads govern anchor design 


## Anchor Load Aggregation

Loads from all connected lines are combined into a **single anchor-level demand**, integrating both **vectorial force resolution and torsional effects**. 
This enables the transition from a multi-line system to a unified load state suitable for capacity verification.

### Shared Anchor Load Resolution

<div align="center">
  <img src="/img/posts/morie_anchor/shared_anchor_planview.png" 
       alt="Plan view of shared anchor showing resolved horizontal load vectors from multiple mooring lines" 
       width="500">
</div>
*Figure 7 – Load vectors acting on a shared anchor.*

Each line load is decomposed according to its directional contribution, allowing horizontal forces to be combined through vector summation into a single 
equivalent resultant. Vertical components are accumulated directly, forming a unified 3D force state at the anchor.

### Torsional Effects

<div align="center">
  <img src="/img/posts/morie_anchor/shared_anchor.png" 
       alt="System-level view of shared anchor interaction showing multiple line load contributions and resulting load state" 
       width="400">
</div>
*Figure 8 – Shared-anchor interaction.*

In parallel, torsional demand arises from the misalignment between load directions and padeye geometry. Horizontal forces acting at an eccentricity generate 
rotational effects, with each line contributing to the overall torsional demand. The total torsion reflects the cumulative influence of all connected lines within 
the shared-anchor system.

### Engineering Interpretation

This step converts:

> Multiple line forces → Unified anchor-level load state (V, H, M, T)

This is the **critical interface between physics and design**, where distributed mooring interactions are reduced to a **single 3D load state with associated torsion**, 
governing anchor capacity verification. 

## Capacity Methodology Basis

The suction pile capacity workflow used in this study is based on the Kay / Kay & Palix VHM resistance-envelope formulation for caissons in undrained soils.

The methodology represents the anchor response through a combined VHM interaction surface, where:

- V = vertical load  
- H = horizontal load  
- M = overturning moment about a horizontal axis  

The formulation is derived from finite-element-based resistance envelopes for suction caissons under combined loading and is used here as a preliminary engineering assessment method.

This study does not use a direct industry-standard code formulation for suction pile capacity. Instead, it adopts the Kay VHM framework as a physically consistent capacity-screening methodology suitable for early-stage floating offshore wind assessment.


## Suction Pile Uncoupled Capacity

<div align="center">
  <img src="/img/posts/morie_anchor/suction_plot.png" 
       alt="Suction pile geometry showing diameter, embedded length, and padeye position used for anchor capacity evaluation" 
       width="600">
</div>
*Figure 9 – Suction pile geometry.*

The suction pile capacity is evaluated by considering both **vertical and horizontal resistance mechanisms**, which together define the admissible load domain of the anchor.

<div align="center">
  <img src="/img/posts/morie_anchor/anchor_failure_modes.PNG" 
       alt="Suction pile failure mechanisms including uplift, sliding, and rotational modes under combined loading" 
       width="600">
</div>
*Figure 10 – Vertical failure mechanisms.*

Vertical capacity is governed by a combination of failure modes, including reverse end bearing, shaft resistance and potential plug or soil failure mechanisms. 
The governing value is controlled by the most critical of these mechanisms depending on the loading conditions.

Horizontal capacity develops through lateral soil resistance mobilized along the embedded length of the pile. This response depends on soil strength, stiffness 
and the interaction between the pile and surrounding ground, with contributions from both shallow and deep failure mechanisms.

### Engineering Interpretation

Capacity depends on:

- Pile geometry and slenderness ratio (L/D)  
- Combined horizontal and vertical loading  
- Load application point (padeye position)  
- Layered soil profile and strength distribution  

The anchor response is inherently **multi-axial**, where vertical and horizontal resistances are coupled and must be assessed together to define the feasible load envelope.


## Load–Capacity Interaction Model

<div align="center">
  <img src="/img/posts/morie_anchor/anchor_ellipsoid.PNG" 
       alt="Tongue-shaped 3D VHM resistance envelope for suction caissons under combined loading" 
       width="500">
</div>
*Figure 11 – Tongue-shaped 3D VHM resistance envelope following the Kay / Kay & Palix caisson formulation.*

The tongue-shaped geometry of the VHM resistance envelope reflects the nonlinear interaction between vertical load, horizontal load and overturning moment in suction caissons under combined loading.

As one load component increases, the admissible capacity available for the remaining components progressively decreases, producing a coupled resistance domain rather than independent capacity limits.This interaction behavior is a defining characteristic of caisson response under multi-axial loading and forms the basis of the Kay / Kay & Palix preliminary assessment methodology adopted in this study.

<div align="center">
  <img src="/img/posts/morie_anchor/capacity_ellipsoid.png" 
       alt="VHM interaction surface representing combined vertical, horizontal, and moment capacity of suction pile anchor" 
       width="600">
</div>
*Figure 12 – VHM interaction surface.*

<div align="center">
  <img src="/img/posts/morie_anchor/capacity_envelope.png" 
       alt="VH capacity envelope showing allowable combinations of vertical and horizontal loads for suction pile design" 
       width="600">
</div>
*Figure 13 – VH capacity envelope.*

### Engineering Interpretation

The interaction model defines the admissible combinations of:

- Vertical load (V)
- Horizontal load (H)
- Overturning moment (M)

that the suction caisson can sustain simultaneously.

The resulting resistance domain forms a tongue-shaped VHM envelope derived from the Kay / Kay & Palix formulation for caissons in undrained soils.

A load condition is considered feasible only if it lies within the interaction surface, ensuring that the governing resistance mechanisms remain within admissible limits.

Torsional demand generated by padeye eccentricity is evaluated separately from the VHM interaction surface.


## Outputs Generated

- Concomitant load states  
- Padeye loads
- Shared-anchor load evaluation 
- Resultant anchor loads (Ha, Va, Ta) at padeye elevation 
- Preliminary anchor sizing and assessment    
- Capacity envelopes  
- Utilization factors  


## Engineering Applications

The outputs support:

- Shared-anchor verification  
- Preliminary anchor sizing under representative extreme loading conditions
- Geotechnical design decisions  
- Preliminary anchor optimization workflows  

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

It provides the **geotechnical transition from anchor demand to capacity-assessed design**.  


## Why It Matters Commercially

Shared-anchor strategies only create value if they remain geotechnically feasible.

- Assesses the geotechnical feasibility of shared-anchor concepts  
- Reduces unnecessary overdesign  
- Links system loads to foundation cost  
- Ensures geotechnical feasibility  

This is where:

- Shared-anchor layout assumptions are geotechnically assessed 
- Anchor cost is determined  
- System design becomes geotechnically assessable   


## Aspects to Improve

- Soil–mooring static vs dynamic decoupling loads  
- Probabilistic assessment of design loads  
- Optimization anchor design loops 
- Cyclic loading capacity
- Seismic analysis

Anchor capacity alone does not guarantee suction installation feasibility.

Additional installation checks may be required for:

- Hydraulic gradient limitations
- Piping risk
- Cavitation
- Soil plug behavior
- Achievable penetration depth

These aspects remain outside the present capacity-screening workflow. 


## Design Philosophy

This study reflects the Morie Analytics approach:

- Physics-informed  
- Modular  
- Traceable  
- Engineering-focused  
- Scalable    
