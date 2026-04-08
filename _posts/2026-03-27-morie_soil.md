---
layout: post
title: Local Soil Reconstruction & Subsurface Intelligence – Celtic Sea
image: "/img/posts/morie_soil/morie_soil2.png"
tags: [Offshore Floating Wind, Geotechnical Engineering, Soil Modeling, Tomography, Floating Wind, Anchors, Python]
---

# Celtic Sea Floating Offshore Wind – Local Soil Reconstruction & Subsurface Intelligence

## Executive Summary

This study establishes the **soil reconstruction layer** of Morie Analytics by transforming sparse geotechnical information into **engineering-ready soil profiles at anchor locations**.

Starting from a layout generated in **morie_layout**, the workflow constructs a localized soil domain, generates a synthetic ground truth model, emulates **tomographic sampling**, and reconstructs vertical soil profiles using interpolation techniques.

The result is a **reproducible framework for anchor-level soil characterization**, bridging the gap between spatial layout design and geotechnical engineering inputs.

> Site intelligence → Layout generation → **Soil reconstruction** → Mooring physics → Anchor verification → Cable optimization


## Project Scope

- Local domain extraction from selected floater cluster
- Cropping of bathymetry and soil datasets
- Synthetic layered soil model generation
- Tomographic sampling using sectional planes
- Soil profile reconstruction via interpolation
- Boundary detection and validation
- Multi-anchor soil characterization

This study converts **layout intelligence into anchor-ready subsurface inputs**.


## Engineering Context

Following layout definition, the next geotechnical question is:

> **What soil profile is acting at each anchor location?**

Anchor and mooring design depend critically on:

- Soil stratigraphy
- Layer boundaries
- Spatial variability
- Localized geotechnical interpretation

However, early-stage offshore projects typically rely on:

- Sparse CPT data
- Limited geotechnical sections
- Incomplete subsurface coverage

This workflow introduces a **localized reconstruction methodology**, where sparse sectional information is converted into soil profiles suitable for downstream engineering analysis.


## Inputs and Data Sources

This study builds directly on upstream Morie Analytics outputs:

### From `morie_site`

- Bathymetry grid  
- Soil classification grid  
- Lease boundary context 

### From `morie_layout`

- Selected floater cluster  
- FOWT coordinates  
- Anchor coordinates  
- Local layout footprint   

### Additional Inputs

- Layered soil profile definitions (YAML)  
- Cropped local-domain datasets  
- Synthetic soil-model parameters  

All inputs are aligned in a **common projected coordinate system**.

This provides the **subsurface data framework for anchor-level characterization**.


## Technical Architecture

The workflow is implemented in Python using:

- `numpy` → numerical operations  
- `matplotlib` → visualization  
- `yaml` → configuration handling  
- `pickle` → intermediate storage  
- `famodel` → layout and anchor extraction  

Core modules:

- `layout_domain` → domain cropping around selected layout  
- `truth_soil_model` → synthetic layered soil generation  
- `tomographic_grid` → plane definition for soil sampling  
- `soil_sampling` → property extraction along planes  
- `profile_reconstruction` → interpolation at anchor locations  
- `boundary_detection` → layer interface identification  
- `soil_visualization` → validation and plotting   

### System Flow

Layout Geometry → Domain Extraction → Soil Reconstruction → Anchor Profiles

The architecture ensures **traceability from spatial inputs to geotechnical outputs**.


## Processing Workflow

1. Load selected layout and soil model  
2. Extract FOWT and anchor coordinates  
3. Define cropped local domain  
4. Generate synthetic soil model  
5. Build tomographic sampling grid  
6. Sample soil properties along planes  
7. Reconstruct profiles at anchor locations  
8. Detect layer boundaries  
9. Validate reconstruction against truth  
10. Select representative anchor location  

This converts **layout geometry into anchor-level soil profiles**.


## Local Domain Definition

The workflow begins by defining a **localized engineering domain** around the selected floater cluster.

<div align="center">
  <img src="/img/posts/morie_soil/00_lease_crop_context.png"
       alt="Lease boundary and cropped local domain showing selected floating wind cluster and anchor positions within the Celtic Sea lease area"
       width="500">
</div>
_Figure 1 – Lease boundary and cropped local soil domain highlighting the selected floater cluster and associated anchor positions._

### Engineering Significance

This figure establishes:

- The relationship between **lease-scale site context** and **local soil study area**
- The cropped analysis window used for detailed subsurface reconstruction
- Spatial continuity from `morie_site` and `morie_layout` into geotechnical analysis

<div align="center">
  <img src="/img/posts/morie_soil/01_cropped_bathy.png"
       alt="Cropped bathymetry map of the local domain showing water depth distribution around selected floating wind turbine cluster"
       width="500">
</div>
_Figure 2 – Cropped bathymetry defining the local engineering domain._

<div align="center">
  <img src="/img/posts/morie_soil/02_cropped_soil.png"
       alt="Cropped seabed classification map showing local sediment distribution within selected floating wind farm domain"
       width="500">
</div>
_Figure 3 – Cropped soil classification aligned with the local layout domain._

### Engineering Significance

These local-domain products define:

- A focused computational region around the layout
- Alignment between geometry and subsurface inputs
- The starting point for localized truth-model generation


## Synthetic Soil Model (Ground Truth)

A synthetic truth model is generated over the cropped local domain to provide a controlled subsurface reference.

<div align="center">
  <img src="/img/posts/morie_soil/03_truth_surfaces.png"
       alt="Synthetic layered soil model showing spatial variation of layer boundaries Z1 and Z2 across the local domain"
       width="500">
</div>
_Figure 4 – Synthetic ground truth soil model with spatially varying layer interfaces._

### Model Characteristics

- Three-layer sand system
- Interfaces: **Z1** and **Z2**
- Spatially varying layer boundaries
- Continuous variation of:
  - Friction angle, φ
  - Relative density, Dr
  - Unit weight, γ

### Engineering Significance

The truth model provides:

- A controlled reference model
- Known boundaries for validation
- A benchmark to quantify reconstruction performance


## Tomographic Sampling Framework

To emulate realistic geotechnical data availability, the workflow defines a sparse tomographic sampling framework.

<div align="center">
  <img src="/img/posts/morie_soil/04_tomographic_layout.png"
       alt="Tomographic sampling layout showing XZ and YZ sectional planes used to emulate geotechnical investigation coverage"
       width="500">
</div>
_Figure 5 – Tomographic acquisition grid representing sparse geotechnical sampling across the local domain._

### Configuration

- 4 XZ planes
- 4 YZ planes
- Single-point validation location inside the cluster
- Full anchor set preserved for later reconstruction

### Engineering Significance

This step represents:

- CPT-style investigation lines
- Sectional surveys
- Limited geotechnical campaigns under realistic coverage constraints


## Soil Section Sampling

The synthetic truth model is sampled along each tomographic plane to generate the available sectional dataset.

<div align="center">
  <img src="/img/posts/morie_soil/05_xz01_layer_id.png"
       alt="Vertical XZ soil section showing reconstructed stratigraphic layer distribution across depth and horizontal distance in the sampled plane"
       width="500">
</div>
_Figure 6 – Example XZ section showing vertical layering and lateral variability._

<div align="center">
  <img src="/img/posts/morie_soil/06_yz01_layer_id.png"
       alt="Vertical YZ soil section showing reconstructed stratigraphic layer distribution across depth and horizontal distance in the sampled plane"
       width="500">
</div>
_Figure 7 – Example YZ section showing vertical layering and lateral variability._

### Engineering Significance

These sections form the **available dataset**, capturing:

- Vertical layer stacking
- Lateral variation across the domain
- Sparse but structured information for downstream interpolation


## Profile Reconstruction

A single-point proof of concept is first used to validate the reconstruction methodology within the selected layout.

<div align="center">
  <img src="/img/posts/morie_soil/07_profile_comparison_phi.png"
       alt="Comparison of reconstructed and ground truth soil profiles showing accuracy of interpolation-based soil property estimation"
       width="500">
</div>
_Figure 8 – Reconstructed vs ground truth soil profile at the single-point validation location._

### Method

- Inverse Distance Weighting (IDW)
- Multi-plane interpolation from XZ and YZ sections

### Engineering Output

- Continuous φ(z), Dr(z), γ(z)
- Local profile reconstruction from sparse sections
- Validation of the proof-of-concept interpolation approach


## Boundary Detection & Validation

The reconstructed profile is then converted into discrete engineering layers through boundary detection.

<div align="center">
  <img src="/img/posts/morie_soil/08_boundary_comparison.png"
       alt="Comparison of detected and true soil layer boundaries demonstrating accuracy of boundary identification algorithm"
       width="500">
</div>
_Figure 9 – Boundary detection accuracy at the single-point validation location._

### Results

- Z1 mean error ≈ 0.30 m
- Z2 mean error ≈ 0.42 m
- Maximum error < 1 m

### Engineering Significance

This step transforms reconstructed profiles into:

- Discrete engineering layers
- Inputs for capacity models
- Quantified reconstruction accuracy


## Multi-Anchor Evaluation

Following proof-of-concept validation, the workflow is applied across all anchors in the selected layout.

- 24 anchors evaluated
- Independent reconstruction at each anchor location
- Boundary comparison metrics computed for all anchors
- Ranking performed based on total boundary error

### Selected Anchor

- **fowt1b** → selected as downstream handoff anchor for `morie_anchor`

This selection is now formalized in the workflow and exported for the downstream case study.

### Engineering Significance

This step ensures that the soil-reconstruction module produces **actionable anchor-specific outputs**, not only validation figures.

***

## Anchor-Level Soil Profile (fowt1b)

The selected anchor **fowt1b** is exported with its fully reconstructed soil profile in a structured format (`profile_map`), directly usable in downstream anchor capacity models.

This structure represents the **final engineering output** of the soil reconstruction workflow.

### Profile Structure

```python
profile_map = {
    'layers': [
        {
            'type': 'sand',
            'z_top': stick-up_length,
            'z_bottom': Z1 + stick-up_length,
            'gamma_top': 9.0,
            'gamma_bot': 10.0,
            'phi_top': 30.0,
            'phi_bot': 32.0,
            'Dr_top': 60.0,
            'Dr_bot': 75.0},
        {
            'type': 'sand',
            'z_top': Z1 + stick-up_length,
            'z_bot': Z2 + stick-up_length,
            'gamma_top': 10.0,
            'gamma_bot': 11.0,
            'phi_top': 32.0,
            'phi_bot': 37.0,
            'Dr_top': 75.0,
            'Dr_bot': 85.0},
        {
            'type': 'sand',
            'z_top': Z2 + stick-up_length,
            'z_bot': Zmax + stick-up_length,
            'gamma_top': 11.0,
            'gamma_bot': 12.0,
            'phi_top': 37.0,
            'phi_bot': 40.0,
            'Dr_top': 85.0,
            'Dr_bot': 95.0}]}
```

## Outputs Generated

The workflow produces:

- Lease-to-local crop context figure
- Cropped bathymetry and soil grids
- Synthetic truth soil model
- Tomographic section plots
- Single-point profile validation plots
- Boundary detection results
- Anchor-level soil datasets
- Selected downstream anchor definition

These outputs are directly usable in the next engineering modules.


## Engineering Applications

The outputs support:

- Anchor design input generation
- Soil-structure interaction modeling
- Early-stage geotechnical interpretation
- Validation of sparse-data reconstruction
- Integration with anchor capacity workflows

This transforms sparse subsurface information into **engineering decision inputs**.


## Relationship to Other Morie Study Cases

This study is the **subsurface intelligence bridge** of the Morie Analytics workflow.

### Receives from:

- **morie_site** → lease boundary, bathymetry, soil grids
- **morie_layout** → floater cluster and anchor coordinates

### Feeds into:

- **morie_anchor** → selected anchor profile and boundary definition
- **morie_mooring** → soil-informed assumptions for embedded load transfer
- **morie_cable** → local seabed interpretation for downstream routing logic

It provides the **geotechnical transition from layout geometry to anchor design**.


## Why It Matters Commercially

- Reduces uncertainty in early-stage geotechnical interpretation
- Enables engineering decisions with limited site data
- Improves reliability of anchor sizing inputs
- Supports scalable offshore development workflows
- Bridges the gap between GIS-scale data and anchor-scale design

This is where **subsurface uncertainty becomes quantifiable and manageable**.


## Aspects to Improve

- Integration with real CPT datasets
- Multi-soil systems (clay, sand, rock)
- Uncertainty quantification
- Adaptive sampling strategies
- Machine learning-based reconstruction

These extensions would move the workflow closer to **project-grade geotechnical intelligence**.


## Design Philosophy

This study reflects the Morie Analytics approach:

- Physics-informed  
- Modular  
- Traceable  
- Engineering-focused  
- Scalable  


## How to Run

1. Place datasets in `celtic_sea_share/`
2. Install dependencies:

- `numpy`
- `matplotlib`
- `pyyaml`
- `pickle`
- `famodel`

3. Execute:

```bash
python morie_soil.py
```