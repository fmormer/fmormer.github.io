---
layout: post
title: Layout Generation & Topology Optimization – Celtic Sea
image: "/posts/morie_layout/2dfarm_layout.png"
tags: [Offshore Wind, Layout Optimization, Hex Grid, Floating Wind, GIS, Python]
---

# Celtic Sea Floating Offshore Wind – Layout Generation & Topology Optimization

This project establishes the first step of the Morie Analytics workflow by introducing a structured methodology for generating **floating wind farm layouts from site data**.

Using bathymetry and soil datasets, a modular Python pipeline is developed to transform **public marine data into engineering-ready floater configurations**, based on deterministic spatial logic and topology-driven optimization.

The workflow bridges the gap between **site characterization and engineering design**, enabling consistent generation of layout candidates that can be directly propagated into **mooring and anchor systems**.

The objective is to replace ad-hoc placement strategies with a **reproducible, data-driven layout generation framework**.

---

## Project Scope

- **Site-driven layout generation**
- **Bathymetry and soil-constrained feasibility filtering**
- **Hexagonal lattice-based floater placement**
- **Topology-driven cluster optimization**
- **YAML-based model generation for downstream workflows**
- Integration with:
  - Mooring system generation  
  - Shared-anchor detection  
  - Anchor design workflows  

The workflow transforms raw spatial data into **engineering-ready layout configurations**, ensuring full traceability from:

```text
Site Data → Feasible Region → Layout → Mooring → Anchors
```

---

## 1. Site Data Processing & Spatial Framework

The workflow begins by transforming raw marine datasets into a consistent engineering framework.

### Data Sources

- **Bathymetry**: GEBCO grid (ASCII format)  
- **Soil Classification**: EMODnet seabed substrate (Folk-7 system)  
- **Soil Profiles**: Layered YAML profiles mapped to grid labels  

### Processing Steps

- Load bathymetry and soil grids  
- Validate grid alignment (same coordinates and resolution)  
- Map soil labels to engineering soil properties  
- Generate 2D visualizations:
  - Bathymetry contours  
  - Soil classification maps  

<div align="center">
  <img src="/img/posts/morie_layout/2dfarm_bathy_2.png" width="500">
</div>
*Figure 1 – Bathymetry contour map of the Celtic Sea lease area, showing depth variation across the site.*

<div align="center">
  <img src="/img/posts/morie_layout/2dfarm_soil_2_folk7_EMOD.png" width="500">
</div>
*Figure 2 – Seabed soil classification using the EMODnet Folk-7 system, mapped across the lease area.*

---

### Engineering Significance

This step establishes:

- A **common spatial reference system**  
- Consistent mapping between bathymetry and soil  
- A foundation for engineering filtering and layout generation  

---

## 2. Suitability Region Detection

Feasible regions are identified using combined engineering constraints.

### Criteria

- **Depth range**: 85–95 m  
- **Soil types**: Engineering-suitable sediments (Folk groups 1xx–2xx)  

### Method

- Apply bathymetry mask  
- Apply soil classification mask  
- Combine into a single feasibility map  

```python
combined_mask = depth_mask & soil_mask
```

<div align="center">
  <img src="/img/posts/morie_layout/2dfarm_overlay.png" width="500">
</div>
*Figure 3 – Suitability region derived from combined bathymetry and soil constraints, defining feasible areas for floater placement.*

---

### Physical Interpretation

The suitability region represents:

- Areas where installation is feasible  
- Soil conditions compatible with anchor systems  
- Depth ranges suitable for floating wind deployment  

---

### Engineering Significance

This step defines the **engineering domain** for layout generation and ensures that all candidate floater locations:

- Are physically feasible  
- Respect seabed constraints  
- Align with downstream design requirements  

---

## 3. Hexagonal Lattice Generation

A structured hexagonal grid is generated within the feasible region.

### Parameters

- **SPACING** = 800 m  
- **BUFFER** = 400 m (lease setback)  
- Orientation = 30°  

### Process

- Apply buffer to lease boundary  
- Generate full hex lattice  
- Filter hex centers using suitability mask  

<div align="center">
  <img src="/img/posts/morie_layout/2dfarm_hexoverlay.png" width="500">
</div>
*Figure 4 – Hexagonal lattice generated within the buffered lease area, with valid floater positions filtered by suitability criteria.*

---

### Physical Interpretation

The hexagonal grid provides:

- Uniform spacing between floaters  
- Maximum packing efficiency  
- Consistent neighbor relationships  

---

### Engineering Significance

This approach ensures:

- Deterministic floater placement  
- Reproducibility across scenarios  
- Compatibility with shared-anchor configurations  

---

## 4. Cluster Optimization (Topology-Based)

A fixed **8-node cluster template** is used to identify optimal floater configurations.

### Algorithm

- Slide cluster across all valid hex centers  
- Verify full cluster feasibility  
- Compute connectivity metrics  
- Select cluster maximizing internal adjacency  

### Neighbor Detection

- Distance matrix between centers  
- Minimum spacing defines adjacency  
- Neighbor count per node  

---

### Metrics

| Metric | Description |
|--------|------------|
| `n_floaters` | 8 |
| `avg_neighbors` | Mean connectivity |
| `min_neighbors` | Weakest node |
| `score` | Connectivity metric |

---

### Visualization

<div align="center">
  <img src="/img/posts/morie_layout/2dfarm_layout.png" width="500">
</div>
*Figure 5 – Optimal 8-node floater cluster selected using topology-based connectivity optimization.*

---

### Physical Interpretation

Connectivity reflects:

- Potential for shared anchors  
- Structural compactness of layout  
- Interaction between floaters  

---

### Engineering Significance

This step replaces:

> heuristic layout selection  

with:

> **topology-driven optimization**

providing a proxy for anchor-sharing efficiency before detailed modeling.

---

## 5. Layout Integration into Engineering Model

The selected cluster is injected into a project YAML file.

### Process

- Replace floater coordinates  
- Maintain project structure  
- Generate new layout configuration  

### Output

- `modified_celticsea.yaml`

---

### Engineering Significance

This step bridges:

```text
Layout Optimization → Mooring System Modeling
```

ensuring seamless integration with downstream workflows.

---

## 6. Mooring & Anchor Topology Generation

Following layout generation:

- Mooring systems are instantiated  
- Anchor locations are generated  
- Coincident anchors are merged  
- Attachment counts are computed  

<div align="center">
  <img src="/img/posts/morie_layout/2dfarm_layout_anchor.png" width="500">
</div>
*Figure 6 – Resulting anchor topology after mooring system generation and shared-anchor merging, showing connectivity across the layout.*

---

### Anchor Classification

| Attachments | Meaning |
|-------------|--------|
| 1 | Single-line anchor |
| 2 | Shared anchor |
| 3 | Fully shared anchor |

---

### Engineering Significance

This step defines:

- Load transfer topology  
- Anchor-sharing configurations  
- Inputs for anchor design workflows  

---

## 7. Integrated Python Workflow

All steps are implemented in a modular pipeline:

```python
# Load project and site data
project = Project('original_celticsea.yaml')
project.loadSoil(...)

# Build suitability mask
combined_mask = depth_mask & soil_mask

# Generate hex grid
all_hex, valid_hex = generate_hex_turbine_array(...)

# Optimize layout
best_centers = slide_fixed8_best(valid_hex)

# Inject into YAML
inject_selected_cluster_into_yaml(...)

# Generate moorings and anchors
project.getMoorPyArray()
merge_shared_anchors(project)
```

---

## Engineering Applications

- Layout feasibility screening  
- Shared-anchor layout optimization  
- Mooring system initialization  
- Anchor demand preparation  
- Farm-scale spatial planning  

---

## Engineering Value

This workflow demonstrates how to:

> Convert **site data into engineering-ready floating wind layouts**

Bridging:

- Geospatial data  
- Layout generation  
- Mooring systems  
- Anchor topology  

It enables:

- Deterministic design workflows  
- Reduced uncertainty in early-stage design  
- Direct integration across disciplines  

---

## Next Steps

- Multi-cluster optimization  
- Integration with mooring load analysis (RAFT)  
- Anchor capacity verification  
- Cable routing constraints  
- Surrogate-based layout optimization  

---

## Morie Analytics Vision

At Morie Analytics, the goal is to build:

> **Integrated Offshore Layout Intelligence for Floating Wind**

This layout workflow forms the foundation for:

- Mooring system analysis  
- Anchor design optimization  
- Full farm-level engineering integration  

---

## Related Work

- Mooring System Generation & Load Analysis  
- Shared Anchor Load Resolution & Capacity Verification  
- Dynamic Cable Design & Optimization  

---