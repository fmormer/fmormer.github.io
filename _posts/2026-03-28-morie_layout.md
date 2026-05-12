---
layout: post
title: Generation & Spatial Topology Screening 
image: "/img/posts/morie_layout/morie_layout.png"
tags: [Offshore Floating Wind, Layout Optimization, Hex Grid, Floating Wind, GIS, Python]
---

# Celtic Sea Floating Offshore Wind – Layout Generation & Spatial Topology Screening

## Executive Summary

This study establishes the **layout generation layer** of Morie Analytics by transforming site-level geospatial data into **engineering-ready floating wind farm configurations**.

Using bathymetry and seabed classification from `morie_site`, the workflow identifies feasible regions, generates a constrained hexagonal lattice and selects optimal floater clusters using **topology-driven screening**.

The result is a **deterministic and reproducible layout generation framework** that replaces heuristic placement with **engineering-driven system configuration**. In conventional workflows, layout is often treated as a geometric or wind-driven problem.

In floating wind, it is a **system design problem**. The reference case corresponds to a **120 MW floating wind cluster**, bridging layout generation with real project-scale design.

> Site intelligence → **Layout generation** → Soil reconstruction → Mooring physics → Anchor verification → Cable optimization


## Project Scope

- Site-driven layout generation based on processed geospatial data  
- Bathymetry and soil-constrained feasibility filtering  
- Hexagonal lattice-based floater placement  
- Topology-driven cluster screening 
- Model generation for downstream workflows  
- Integration with mooring and anchor modules  

This study converts **site intelligence into structured spatial system design decisions**.

The reference configuration consists of:

- **8 floating wind turbine generators (WTGs)**  
- **15 MW nominal capacity per unit**  
- **Total installed capacity: 120 MW**

This defines a **cluster-scale floating wind system**, used to evaluate layout feasibility, topology optimization and downstream engineering workflows.


## Engineering Context

Following site characterization, the next critical step in offshore wind design is:

> **Where do we place the turbines?**

At this stage, engineers must balance:

- Lease boundaries and setbacks  
- Water depth constraints
- Wake effects and overall wind turbine performance  
- Seabed conditions  
- Mooring footprint interactions  
- Anchor-sharing potential  

Traditional approaches rely on manual placement or coarse grids. These approaches fail to capture the strong coupling between layout, mooring systems and anchor design.

This workflow introduces a **lattice-driven methodology**, where layout is derived from physical feasibility, spatial structure, and system connectivity.

At this stage, wake interactions and AEP optimization are intentionally treated as secondary constraints.

The focus of this workflow is the generation of engineering-compatible spatial configurations suitable for downstream mooring, anchor and cable analysis.

Detailed aerodynamic optimization would require coupling with dedicated wake models and site-specific wind resource assessment.


## Inputs and Data Sources

This study builds directly on upstream Morie Analytics outputs:

### From `morie_site`

- Bathymetry and soil classification grids
- Lease boundary definitions  

### Additional Inputs

- Layered soil profiles  
- Layout parameters (spacing, buffer, orientation)  

All inputs are aligned in a **common projected coordinate system**.

This provides the **spatial constraints required for layout generation**.


## System Flow

Site Intelligence → Feasibility Filtering → Lattice Generation → Topology Screening → System Configuration

The architecture ensures **direct continuity with downstream physics-based modules**.

### Processing Workflow

1. Load bathymetry and soil data from `morie_site`  
2. Build engineering suitability mask  
3. Generate hexagonal lattice within buffered lease  
4. Filter valid floater positions  
5. Slide cluster template across lattice  
6. Evaluate connectivity metrics  
7. Select optimal cluster  
8. Inject layout into project YAML  
9. Instantiate mooring systems and anchors  
10. Merge shared anchors and extract topology  

This converts **site constraints into structured floating wind farm layouts**.


## Bathymetry & Soil Context

<div align="center">
  <img src="/img/posts/morie_layout/2dfarm_bathy_2.png" 
       alt="2D bathymetry map of the Celtic Sea showing water depth variations across the lease area used for floating wind layout constraints" 
       width="500">
</div>
*Figure 1 – Lease-scale bathymetry used to constrain feasible layout regions.*

<div align="center">
  <img src="/img/posts/morie_layout/2dfarm_soil_2_folk7_EMOD.png" 
       alt="Seabed classification map using EMODnet Folk-7 system showing spatial distribution of sediment types for offshore wind foundation and anchor design" 
       width="500">
</div>
*Figure 2 – Seabed classification based on EMODnet Folk-7 system.*

### Engineering Significance

These datasets define:

- Feasible depth and slope ranges  
- Soil conditions compatible with anchor systems  
- Spatial constraints for layout generation  


## Suitability Region Detection

<div align="center">
  <img src="/img/posts/morie_layout/2dfarm_overlay.png" 
       alt="Suitability map showing feasible floating wind farm regions derived from combined bathymetry depth limits and seabed soil constraints" 
       width="500">
</div>
*Figure 3 – Feasible region derived from combined bathymetry and soil constraints.*

### Criteria

Filtering relevant site criteria:

- Depth: **from 88 m to 94 m**  
- Soil: Sediment classes preliminarily compatible with the selected anchor concept assumptions - 2.0. Sand (Multiscale - folk 7)   

### Engineering Significance

Defines the **valid design domain** where:

- Standardization of the assets
- Mooring configurations are coherent across the site 
- Anchor concepts remain preliminarily compatible with the selected site constraints 
- Installation equipment and techniques are feasible  


## Hexagonal Lattice Generation

<div align="center">
  <img src="/img/posts/morie_layout/2dfarm_hexoverlay.png" 
       alt="Hexagonal grid layout overlaid on feasible offshore wind area showing filtered turbine positions based on bathymetry and soil constraints" 
       width="500">
</div>
*Figure 4 – Hexagonal lattice filtered by feasibility constraints.*

The hexagonal structure provides uniform neighbor relationships and consistent spatial spacing, which are advantageous for evaluating shared-anchor compatibility and mooring connectivity patterns.

### Parameters

- Spacing: 800 m  
- Buffer: 400 m  
- Orientation: 30°

The selected spacing is used here as a demonstrative engineering configuration and should not be interpreted as an aerodynamically optimized arrangement for commercial-scale deployment.  

### Engineering Significance

The hex grid ensures:

- Uniform spacing  
- Deterministic placement  
- Compatibility with shared-anchor layouts  


## Cluster Optimization (Topology-Driven)

<div align="center">
  <img src="/img/posts/morie_layout/2dfarm_layout.png" 
       alt="Selected 8-turbine cluster within hexagonal grid showing selected floating wind layout based on connectivity and feasibility metrics" 
       width="500">
</div>
*Figure 5 – Selected 8-node cluster identified through topological compactness screening.*

The selected cluster represents a **120 MW floating wind configuration**, enabling system-level evaluation at a realistic project scale.

### Methodology

- Slide fixed cluster across lattice  
- Evaluate feasibility  
- Compute connectivity metrics  

### Key Metrics

- `avg_neighbors` → compactness  
- `min_neighbors` → weakest node  
- `score` → Topological Compactness Index (TCI) 

### Engineering Insight

The Topological Compactness Index (TCI) is introduced here as a spatial screening metric intended to identify geometric configurations potentially compatible with shared-anchor mooring arrangements.

The metric evaluates local floater connectivity and spatial compactness within the lease area prior to detailed mooring generation.

At this stage, the TCI should not be interpreted as:

- A wake optimization metric  
- An annual energy production (AEP) indicator  
- A hydrodynamic efficiency metric  
- A full-system economic optimization metric  

Instead, it acts as a first-order indicator of geometric proximity and potential anchor-sharing compatibility.

Actual shared-anchor feasibility remains dependent on downstream engineering parameters including:

- Mooring heading assignment  
- Anchor radius  
- Mooring line orientation  
- Dynamic system response  
- Boundary effects within the lease area  

This enables early-stage spatial screening prior to detailed physics-based analysis.


## Mooring & Anchor Topology Generation

<div align="center">
  <img src="/img/posts/morie_layout/2dfarm_layout_anchor.png" 
       alt="Anchor-sharing topology map showing mooring line connections and shared anchor nodes across the floating wind farm layout" 
       width="500">
</div>
*Figure 6 – Anchor-sharing topology derived from mooring system generation.*

This step effectively defines the **load pathways** of the system, linking spatial layout to structural behavior.

### Outputs

- Anchor coordinates  
- Shared anchor configurations 
- Attachment counts color code (1–3 lines per anchor)  

### Engineering Significance

This step defines:

- Load aggregation structure  
- Anchor-sharing potential  
- Location inputs for anchor sizing  


## System-Level Representation

<div align="center">
  <img src="/img/posts/morie_layout/3D_cropped_bathy.png" 
       alt="3D visualization of floating wind farm layout including bathymetry surface, turbine positions, mooring lines, and anchor locations showing full system integration" 
       width="700">
</div>
*Figure 7 – Integrated system view combining bathymetry, layout, mooring configuration, and anchor positions.*

### Engineering Significance

This visualization represents the transition from **spatial layout** to **physical system configuration**.

It captures:

- Bathymetry-driven placement of floaters  
- Mooring system geometry and orientation  
- Anchor locations and sharing structure  
- Interaction between layout and subsea infrastructure  

This is where layout becomes an **engineered offshore system**.


## Outputs Generated

For selected lease area:

- Selected floater coordinates  
- Modified project file 
- Suitability maps  
- Hex grid and cluster visualizations
- Anchor topology maps

These outputs are directly usable in:

- Mooring analysis  
- Anchor design  
- Cable routing  


## Engineering Applications

The outputs support:

- Layout feasibility screening  
- Shared-anchor optimization  
- Mooring spacing definition  
- Pre-anchor design workflows  
- Farm-scale planning  

This enables:

**Manual positioning → Engineering-driven system design**


## Relationship to Other Morie Study Cases

### Receives from:
- **morie_site** → bathymetry, soil and lease area boundary constraints  

### Feeds into:
- **morie_soil** → localized soil modeling around selected cluster  
- **morie_mooring** → system geometry and equilibrium analysis  
- **morie_anchor** → anchor load assessment and capacity design check  
- **morie_cable** → cable routing and configuration  

This module is the **bridge between site data** and **system design.**


## Why It Matters Commercially

Layout decisions strongly influence **CAPEX, installation strategy, and system feasibility.**

- Reduces uncertainty in early-stage layout decisions  
- Enables rapid comparison of layout scenarios  
- Improves mooring- and anchor-sharing efficiency  
- Supports scalable farm design workflows  
- Bridges GIS and engineering domains  

This is where:

- Layout becomes a strategic design variable  
- System configuration drives cost and performance  
- Engineering replaces heuristic placement  


## Aspects to Improve

- Multi-cluster optimization across full lease  
- Integration with dynamic load analysis and wake effects for production assessment 
- Inclusion of cable constraints in optimization  
- Cost-driven objective functions  
- Machine learning-based layout selection  


## Design Philosophy

This study reflects the Morie Analytics approach:

- Physics-informed  
- Modular  
- Traceable  
- Engineering-focused  
- Scalable  
