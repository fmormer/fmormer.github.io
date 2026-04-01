---
layout: post
title: Local Soil Reconstruction & Subsurface Intelligence – Celtic Sea
image: "/posts/morie_soil/04_tomographic_layout.png"
tags: [Offshore Floating Wind, Geotechnical Engineering, Soil Modeling, Tomography, Floating Wind, Anchors, Python]
---

# Celtic Sea Floating Offshore Wind – Local Soil Reconstruction & Subsurface Intelligence

## Executive Summary

This study establishes the **soil reconstruction layer** of Morie Analytics by transforming sparse geotechnical information into **engineering-ready soil profiles at anchor locations**.

Starting from a layout generated in **morie_layout**, the workflow constructs a localized soil domain, generates a synthetic ground truth model, emulates **tomographic sampling**, and reconstructs vertical soil profiles using interpolation techniques.

The result is a **reproducible framework for anchor-level soil characterization**, bridging the gap between spatial layout design and geotechnical engineering inputs.

> Site intelligence → Layout generation → **Soil reconstruction** → Mooring physics → Anchor verification → Cable optimization

---

## Project Scope

- Local domain extraction from selected floater cluster  
- Cropping of bathymetry and soil datasets  
- Synthetic layered soil model generation (truth)  
- Tomographic sampling using sectional planes  
- Soil profile reconstruction via interpolation  
- Boundary detection and validation  
- Multi-anchor soil characterization  

This study transforms:

> **Layout → Local Soil Model → Anchor Design Inputs**

---

## Engineering Context

Anchor and mooring design depend critically on:

- soil stratigraphy  
- layer boundaries  
- spatial variability  

However, early-stage offshore projects typically rely on:

- sparse CPT data  
- limited geotechnical sections  
- incomplete subsurface coverage  

This workflow emulates that reality and provides a structured way to:

- reconstruct soil profiles from limited data  
- quantify uncertainty  
- generate inputs suitable for engineering design  

---

## Inputs and Data Sources

This study builds directly on:

### From `morie_layout`:
- Selected floater cluster  
- Anchor coordinates  
- Local spatial domain  

### From `morie_site`:
- Bathymetry grids  
- Soil classification grids  

Additional inputs:

- Layered soil profile definitions (YAML)  

---

## Technical Architecture

The workflow is implemented in Python using:

- `numpy` → numerical operations  
- `matplotlib` → visualization  
- custom modular utilities for each step  

Core modules:

- domain extraction  
- synthetic soil generation  
- tomographic grid definition  
- soil sampling  
- profile reconstruction  
- boundary detection  

The structure ensures **full traceability from data to engineering output**.

---

## Processing Workflow

1. Load layout and extract anchor positions  
2. Define local domain around cluster  
3. Crop bathymetry and soil grids  
4. Generate synthetic soil model (truth)  
5. Define tomographic acquisition grid  
6. Sample soil properties along planes  
7. Reconstruct profiles at anchor locations  
8. Detect layer boundaries  
9. Compare against truth  
10. Evaluate reconstruction across all anchors  

---

## Local Domain Definition

<div align="center">
  <img src="/img/posts/morie_soil/01_cropped_bathy.png" 
       alt="Cropped bathymetry map of the local domain showing water depth distribution around selected floating wind turbine cluster" 
       width="500">
</div>
*Figure 1 – Cropped bathymetry defining the local engineering domain.*

<div align="center">
  <img src="/img/posts/morie_soil/02_cropped_soil.png" 
       alt="Cropped seabed classification map showing local sediment distribution within selected floating wind farm domain" 
       width="500">
</div>
*Figure 2 – Cropped soil classification aligned with the local layout domain.*

### Engineering Significance

Defines:

- a **localized engineering domain**  
- alignment between layout and subsurface data  
- reduced computational complexity  

---

## Synthetic Soil Model (Ground Truth)

<div align="center">
  <img src="/img/posts/morie_soil/03_truth_surfaces.png" 
       alt="Synthetic layered soil model showing spatial variation of layer boundaries Z1 and Z2 across the local domain" 
       width="500">
</div>
*Figure 3 – Synthetic ground truth soil model with spatially varying layer interfaces.*

### Model Characteristics

- Three-layer sand system  
- Interfaces: **Z1 and Z2**  
- Spatial variation using smooth functions  
- Continuous variation of φ, Dr, γ  

### Engineering Significance

Provides:

- a controlled reference model  
- known layer boundaries  
- benchmark for reconstruction accuracy  

---

## Tomographic Sampling Framework

<div align="center">
  <img src="/img/posts/morie_soil/04_tomographic_layout.png" 
       alt="Tomographic sampling layout showing XZ and YZ sectional planes used to emulate geotechnical investigation coverage" 
       width="500">
</div>
*Figure 4 – Tomographic acquisition grid representing sparse geotechnical sampling.*

### Configuration

- 4 XZ planes  
- 4 YZ planes  

### Engineering Interpretation

Represents:

- CPT campaigns  
- sectional surveys  
- limited geotechnical investigations  

---

## Soil Section Sampling

<div align="center">
  <img src="/img/posts/morie_soil/05_xz01_phi.png" 
       alt="Vertical XZ soil section showing variation of friction angle phi across depth and horizontal distance in sampled plane" 
       width="500">
</div>
*Figure 5 – XZ section illustrating vertical soil layering and lateral variability.*

<div align="center">
  <img src="/img/posts/morie_soil/06_yz01_phi.png" 
       alt="Vertical YZ soil section showing variation of friction angle phi across depth and horizontal distance in sampled plane" 
       width="500">
</div>
*Figure 6 – YZ section illustrating vertical soil layering and lateral variability.*

### Engineering Significance

These sections represent the **available dataset**, capturing:

- vertical layering  
- lateral variability  
- sparse measurement coverage  

---

## Profile Reconstruction

<div align="center">
  <img src="/img/posts/morie_soil/07_profile_comparison_phi.png" 
       alt="Comparison of reconstructed and ground truth soil profiles showing accuracy of interpolation-based soil property estimation" 
       width="500">
</div>
*Figure 7 – Reconstructed vs ground truth soil profiles at anchor location.*

### Method

- Inverse Distance Weighting (IDW)  
- Multi-plane interpolation  

### Engineering Output

- Continuous φ(z), Dr(z), γ(z)  
- Anchor-specific soil profiles  

---

## Boundary Detection & Validation

<div align="center">
  <img src="/img/posts/morie_soil/08_boundary_comparison.png" 
       alt="Comparison of detected and true soil layer boundaries demonstrating accuracy of boundary identification algorithm" 
       width="500">
</div>
*Figure 8 – Boundary detection accuracy for reconstructed soil layers.*

### Results

- Z1 error ≈ 0.30 m (mean)  
- Z2 error ≈ 0.42 m (mean)  
- Maximum error < 1 m  

### Engineering Significance

Transforms reconstructed profiles into:

- discrete engineering layers  
- inputs for capacity models  
- validated subsurface representation  

---

## Multi-Anchor Evaluation

- 24 anchors evaluated  
- independent reconstruction per location  
- anchors ranked by reconstruction accuracy  

### Selected Anchor

- **fowt6c** → best agreement with truth  

This anchor becomes the **handoff point to morie_anchor**.

---

## Outputs Generated

- Cropped bathymetry and soil grids  
- Synthetic soil model (truth)  
- Tomographic sections  
- Reconstructed profiles  
- Boundary detection results  
- Anchor-level soil datasets  

---

## Engineering Applications

- Anchor design input generation  
- Soil-structure interaction modeling  
- Early-stage geotechnical interpretation  
- Validation of sparse-data reconstruction  
- Integration with anchor capacity workflows  

---

## Relationship to Other Morie Study Cases

### Receives from:
- **morie_layout** → floater and anchor locations  
- **morie_site** → bathymetry and soil grids  

### Feeds into:
- **morie_anchor** → soil profiles for capacity design  
- **morie_mooring** (indirectly) → soil-informed load transfer assumptions  

This module is the **bridge between layout geometry and geotechnical design**.

---

## Why It Matters Commercially

- Reduces uncertainty in early-stage geotechnical design  
- Enables engineering decisions with limited data  
- Improves anchor sizing reliability  
- Supports scalable offshore development workflows  
- Bridges gap between GIS and geotechnical engineering  

This is where **subsurface uncertainty becomes quantifiable and manageable**.

---

## Aspects to Improve

- Integration with real CPT datasets  
- Multi-soil systems (clay, sand, rock)  
- Uncertainty quantification  
- Adaptive sampling strategies  
- Machine learning-based reconstruction  

---

## Design Philosophy

This study reflects Morie Analytics principles:

- physics-informed modeling  
- data-driven reconstruction  
- modular workflow design  
- engineering usability  
- scalability across projects  

---

## How to Run

1. Place datasets in `celtic_sea_share/`  
2. Install dependencies:

   - `numpy`  
   - `matplotlib` 
   - `geopandas`  
   - `xarray`   

3. Execute:

```bash
python morie_soil.py
```