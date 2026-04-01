---
layout: post
title: Dynamic Cable Design & Configuration Optimization – Celtic Sea
image: "/posts/morie_cable/cable_opt_config.png"
tags: [Offshore Floating Wind, Dynamic Cables, Floating Wind, Cable Optimization, RAFT, MoorPy, Python]
---

# Celtic Sea Floating Offshore Wind – Dynamic Cable Design & Configuration Optimization

## Executive Summary

This study establishes the **dynamic cable engineering layer** of Morie Analytics by transforming **floater motion and site geometry into optimized cable configurations**.

Building on outputs from **morie_layout**, **morie_mooring**, and **morie_anchor**, the workflow integrates bathymetry, mooring-derived offsets, and hydrodynamic response (RAFT) to design **constraint-compliant dynamic power cables**.

A representative floating wind turbine (FOWT) is selected, and a standalone cable system is optimized under realistic motion conditions, ensuring consistency across:

> **Site → Layout → Mooring → Anchor → Cable**

This module closes the system loop by connecting **structural response to electrical infrastructure design**.

---

## Project Scope

- Dynamic cable configuration (seabed to floater)  
- Integration of bathymetry and platform geometry  
- Mooring-derived mean offset (watch circle)  
- Hydrodynamic motion from RAFT (surge & sway)  
- Constraint-based cable optimization  
- Evaluation of sag, curvature, tension, and touchdown  
- Modular Python workflow for reproducibility  

This workflow transforms:

> **Floater Motion → Cable Geometry → Constraint Verification → Optimized Design**

---

## Engineering Context

Dynamic power cables are critical components in floating offshore wind systems, enabling energy transfer between floating turbines and subsea infrastructure.

Unlike static cables, dynamic cables must accommodate:

- large floater excursions  
- cyclic hydrodynamic motion  
- seabed interaction  
- geometric constraints  

Traditional approaches rely on assumed motions. This workflow instead uses:

- **MoorPy → mean offset (watch circle)**  
- **RAFT → dynamic response (surge/sway)**  

This ensures that cable design reflects **real system physics**.

---

## Inputs and Dependencies

### From previous Morie modules

- **morie_layout** → floater position and geometry  
- **morie_site** → bathymetry grid  
- **morie_mooring** → platform offset (watch circle)  
- **morie_anchor** → system constraints context  

### Additional inputs

- YAML farm configuration  
- Platform fairlead definition  
- Hydrodynamic simulation outputs (RAFT)  

---

## Technical Architecture

The workflow combines geometry, physics, and optimization:

- Bathymetry extraction  
- Mooring equilibrium analysis  
- Hydrodynamic response evaluation  
- Cable configuration solver  
- Constraint-based optimization  

### Architectural Flow

```text
Bathymetry + Platform Geometry
              ↓
MoorPy (Offset / Watch Circle)
              ↓
RAFT (Dynamic Motion)
              ↓
Cable Geometry Definition
              ↓
Constraint-Based Optimization
              ↓
Optimized Cable Configuration
```

---

## Processing Workflow

1. Load farm configuration (YAML)  
2. Extract bathymetry at selected floater  
3. Define fairlead geometry  
4. Compute mooring-derived offset  
5. Extract RAFT dynamic motion  
6. Define cable model and variables  
7. Apply constraints  
8. Run optimization  
9. Evaluate final configuration  

---

## Cable System Definition

The cable is modeled as a multi-segment system connecting:

- seabed touchdown point  
- suspended spans with buoyancy  
- floater fairlead  

Fairlead position:

```
rBFair = [rFair, 0, zFair]
```

Where:

- rFair → radial distance  
- zFair → vertical position  

---

### Initial Configuration

<div align="center">
  <img src="/img/posts/morie_cable/cable_initial_config.png" 
       alt="Initial dynamic cable configuration showing seabed touchdown, suspended spans, and connection to floating wind turbine fairlead before optimization" 
       width="500">
</div>
*Figure 1 – Initial cable configuration prior to optimization.*

---

## Mooring-Derived Offset

Floater offset is obtained using MoorPy watch circle analysis:

```
offset = max( √(dx² + dy²) )
```

### Engineering Meaning

- Defines quasi-static excursion  
- Sets horizontal boundary condition for cable  

---

## Hydrodynamic Motion (RAFT)

Dynamic motion is derived from RAFT:

```
x_ampl = √(surge_max² + sway_max²)
```

### Engineering Meaning

- Captures wave-induced motion  
- Defines oscillatory cable loading  

---

## Cable Design Model

The cable configuration accounts for:

- self-weight  
- buoyancy modules  
- seabed interaction  
- dynamic boundary conditions  

### Key Inputs

- water depth  
- fairlead position  
- offset  
- dynamic amplitude  

---

## Optimization Problem

### Design Variables

- segment lengths  
- buoyancy distribution  
- lay lengths  

### Constraints

- minimum lay length  
- maximum sag  
- curvature limits  
- tension safety factors  
- touchdown range  

### Objective

- minimize cost  
- ensure full constraint compliance  

---

## Optimization Convergence

<div align="center">
  <img src="/img/posts/morie_cable/cable_board.png" 
       alt="Optimization convergence plot showing cost reduction and constraint satisfaction during dynamic cable configuration optimization process" 
       width="650">
</div>
*Figure 2 – Optimization convergence showing cost evolution and constraint satisfaction.*

---

## Optimized Configuration

<div align="center">
  <img src="/img/posts/morie_cable/cable_opt_config.png" 
       alt="Optimized dynamic cable configuration satisfying sag, curvature, tension, and seabed interaction constraints under realistic floater motion" 
       width="500">
</div>
*Figure 3 – Optimized cable configuration satisfying all constraints.*

---

## Outputs Generated

- optimized cable geometry  
- constraint verification results  
- cost evolution  
- curvature and sag profiles  
- tension safety checks  

---

## Engineering Applications

- dynamic cable concept design  
- constraint-driven optimization  
- coupling between mooring and cable systems  
- early-stage engineering assessment  

This module enables:

> **Physics-based cable design integrated with full system behavior**

---

## Relationship to Other Morie Study Cases

### Receives from

- **morie_site** → bathymetry  
- **morie_layout** → geometry  
- **morie_mooring** → offsets  
- **morie_anchor** → system constraints  

### Completes

- Full offshore wind system workflow  

> **Site → Layout → Mooring → Anchor → Cable**

---

## Why It Matters Commercially

- reduces overdesign of cables  
- improves installation feasibility  
- ensures constraint-compliant configurations  
- integrates structural and electrical design  

This is where:

> **motion-driven engineering meets power transmission design**

---

## Aspects to Improve

- fatigue and time-domain analysis  
- probabilistic motion envelopes  
- multi-cable system interactions  
- electrical performance coupling  
- full farm-level cable routing  

---

## Design Philosophy

- physics-based modeling  
- modular architecture  
- reproducibility  
- engineering usability  
- scalability to farm-level design  

---

## How to Run

1. Place required inputs:

   - YAML farm file  
   - bathymetry grid  
   - RAFT results  

2. Install dependencies:

   - `numpy`  
   - `matplotlib`  
   - `scipy`  
   - `FAModel`  
   - `MoorPy`  
   - `RAFT`  

3. Execute:

```bash
python morie_cable.py
```