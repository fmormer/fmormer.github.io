---
layout: post
title: Mooring System Generation & Load Analysis – Celtic Sea
image: "/posts/shared_anchor_planview.png"
tags: [Offshore Wind, Mooring Systems, RAFT, MoorPy, Shared Anchors, Python]
---

# Celtic Sea Floating Offshore Wind – Mooring System Generation & Load Analysis

This project extends the site characterization and layout optimization workflow by introducing a structured methodology for generating, simulating, and analyzing floating offshore wind mooring systems.

Using YAML-based farm definitions, bathymetry and soil datasets, and integrated simulation tools (MoorPy and RAFT), a modular Python workflow is developed to transform floater layouts into physically consistent mooring systems and extract critical load cases for engineering assessment.

The objective is to formalize mooring system modeling into a reproducible computational pipeline that bridges geometry, environmental loading, and anchor design inputs.

---

## Project Scope

- **Farm-scale mooring system generation**
- **Shared-anchor configurations enabled**
- **Multiple environmental load cases evaluated**
- ~**100 frequency bins per simulation**
- **360 s reconstructed time series per case**
- Automated extraction of **critical load envelopes**

The workflow transforms layout candidates into engineering-ready mooring load datasets suitable for anchor design and system optimization.

---

## 1. Mooring System Definition

Mooring systems are generated from floater layouts using deterministic geometric rules.

Key assumptions:

- **3 mooring lines per floater**
- **120° angular spacing**
- Fixed **anchor radius**
- Consistent **heading conventions**

<div align="center">
  <img src="/img/posts/shared_anchor_planview.png" alt="Shared Anchor Plan View" width="500">
</div>
*Figure 1 – Plan view of shared-anchor configuration and mooring line headings.*

Processing steps:

- Assign mooring headings based on floater orientation  
- Generate anchor locations from radial projection  
- Define line connectivity (floater → anchor)  
- Ensure geometric consistency across the farm  

Shared-anchor configurations emerge naturally where anchor locations coincide.

---

## 2. Shared Anchor Detection & Topology

Floating wind layouts often allow multiple floaters to share anchor points.

Processing steps:

- Detect coincident anchor coordinates  
- Merge anchors into unified nodes  
- Reassign mooring line connectivity  
- Preserve load contributions from all connected lines  

This enables:

- Reduction in total anchor count  
- Improved layout compactness  
- Coupled load transfer between floaters  

Shared-anchor topology becomes a key driver of system efficiency.

---

## 3. Pretension & Equilibrium (MoorPy)

Before dynamic analysis, the mooring system must satisfy static equilibrium.

Processing steps:

- Adjust line lengths to meet target pretension  
- Solve equilibrium using **MoorPy**  
- Validate force balance at each floater  
- Compute initial line tensions and geometry  

Outputs:

- Equilibrium configuration  
- Pretension levels per line  
- Watch circle behavior (platform excursion limits)  

Pretension consistency is critical for ensuring comparable load response across lines and floaters.

---

## 4. Environmental Load Case Definition

Mooring loads are evaluated under multiple environmental conditions.

Key variable:

- **Wave heading (θ)**

For each case:

- Environmental forcing is applied  
- Mooring response is computed  
- Line tensions are recorded  

<div align="center">
  <img src="/img/posts/raft_heading_cases.png" alt="Wave Heading Cases" width="500">
</div>
*Figure 2 – Environmental load cases defined by wave heading variation.*

This enables directional sensitivity analysis of mooring system performance.

---

## 5. Dynamic Mooring Analysis (RAFT)

Dynamic response is evaluated using **RAFT frequency-domain simulations**.

Processing steps:

- Convert project into RAFT-compatible model  
- Run simulations for all load cases  
- Compute frequency-domain responses  
- Extract mooring line tension spectra  

Outputs:

- Mean tension  
- Standard deviation  
- Maximum and minimum loads  
- Power Spectral Density (PSD)  

This provides a statistical description of mooring loads across sea states.

---

## 6. Critical Load Case Identification

For engineering design, the governing load case must be identified.

Processing logic:

- Evaluate all load cases per mooring line  
- Identify maximum tension across cases  
- Select the **critical environmental condition**  
- Propagate this case to define design loads  

This ensures that:

- Anchor design is based on **worst-case loading**
- Shared anchors account for **combined line effects**

---

## 7. Time-Domain Reconstruction

To support fatigue and extreme analysis, time series are reconstructed from spectral data.

Processing steps:

- Use PSD outputs from RAFT  
- Generate stochastic time series  
- Validate reconstructed statistics against simulation outputs  

Outputs:

- 360-second tension time histories  
- Peak load validation  
- Statistical consistency checks  

This bridges frequency-domain analysis with time-domain engineering requirements.

---

## 8. Integrated Python Workflow

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