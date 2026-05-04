---
layout: post
title: Physics-Informed Anchor Design & Machine Learning Surrogate
image: "/img/posts/morie_anchorAI/morie_anchorAI2.png"
tags: [Offshore Floating Wind, Anchors, Machine Learning, Suction Piles, Surrogate Models, Python]
---

# Celtic Sea Floating Offshore Wind – Physics-Informed Anchor Design & Machine Learning Surrogate

## Executive Summary

This study establishes the **predictive anchor design layer** of Morie Analytics by transforming physics-based anchor verification into a **lease-scale machine learning capability**.

Building on `morie_anchor`, the workflow replaces the iterative suction pile sizing loop with a **physics-informed surrogate model**, trained on synthetic data generated from validated capacity formulations.

The surrogate is structured to mirror the underlying physics, separating load transfer and capacity mechanisms into two learnable stages.

The result is a **reproducible and scalable framework** that predicts anchor loads and dimensions in milliseconds, enabling full-domain evaluation and system-level decision support.

This module represents the transition from **point-based engineering verification to continuous predictive capability**.

> Site intelligence → Layout generation → Soil reconstruction → Mooring physics → Anchor verification → **AnchorAI prediction** → Atlas visualization


## Project Scope

- Physics-based dataset generation using anchor capacity models  
- Load transfer and capacity solving across spatial samples  
- Feature engineering from soil and load fields  
- Training of a two-stage machine learning surrogate  
- Validation under spatial generalization conditions  
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

This approach is robust, but computationally expensive.

At lease scale, where thousands of anchor locations must be evaluated, the process becomes prohibitive.

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

- Load transfer (`getTransferLoad`)  
- Capacity model (`getCapacitySuction`)  

### Additional Inputs

- Spatial sampling domain  
- Scenario definitions  
- Model configuration parameters  

All inputs are integrated into a **data-driven engineering framework**.

This provides the **training data foundation for surrogate modeling**.


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


## Surrogate Model Architecture

The surrogate model follows a **two-stage cascade**, mirroring the engineering process.

### Stage A — Surrogate of Load Transfer Physics

Inputs:

- Depth  
- Soil features  
- Mudline loads  

Outputs:

- Padeye loads (`Ha, Va, Ta, thetaa`)

---

### Stage B — Surrogate of Anchor Capacity Design

Inputs:

- Depth  
- Soil features  
- Padeye loads  

Outputs:

- Diameter (D)  
- Length (L)  
- Mass  

---

### Engineering Significance

This structure preserves:

- Physical causality  
- Separation of mechanisms  
- Interpretability of results  

Rather than treating anchor design as a black-box regression problem.


## Interpretation of Stage A and Stage B

The two-stage structure mirrors the original physics-based workflow.

In the reference formulation (`morie_anchor`):

- Mudline loads are transferred to padeye level using **embedded line mechanics and soil interaction models**
- Anchor dimensions are obtained by solving a **capacity-constrained optimization problem (UC ≈ 1)**

In Morie AnchorAI:

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

### Methodology

- Spatial sampling across lease domain  
- Soil reconstruction via interpolation  
- Load extraction from mooring fields  
- Capacity solving via iterative physics model  

Each sample produces:

- Input features (soil + loads)  
- Target outputs (D, L, Mass at UC ≈ 1)  

As described in the repository:

> The surrogate replaces the iterative capacity loop with a learned mapping from spatial inputs to anchor design outputs


### Engineering Significance

This ensures:

- Physical consistency of training data  
- Full control over design space  
- Reproducibility of results  


## Model Performance

The trained model demonstrates strong predictive capability under spatial generalization.

### Key Results

- Accurate prediction of **D and L** across unseen regions  
- Robust load transformation in Stage A  
- Reduced performance for mass extrapolation outside training domain  

### Engineering Interpretation

- Geometry predictions remain stable  
- Soil-driven variability dominates results  
- Extrapolation limits reflect physical domain boundaries  

This confirms that the model captures **underlying engineering behavior**, not only statistical correlations.


## Lease-Scale Prediction

The surrogate enables evaluation across the full lease area.

<div align="center">
  <img src="/img/posts/morie_anchorAI/heatmap_mass.png"
       alt="Lease-scale prediction of suction pile mass showing spatial variability driven by subsurface conditions"
       width="600">
</div>
*Figure 1 – Lease-scale prediction of anchor mass using the surrogate model.*

### Example Output

- 40 × 40 grid evaluation (1,600 points)  
- Mass range variation: ~25 t (~17% of mean)

This level of variation has direct implications for:

- Anchor standardization strategies  
- Installation planning and logistics  
- Cost distribution across the lease  

It highlights that even within a seemingly uniform sand domain, **subsurface variability alone can drive significant differences in anchor sizing**.  

### Key Insight

> Soil layer geometry (Z1, Z2) drives ~95% of anchor mass variability

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

- Physics-informed  
- Modular  
- Traceable  
- Engineering-focused  
- Scalable  