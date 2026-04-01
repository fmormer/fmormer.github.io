---
layout: post
title: Layout Generation & Topology Optimization – Celtic Sea
image: "/posts/morie_layout/2dfarm_layout.png"
tags: [Offshore Floating Wind, Layout Optimization, Hex Grid, Floating Wind, GIS, Python]
---

# Celtic Sea Floating Offshore Wind – Layout Generation & Topology Optimization

## Executive Summary

This study establishes the **layout generation layer** of Morie Analytics by transforming site-level geospatial data into **engineering-ready floating wind farm configurations**.

Using bathymetry and seabed classification from **morie_site**, the workflow identifies feasible regions, generates a constrained hexagonal lattice, and selects optimal floater clusters using **topology-driven optimization**.

The result is a **deterministic and reproducible layout generation framework** that directly integrates with mooring and anchor models, replacing heuristic placement strategies with structured engineering logic.

> Site intelligence → **Layout generation** → Soil reconstruction → Mooring physics → Anchor verification → Cable optimization

---

## Project Scope

- Site-driven layout generation based on processed geospatial data  
- Bathymetry and soil-constrained feasibility filtering  
- Hexagonal lattice-based floater placement  
- Topology-driven cluster optimization (8-node template)  
- YAML-based model generation for downstream workflows  
- Integration with:
  - Mooring system generation  
  - Shared-anchor detection  
  - Anchor design workflows  

This study converts **site intelligence into spatial design decisions**.

---

## Engineering Context

Following site characterization, the next critical step in offshore wind design is:

> **Where do we place the turbines?**

At this stage, engineers must balance:

- Lease boundaries and setback buffers  
- Water depth constraints  
- Seabed conditions  
- Mooring footprint interactions  
- Anchor-sharing potential  

Traditional approaches rely on manual placement or coarse grids.

This workflow introduces a **lattice-first methodology**, where layout is derived from:

- Physical feasibility  
- Spatial structure  
- Connectivity metrics  

---

## Inputs and Data Sources

This study builds directly on **morie_site outputs** for each lease area:

- Bathymetry grids (`bathy_*.txt`)  
- Soil classification grids (`soil_*.txt`)  
- Lease boundary definitions  

Additional inputs:

- Layered soil profiles (YAML mapping)  
- Layout parameters (spacing, buffer, orientation)  

All inputs are aligned in a **common coordinate system**.

---

## Technical Architecture

The workflow is implemented in Python using:

- `numpy`, `scipy` → numerical operations  
- `matplotlib` → visualization  
- `pyyaml` → configuration management  
- `famodel`, `MoorPy` → system integration  

Core modules:

- `populate_array_hexgrid.py` → lattice generation  
- `hex_cluster_optimizer.py` → cluster selection  
- `inject_cluster_yaml.py` → model integration  
- `merge_shared_anchors.py` → anchor topology  

The architecture ensures **direct continuity with downstream physics-based models**.

---

## Processing Workflow

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

---

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

- Feasible depth ranges  
- Soil conditions compatible with anchor systems  
- Spatial constraints for layout generation  

---

## Suitability Region Detection

<div align="center">
  <img src="/img/posts/morie_layout/2dfarm_overlay.png" 
       alt="Suitability map showing feasible floating wind farm regions derived from combined bathymetry depth limits and seabed soil constraints" 
       width="500">
</div>
*Figure 3 – Feasible region derived from combined bathymetry and soil constraints.*

### Criteria

- Depth: **from 88 m to 94 m**  
- Soil: Engineering-suitable sediments - 2.0. Sand (Multiscale - folk 7)   

### Engineering Significance

Defines the **valid design domain** where:

- Installation is feasible  
- Anchor systems are viable  
- Mooring configurations are realistic  

---

## Hexagonal Lattice Generation

<div align="center">
  <img src="/img/posts/morie_layout/2dfarm_hexoverlay.png" 
       alt="Hexagonal grid layout overlaid on feasible offshore wind area showing filtered turbine positions based on bathymetry and soil constraints" 
       width="500">
</div>
*Figure 4 – Hexagonal lattice filtered by feasibility constraints.*

### Parameters

- Spacing: 800 m  
- Buffer: 400 m  
- Orientation: 30°  

### Engineering Significance

The hex grid ensures:

- Uniform spacing  
- Deterministic placement  
- Compatibility with shared-anchor layouts  

---

## Cluster Optimization (Topology-Driven)

<div align="center">
  <img src="/img/posts/morie_layout/2dfarm_layout.png" 
       alt="Selected 8-turbine cluster within hexagonal grid showing optimized floating wind layout based on connectivity and feasibility metrics" 
       width="500">
</div>
*Figure 5 – Optimal 8-node cluster selected based on connectivity metrics.*

### Methodology

- Slide fixed cluster across lattice  
- Evaluate feasibility  
- Compute connectivity metrics  

### Key Metrics

- `avg_neighbors` → compactness  
- `min_neighbors` → weakest node  
- `score` → overall topology quality  

### Engineering Insight

Connectivity acts as a **proxy for shared-anchor efficiency**, enabling layout optimization without full physics-based modeling.

---

## Mooring & Anchor Topology Generation

<div align="center">
  <img src="/img/posts/morie_layout/2dfarm_layout_anchor.png" 
       alt="Anchor-sharing topology map showing mooring line connections and shared anchor nodes across the floating wind farm layout" 
       width="500">
</div>
*Figure 6 – Anchor-sharing topology derived from mooring system generation.*

### Outputs

- Anchor coordinates  
- Attachment counts (1–3 lines per anchor)  
- Shared anchor configurations  

### Engineering Significance

This step defines:

- Load aggregation structure  
- Anchor-sharing potential  
- Inputs for anchor sizing  

---

## Outputs Generated

- Optimized floater coordinates  
- Modified project YAML (`modified_celticsea.yaml`)  
- Suitability maps  
- Hex grid and cluster visualizations  
- Anchor topology maps  

These outputs are directly usable in:

- Mooring analysis  
- Anchor design  
- Cable routing  

---

## Engineering Applications

- Layout feasibility screening  
- Shared-anchor optimization  
- Mooring spacing definition  
- Pre-anchor design workflows  
- Farm-scale planning  

This transforms layout from:

> **manual positioning → engineering-driven system design**

---

## Relationship to Other Morie Study Cases

### Receives from:
- **morie_site** → bathymetry, soil, lease constraints  

### Feeds into:
- **morie_soil** → localized soil modeling around selected cluster  
- **morie_mooring** → system geometry and equilibrium analysis  
- **morie_anchor** → anchor load and capacity design  
- **morie_cable** → cable routing and configuration  

This module is the **bridge between site data and system design**.

---

## Why It Matters Commercially

- Reduces uncertainty in early-stage layout decisions  
- Enables rapid comparison of layout scenarios  
- Improves anchor-sharing efficiency  
- Supports scalable farm design workflows  
- Bridges GIS and engineering domains  

This is where **layout becomes a strategic design variable**, not just a geometric exercise.

---

## Aspects to Improve

- Multi-cluster optimization across full lease  
- Integration with dynamic load analysis (RAFT)  
- Inclusion of cable constraints in optimization  
- Cost-driven objective functions  
- Machine learning-based layout selection  

---

## Design Philosophy

This study reflects Morie Analytics principles:

- Deterministic design logic  
- Topology-driven optimization  
- Modular workflows  
- Integration with physics-based models  
- Scalability to farm-level design  

---

## How to Run

1. Place input datasets in `celtic_sea_share/`  
2. Install dependencies:

   - `numpy`
   - `matplotlib`   
   - `scipy`  
   - `pyyaml`  
   - `famodel`  
   - `MoorPy`  

3. Execute:

```bash
python morie_layout.py
```