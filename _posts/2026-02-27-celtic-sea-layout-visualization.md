---
layout: post
title: Hex-Based Floater Layout Optimization – Celtic Sea
image: "/posts/hexgrid_overlay.png"
tags: [Offshore Wind, Layout Optimization, Hex Grid, Topology, Python]
---

# Celtic Sea Floating Offshore Wind – Hexagonal Lattice Layout Optimization

This project extends the structured site-characterization workflow by introducing a deterministic floater placement methodology based on hexagonal lattice theory.

Using processed lease geometry, bathymetry, and seabed suitability layers, a constrained hexagonal grid is generated within the lease area. A fixed 8-node cluster is then evaluated using topology-driven connectivity metrics to identify compact, engineering-consistent floater arrangements.

The objective is to formalize early-stage layout screening into a reproducible computational framework that replaces ad-hoc spatial placement with deterministic, constraint-aware logic.

---

## Project Scope

- Structured hexagonal lattice generation inside buffered lease area  
- Depth and soil suitability filtering  
- Axial coordinate indexing  
- Sliding fixed 8-node cluster optimization  
- Connectivity-based scoring  
- Visualization of layout feasibility and topology  

The workflow transforms processed site data into engineering-ready layout candidates suitable for early-stage floating wind feasibility studies.

---

## 1. Lease & Suitability Filtering

The lease boundary defines the spatial domain for candidate floater placement.

Processing steps:

- Import projected lease polygon
- Apply setback buffer
- Mask non-developable areas
- Intersect soil suitability layers
- Enforce depth constraints

<div align="center">
  <img src="/img/posts/suitability_overlay.png" alt="Lease Suitability Filtering" width="500">
</div>
*Figure 1 – Lease boundary with soil suitability masking.*

Suitability filtering ensures that lattice generation occurs only within technically viable regions.

---

## 2. Hexagonal Lattice Generation

A regular hexagonal lattice is generated inside the filtered lease region.

Key geometric definitions:

| Parameter | Definition |
|------------|------------|
| `SPACING` | Center → vertex distance |
| Orientation | 30° |
| Coordinate System | Axial indexing |

Spacing consistency ensures:

- Repeatable geometric definition  
- Uniform mooring spacing assumptions  
- Scalable cluster evaluation  

<div align="center">
  <img src="/img/posts/hexgrid_overlay.png" alt="Hex Grid Overlay" width="500">
</div>
*Figure 2 – Buffered lease region populated with hexagonal lattice.*

The lattice forms the discrete spatial candidate set for cluster evaluation.

---

## 3. Bathymetric Context Integration

Bathymetry directly influences mooring footprint, anchor feasibility, and installation complexity.

Depth is incorporated as a filtering constraint and contextual visualization layer.

<div align="center">
  <img src="/img/posts/2dfarm_bathy_2.png" alt="Bathymetry Overlay" width="500">
</div>
*Figure 3 – GEBCO bathymetry intersected with lease polygon.*

Depth thresholds remove infeasible lattice nodes prior to optimization.

---

## 4. Soil Classification Integration

Sediment classification informs anchor concept feasibility screening.

<div align="center">
  <img src="/img/posts/2dfarm_soil_2.png" alt="Soil Classification Overlay" width="500">
</div>
*Figure 4 – Soil type distribution within lease boundary.*

Soil filtering supports early evaluation of:

- Suction anchor feasibility  
- Driven pile potential  
- Shared-anchor suitability  

Only lattice nodes satisfying soil constraints are retained.

---

## 5. Fixed 8-Node Cluster Optimization

A fixed 8-node axial cluster is defined and slid across all valid lattice seeds.

Algorithmic steps:

1. Convert valid hex centers to axial indices.
2. Translate fixed cluster template.
3. Verify full cluster validity.
4. Compute adjacency counts.
5. Score connectivity.

### Scoring Philosophy

- Interior nodes increase score.
- Peripheral nodes reduce score.
- Pure topology evaluation (no anchor geometry modeling).

<div align="center">
  <img src="/img/posts/slide_overlay.png" alt="Selected Cluster" width="500">
</div>
*Figure 5 – Optimal 8-node cluster placement after connectivity scoring.*

Connectivity serves as a proxy for anchor-sharing potential and layout compactness.

---

## 6. Quantitative Metrics

Cluster evaluation metrics include:

| Metric | Description |
|--------|------------|
| `n_floaters` | Total cluster nodes (8) |
| `avg_neighbors` | Mean internal connectivity |
| `min_neighbors` | Weakest-connected node |
| `n_deg0` | Isolated nodes |
| `n_deg1` | Single-neighbor nodes |
| `score` | Connectivity-weighted metric |

This provides a deterministic basis for layout comparison.

---

## 7. Integrated Python Workflow

All processing is implemented in Python using structured modular scripts:

```python
# Example lattice generation
valid_hex = generate_hex_turbine_array(
    lease_polygon,
    spacing=SPACING,
    soil_mask=soil_filter,
    depth_mask=depth_filter
)

best_cluster = optimize_hex_cluster(valid_hex)
