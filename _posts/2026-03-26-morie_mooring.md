---
layout: post
title: Mooring System Generation & Load Analysis – Celtic Sea
image: "/posts/morie_mooring/shared_anchor_planview.png"
tags: [Offshore Floating Wind, Mooring Systems, RAFT, MoorPy, Shared Anchors, Python]
---

# Celtic Sea Floating Offshore Wind – Mooring System Generation & Load Analysis

## Executive Summary

This study establishes the **mooring physics layer** of Morie Analytics by transforming floating wind layouts into **physically consistent mooring systems and design-ready load outputs**.

Using YAML-based farm definitions, bathymetry and soil datasets, and integrated simulation tools (primarily MoorPy, with optional RAFT coupling), a modular Python workflow is developed to generate mooring configurations and extract **padeye-level loads (horizontal, vertical, and directional)** for engineering assessment.

A key objective of the workflow is to explicitly bridge **mooring system behavior and anchor demand**, enabling consistent transformation of line-level forces into **design-ready anchor loads (H, V, θ)**.

The result is a **reproducible computational pipeline** that connects geometry, equilibrium physics, and load transfer mechanisms into downstream anchor design inputs.

> Site intelligence → Layout generation → Soil reconstruction → **Mooring physics** → Anchor verification → Cable optimization
---

## Project Scope

- **Farm-scale mooring system generation**
- **Shared-anchor configurations enabled through geometric alignment**
- **Padeye-level load extraction (Ha, Va, θ) for each mooring line**
- **Shared-anchor load aggregation into resultant (H, V, θ)**
- Optional evaluation of **multiple environmental load cases**
- Optional dynamic extension using **RAFT (frequency-domain and time-domain reconstruction)**

The workflow transforms layout candidates into **engineering-ready mooring and anchor load datasets**, ensuring full traceability from:

```text
Layout → Mooring System → Line Loads → Anchor Demand
```

---

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

---

## Inputs and Dependencies

### From previous Morie studies

- **morie_layout** → floater positions, anchor geometry, shared-anchor topology
- **morie_site** → bathymetry, spatial domain, lease constraints
- **morie_soil** → soil interpretation framework used downstream in anchor design

### Additional inputs

- YAML-based floating wind farm configuration
- Mooring line properties and segment definitions
- Environmental load cases (wave headings and dynamic forcing assumptions)

These inputs are harmonized into a simulation-ready framework compatible with **FAModel**, **MoorPy**, and **RAFT**.

---

## Technical Architecture

The workflow is built on a modular architecture that separates **geometry definition**, **physics-based simulation**, and **load post-processing**.

### Core components

- `morie_mooring.py` → main execution script
- `FAModel` → project structure, geometry, and data handling
- `MoorPy` → static equilibrium solution
- `RAFT` → dynamic response and spectral output
- `merge_shared_anchors.py` → shared-anchor identification and merging

### Architectural flow

```text
YAML + Bathymetry + Layout Geometry
                ↓
      Mooring System Definition
                ↓
      Shared Anchor Detection
                ↓
       Pretension & Equilibrium
                ↓
   Dynamic Response & Load Cases
                ↓
   Padeye Load Extraction (Ha, Va, θ)
                ↓
 Shared Anchor Aggregation (H, V, θ)
                ↓
   Anchor Design Inputs for morie_anchor
```

This structure keeps the workflow reproducible and scalable while preserving physical traceability between intermediate steps.

---

## Processing Workflow

For a selected floating offshore wind layout, the workflow follows these stages:

1. Load floating wind farm configuration from YAML
2. Generate mooring geometry from floater positions and heading rules
3. Detect and merge coincident anchors to define shared-anchor nodes
4. Adjust line lengths and pretension to establish equilibrium
5. Solve the static mooring system in MoorPy
6. Evaluate environmental response and dynamic loading in RAFT
7. Identify the governing load case
8. Reconstruct time-domain tension histories
9. Extract padeye loads at anchor connection points
10. Aggregate line-level forces into anchor-level demand

This converts a geometric array layout into **design-ready loads for anchor verification**.

---

## 1. Mooring System Definition

Mooring systems are generated from floater layouts using deterministic geometric rules that define both **line topology and load transfer paths** across the farm.

Each floater is connected to the seabed through a set of mooring lines defined by consistent spatial and directional constraints.

### Key Assumptions

- **3 mooring lines per floater**
- **120° angular spacing (radial symmetry)**
- Fixed **anchor radius** from floater position
- Consistent **heading conventions in global coordinates**

<div align="center">
  <img src="/img/posts/morie_mooring/2dfarm_layout.png" 
       alt="Plan view of floating wind farm mooring layout showing floater positions, mooring line headings, and anchor locations" 
       width="500">
</div>
*Figure 1 – Plan view of mooring system geometry showing floater positions, line headings and anchor locations.*

### Geometric Construction

For each floater:

- Mooring line headings are assigned relative to a global reference system
- Anchor locations are generated by radial projection at a prescribed distance
- Line connectivity is defined between floater fairleads and seabed anchor points
- Angular spacing is enforced to maintain system symmetry and consistency

This process ensures that all mooring systems across the farm are **geometrically consistent and reproducible**, enabling scalable analysis.

---

### Shared Anchor Configuration

Due to the structured layout and fixed anchor radius, anchor locations from different floaters may coincide.

When this occurs:

- Multiple mooring lines are connected to a single anchor
- A **shared-anchor configuration** is formed
- Load contributions from multiple floaters are transferred to a common point

<div align="center">
  <img src="/img/posts/morie_mooring/2dfarm_shared.png" 
       alt="Plan view of floating wind farm showing shared-anchor configurations with anchors connected to one, two, or three mooring lines" 
       width="500">
</div>
*Figure 2 – Plan view of mooring system geometry showing floater positions, line headings and anchor counts (1, 2 or 3 shared anchors).*

This is not incidental, but a **deliberate outcome of layout topology**, enabling:

- Reduction in total anchor count
- Increased system compactness
- Coupled load interaction between floaters

The resulting topology defines the **foundation for load aggregation**, where multiple line forces must be combined into a single anchor demand.

---

## 2. Shared Anchor Detection & Topology

Following geometric generation of anchor locations, coincident anchors are identified and merged to define **shared-anchor nodes** within the farm.

This step transforms the mooring layout from a set of independent systems into a **connected network of load transfer points**, where multiple mooring lines may act on a single anchor.

### Detection & Merging

Shared anchors are identified through spatial analysis of anchor coordinates:

- Detect coincident or near-coincident anchor locations
- Merge anchors into unified nodes
- Reassign all connected mooring lines to the merged anchor
- Maintain full connectivity between floaters and shared anchor points

This ensures a consistent representation of the physical system, where each anchor node may receive loads from multiple lines.

<div align="center">
  <img src="/img/posts/morie_mooring/shared_anchor_planview.png" 
       alt="Shared-anchor topology map showing floater positions, mooring line headings, and merged anchor nodes across the farm" 
       width="500">
</div>
*Figure 3 – Plan view of mooring system geometry showing floater positions, line headings and anchor labels.*

### Topological Implications

The resulting system is no longer a collection of independent moorings, but a **coupled network** in which:

- Multiple floaters contribute to a single anchor load
- Load directions may differ between contributing lines
- Interaction effects arise due to shared load paths

This introduces a key engineering consideration:

> **anchor loads must be evaluated as the vector combination of all connected mooring lines**

### Engineering Significance

Shared-anchor configurations enable:

- Reduction in total anchor count
- More compact farm layouts
- Efficient use of seabed footprint

However, they also require:

- Accurate aggregation of line-level loads
- Resolution of directional load components
- Consistent transformation into anchor-level demand

This topology defines the **interface between mooring system behavior and anchor design**, where individual line forces are combined into resultant loads acting at each anchor.

---

## 3. Pretension & Equilibrium (MoorPy)

Following geometric definition and shared-anchor topology, the mooring system is brought into **static equilibrium** to establish a physically consistent baseline configuration.

This step ensures that all subsequent analysis is performed from a state that satisfies force balance between mooring lines, floaters, and seabed anchor points.

### Equilibrium Solution

The equilibrium configuration is solved using **MoorPy**, which computes the nonlinear response of the mooring system under prescribed geometry and pretension conditions.

Processing steps:

- Adjust line lengths to achieve target pretension levels
- Solve static equilibrium of the full mooring system
- Validate force balance at each floater
- Compute line tensions, angles, and catenary geometry

### Physical Interpretation

At equilibrium:

- Mooring lines define the **initial load distribution** in the system
- Each line transmits force between the floater fairlead and seabed anchor
- The system geometry determines load direction and magnitude
- Pretension establishes restoring stiffness and excursion behavior

### Outputs

- Equilibrium configuration of the mooring system
- Pretension levels per line
- Line geometry and orientation
- Watch circle behavior and restoring response

<div align="center">
  <img src="/img/posts/morie_mooring/mooring_profile.png" 
       alt="Mooring line profile showing catenary geometry between fairlead and anchor with seabed interaction and load transfer path" 
       width="500">
</div>
*Figure 4 – Mooring line profile showing catenary geometry between fairlead and anchor.*

The line profile illustrates:

- Catenary behavior under self-weight and pretension
- Touchdown region and seabed interaction
- Load direction at the anchor
- Distribution of horizontal and vertical force components

This provides a direct physical interpretation of how forces are transferred from the floater to the seabed.

### Engineering Significance

The equilibrium configuration defines the **baseline mechanical state** of the mooring system.

Key implications:

- Pretension controls system stiffness and restoring behavior
- Line geometry governs load direction and distribution
- Consistent pretension ensures comparable response across mooring lines

Accurate equilibrium representation is therefore essential for:

- Reliable evaluation of mooring system performance
- Consistent comparison between configurations
- Providing physically meaningful inputs to downstream analysis workflows

---

## 4. Environmental & Dynamic Mooring Response

Following the equilibrium solution, mooring system response is evaluated under varying environmental conditions to capture directional and dynamic effects on line loading.

### Load Case Definition

The primary variable considered is:

- **Wave heading (θ)**

For each case:

- Environmental forcing is applied
- Mooring response is evaluated relative to equilibrium
- Directional redistribution of line loads is monitored

### Dynamic Simulation (RAFT)

To capture system response under wave excitation, frequency-domain simulations are performed using **RAFT**.

- Simulations are run across a range of wave frequencies
- Mooring line responses are computed for each frequency component
- Line tension spectra are extracted for comparison across headings

<div align="center">
  <img src="/img/posts/morie_mooring/raft_heading_cases.png" 
       alt="Environmental load cases and frequency-domain mooring response across multiple wave headings for floating offshore wind system" 
       width="500">
</div>
*Figure 5 – Environmental load cases and corresponding frequency-domain response.*

### Physical Interpretation

Environmental loading introduces:

- Direction-dependent load redistribution
- Oscillatory tension due to wave excitation
- Frequency-dependent amplification of loads

### Outputs

- Mean tension
- Standard deviation
- Maximum and minimum loads
- Power Spectral Density (PSD)

The PSD describes how load energy is distributed across frequencies, highlighting dominant response modes and the sensitivity of each mooring line to dynamic forcing.

### Engineering Significance

This combined analysis enables:

- Evaluation of **directional sensitivity** of mooring loads
- Quantification of **dynamic load variability**
- Identification of **critical loading conditions** for further assessment

It extends the equilibrium-based analysis by incorporating both **environmental directionality and dynamic system response**.

---

## 5. Critical Load Case Identification

Following evaluation of environmental and dynamic response, the governing load case is identified to support engineering assessment.

This step determines which environmental condition produces the **most demanding mooring response**, forming the basis for subsequent analysis.

### Selection Criteria

For each mooring line:

- Tension responses are evaluated across all environmental load cases
- Peak tension values are identified, including dynamic extrema
- The load case producing the **maximum response** is selected

This defines the **critical environmental condition** for the system.

### Physical Interpretation

The critical load case typically corresponds to:

- Alignment of environmental forcing with one or more mooring lines
- Maximum load concentration in windward lines
- Combined effects of directional loading and dynamic amplification

This reflects the condition under which the mooring system experiences its **highest stress state**.

### Engineering Significance

Identifying the governing load case enables:

- Consistent comparison of mooring system performance across configurations
- Definition of **design-driving load conditions**
- Selection of representative scenarios for further analysis, such as time-domain reconstruction

The resulting load case provides a **physically consistent and conservative basis** for downstream design workflows.

---

## 6. Time-Domain Reconstruction

To support fatigue and extreme load assessment, representative time series of mooring line tension are reconstructed from frequency-domain results.

This step translates spectral response data into **time-resolved load signals**, enabling evaluation of load evolution under realistic conditions.

### Methodology

For the selected critical load case:

- PSD outputs from dynamic analysis are used
- Stochastic time series are generated consistent with the spectral response
- Reconstructed signals are validated against the original response statistics

### Outputs

- 360-second tension time histories
- Peak load verification
- Statistical consistency in mean, variance, and extrema

### Physical Interpretation

The reconstructed time series represents:

- Oscillatory loading due to wave-induced motion
- Temporal variation in mooring line tension
- Occurrence of peak loads within a realistic time window

<div align="center">
  <img src="/img/posts/morie_mooring/mooring_loads.png" 
       alt="Reconstructed mooring line tension time series showing dynamic load variation and peak response under selected environmental case" 
       width="500">
</div>
*Figure 6 – Time-domain reconstruction of mooring line tension.*

### Engineering Significance

Time-domain reconstruction enables:

- Assessment of **extreme load events** within a time history
- Input for **fatigue analysis and cycle counting**
- Validation of peak responses identified in frequency-domain analysis

This step completes the workflow by bridging **spectral response analysis and time-domain engineering requirements**.

---

## 7. Integrated Python Workflow

All steps are implemented in a modular Python pipeline:

```python
# Load project
project = Project('floating_farm.yaml')

# Generate mooring system
project.generate_moorings()

# Merge shared anchors
merge_shared_anchors(project)

# Solve equilibrium
project.solve_mooring_equilibrium()

# Run RAFT simulations
results = run_raft_cases(project)

# Extract critical loads
critical_case = get_max_tension_case(results)
```

This structure highlights the connection between:

- Geometry definition
- Shared-anchor topology
- Static equilibrium
- Dynamic response
- Load extraction for anchor design

---

## 8. Load Extraction

Following identification of the critical load case and reconstruction of time-domain signals, loads are extracted at the **padeye level** for each mooring line.

This step converts global mooring response into **local load components at the anchor connection point**, which are required for engineering design.

### Padeye Load Components

For each mooring line:

- Horizontal load → **Ha**
- Vertical load → **Va**
- Direction → **θ**

### Load Transformation

To enable consistent aggregation across multiple lines, horizontal loads are resolved into global components:

```python
Hx = Ha * cos(theta)
Hy = Ha * sin(theta)
```

This transformation allows all line contributions to be expressed in a **common coordinate system**.

### Engineering Significance

Padeye-level load extraction ensures:

- Direct compatibility with anchor design models
- Consistent representation of load direction and magnitude
- Traceability from mooring response to anchor demand

---

## 9. Anchor Load Aggregation

For each shared anchor, loads from all connected mooring lines are combined to obtain the **resultant anchor demand**.

### Aggregation Procedure

For each anchor:

- Sum horizontal components across all connected lines
- Sum vertical loads directly
- Compute resultant magnitude and direction

### Outputs

- Resultant horizontal load → **H**
- Total vertical load → **V**
- Load direction → **θ**

### Engineering Interpretation

This step converts:

> **Multiple line-level forces → Single anchor-level demand**

This is the key interface between:

- Mooring system analysis
- Anchor capacity design

---

## Outputs Generated

The workflow produces the following outputs:

### Mooring-Level Outputs

- Farm-scale mooring geometry
- Shared-anchor topology
- Equilibrium configuration and pretension levels
- Line tensions, angles, and catenary geometry
- Padeye-level loads (Ha, Va, θ)

### Dynamic Outputs

- Frequency-domain response metrics
- PSD-based tension characterization
- Critical load case identification
- Time-domain tension histories

### Anchor-Level Outputs

- Resultant horizontal load (H)
- Total vertical load (V)
- Load direction (θ)
- Identification of contributing mooring lines per anchor

These outputs provide direct inputs for **morie_anchor** and establish a physically consistent link between system behavior and foundation demand.

---

## Engineering Applications

The structured outputs support the following engineering applications:

- **Shared-anchor load evaluation**
- **Anchor sizing and capacity verification**
- **Mooring system configuration and optimization**
- **Load consistency and validation**
- **Environmental sensitivity studies**
- **Fatigue and extreme load assessment**

Overall, the workflow enables a scalable and consistent approach to:

```text
Mooring System Behavior → Anchor Demand → Design Verification
```

---

## Relationship to Other Morie Studies

### Receives from

- **morie_layout** → floater geometry, spatial arrangement, shared-anchor topology
- **morie_site** → bathymetry and site-scale spatial definition
- **morie_soil** → subsurface interpretation framework used downstream in anchor design

### Feeds into

- **morie_anchor** → anchor capacity design and verification
- **morie_cable** → indirectly, through floater arrangement and system configuration constraints

This module acts as the **physics engine of the Morie Analytics workflow**, translating geometry into forces and forces into design demand.

---

## Why It Matters Commercially

This workflow provides commercial value by:

- Reducing overdesign in anchor systems
- Enabling shared-anchor strategies that reduce installation cost
- Providing traceable load paths from system analysis to design checks
- Supporting rapid comparison of alternative layouts and mooring configurations
- Improving confidence in early-stage floating wind engineering decisions

It is the point in the pipeline where:

> **physics meets cost, and configuration becomes design strategy**

---

## Aspects to Improve

Future extensions could include:

- Fully coupled soil–mooring interaction
- Nonlinear seabed contact models
- Probabilistic environmental load cases
- Automated optimization loops across geometry, pretension, and anchor demand
- Integration with installation and operability constraints
- Batch evaluation of multiple farm-scale layouts

These developments would strengthen the workflow as a decision-support tool for both engineering design and commercial optimization.

---

## Design Philosophy

This project is built on the following principles:

- **Reproducibility**
- **Modular architecture**
- **Integration of geometry and physics**
- **Traceability from system response to design input**
- **Engineering usability of outputs**
- **Scalability to farm-level analysis**

The workflow demonstrates how mooring system modeling can be transformed into a **structured, data-driven engineering process** where system mechanics directly inform foundation design.

---

## How to Run

1. Place datasets in `celtic_sea_share/`  
2. Install dependencies:

	- `numpy`
	- `matplotlib`
	- `scipy`
	- `pyyaml`
	- `FAModel`
	- `MoorPy`
	- `RAFT` (optional for dynamic extension)

3. Execute:

```bash
python morie_mooring.py
```

