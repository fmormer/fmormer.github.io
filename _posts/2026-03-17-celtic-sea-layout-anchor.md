---
layout: post
title: Shared Anchor Load Resolution & Capacity Verification – Celtic Sea
image: "/posts/suction_plot.png"
tags: [Offshore Wind, Anchors, Suction Piles, Shared Anchors, Geotechnical Engineering, Python]
---

# Celtic Sea Floating Offshore Wind – Shared Anchor Load Resolution & Capacity Verification

This project extends the mooring system workflow by introducing a structured methodology to transform **dynamic mooring loads into anchor design loads** and verify **suction pile capacity under combined loading**.

Using reconstructed time series from RAFT simulations, embedded chain mechanics, and layered soil models, a modular Python pipeline is developed to bridge **hydrodynamics, mooring mechanics, and geotechnical design**.

The objective is to formalize anchor design into a reproducible computational workflow that captures **realistic multi-line loading conditions** in floating offshore wind farms.

---

## Project Scope

- **Dynamic → static load transformation**
- **Shared-anchor load resolution**
- **Concomitant multi-line loading**
- **Torsional load assessment**
- **Layered-soil suction pile capacity**
- Full **VH–M interaction verification**

This workflow converts mooring simulation outputs into **engineering-ready anchor design loads**.

---

## 1. From Mooring Dynamics to Anchor Loads

Mooring loads are obtained from RAFT simulations and reconstructed into time series.

<div align="center">
  <img src="/img/posts/mooring_loads.png" width="700">
</div>
*Figure 1 – Synthetic tension time series with design peak definition.*

The design load is defined as:

```
T_design = T_mean + 3.8σ
```

This provides a realistic representation of extreme loading while preserving spectral characteristics.

---

## 2. Critical Event & Concomitant Loads

The governing load case is not defined by independent maxima.

Instead:

- Identify **peak tension in the dominant line**
- Extract **simultaneous loads in all other lines**

<div align="center">
  <img src="/img/posts/concomitant_loads.png" width="700">
</div>
*Figure 2 – Concomitant load extraction at the governing event.*

This produces the **true load state** acting on the shared anchor.

---

## 3. Load Transfer Through Embedded Chain

Loads at the mudline are transferred to the anchor padeye through the embedded chain.

Key effects:

- Soil resistance  
- Inverse catenary geometry  
- Chain weight  

Outputs per line:

- Horizontal load (Ha)  
- Vertical load (Va)  
- Padeye angle  

This step connects **mooring mechanics to geotechnical loading**.

---

## 4. Shared Anchor Load Resolution

Each mooring line contributes a directional load.

<div align="center">
  <img src="/img/posts/shared_anchor_planview2.png" width="500">
</div>
*Figure 3 – Plan view of shared anchor with multi-line load vectors.*

Resolution:

```
Hx = Ha cos(ψ)
Hy = Ha sin(ψ)
```

Total loads:

```
H_total = √(Hx² + Hy²)
V_total = Σ Va
```

Resultant:

```
R = √(H_total² + V_total²)
```

This defines the **true 3D load state at the anchor**.

---

## 5. Torsional Load from Lug Misalignment

Shared anchors experience torsion due to misalignment between:

- Mooring line direction  
- Padeye orientation  

Torque per line:

```
T_i = H_a,i × r_lug × sin(ψ_lug)
```

Total torsion:

```
T_total = Σ |T_i|
```

✔️ Absolute summation prevents unrealistic cancellation  
✔️ Critical for suction pile performance  

---

## 6. Farm-Scale Context

The anchor does not operate in isolation.

<div align="center">
  <img src="/img/posts/shared_anchor.png" width="600">
</div>
*Figure 4 – Farm-scale mooring system with shared-anchor topology.*

Shared anchors:

- Couple multiple floaters  
- Amplify load interaction  
- Reduce infrastructure count  

But require **accurate multi-line load modeling**.

---

## 7. Suction Pile Capacity Model

Capacity is evaluated using a layered-soil model.

### Vertical Capacity

Three governing mechanisms:

1. Tip bearing  
2. Shaft friction  
3. Plug + external resistance  

```
V_max = min(V1, V2, V3)
```

---

### Horizontal Capacity

Derived from:

- Distributed side resistance  
- Integration along pile length  

---

## 8. VH Capacity Envelope

The interaction between horizontal and vertical loads is evaluated.

<div align="center">
  <img src="/img/posts/capacity_envelope.png" width="600">
</div>
*Figure 5 – VH capacity envelope with applied load.*

The applied load must lie within the envelope:

- Inside → safe  
- Outside → failure  

---

## 9. Combined Loading with Moment (VH–M)

Torsion introduces additional demand.

<div align="center">
  <img src="/img/posts/capacity_ellipsoid.png" width="600">
</div>
*Figure 6 – VH–M interaction envelope.*

This enables:

- Full 3D load verification  
- Identification of governing failure mode  
- Quantification of utilization  

---

## 10. Integrated Python Workflow

All steps are implemented in a modular pipeline:

```python
# Load mooring results
loads = load_mooring_results()

# Identify dominant event
event = find_peak_event(loads)

# Extract concomitant loads
concomitant = extract_concomitant(loads, event)

# Transfer to padeye
padeye_loads = transfer_to_padeye(concomitant)

# Resolve shared anchor loads
anchor_load = resolve_anchor_load(padeye_loads)

# Compute torsion
T = compute_torsion(anchor_load)

# Evaluate capacity
capacity = getCapacitySuction(anchor_load, soil_profile)
```

---

## Engineering Applications

- Shared-anchor design for floating wind  
- Multi-line load resolution  
- Anchor sizing under combined loading  
- Torsional load assessment  
- Layout optimization support  

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

- Multi-case probabilistic envelopes  
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
