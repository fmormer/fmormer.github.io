---
layout: post
title: Local Soil Reconstruction for Floating Offshore Wind – Celtic Sea
image: "/posts/morie_soil/tomographic_layout.png"
tags: [Offshore Wind, Geotechnical Engineering, Soil Modeling, Tomography, Floating Wind, Anchors, Python]
---

# Celtic Sea Floating Offshore Wind – Local Soil Reconstruction & Tomographic Characterization

This project develops a structured methodology to transform **localized site data and sparse subsurface information into engineering-ready soil profiles** for floating offshore wind applications.

Starting from a selected floater layout, a modular Python workflow is implemented to construct a **synthetic ground truth model**, emulate **tomographic sampling**, and reconstruct **vertical soil profiles at anchor locations**.

The workflow bridges the gap between **layout definition and anchor design**, enabling consistent geotechnical inputs for downstream engineering analysis.

---

## Project Scope

- Local domain definition from floating wind layout  
- Cropping of bathymetry and soil datasets  
- Synthetic layered soil model generation  
- Tomographic sampling using sectional planes  
- Profile reconstruction via interpolation  
- Boundary detection and validation  
- Anchor-level soil characterization  

The workflow transforms spatial and subsurface data into:

Layout → Soil Model → Anchor Design Inputs

---

## 1. Local Domain Definition

The workflow begins by extracting a **localized engineering domain** from the selected floating wind layout.

### Methodology

- Import floater and anchor coordinates from YAML  
- Define a bounding region around the layout  
- Apply buffer distance (~800 m)  
- Crop bathymetry and soil grids  

<div align="center">
  <img src="/img/posts/morie_soil/plot_bathy.png" width="500">
</div>
*Figure 1 – Cropped bathymetry grid representing the local depth variation within the selected floating wind cluster.*

<div align="center">
  <img src="/img/posts/morie_soil/plot_soil.png" width="500">
</div>
*Figure 2 – Cropped soil classification map showing dominant seabed material within the local domain.*

### Engineering Significance

This step establishes:

- A **consistent spatial reference** for all datasets  
- A **reduced computational domain**  
- Alignment between layout geometry and soil conditions  

---

## 2. Synthetic Soil Model (Truth)

A synthetic layered soil model is constructed to represent the **ground truth subsurface**.

### Model Definition

- Three sand layers  
- Two interfaces: **Z1 and Z2**  
- Spatial variation defined using smooth sinusoidal functions  
- Continuous variation of:
  - Friction angle (φ)  
  - Relative density (Dr)  
  - Unit weight (γ)  

<div align="center">
  <img src="/img/posts/morie_soil/truth_surfaces.png" width="700">
</div>
*Figure 3 – Synthetic soil layer interfaces (Z1 and Z2) defining the ground truth stratigraphy.*

### Engineering Significance

The truth model provides:

- A **controlled reference system**  
- Known layer boundaries for validation  
- A benchmark to quantify reconstruction accuracy  

---

## 3. Tomographic Grid Definition

To emulate realistic geotechnical data availability, a **tomographic acquisition grid** is defined.

### Configuration

- 4 XZ planes (constant y)  
- 4 YZ planes (constant x)  
- Planes intersect key layout regions  

<div align="center">
  <img src="/img/posts/morie_soil/tomographic_layout.png" width="500">
</div>
*Figure 4 – Tomographic sampling layout showing FOWTs, anchors, and sectional planes used for soil reconstruction.*

### Engineering Significance

This step represents:

- Sparse CPT campaigns  
- Limited geotechnical sections  
- Realistic data acquisition constraints  

---

## 4. Tomographic Soil Sampling

The synthetic soil model is sampled along each tomographic plane.

### Outputs

- Depth-dependent φ distributions  
- Layer transitions along sections  
- Continuous property fields  

<div align="center">
  <img src="/img/posts/morie_soil/xz01_phi.png" width="500">
</div>
*Figure 5 – XZ sectional view showing variation of friction angle (φ) with depth.*

<div align="center">
  <img src="/img/posts/morie_soil/yz01_phi.png" width="500">
</div>
*Figure 6 – YZ sectional view showing reconstructed soil structure along orthogonal direction.*

### Engineering Significance

These sections form the **available measurement dataset**, capturing:

- Vertical layering  
- Lateral variability  
- Sparse spatial coverage  

---

## 5. Profile Reconstruction

Vertical soil profiles are reconstructed at anchor locations using **inverse-distance weighting (IDW)**.

### Method

- Combine contributions from all tomographic planes  
- Interpolate soil properties at target locations  
- Generate continuous depth profiles  

<div align="center">
  <img src="/img/posts/morie_soil/profile_comparison_phi.png" width="500">
</div>
*Figure 7 – Comparison between reconstructed and ground truth soil profiles at a representative anchor location.*

### Engineering Significance

This step converts sparse data into:

- **Continuous soil profiles**  
- **Anchor-specific geotechnical inputs**  
- A usable format for engineering models  

---

## 6. Boundary Detection & Validation

Layer boundaries are identified from reconstructed profiles.

### Method

- Threshold-based detection on φ  
- Identification of Z1 and Z2 interfaces  
- Comparison with ground truth  

<div align="center">
  <img src="/img/posts/morie_soil/boundary_comparison.png" width="500">
</div>
*Figure 8 – Comparison between detected and true layer boundaries (Z1 and Z2).*

### Engineering Significance

This step translates reconstructed profiles into:

- **Discrete engineering layers**  
- Inputs for capacity models  
- Quantified reconstruction accuracy  

---

## 7. Multi-Anchor Evaluation

The reconstruction workflow is applied across all anchor locations.

### Results

- 24 anchor points evaluated  
- Independent profile reconstruction per location  
- Error metrics computed for each anchor  

### Key Findings

- Mean Z1 error ≈ 0.30 m  
- Mean Z2 error ≈ 0.42 m  
- Maximum error < 1 m  

The anchor with best performance:

- **fowt6c**

### Engineering Significance

This enables:

- Selection of representative anchors  
- Confidence in reconstruction methodology  
- Validation across spatial variability  

---

## 8. Integrated Python Workflow

All steps are implemented in a modular pipeline:

    # Load project
    project = Project('modified_celticsea.yaml')

    # Extract layout domain
    domain = define_local_domain(project)

    # Crop spatial data
    bathy_crop, soil_crop = crop_grids(domain)

    # Generate truth soil model
    truth = build_truth_model(bathy_crop)

    # Define tomographic grid
    planes = generate_tomographic_grid(domain)

    # Sample soil along planes
    sections = sample_soil_planes(truth, planes)

    # Reconstruct profiles at anchors
    profiles = reconstruct_profiles(sections, anchors)

    # Detect boundaries
    boundaries = detect_layer_interfaces(profiles)

---

## Engineering Applications

- Anchor-level soil characterization  
- Early-stage geotechnical interpretation  
- Integration with anchor capacity models  
- Support for mooring and layout optimization  
- Validation of sparse-data reconstruction methods  

---

## Engineering Value

This workflow demonstrates how to:

> Convert **limited subsurface data into reliable engineering soil profiles**

Bridging:

- Spatial layout definition  
- Subsurface modeling  
- Anchor design requirements  

It enables:

- Reduced uncertainty in early-stage design  
- Scalable geotechnical workflows  
- Integration across offshore engineering disciplines  

---

## Next Steps

- Extension to multi-soil systems (clay, sand, rock)  
- Integration with real CPT datasets  
- Uncertainty quantification  
- Adaptive sampling strategies  
- Coupling with anchor capacity models  

---

## Morie Analytics Vision

At Morie Analytics, the goal is to build:

> **Integrated Seabed Intelligence for Floating Offshore Wind**

This soil reconstruction workflow enables:

- Digital subsurface modeling  
- Scalable anchor design inputs  
- Seamless integration across layout, mooring, and anchor systems  

---

## Related Work

- Layout Generation & Topology Optimization  
- Mooring System Analysis & Load Reconstruction  
- Shared Anchor Load Resolution & Capacity Verification  
- Dynamic Cable Design & Optimization  

---