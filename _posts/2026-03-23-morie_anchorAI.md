---
layout: post
title: Physics-Informed Anchor Design & Machine Learning Surrogate
image: "/img/posts/morie_anchorAI/morie_anchorAI.png"
tags: [Offshore Floating Wind, Anchors, Machine Learning, Suction Piles, Surrogate Models, Python]
---

# Celtic Sea Floating Offshore Wind – Physics-Informed Anchor Design & Machine Learning Surrogate

## Executive Summary

This study establishes the **predictive anchor design layer** of Morie Analytics by transforming physics-based anchor verification into a **lease-scale machine learning capability**.

Building on the coupled outputs of `morie_soil`, `morie_mooring` and `morie_anchor`, the workflow replaces the iterative suction pile sizing loop with a **physics-informed surrogate model** trained on synthetic engineering data generated from the integrated offshore design chain.

The surrogate architecture mirrors the underlying engineering workflow, preserving the causal separation between soil reconstruction, mooring-load transfer and anchor-capacity response through a two-stage predictive cascade.

The result is a **reproducible and scalable framework** that predicts anchor loads and dimensions in milliseconds, enabling full-domain evaluation and system-level decision support.

This module represents the transition from point-based offshore engineering verification to lease-scale predictive capability across the integrated floating wind workflow.

> Site intelligence → Layout generation → Soil reconstruction → Mooring physics → Anchor verification → **Anchor prediction** → Atlas visualization


## Project Scope

- Physics-based dataset generation using anchor capacity models  
- Load transfer and capacity solving across spatial samples  
- Feature engineering from soil and load fields  
- Training of a two-stage machine learning surrogate  
- Validation within the cropped local engineering domain  
- Lease-scale prediction and mapping  

This study converts **iterative anchor design into a scalable predictive framework**.


## Engineering Context

Anchor design in floating offshore wind is governed by:

- Layered soil resistance  
- Load transfer from mooring lines  
- Eccentric padeye loading  
- Combined VHM interaction constraints  

In `morie_anchor`, this is solved through an iterative process:

> Find (D, L) such that **UC ≈ 1**

This approach is robust, but computationally expensive. At lease scale, where thousands of anchor locations must be evaluated, the process becomes prohibitive.

This workflow introduces a new approach:

> Learn the physics → Replace the iteration → Scale the solution


## Inputs and Data Sources

This study builds directly on upstream Morie Analytics outputs:

### From `morie_soil`

- Layered soil profiles  
- Spatial variation of soil parameters  

### From `morie_mooring`

- Mudline load fields  
- Scenario-based load cases  

### From `morie_anchor`

- Load transfer from mudline-to-padeye 
- Capacity model  

### Additional Inputs

- Spatial sampling domain  
- Scenario definitions  
- Model configuration parameters  

All inputs are integrated into a **data-driven engineering framework**, this provides the **training data foundation for surrogate modeling**.


## System Flow

Spatial Sampling → Physics Solver → Dataset Generation → Model Training → Prediction

The architecture ensures **traceability from physics-based design to machine learning prediction**.

### Processing Workflow

1. Sample spatial domain (x, y, depth)  
2. Query soil properties  
3. Query mudline loads from mooring fields  
4. Transfer loads to padeye (physics-based)  
5. Solve anchor capacity (UC ≈ 1)  
6. Store optimal design (D, L, Mass)  
7. Train surrogate model  
8. Validate on spatial holdout  
9. Deploy for prediction  

This converts **physics-based simulations into predictive capability**.

## Design Basis

This workflow is intended as a site-conditioned surrogate framework suitable for preliminary lease-scale anchor assessment.

The current implementation is trained exclusively on:

- The cropped Celtic Sea sand domain from `morie_soil`
- Narrow water-depth variation (~88–94 m) from `morie_site` 
- Fixed suction-pile configuration assumptions from `morie_anchor`  
- Limited environmental loading scenarios from `morie_mooring`  

The surrogate is therefore intended for interpolation within the trained design space rather than for extrapolation to arbitrary offshore environments.

The workflow does not currently include:

- Multi-soil environments (clay/rock)  
- Installation effects  
- Cyclic degradation  
- Dynamic foundation response  
- Probabilistic uncertainty quantification  
- Multi-anchor interaction effects

## Surrogate Model Architecture

The surrogate model follows a **two-stage cascade**, mirroring the engineering process.

The present implementation uses a two-stage Random Forest surrogate, although the layered architecture shown conceptually is compatible with future deep-learning implementations.

### Stage A — Surrogate of Load Transfer Physics

Inputs:

- Depth  
- Soil features (`morie_soil`)
- Mudline loads (`morie_mooring`) 

Outputs:

- Padeye loads 

### Stage B — Surrogate of Anchor Capacity Design

Inputs:

- Soil features (`morie_soil`)
- Padeye loads

Outputs:

- Diameter (D)  
- Length (L)  
- Mass  

### Engineering Significance

This structure preserves:

- Physical causality  
- Separation of mechanisms  
- Interpretability of results  

Rather than treating anchor design as a black-box regression problem. This decomposition also improves interpretability and error traceability.

Stage A captures the transformation of mudline loads into embedded padeye demand, while Stage B learns the resulting capacity-constrained anchor sizing behavior.
The separation allows prediction errors to be associated with specific physical mechanisms rather than being absorbed into a single black-box model.


## Interpretation of Stage A and Stage B

The two-stage structure mirrors the original physics-based workflow.

In the `morie_anchor` reference formulation:

- Mudline loads are transferred to padeye level using **embedded line mechanics and soil interaction models**
- Anchor dimensions are obtained by solving a **capacity-constrained optimization problem (UC ≈ 1)**

In `morie_anchorAI`:

- **Stage A** acts as a surrogate of the **mudline-to-padeye load transfer process**, learning the combined effects of:
  - Soil friction and strength  
  - Embedded chain behavior  
  - Load redistribution along the seabed  

- **Stage B** acts as a surrogate of the **anchor capacity optimization loop**, mapping padeye loads to feasible anchor dimensions.

This decomposition preserves the physical structure of the problem while enabling scalable prediction.

> The model does not replace physics — it learns its outcomes and structure.

This enables the decomposition of complex engineering workflows into scalable predictive components, while preserving physical consistency.


## Dataset Generation

The dataset is generated entirely from **physics-based simulations**.

### Mooring Load Screening for Stage A

Before surrogate training, a lease-scale mooring screening campaign is performed to construct the mudline load fields used by Stage A.

A hexagonal grid of probe FOWTs is distributed across the cropped Celtic Sea lease domain, and each floater is evaluated through directional watch-circle sweeps using 
the `morie_mooring` workflow. The resulting anchor-level mudline loads (`Tm`, `θm`) are stored as spatial load planes and later queried internally by the surrogate during inference.

The selected configuration uses:

- Hex spacing: 800 m  
- Inner buffer: 300 m  
- 52 probe FOWTs  
- 156 anchors (143 inside cropped-domain)

This configuration provides a balance between:
- Spatial coverage
- Load-field interpolation quality
- Computational cost

<div align="center">
  <img src="/img/posts/morie_anchorAI/hexgrid_layout_preview_s800_b300.png"
       alt="Hexagonal probe layout used to construct mudline load planes for Stage A mooring screening"
       width="650">
</div>

*Figure 1 – Hexagonal probe-FOWT layout used to generate lease-scale mudline load fields for Stage A surrogate training.*

### Methodology

- Spatial sampling across lease domain  
- Soil reconstruction via interpolation  
- Load extraction from mooring fields  
- Capacity solving via iterative physics model  

Each sample produces:

- Input features (soil + loads)  
- Target outputs (D, L, Mass at UC ≈ 1)  

> The surrogate replaces the iterative capacity loop with a learned mapping from spatial inputs to anchor design outputs


### Engineering Significance

This ensures:

- Physical consistency of training data  
- Full control over design space  
- Reproducibility of results  


## Model Performance

The trained model demonstrates strong predictive capability within the cropped local engineering domain established in `morie_soil`.

### Key Results

- Accurate prediction of **D and L** within the cropped local domain 
- Robust load transformation in Stage A  
- No physically reliable prediction capability outside the trained design domain 

### Engineering Interpretation

- Geometry predictions remain stable  
- Soil-driven variability dominates results  
- Extrapolation limits reflect physical domain boundaries  

Multiple (D, L) combinations can produce mechanically equivalent solutions along the UC ≈ 1 solution while preserving somehow similar overall anchor mass.

This explains why global mass predictions remain more robust than individual geometric variables such as diameter, 
the model captures **underlying engineering behavior**, not only statistical correlations.


## Lease-Scale Prediction

The surrogate enables rapid evaluation across the conditioned lease-scale domain.

<div align="center">
  <img src="/img/posts/morie_anchorAI/predict_heatmap.png"
       alt="Lease-scale prediction of suction pile mass showing spatial variability driven by subsurface conditions"
       width="600">
</div>
*Figure 2 – Lease-scale prediction of anchor mass using the surrogate model.*

### Example Output

- 40 × 40 grid evaluation (1,600 points)  
- Mass range variation: ~25 t (~17% of mean)

This level of variation has direct implications for:

- Anchor standardization strategies  
- Installation planning and logistics  
- Cost distribution across the lease  

It highlights that even within a seemingly uniform sand domain, **subsurface variability alone can drive significant differences in anchor sizing**.  

### Spatial Drivers of Anchor Mass

Within the constrained Celtic Sea cropped-domain configuration used in this study, spatial variability in suction-pile mass is dominated by the reconstructed subsurface geometry, 
particularly the Z1 and Z2 layer boundaries.

In the current sand-only domain:

- Soil layer geometry accounts for ~95% of the spatial variability in predicted pile mass  
- Mudline load variation contributes secondarily  
- Raw spatial coordinates become largely irrelevant once the upstream soil and load fields are resolved  

This behavior is specific to the present site-conditioned surrogate and should not be interpreted as a universal result for offshore anchor design.

The result instead highlights that, within the studied domain, variations in bearing stratigraphy exert a stronger influence on anchor sizing than the relatively limited variation in load magnitude.

### Engineering Implication

This result confirms that, within the studied domain:

- Anchor design is primarily controlled by **subsurface structure**, not by load magnitude  
- Layout position only matters through its interaction with soil variability  

This shifts the design focus from:

→ Load-driven sizing  

to  

→ Soil-driven optimization  

This has direct consequences for early-stage design strategies, particularly in:

- Anchor clustering  
- Layout standardization  
- Cost-driven decision making

### Engineering Interpretation

- Soil stratigraphy controls design  
- Load variation plays a secondary role  
- Spatial location is only relevant through underlying fields  

This validates core geotechnical principles at scale.


## Outputs Generated

- Training dataset  
- Trained machine learning models  
- Validation metrics and plots  
- Lease-scale prediction grids  
- Anchor design outputs (D, L, Mass)  

These outputs are directly usable in downstream decision frameworks.


## Engineering Applications

The outputs support:

- Lease-scale anchor sizing  
- Sensitivity analysis across scenarios  
- Rapid evaluation of layout alternatives  
- Integration into optimization workflows  
- Cost and feasibility mapping  

This enables:

**Anchor Design → Predictive Mapping → System-Level Decisions**


## Relationship to Other Morie Study Cases

This study is the **predictive extension of the anchor workflow**.

### Receives from

- **morie_site** → spatial context  
- **morie_layout** → system geometry  
- **morie_soil** → subsurface characterization  
- **morie_mooring** → load fields  
- **morie_anchor** → physics-based design logic  

### Feeds into

- **morie_atlas** → lease-scale visualization and decision support  

It provides the **transition from physics-based design to scalable prediction**.


## Why It Matters Commercially

- Enables lease-scale anchor assessment in real time  
- Reduces computational cost of early-stage design  
- Supports rapid scenario evaluation  
- Improves integration across engineering disciplines  
- Bridges physics-based models with data-driven workflows  

This is where:

- Engineering becomes scalable  
- Design becomes interactive  
- Decisions become data-driven  


## Aspects to Improve

- Extension to multi-soil environments (clay, rock)  
- Inclusion of installation and cyclic effects  
- Uncertainty quantification  
- Expansion of training domain  
- Integration with optimization frameworks  

These extensions would move the workflow toward **fully predictive offshore design systems**.


## Design Philosophy

This study reflects the Morie Analytics approach:

- **Physics-informed**: labels originate from the validated `morie_anchor` capacity formulations.
- **Mechanism-preserving**: the two-stage cascade mirrors the underlying engineering workflow.
- **Reproducible**: all datasets and models are generated from deterministic configuration-driven pipelines.
- **Scalable**: millisecond-level prediction enables lease-scale evaluation and interactive engineering workflows.
- **Site-conditioned**: the surrogate is explicitly tied to reconstructed soil and load fields from the Celtic Sea domain.