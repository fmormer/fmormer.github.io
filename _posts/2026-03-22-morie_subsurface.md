---
layout: post
title: AI-Assisted Subsurface Intelligence & Sparse-Data Reconstruction
image: "/img/posts/morie_subsurface/morie_subsurface.png"
tags: [Offshore Floating Wind, Geotechnical Engineering, Artificial Intelligence, Subsurface Modeling, CPT, SchemaGAN, GeoSyn, Python]
---

# Celtic Sea Floating Offshore Wind – AI-Assisted Subsurface Intelligence & Sparse-Data Reconstruction


## Executive Summary

This study establishes the **AI-assisted subsurface intelligence layer** of Morie Analytics by extending the deterministic reconstruction workflow developed in `morie_soil` toward a generative and reconstruction-driven geotechnical framework.

The workflow combines:

- Synthetic geological generation  
- Sparse CPT-style sampling  
- AI-based subsurface reconstruction  
- Engineering-aware soil interpretation  
- Reconstruction-quality validation  

within a unified offshore engineering pipeline.

Building on the same cropped Celtic Sea domain, floating wind layout and anchor-sharing configuration used across the Morie ecosystem, the workflow introduces a new approach where AI supports the reconstruction of offshore subsurface behavior from limited investigation data.

Unlike purely statistical interpolation approaches, the methodology combines:

- **GeoSyn** → synthetic truth generation  
- **SchemaGAN** → sparse-data reconstruction  
- **Ic-based engineering mapping** → derivation of engineering soil parameters  
- **Validation workflows** → quantitative reconstruction assessment  

The result is a reproducible framework capable of transforming sparse offshore geotechnical information into engineering-ready subsurface intelligence suitable for downstream anchor and mooring workflows.

This study represents the transition from:

> Deterministic soil interpolation  

toward:

> Engineering-aware AI reconstruction of offshore subsurface systems.

> Site intelligence → Layout generation → Soil reconstruction → **AI subsurface intelligence** → Mooring physics → Anchor verification → Anchor prediction

<div align="center">
  <img src="/img/posts/morie_subsurface/morie_subsurface.png"
       alt="Integrated SchemaGAN-based offshore subsurface reconstruction workflow for floating offshore wind"
       width="1000">
</div>

*Figure 1 – Integrated AI-assisted subsurface intelligence workflow linking `morie_site`, `morie_layout` and `morie_soil` into engineering-ready offshore reconstruction fields using SchemaGAN.*


## Project Scope

- Synthetic geological truth generation  
- Sparse CPT-style sampling  
- AI-assisted subsurface reconstruction  
- Ic-based engineering parameter derivation  
- Reconstruction validation against held-out truth  
- Engineering-aware interpretation of reconstructed fields  
- Integration with downstream anchor workflows  

This study converts:

**Sparse offshore geotechnical observations → engineering-ready subsurface intelligence**.


## Engineering Context

Early-stage floating offshore wind developments face a fundamental challenge:

> How can reliable geotechnical understanding be constructed from sparse offshore investigation data?

In real projects:

- CPT campaigns are expensive  
- Investigation density is limited  
- Spatial variability characterization needs to adapt to floating wind needs  
- Engineering decisions must often be made before full site characterization is available  

In `morie_soil`, this problem was approached through deterministic tomographic reconstruction.

This study extends the concept further:

> Generate plausible offshore geology → sparse sampling → reconstruction with AI → validation of engineering implications

The workflow does not attempt to blindly predict soil properties from coordinates. Instead, it reconstructs offshore 
subsurface behavior under engineering constraints while preserving geological continuity and spatial structure.


## Inputs and Data Sources

This study builds directly on upstream Morie Analytics outputs.

### From `morie_site`

- Bathymetry grids  
- Soil classification context  
- Cropped lease-area geometry  

### From `morie_layout`

- Floating wind layout  
- Shared-anchor configurations  
- Anchor coordinates  

### From `morie_soil`

- Three-layer Celtic Sea sand profile  
- Cropped local domain  
- Deterministic reconstruction logic  
- Engineering calibration endpoints  

### Additional Inputs

- GeoSyn synthetic geology framework  
- Sparse CPT-style sampling definitions  
- SchemaGAN reconstruction architecture  
- Ic-to-engineering parameter mappings  

All inputs remain aligned within the same cropped Celtic Sea engineering domain used throughout the Morie ecosystem.

This provides continuity across:

- Layout definition  
- Soil characterization  
- Mooring analysis  
- Anchor engineering  
- AI-assisted reconstruction workflows


## System Flow

GeoSyn Truth Generation → Sparse CPT Sampling → SchemaGAN Reconstruction → Engineering Mapping → Validation

The architecture preserves the following aspects throughout the reconstruction process:

- Geological continuity  
- Engineering traceability  
- Reproducibility of results  

### Processing Workflow

1. Load cropped Celtic Sea engineering domain  
2. Generate synthetic geological truth fields  
3. Sample sparse CPT-style observations  
4. Build sparse reconstruction datasets  
5. Train SchemaGAN reconstruction model  
6. Reconstruct subsurface fields  
7. Derive engineering soil parameters  
8. Validate reconstruction against truth  
9. Export engineering-ready outputs  

This converts:

**Sparse offshore investigation data → reconstructed engineering fields**.


## Local Engineering Domain

The workflow inherits the same cropped Celtic Sea local engineering domain used in `morie_soil`.

This ensures continuity across:

- Bathymetry  
- Soil classification  
- Floating wind layout  
- Anchor positions  
- Downstream engineering workflows  

The selected domain preserves:

- Realistic offshore scale  
- Representative anchor spacing  
- Layered soil behavior  
- Spatial variability consistent within Morie's portfolio


## Celtic Sea Sand-State Model

The study inherits the same three-layer sand profile used in `morie_soil`.

### Base Soil Structure Implementation

The current implementation is intentionally restricted to sand-dominated offshore environments and should not be interpreted as a complete representation of Celtic Sea geology.

The objective is to establish and validate the reconstruction workflow within a controlled geotechnical setting before extending the methodology toward clay, mixed-facies and rock environments.

| Layer | Description       |
|------ |------------------ |
|   1   | Loose sand        |
|   2   | Medium sand       |
|   3   | Medium-dense sand |

### Latent Soil-State Representation

The workflow introduces a key latent variable:

> **Ic — Robertson's Soil Behaviour Type Index (Robertson, 2010)**

Ic is a dimensionless CPT-derived parameter that provides a compact representation of soil behavior and can be calculated directly from cone penetration test measurements.

Following the SchemaGAN methodology, Ic is reconstructed as the primary subsurface variable because it preserves behavioral information while remaining suitable for image-based geological reconstruction.

Rather than independently reconstructing engineering parameters such as friction angle or relative density, the workflow first reconstructs the Ic field and subsequently derives engineering 
parameters through consistent interpretation relationships.

### Engineering Parameters Derived

The reconstructed Ic field is translated into engineering-ready soil parameters including:

- Relative density (Dr)
- Friction angle (φ)
- Submerged unit weight (γ)

### Engineering Significance

This approach preserves consistency while avoiding the need to independently reconstruct multiple engineering parameters between:

- Geological structure
- Soil behavior
- Engineering interpretation

The result is a reconstruction workflow that remains geotechnically interpretable while producing outputs directly usable within downstream offshore engineering analyses.  


## GeoSyn Synthetic Truth Generation

The workflow begins by generating synthetic offshore geological realizations using an adapted GeoSyn framework.

<div align="center">
  <img src="/img/posts/morie_subsurface/01_geosyn_truth.png"
       alt="Synthetic offshore geological realization generated using GeoSyn over the cropped Celtic Sea floating wind domain"
       width="650">
</div>

*Figure 2 – Example synthetic offshore geological realization generated using the GeoSyn framework.*

The original GeoSyn methodology is adapted from generic geotechnical environments toward:

- Offshore sand-dominated geology  
- Marine depositional continuity  
- Anisotropic offshore variability  
- Celtic Sea layered behavior  

### Engineering Significance

The synthetic truth model provides:

- Controlled geological references  
- Known subsurface states  
- Reproducible validation targets  

This enables quantitative assessment of reconstruction quality before application to real offshore investigation datasets.


## Sparse CPT Sampling Framework

The synthetic truth fields are sparsely sampled using CPT-style vertical observations.

<div align="center">
  <img src="/img/posts/morie_subsurface/02_sparse_cpt_sampling.png"
       alt="Sparse CPT-style sampling layout showing limited offshore investigation points within the reconstructed subsurface domain"
       width="650">
</div>

*Figure 3 – Sparse CPT-style sampling used to emulate realistic offshore site investigation density.*

The sampling strategy intentionally reproduces realistic offshore constraints:

- Limited investigation density from initial studies 
- Large spatial gaps  
- Sparse vertical observations resembling initial investigation 
- Incomplete subsurface coverage  

Each realization is sampled independently to produce:

- Sparse Ic observations  
- Observation masks  
- Reconstruction input datasets  

### Engineering Significance

This step reproduces one of the central challenges of offshore geotechnics:

> Reconstructing reliable subsurface behavior from limited investigation campaigns.


## SchemaGAN Reconstruction

The reconstruction architecture follows:

- U-Net generator  
- PatchGAN discriminator  
- Sparse-to-dense conditional reconstruction  

### What is a GAN?

A Generative Adversarial Network (GAN) is an AI architecture composed of two neural networks that learn together through competition.

- The generator attempts to reconstruct realistic subsurface fields from sparse CPT observations.
- The discriminator attempts to distinguish between reconstructed fields and known geological truth.

Through this adversarial training process, the generator progressively learns to produce reconstructions that preserve geological structure, layering continuity and spatial variability.

Unlike conventional interpolation methods, which estimate values directly between observations, GAN-based reconstruction learns the underlying patterns present within geological systems 
and uses them to infer geologically consistent subsurface behavior between locations.

Rather than performing simple interpolation, the model learns:

- Geological continuity  
- Spatial transitions  
- Offshore layering behavior  
- Latent soil-state distributions  

### Engineering Significance

Within floating offshore wind engineering needs the workflow introduces:

- AI-assisted geological reconstruction  
- Continuity-aware subsurface inference  
- Engineering-consistent spatial reconstruction  


## Ic-to-Engineering Mapping

Once reconstructed, the Ic fields are translated into engineering-ready soil parameters.

<div align="center">
  <img src="/img/posts/morie_subsurface/04_engineering_mapping.png"
       alt="Engineering-aware translation of reconstructed Ic fields into relative density friction angle unit weight and CPT resistance"
       width="650">
</div>

*Figure 4 – Engineering mapping from reconstructed Ic fields into engineering soil parameters.*

The reconstruction pipeline derives:

- Relative density (Dr)
- Friction angle (φ)
- Effective submerged unit weight (γ')

This translation preserves engineering consistency between:

- Geology  
- Soil behavior  
- Engineering interpretation  

Rather than treating them as independent regression outputs.

### Engineering Significance

This enables reconstructed AI fields to become directly usable by:

- Anchor sizing workflows  
- Soil-structure interaction models  
- Mooring analysis  
- Geotechnical screening studies  


## Validation & Reconstruction Accuracy

A key aspect of the workflow is that reconstruction quality is validated against known synthetic truth.

<div align="center">
  <img src="/img/posts/morie_subsurface/05_validation_comparison.png"
       alt="Comparison between reconstructed and ground-truth offshore subsurface fields showing reconstruction accuracy and spatial continuity"
       width="650">
</div>

*Figure 5 – Validation of reconstructed offshore subsurface fields against synthetic truth.*

### Validation Metrics

The workflow evaluates:

- Ic reconstruction accuracy  
- Relative density reconstruction  
- Friction angle reconstruction  
- Unit weight reconstruction  
- Boundary recovery performance  

### Example Results

| Metric    | Mean Value  |
|---------- |------------ |
| MAE (Ic)  | ~0.03       |
| RMSE (Ic) | ~0.04       |
| RMSE (Dr) | ~5%         |
| RMSE (φ)  | ~0.4°       |
| RMSE (γ') | ~0.13 kN/m³ |

### Engineering Interpretation

The results demonstrate that:

- Sparse-data reconstruction preserves engineering trends  
- Reconstruction quality remains stable across held-out realizations  
- Engineering parameter derivation remains physically coherent  

The workflow therefore reconstructs not only geological structure, but also the engineering behavior required for downstream offshore design workflows.

While Figure 5 evaluates reconstruction quality in the latent Ic space, offshore engineering decisions ultimately depend on derived parameters such as friction angle and relative density. 
Figure 6 therefore evaluates whether the reconstructed Ic fields preserve the engineering behavior required for anchor and mooring design workflows.

<div align="center">
  <img src="/img/posts/morie_subsurface/06_parameter_comparison.png"
       alt="Engineering parameter comparison between truth and reconstructed fields for friction angle and relative density"
       width="850">
</div>

*Figure 6 – Engineering-aware comparison between truth and reconstructed fields for friction angle and relative density including associated reconstruction errors.*

While individual realizations help illustrate reconstruction behavior locally, offshore engineering workflows require validation across many geological scenarios.
To evaluate robustness, the reconstruction metrics are aggregated across both training and validation realizations.
The statistical distributions below demonstrate that reconstruction performance remains stable across unseen geological configurations while preserving engineering-consistent parameter behavior.

<div align="center">
  <img src="/img/posts/morie_subsurface/07_validation_boxplot.png"
       alt="Distribution of reconstruction errors across training and validation realizations"
       width="850">
</div>

*Figure 7 – Distribution of reconstruction errors across training and validation realizations for Ic, friction angle and relative density predictions.*

The relatively narrow spread between training and validation distributions indicates limited overfitting within the GeoSyn-generated dataset distribution used in this study.
These results should therefore be interpreted as reconstruction performance bounds within the synthetic geological domain rather than estimates of real-world reconstruction accuracy.

Validation against real offshore CPT datasets remains an important next step for future development.

## Relationship with `morie_sample`

The adaptive CPT investigation-planning layer is intentionally separated into the following sibling study case:

> `morie_sample`

This separation preserves architectural clarity across the Morie ecosystem.

### `morie_subsurface`

Focuses on:

- Reconstruction quality  
- Geological realism  
- Engineering-aware AI fields  

### `morie_sample`

Focuses on:

- Adaptive CPT placement  
- Reinforcement learning  
- Investigation optimization  
- Uncertainty reduction strategies  

Together, the two study cases establish a unified offshore subsurface intelligence framework.


## Outputs Generated

The workflow produces:

- Synthetic geological realizations  
- Sparse CPT datasets  
- Reconstructed subsurface fields  
- Engineering parameter maps  
- Validation metrics and reports  
- Reconstruction comparison figures  
- Engineering-ready soil fields  

These outputs are directly usable in downstream offshore engineering workflows.


## Engineering Applications

The outputs support:

- Early-stage geotechnical assessment  
- Sparse-data interpretation workflows  
- Anchor engineering studies  
- Offshore uncertainty reduction  
- Soil-informed mooring analysis  
- Engineering-aware AI workflows  

This enables:

**Sparse Offshore Data → AI Reconstruction → Engineering Decisions**


## Relationship to Other Morie Study Cases

This study establishes the AI-driven extension of the Morie subsurface workflow.

### Receives from

- **morie_site** → environmental context  
- **morie_layout** → floating wind geometry  
- **morie_soil** → deterministic soil reconstruction framework  

### Feeds into

- **morie_sample** → adaptive CPT optimization  
- **morie_anchor** → anchor engineering  
- **morie_atlas** → predictive anchor workflows and lease-scale visualization

It provides the transition from:

> Deterministic subsurface interpretation  

toward:

> Engineering-aware AI reconstruction and offshore intelligence.


## Why It Matters Commercially?

- Reduces uncertainty during early-stage offshore development  
- Supports engineering decisions under sparse investigation conditions  
- Bridges AI workflows with engineering interpretation  
- Enables scalable geotechnical reconstruction workflows  
- Improves integration between geology and offshore design  

This is where:

- Geotechnics becomes data-driven  
- Reconstruction becomes engineering-aware  
- Offshore AI becomes physically interpretable  


## Aspects to Improve

- Validation against real offshore CPT datasets and site investigation campaigns
- Benchmarking against conventional interpolation approaches such as ordinary kriging and inverse-distance weighting
- Extension toward clay, mixed-facies and rock environments  
- Native 3D reconstruction workflows  
- Reconstruction uncertainty quantification and confidence mapping  
- Cloud-scale reconstruction training  
- Integration with adaptive CPT optimization through `morie_sample`  

These extensions would move the workflow toward:

> Fully integrated offshore subsurface intelligence systems.


## Design Philosophy

This study reflects the Morie Analytics approach:

- **Physics-informed**: reconstruction targets are derived from geotechnical behavior and engineering-consistent soil-state representations.
- **Geology-aware**: the workflow preserves offshore layering continuity and spatial depositional structure rather than performing generic interpolation.
- **Mechanism-preserving**: the reconstruction pipeline mirrors the sequence from sparse investigation data to engineering interpretation.
- **Reproducible**: synthetic truth generation, sparse sampling and reconstruction workflows are fully configuration-driven.
- **Engineering-ready**: reconstructed Ic fields are directly translated into parameters usable in mooring and anchor workflows.
- **Site-conditioned**: the framework is explicitly tied to the reconstructed Celtic Sea offshore domain and associated floating wind context.


## Research Foundations

The reconstruction methodology presented in this study builds upon concepts introduced in the SchemaGAN framework developed by:

- Fabian A. Campos-Montero
- Bruno Zuada Coelho
- Evangelia Smyrniou
- Riccardo Taormina
- Philip J. Vardon

particularly regarding sparse-data subsurface reconstruction using conditional generative adversarial networks for geotechnical applications.

Within Morie Analytics, the methodology is adapted toward:

- Offshore floating wind environments
- Celtic Sea sand-state reconstruction
- Engineering-aware Ic-based parameter mapping
- Downstream anchor and mooring workflows