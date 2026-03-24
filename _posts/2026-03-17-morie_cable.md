---
layout: post
title: Dynamic Cable Design & Optimization – Celtic Sea
image: "/posts/morie_cable/cable_opt_config.png"
tags: [Offshore Wind, Dynamic Cables, Floating Wind, Cable Optimization, RAFT, MoorPy, Python]
---

# Celtic Sea Floating Offshore Wind – Dynamic Cable Design & Optimization

This project extends the Morie Analytics workflow by introducing a structured methodology for designing and optimizing dynamic power cables in floating offshore wind systems.

Building upon site characterization, layout generation, mooring system analysis, and anchor load resolution, this workflow integrates bathymetry, floater motion, and hydrodynamic response into a unified cable design framework.

A representative floating wind turbine (FOWT) is selected, and a standalone dynamic cable connecting the seabed to the floater is optimized under realistic motion conditions derived from MoorPy and RAFT.

The objective is to formalize dynamic cable design into a reproducible computational pipeline that captures geometry, physics, and constraint-driven optimization, ensuring consistency across:

Site → Layout → Mooring → Anchor → Cable

---

## Project Scope

- Dynamic cable configuration design (seabed to floater)
- Integration of bathymetry and platform geometry
- Mooring-derived mean offset (watch circle)
- Hydrodynamic motion from RAFT (surge & sway)
- Constraint-based cable optimization
- Evaluation of curvature, sag, tension, and touchdown
- Modular Python implementation for reproducible workflows  

The workflow transforms motion-driven inputs into engineering-ready cable configurations, ensuring full traceability from:

Mooring Response → Hydrodynamic Motion → Cable Geometry → Constraint Verification

---

## 1. Cable System Definition & Geometry

The dynamic cable is defined as a multi-segment system connecting:

- seabed touchdown point
- suspended cable sections with distributed buoyancy
- floater fairlead connection

The geometry is derived from platform data:

- Water depth from bathymetry grid
- Fairlead position from platform definition

rBFair = [rFair, 0, zFair]

Where:

- rFair → radial distance from platform center
- zFair → vertical position of fairlead

---

### Physical Interpretation

The cable must accommodate:

- vertical span (water depth)
- horizontal excursion (floater motion)
- geometric constraints (curvature, sag, touchdown location)

---

### Engineering Significance

This defines the baseline geometric problem linking seabed conditions, floater configuration, and cable routing.

---

<div align="center">
  <img src="/img/posts/morie_cable/cable_initial_config.png" width="500">
</div>
*Figure 1 – Initial dynamic cable configuration prior to optimization, showing baseline geometry under combined offset and dynamic motion conditions.*

---

## 2. Mooring-Derived Floater Offset

Floater offset is computed using MoorPy watch circle analysis.

### Methodology

- Solve mooring system equilibrium
- Evaluate platform excursion across headings
- Compute radial displacement

offset = max( √(dx² + dy²) )

---

### Physical Interpretation

This represents the mean excursion envelope of the floater due to mooring restoring forces and environmental loading.

---

### Engineering Significance

Defines the maximum horizontal displacement of the fairlead and the quasi-static boundary condition for cable design.

---

## 3. Hydrodynamic Motion (RAFT)

Dynamic motion is obtained from RAFT simulations.

### Methodology

- Frequency-domain analysis
- Extraction of surge and sway response

x_ampl = √(surge_max² + sway_max²)

---

### Physical Interpretation

Represents oscillatory motion due to waves and dynamic amplification of floater displacement.

---

### Engineering Significance

Combines with offset to define:

Total motion envelope = mean offset + dynamic amplitude

This is critical for curvature evaluation, fatigue considerations, and extreme load cases.

---

## 4. Cable Design Model

The cable is modeled using a multi-segment configuration with:

- seabed contact region
- suspended spans
- buoyancy-controlled sections

### Key Inputs

- water depth
- fairlead position
- mooring-derived offset
- RAFT-derived dynamic amplitude

---

### Physical Interpretation

The cable adopts a catenary-like shape influenced by self-weight, buoyancy modules, and boundary motion.

---

### Engineering Significance

Defines how loads are transferred to the floater, how curvature develops along the cable, and how seabed interaction occurs.

---

## 5. Optimization Problem

The cable configuration is optimized using a constraint-based formulation.

### Design Variables

- segment lengths
- buoyancy distribution
- lay lengths

---

### Constraints

- Minimum lay length
- Maximum sag
- Curvature limits
- Tension safety factors
- Touchdown range

---

### Objective

Minimize cost while satisfying all constraints.

---

<div align="center">
  <img src="/img/posts/morie_cable/cable_board.png" width="600">
</div>
*Figure 2 – Optimization convergence showing cost evolution and constraint satisfaction across function evaluations.*

---

### Physical Interpretation

The optimization process explores feasible cable shapes, trade-offs between curvature and tension, and the influence of buoyancy distribution.

---

### Engineering Significance

Ensures constraint-compliant design, efficient material usage, and physically realistic cable behavior.

---

## 6. Optimization Results

The optimized cable configuration satisfies all imposed constraints while maintaining a physically consistent geometry under combined motion conditions.

---

<div align="center">
  <img src="/img/posts/morie_cable/cable_opt_config.png" width="500">
</div>
*Figure 3 – Optimized dynamic cable configuration satisfying all geometric, curvature, and tension constraints under realistic floater motion conditions.*

---

### Physical Interpretation

The optimized configuration demonstrates controlled curvature distribution, stable touchdown behavior, and balanced tension along the cable.

---

### Engineering Significance

The final design ensures structural integrity, compliance with installation constraints, and robustness under operational conditions.

---

## 7. Integrated Python Workflow

All steps are implemented in a modular pipeline:

```python
# Load project
project = Project('floating_farm.yaml')

# Extract bathymetry and platform geometry
depth = get_depth(project, fowt_id)
rBFair = get_fairlead_position(project)

# Compute mooring offset
offset = compute_watch_circle(project)

# Run RAFT simulations
raft_results = run_raft(project)

# Extract dynamic amplitude
x_ampl = extract_motion_amplitude(raft_results)

# Define cable design
cable = CableDesign(depth, rBFair, offset, x_ampl)

# Run optimization
cable.optimize()

# Plot results
cable.plot()