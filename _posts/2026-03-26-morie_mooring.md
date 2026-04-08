---
layout: post
title: Mooring System Generation & Load Analysis 
image: "/img/posts/morie_mooring/morie_mooring2.png"
tags: [Offshore Floating Wind, Mooring Systems, RAFT, MoorPy, Shared Anchors, Python]
---

# Celtic Sea Floating Offshore Wind – Mooring System Generation & Load Analysis

## Executive Summary

This study establishes the **mooring physics layer** of Morie Analytics by transforming floating wind layouts into **physically consistent mooring systems and design-ready load outputs**.

Using YAML-based configurations and simulation tools, the workflow generates mooring systems and extracts **mudline-level loads** for engineering assessment that will be transformed into **padeye-level loads** in the following study case.

The result is a **reproducible computational pipeline** that connects geometry, equilibrium physics, and load transfer into downstream anchor design inputs.

This module represents the first stage where **physical system behavior governs design outcomes**, transitioning from geometry to force-driven engineering.

> Site intelligence → Layout generation → Soil reconstruction → **Mooring physics** → Anchor verification → Cable optimization


## Project Scope

- Mooring system generation  
- Shared-anchor configurations  
- Mudline load extraction  
- Load aggregation  
- Environmental load case evaluation  
- Optional dynamic response analysis  

This study converts **layout geometry into design-driving loads**.


## Engineering Context

Floating wind farms increasingly adopt shared-anchor configurations, introducing **coupled load interaction**.

Accurate design requires:

- Geometry and pretension  
- Static equilibrium  
- Directional loading  
- Dynamic amplification  
- Load transfer to anchors  

Traditional workflows separate mooring and anchor design.

This workflow provides a **continuous mechanical link** from layout to anchor demand.


## Inputs and Data Sources

This study builds directly on upstream Morie Analytics outputs:

### From `morie_site`

- Bathymetry grids  
- Spatial domain  

### From `morie_layout`

- Floater positions  
- Anchor coordinates  
- Shared-anchor topology  

### Additional Inputs

- YAML-based farm configuration  
- Mooring line properties  
- Environmental load cases  

All inputs are integrated into a **simulation-ready framework**.

This provides the **mechanical inputs required for load generation**.


## Technical Architecture

The workflow is implemented in Python using:

- `numpy`, `scipy` → numerical operations  
- `matplotlib` → visualization  
- `famodel` → system definition and data handling  
- `MoorPy` → static equilibrium solver  
- `RAFT` → frequency-domain dynamic response  

Core modules:

- system initialization → project setup and soil loading  
- domain extraction → local cropped study area definition  
- shared-anchor merging → topology consolidation  
- mooring configuration → generation of unique line setups  
- pretension adjustment → chain length tuning for target loads  
- equilibrium solver → static system solution  
- watch circle evaluation → platform offset computation  
- RAFT interface → dynamic response simulation  
- load reconstruction → stochastic time-series generation from PSD    
- load extraction → mudline elevation  

### System Flow

Layout → Mooring Definition → Equilibrium → Dynamic Response → Load Extraction

The architecture ensures **traceability from geometry to load outputs**.


## Processing Workflow

1. Load farm configuration  
2. Generate mooring geometry  
3. Detect and merge shared anchors  
4. Adjust line lengths and pretension  
5. Solve static equilibrium  
6. Evaluate environmental response  
7. Identify governing load case  
8. Reconstruct time-domain response  
9. Extract padeye loads  
10. Aggregate anchor demand  

This converts **system geometry into design-driving loads**.


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


## Load Extraction

Loads are extracted at the **mudline connection point**:

- Horizontal → Hm  
- Vertical → Vm  
- Direction → θm  


## Anchor Load Aggregation

Loads from all connected lines are combined into **anchor-level demand**.

### Engineering Interpretation

This step converts:

> Multiple line forces → Single design load

Resulting in:

- H (horizontal component of the mooring line tension load)  
- V (vertical component of the mooring line tension load)  
- θ (angle with the horizontal seabed plane)  

This is the **critical interface between physics and design**.


## Outputs Generated

### Mooring-Level Outputs

- Mooring geometry and topology  
- Equilibrium configuration  
- Line tensions and profiles  
- Mudline loads (Hm, Vm, θm)  

### Dynamic Outputs

- Frequency-domain response  
- PSD characterization  
- Critical load case  
- Time-domain tension histories  

### Anchor-Level Outputs

- Resultant loads (H, V, θ)  
- Load contribution per line  


## Engineering Applications

- Mooring system optimization  
- Environmental sensitivity studies
- Offset sensitivity analysis for dynamic cable coupling  
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
	- `scipy`  
	- `pyyaml`  
	- `FAModel`  
	- `MoorPy`  
	- `RAFT`  

3. Execute:

```bash
python morie_mooring.py
```