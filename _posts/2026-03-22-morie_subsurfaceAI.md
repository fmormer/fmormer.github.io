---
layout: post
title: AI-Assisted Subsurface Intelligence & Sparse-Data Reconstruction
image: "/img/posts/morie_subsurfaceAI/morie_subsurfaceAI.png"
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
- **IC-based engineering mapping** → derivation of engineering soil parameters  
- **Validation workflows** → quantitative reconstruction assessment  

The result is a reproducible framework capable of transforming sparse offshore geotechnical information into engineering-ready subsurface intelligence suitable for downstream anchor and mooring workflows.

This study represents the transition from:

> deterministic soil interpolation  

toward:

> engineering-aware AI reconstruction of offshore subsurface systems.

> Site intelligence → Layout generation → Soil reconstruction → **AI subsurface intelligence** → Mooring physics → Anchor verification → Anchor prediction


## Project Scope

- Synthetic geological truth generation  
- Sparse CPT-style sampling  
- AI-assisted subsurface reconstruction  
- IC-based engineering parameter derivation  
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
- Spatial variability is poorly resolved  
- Engineering decisions must often be made before full site characterization is available  

In `morie_soil`, this problem was approached through deterministic tomographic reconstruction.

This study extends the concept further:

> Generate plausible offshore geology → sparsely sample it → reconstruct it with AI → validate the engineering implications

The workflow does not attempt to blindly predict soil properties from coordinates.

Instead, it reconstructs offshore subsurface behavior under engineering constraints while preserving geological continuity and spatial structure.


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
- IC-to-engineering parameter mappings  

All inputs remain aligned within the same cropped Celtic Sea engineering domain used throughout the Morie ecosystem.

This provides continuity across:

- layout definition  
- soil characterization  
- mooring analysis  
- anchor engineering  
- AI-assisted reconstruction workflows


## System Flow

GeoSyn Truth Generation → Sparse CPT Sampling → SchemaGAN Reconstruction → Engineering Mapping → Validation

The architecture preserves:

- geological continuity  
- engineering traceability  
- reproducibility of results  

throughout the reconstruction process.

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

- bathymetry  
- soil classification  
- floating wind layout  
- anchor positions  
- downstream engineering workflows  

The selected domain preserves:

- realistic offshore scale  
- representative anchor spacing  
- layered sand behavior  
- spatial variability consistent with the Morie portfolio


## Celtic Sea Sand-State Model

The study inherits the same three-layer sand profile used in `morie_soil`.

### Base Soil Structure

| Layer | Description |
|---|---|
| Layer 1 | Loose sand |
| Layer 2 | Medium sand |
| Layer 3 | Medium-dense sand |

The workflow introduces a key latent variable:

> **IC — behavioral soil-state index**

Rather than directly reconstructing friction angle or relative density independently, the workflow reconstructs IC as the central behavioral representation of the subsurface.

Engineering parameters are then derived consistently from the reconstructed IC field.

### Engineering Parameters Derived

- Relative density (Dr)
- Friction angle (φ)
- Submerged unit weight (γ)
- CPT resistance (qc)

### Engineering Significance

This preserves:

- geological consistency  
- behavioral continuity  
- physically coherent parameter relationships  

across the reconstructed domain.


## GeoSyn Synthetic Truth Generation

The workflow begins by generating synthetic offshore geological realizations using an adapted GeoSyn framework.

<div align="center">
  <img src="/img/posts/morie_subsurfaceAI/01_geosyn_truth.png"
       alt="Synthetic offshore geological realization generated using GeoSyn over the cropped Celtic Sea floating wind domain"
       width="650">
</div>

*Figure 1 – Example synthetic offshore geological realization generated using the GeoSyn framework.*

The original GeoSyn methodology is adapted from generic geotechnical environments toward:

- offshore sand-dominated geology  
- marine depositional continuity  
- anisotropic offshore variability  
- Celtic Sea layered behavior  

### Engineering Significance

The synthetic truth model provides:

- controlled geological references  
- known subsurface states  
- reproducible validation targets  

This enables quantitative assessment of reconstruction quality before application to real offshore investigation datasets.


## Sparse CPT Sampling Framework

The synthetic truth fields are sparsely sampled using CPT-style vertical observations.

<div align="center">
  <img src="/img/posts/morie_subsurfaceAI/02_sparse_cpt_sampling.png"
       alt="Sparse CPT-style sampling layout showing limited offshore investigation points within the reconstructed subsurface domain"
       width="650">
</div>

*Figure 2 – Sparse CPT-style sampling used to emulate realistic offshore site investigation density.*

The sampling strategy intentionally reproduces realistic offshore constraints:

- limited investigation density  
- large spatial gaps  
- sparse vertical observations  
- incomplete subsurface coverage  

Each realization is sampled independently to produce:

- sparse IC observations  
- observation masks  
- reconstruction input datasets  

### Engineering Significance

This step reproduces one of the central challenges of offshore geotechnics:

> reconstructing reliable subsurface behavior from limited investigation campaigns.


## SchemaGAN Reconstruction

The sparse observations are then reconstructed using a 2D SchemaGAN architecture based on conditional generative adversarial networks.

<div align="center">
  <img src="/img/posts/morie_subsurfaceAI/03_schemagan_reconstruction.png"
       alt="SchemaGAN reconstruction showing sparse CPT observations transformed into continuous reconstructed offshore subsurface fields"
       width="650">
</div>

*Figure 3 – SchemaGAN reconstruction of offshore subsurface behavior from sparse CPT-style observations.*

The reconstruction architecture follows:

- U-Net generator  
- PatchGAN discriminator  
- sparse-to-dense conditional reconstruction  

The model learns:

- geological continuity  
- spatial transitions  
- offshore layering behavior  
- latent soil-state distributions  

rather than performing simple interpolation.

### Engineering Significance

The workflow introduces:

- AI-assisted geological reconstruction  
- continuity-aware subsurface inference  
- engineering-consistent spatial reconstruction  

within floating offshore wind engineering.


## IC-to-Engineering Mapping

Once reconstructed, the IC fields are translated into engineering-ready soil parameters.

<div align="center">
  <img src="/img/posts/morie_subsurfaceAI/04_engineering_mapping.png"
       alt="Engineering-aware translation of reconstructed IC fields into relative density friction angle unit weight and CPT resistance"
       width="650">
</div>

*Figure 4 – Engineering mapping from reconstructed IC fields into engineering soil parameters.*

The reconstruction pipeline derives:

- Relative density (Dr)
- Friction angle (φ)
- Submerged unit weight (γ)
- Effective stress (σ'v)
- CPT resistance (qc)

This translation preserves consistency between:

- geology  
- soil behavior  
- engineering interpretation  

rather than treating engineering properties as independent regression outputs.

### Engineering Significance

This enables reconstructed AI fields to become directly usable by:

- anchor sizing workflows  
- soil-structure interaction models  
- mooring analysis  
- geotechnical screening studies  


## Validation & Reconstruction Accuracy

A key aspect of the workflow is that reconstruction quality is validated against known synthetic truth.

<div align="center">
  <img src="/img/posts/morie_subsurfaceAI/05_validation_comparison.png"
       alt="Comparison between reconstructed and ground-truth offshore subsurface fields showing reconstruction accuracy and spatial continuity"
       width="650">
</div>

*Figure 5 – Validation of reconstructed offshore subsurface fields against synthetic truth.*

### Validation Metrics

The workflow evaluates:

- IC reconstruction accuracy  
- Relative density reconstruction  
- Friction angle reconstruction  
- Unit weight reconstruction  
- Boundary recovery performance  

### Example Results

| Metric | Mean Value |
|---|---|
| MAE(IC) | ~0.03 |
| RMSE(IC) | ~0.04 |
| RMSE(Dr) | ~5% |
| RMSE(φ) | ~0.4° |
| RMSE(γ') | ~0.13 kN/m³ |

### Engineering Interpretation

The results demonstrate that:

- sparse-data reconstruction preserves engineering trends  
- reconstruction quality remains stable across held-out realizations  
- engineering parameter derivation remains physically coherent  

The workflow therefore reconstructs not only geology, but also engineering behavior.


## Relationship with `morie_CPTsample`

This study focuses on:

- synthetic geology generation  
- sparse-data reconstruction  
- engineering-aware validation  

The adaptive CPT investigation-planning layer is intentionally separated into the sibling study case:

> `morie_CPTsample`

This separation preserves architectural clarity across the Morie ecosystem.

### `morie_subsurfaceAI`

Focuses on:

- reconstruction quality  
- geological realism  
- engineering-aware AI fields  

### `morie_CPTsample`

Focuses on:

- adaptive CPT placement  
- reinforcement learning  
- investigation optimization  
- uncertainty reduction strategies  

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

- **morie_CPTsample** → adaptive CPT optimization  
- **morie_anchor** → anchor engineering  
- **morie_anchorAI** → predictive anchor workflows  
- **morie_atlas** → lease-scale visualization and orchestration  

It provides the transition from:

> deterministic subsurface interpretation  

toward:

> engineering-aware AI reconstruction and offshore intelligence.


## Why It Matters Commercially

- Reduces uncertainty during early-stage offshore development  
- Supports engineering decisions under sparse investigation conditions  
- Bridges AI workflows with engineering interpretation  
- Enables scalable geotechnical reconstruction workflows  
- Improves integration between geology and offshore design  

This is where:

- geotechnics becomes data-driven  
- reconstruction becomes engineering-aware  
- offshore AI becomes physically interpretable  


## Aspects to Improve

- Real CPT calibration using offshore investigation datasets  
- Extension toward clay and rock environments  
- Native 3D reconstruction workflows  
- Uncertainty quantification  
- Cloud-scale reconstruction training  
- Integration with adaptive CPT optimization  

These extensions would move the workflow toward:

> fully integrated offshore subsurface intelligence systems.


## Design Philosophy

This study reflects the Morie Analytics approach:

- Physics-informed  
- Engineering-aware  
- Geologically consistent  
- Modular  
- Traceable  
- Scalable  

The workflow does not treat AI as a replacement for offshore engineering.

Instead:

> AI becomes a mechanism for reconstructing offshore subsurface behavior under engineering constraints.