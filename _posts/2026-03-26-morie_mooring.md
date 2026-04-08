---
layout: post
title: Mooring System Generation & Load Analysis – Celtic Sea
image: "/img/posts/morie_mooring/morie_mooring2.png"
tags: [Offshore Floating Wind, Mooring Systems, RAFT, MoorPy, Shared Anchors, Python]
---

# Celtic Sea Floating Offshore Wind – Mooring System Generation & Load Analysis

## Executive Summary

This study establishes the **mooring physics layer** of Morie Analytics by transforming floating wind layouts into **physically consistent mooring systems and design-ready load outputs**.

Using YAML-based farm definitions, bathymetry and soil datasets, and integrated simulation tools (primarily MoorPy, with optional RAFT coupling), a modular Python workflow is developed to generate mooring configurations and extract **padeye-level loads (horizontal, vertical, and directional)** for engineering assessment.

A key objective of the workflow is to explicitly bridge **mooring system behavior and anchor demand**, enabling consistent transformation of line-level forces into **design-ready anchor loads (H, V, θ)**.

This module represents the first stage in the workflow where **physical system behavior governs design outcomes**, transitioning from geometric definition to force-driven engineering.

The result is a **reproducible computational pipeline** that connects geometry, equilibrium physics, and load transfer mechanisms into downstream anchor design inputs.

Site intelligence → Layout generation → Soil reconstruction → **Mooring physics** → Anchor verification → Cable optimization


## Project Scope

- Farm-scale mooring system generation  
- Shared-anchor configurations enabled through geometric alignment  
- Padeye-level load extraction (Ha, Va, θ) for each mooring line  
- Shared-anchor load aggregation into resultant (H, V, θ)  
- Evaluation of environmental load cases  
- Optional dynamic extension using RAFT (frequency-domain and time-domain reconstruction)  

This workflow transforms layout candidates into **engineering-ready mooring and anchor load datasets**, ensuring full traceability from:

**Layout → Mooring System → Line Loads → Anchor Demand**


## Engineering Context

Floating offshore wind farms increasingly adopt **shared-anchor configurations** to reduce installation cost and seabed footprint. In these systems, multiple mooring lines from different turbines converge into a single anchor, creating a **coupled load interaction problem** that must be resolved consistently.

Accurate engineering design requires a clear understanding of:

- Mooring system geometry and pretension  
- Static equilibrium and restoring behavior  
- Directional load redistribution under environmental forcing  
- Dynamic amplification of line tensions  
- Translation of line-level forces into **anchor demand**  

A recurring challenge in offshore workflows is that **mooring analysis and anchor design are often treated separately**, with limited traceability between:

- Line tensions from mooring solvers  
- Padeye loads at the anchor connection  
- Resultant loads required by anchor capacity models  

This workflow addresses that disconnect by building an explicit path from **layout geometry to mooring physics to anchor design inputs**.


## Inputs and Data Sources

### From `morie_layout`
- Floater positions  
- Anchor coordinates  
- Shared-anchor topology  

### From `morie_site`
- Bathymetry grids  
- Spatial domain and lease constraints  

### From `morie_soil`
- Soil reconstruction framework (`profile_map`)  
- Local soil parameters influencing load transfer  

### Additional Inputs

- YAML-based floating wind farm configuration  
- Mooring line properties and segment definitions  
- Environmental load cases (wave headings and dynamic forcing assumptions)  

All inputs are harmonized into a simulation-ready framework compatible with **FAModel**, **MoorPy**, and **RAFT**.


## Quantitative Scope & Processing Metrics

- Number of floaters: 8  
- Mooring lines per floater: 3 (total: 24 lines)  
- Shared anchors: typically 12–16 depending on topology  
- Environmental load cases: multiple wave headings (e.g., 12–24)  
- Frequency-domain resolution: ~100 frequency bins per case  
- Time-domain reconstruction: 360 s per critical case  

These metrics highlight the computational scale and reproducibility of the workflow.


## Technical Architecture

The workflow is implemented in Python using:

- `FAModel` → project structure and system definition  
- `MoorPy` → static equilibrium solver  
- `RAFT` → frequency-domain dynamic response  
- `numpy`, `scipy` → numerical operations  
- `matplotlib` → visualization  

Core modules:

- `morie_mooring.py` → main execution pipeline  
- `merge_shared_anchors.py` → shared-anchor detection and merging  
- RAFT interface → dynamic response and PSD extraction  

### System Flow

Layout → Mooring Definition → Equilibrium → Dynamic Response → Load Extraction → Anchor Demand


## Processing Workflow

1. Load floating wind farm configuration from YAML  
2. Generate mooring geometry from floater positions and heading rules  
3. Detect and merge coincident anchors  
4. Adjust line lengths and pretension  
5. Solve static equilibrium using MoorPy  
6. Evaluate environmental response using RAFT  
7. Identify governing load case  
8. Reconstruct time-domain tension histories  
9. Extract padeye-level loads  
10. Aggregate loads into anchor-level demand  

This converts a geometric layout into **design-driving forces for anchor verification**.


## Mooring System Definition

Mooring systems are generated from floater layouts using deterministic geometric rules that define **line topology and load transfer paths**.

### Key Assumptions

- 3 mooring lines per floater  
- 120° angular spacing  
- Fixed anchor radius  
- Global coordinate consistency  

<div align="center">
  <img src="/img/posts/morie_mooring/2dfarm_layout.png" 
       alt="Plan view of floating wind farm mooring layout showing floater positions, mooring line headings, and anchor locations" 
       width="500">
</div>
*Figure 1 – Mooring system geometry showing floater positions, line headings, and anchor locations.*

### Engineering Significance

This deterministic geometry ensures:

- Reproducibility across layouts  
- Compatibility with shared-anchor configurations  
- Consistent load transfer paths  


## Shared Anchor Topology

Coincident anchor locations are merged to define **shared-anchor nodes**, creating a **connected load network**.

<div align="center">
  <img src="/img/posts/morie_mooring/2dfarm_shared.png" 
       alt="Shared-anchor configurations showing anchors connected to one, two, or three mooring lines" 
       width="500">
</div>
*Figure 2 – Shared-anchor configurations showing multiple line connections per anchor.*

### Engineering Significance

Shared anchors enable:

- Reduction in anchor count  
- Compact layouts  
- Cost-efficient seabed usage  

But require:

- Accurate load aggregation  
- Directional load resolution  
- Consistent transformation into anchor demand  


## Pretension & Equilibrium (MoorPy)

The mooring system is solved in **static equilibrium**, establishing the baseline mechanical state.

<div align="center">
  <img src="/img/posts/morie_mooring/mooring_profile.png" 
       alt="Mooring line profile showing catenary geometry between fairlead and anchor with seabed interaction" 
       width="500">
</div>
*Figure 3 – Mooring line catenary profile and load transfer path.*

### Engineering Interpretation

The equilibrium configuration defines:

- Baseline load distribution across lines  
- Dominant horizontal force components driving anchor demand  
- Influence of line geometry on load direction  

Pretension governs:

- System stiffness  
- Load sharing between lines  
- Sensitivity to environmental forcing  


## Environmental & Dynamic Response

Dynamic response is evaluated using **RAFT** across multiple wave headings.

<div align="center">
  <img src="/img/posts/morie_mooring/raft_heading_cases.png" 
       alt="Frequency-domain mooring response across multiple wave headings" 
       width="500">
</div>
*Figure 4 – Environmental load cases and frequency-domain response.*

### Engineering Interpretation

Dynamic loading introduces:

- Direction-dependent load redistribution  
- Oscillatory tension behavior  
- Frequency-dependent amplification  

This reveals how environmental conditions translate into **load variability and extremes**.


## Critical Load Case Identification

The governing load case is selected based on **maximum tension response** across all conditions.

### Engineering Interpretation

Critical conditions typically arise when:

- Wave direction aligns with mooring lines  
- Load concentration occurs in windward lines  
- Dynamic amplification peaks  

This defines the **design-driving scenario** for anchor verification.


## Time-Domain Reconstruction

Time series are reconstructed from PSD outputs to evaluate **extreme and fatigue behavior**.

<div align="center">
  <img src="/img/posts/morie_mooring/mooring_loads.png" 
       alt="Time-domain mooring tension showing dynamic variation and peak loads" 
       width="500">
</div>
*Figure 5 – Time-domain reconstruction of mooring line tension.*

### Engineering Significance

This enables:

- Extreme load identification  
- Fatigue cycle assessment  
- Validation of dynamic response  


## Load Extraction (Padeye Level)

Loads are extracted at the **padeye connection point**:

- Horizontal → Ha  
- Vertical → Va  
- Direction → θ  

### Link with Soil Reconstruction

The transformation from mudline loads to padeye loads depends on:

- Soil friction angle (φ)  
- Relative density (Dr)  
- Embedded line behavior  

These parameters are provided by **morie_soil**, establishing a direct coupling between:

- Mooring response  
- Soil-dependent load transfer  


## Anchor Load Aggregation

Loads from all connected lines are combined into **anchor-level demand**.

### Engineering Interpretation

This step converts:

> Multiple line forces → Single design load

Resulting in:

- H (horizontal resultant)  
- V (vertical load)  
- θ (direction)  

This is the **critical interface between physics and design**.


## Outputs Generated

### Mooring-Level Outputs

- Mooring geometry and topology  
- Equilibrium configuration  
- Line tensions and profiles  
- Padeye loads (Ha, Va, θ)  

### Dynamic Outputs

- Frequency-domain response  
- PSD characterization  
- Critical load case  
- Time-domain tension histories  

### Anchor-Level Outputs

- Resultant loads (H, V, θ)  
- Load contribution per line  


## Engineering Applications

- Shared-anchor load evaluation  
- Anchor sizing and verification  
- Mooring system optimization  
- Environmental sensitivity studies  
- Fatigue and extreme load assessment  

This enables:

**Mooring Behavior → Anchor Demand → Design Verification**


## Relationship to Other Morie Study Cases

This study is the **physics engine** of the Morie Analytics workflow.

### Receives from

- **morie_site** → bathymetry context  
- **morie_layout** → geometry and topology  
- **morie_soil** → soil-dependent load transfer  

### Feeds into

- **morie_anchor** → capacity verification  
- **morie_cable** → system configuration constraints  

It provides the **mechanical transition from system geometry to design-driving loads**.


## Why It Matters Commercially

This workflow enables:

- Reduction of anchor overdesign  
- Validation of shared-anchor strategies  
- Direct linkage between layout decisions and load consequences  
- Improved CAPEX control through load-driven design  

This is the stage where:

- layout decisions become load consequences  
- shared-anchor strategies are validated or rejected  
- system configuration directly impacts cost  


## Aspects to Improve

- Soil–mooring interaction coupling  
- Nonlinear seabed contact models  
- Probabilistic load cases  
- Automated optimization loops  
- Integration with installation constraints  


## Design Philosophy

- Physics-informed modeling  
- Modular architecture  
- Traceability from geometry to loads  
- Engineering usability  
- Scalability  


## How to Run

1. Place datasets in `celtic_sea_share/`  
2. Install dependencies:

- `numpy`  
- `matplotlib`  
- `scipy`  
- `pyyaml`  
- `FAModel`  
- `MoorPy`  
- `RAFT`  

3. Execute:

```bash
python morie_mooring.py