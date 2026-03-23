---
layout: post
title: Shared Anchor Load Resolution & Capacity Verification – Celtic Sea
image: "/posts/morie_anchor/suction_plot.png"
tags: [Offshore Wind, Anchors, Suction Piles, Shared Anchors, Geotechnical Engineering, Python]
---

# Celtic Sea Floating Offshore Wind – Shared Anchor Load Resolution & Capacity Verification

This project extends the mooring system workflow by introducing a structured methodology to transform **dynamic mooring loads into anchor design loads** and verify **suction pile capacity under combined loading**.

Using reconstructed time series from RAFT simulations, embedded chain mechanics, and layered soil models, a modular Python workflow is developed to bridge **hydrodynamics, mooring mechanics, and geotechnical design**.

This case study directly follows the mooring workflow, using **padeye-level loads (Ha, Va, θ)** as inputs for anchor design.

The objective is to formalize anchor design into a reproducible computational pipeline that captures **realistic multi-line loading conditions** in floating offshore wind farms.

---

## Project Scope

- **Dynamic → static load transformation**
- **Shared-anchor load resolution**
- **Concomitant multi-line loading**
- **Torsional load assessment**
- **Layered-soil suction pile capacity**
- Full **VHM interaction verification**

The workflow transforms mooring simulation outputs into **engineering-ready anchor demand and capacity verification**.

---

## 1. Anchor System Definition & Topology

Shared anchor systems are generated from floater layouts using deterministic geometric rules that define both **line connectivity and load transfer paths** across the farm.

Each anchor may be connected to one or multiple mooring lines depending on layout geometry.

<div align="center">
  <img src="/img/posts/morie_anchor/2dfarm_shared.png" width="500">
</div>
*Figure 1 – Plan view of floating wind farm showing shared-anchor configurations.*

---

### Detection & Merging

Shared anchors are identified through spatial analysis of anchor coordinates:

- Detect coincident or near-coincident anchor locations  
- Merge anchors into unified nodes  
- Reassign all connected mooring lines to the merged anchor  
- Preserve full connectivity between floaters and anchors  

<div align="center">
  <img src="/img/posts/morie_anchor/shared_anchor_floaters.png" width="500">
</div>
*Figure 2 – Shared-anchor topology showing multiple mooring lines connected to anchors.*

---

### Engineering Significance

The resulting system forms a **coupled load network**, where:

- Multiple floaters contribute to a single anchor  
- Load directions differ across lines  
- Resultant loads must be evaluated as vector combinations  

---

## 2. Anchor Demand from Mooring System

Anchor loads originate from the mooring system workflow.

For each mooring line, the following quantities are obtained at the padeye:

- Horizontal load (**Ha**)  
- Vertical load (**Va**)  
- Load direction (**θ**)  

These loads represent the **interface between mooring mechanics and anchor design**.

---

## 3. Critical Event & Concomitant Loads

The governing anchor load case is derived from time-domain reconstruction of mooring tensions.

The design tension is defined as:

```
T_design = T_mean + 3.8σ
```

<div align="center">
  <img src="/img/posts/morie_anchor/mooring_loads.png" width="700">
</div>
*Figure 3 – Synthetic tension time series with design peak.*

At the time of peak tension in the dominant line:

- Loads in all other lines are extracted simultaneously  

<div align="center">
  <img src="/img/posts/morie_anchor/concomitant_loads.png" width="700">
</div>
*Figure 4 – Concomitant loads at the governing event.*

This defines the **true multi-line load state acting on the anchor**.

---

## 4. Load Transfer Through Embedded Chain

Loads at the mudline are transferred to the anchor padeye through the embedded chain segment.

This process accounts for:

- Inverse catenary geometry  
- Soil resistance (tangential and normal)  
- Chain self-weight  

<div align="center">
  <img src="/img/posts/morie_anchor/anchor_inverse_catenary.png" width="700">
</div>
*Figure 5 – Inverse catenary load transfer from mudline to padeye.*

Outputs per line:

- Horizontal load at padeye (**Ha**)  
- Vertical load at padeye (**Va**)  
- Load inclination angle  

This step connects **mooring loads to anchor loading conditions**.

---

## 5. Anchor Load Resolution (H, V, T)

Each mooring line contributes a directional load at the anchor.

<div align="center">
  <img src="/img/posts/morie_anchor/shared_anchor_planview.png" width="500">
</div>
*Figure 6 – Load vectors acting on a shared anchor.*

### Horizontal Resolution

```
Hx = Ha cos(ψ)
Hy = Ha sin(ψ)
```

### Total Loads

```
H_total = √(Hx² + Hy²)
V_total = Σ Va
```

### Resultant Load

```
R = √(H_total² + V_total²)
```

---

### Torsional Load

Torsion arises from misalignment between:

- Mooring line direction  
- Padeye orientation  

```
T_i = H_a,i × r_lug × sin(ψ_lug)
T_total = Σ |T_i|
```

<div align="center">
  <img src="/img/posts/morie_anchor/shared_anchor.png" width="600">
</div>
*Figure 7 – Farm-scale context showing shared-anchor load interaction.*

This produces a complete **3D load state (H, V, T)**.

---

## 6. Suction Pile Capacity Model

Anchor capacity is evaluated using a layered-soil suction pile model accounting for:

- Multiple soil types (clay, sand)  
- Depth-dependent properties  
- Padeye position relative to pile  

---

### Vertical Capacity

Three governing mechanisms:

1. Tip bearing  
2. Shaft friction  
3. Plug + external resistance  

```
V_max = max or min(V1, V2, V3)
```
The selection of the load depends on the nature of the impulse. For explosive loads maximum should be selected for sustained loads minimum.

<div align="center">
  <img src="/img/posts/morie_anchor/anchor_failure_modes.png" width="800">
</div>
*Figure 8 – Suction pile vertical failure mechanisms.*

---

### Horizontal Capacity

Derived from:

- Distributed lateral resistance  
- Integration along pile length  
- Load application depth  

---

## 7. Load–Capacity Interaction (VHM & VH)

### VHM Interaction

<div align="center">
  <img src="/img/posts/morie_anchor/capacity_ellipsoid.png" width="600">
</div>
*Figure 9 – VHM interaction surface.*

This enables:

- Full 3D load verification  
- Identification of governing failure mode  
- Quantification of utilization  

---

### VH Envelope

<div align="center">
  <img src="/img/posts/morie_anchor/capacity_envelope.png" width="600">
</div>
*Figure 10 – VH capacity envelope.*

The applied load must lie within the envelope:

- Inside → safe  
- Outside → failure  

---

## 8. Integrated Python Workflow

All steps are implemented in a modular pipeline:

```python
# Load mooring results
loads = load_mooring_results()

# Identify dominant event
event = find_peak_event(loads)

# Extract concomitant loads
concomitant = extract_concomitant(loads, event)

# Transfer loads to padeye
padeye_loads = transfer_to_padeye(concomitant)

# Resolve anchor loads
anchor_load = resolve_anchor_load(padeye_loads)

# Compute torsion
T = compute_torsion(anchor_load)

# Evaluate capacity
capacity = getCapacitySuction(anchor_load, soil_profile)
```

---

## Engineering Applications

- Shared-anchor design for floating wind farms  
- Multi-line load aggregation  
- Anchor sizing under combined loading  
- Torsional load assessment  
- Layout optimization  

---

## Engineering Value

This workflow demonstrates how to:

> Convert **dynamic mooring behavior into reliable anchor design loads**

Bridging:

- Hydrodynamics (RAFT)  
- Mooring mechanics  
- Geotechnical capacity  

It enables:

- Reduced conservatism  
- Improved physical realism  
- Scalable design workflows  

---

## Next Steps

- Multi-case probabilistic load envelopes  
- Automated anchor sizing (D, L optimization)  
- Integration with installation models  
- ML-based surrogate models  
- Lease-scale anchor mapping  

---

## Morie Analytics Vision

At Morie Analytics, the goal is to build:

> **Integrated Anchor & Seabed Intelligence for Floating Offshore Wind**

This anchor workflow is a key component toward:

- Digital seabed twins  
- Farm-scale anchor optimization  
- AI-driven offshore engineering  

---

## Related Work

- Mooring system generation & load analysis  
- Site characterization & soil mapping  
- Full floating wind farm optimization  