---
layout: post
title: Lease Area Site Characterization – Celtic Sea
image: "/posts/morie_site/celtic_sea_lease_areas.png"
tags: [Offshore Floating Wind, Site Characterization, GEBCO, EMODnet, GIS, Python]
---

# Celtic Sea Floating Offshore Wind – Site Intelligence & Spatial Characterization

## Executive Summary

This study establishes the **site intelligence layer** of Morie Analytics by transforming publicly available marine geospatial datasets into **engineering-ready inputs** for floating offshore wind development.

Using Celtic Sea lease areas, **GEBCO 2025 bathymetry**, and **EMODnet seabed classification**, the workflow converts raw regional data into structured spatial products that support early-stage engineering decisions.

The result is a **reproducible Python-based pipeline** that replaces fragmented GIS workflows with a scalable and transparent offshore data-processing framework.

> **Site intelligence** → Layout generation → Soil reconstruction → Mooring physics → Anchor verification → Cable optimization

---

## Project Scope

- Screening of **5 Celtic Sea lease areas**  
- Processing of **GEBCO 2025 bathymetry**  
- Integration of **EMODnet Folk 7 seabed classification**  
- Generation of lease-scale bathymetry and soil maps  
- Validation of local results against regional datasets  

This study focuses on **regional-to-lease scale characterization**, forming the foundation for downstream engineering modules.

---

## Engineering Context

Early-stage floating offshore wind design requires rapid and consistent evaluation of:

- Water depth distribution  
- Seabed conditions  
- Anchor feasibility constraints  
- Mooring footprint implications  
- Installation constraints  

These assessments are often performed manually in GIS environments, leading to inconsistencies across projects.

This workflow introduces a **structured computational alternative**, where public datasets are transformed into standardized engineering inputs.

---

## Inputs and Data Sources

The workflow integrates:

- Celtic Sea lease area boundaries  
- **GEBCO 2025** global bathymetry grid  
- **EMODnet Folk 7** seabed classification  

All datasets are:

- Harmonized into a projected coordinate system  
- Spatially aligned  
- Processed into engineering-ready formats  

---

## Technical Architecture

The workflow is implemented in Python using:

- `geopandas` → spatial data processing  
- `xarray` → bathymetry handling  
- `numpy` → numerical operations  
- `matplotlib` → visualization  

Core modules:

- Lease boundary extraction  
- CRS transformation  
- Bathymetry masking  
- Seabed intersection  

This modular structure ensures **reproducibility, clarity, and scalability**.

---

## Processing Workflow

For each lease area:

1. Import lease boundary  
2. Transform coordinates to projected system  
3. Load GEBCO bathymetry  
4. Mask bathymetry within lease polygon  
5. Load EMODnet seabed data  
6. Intersect seabed classification with lease  
7. Generate plots and structured outputs  

The workflow is fully automated and repeatable across multiple lease areas.

---

## Regional Lease Context

<div align="center">
  <img src="/img/posts/morie_site/celtic_sea_lease_areas.png" 
       alt="Map of Celtic Sea lease areas showing spatial distribution of candidate zones for floating offshore wind development" 
       width="500">
</div>
*Figure 1 – Regional lease areas used as the screening context for floating offshore wind development.*

### Engineering Significance

Offshore design begins at regional scale, where:

- Lease areas compete for feasible conditions  
- Bathymetry and soils vary spatially  
- Design assumptions must remain consistent  

---

## Bathymetry Characterization

<div align="center">
  <img src="/img/posts/morie_site/2farm_bathy_2_folk7.png" 
       alt="Lease-scale bathymetry map showing water depth variations across Celtic Sea offshore wind lease areas" 
       width="500">
</div>
*Figure 2 – Lease-scale bathymetry used to constrain feasible layout regions.*

The bathymetric dataset reveals water depths across the selected Celtic Sea lease areas typically ranging between:

- **~85 m to 100 m** approx.  
- Gentle slopes with gradual depth transitions  

This results in a **bathymetrically smooth environment**, well-suited for floating offshore wind deployment.

### Engineering Significance

Bathymetry directly informs:

- Floater type feasibility
- Mooring line configurations and geometry  
- Anchor radius and footprint  
- Cable routing constraints  

From an engineering perspective, the observed depth range implies:

- **Floating wind is prefered** (fixed-bottom solutions are not economically viable at this depth scale)  
- Mooring systems will operate in a **deep-water regime** (even if its in the shallowest range), where line length and compliance dominate behavior  
- Anchor locations must be designed considering **relevant horizontal offsets and footprint expansion**  

The relatively mild seabed slopes enable:

- Stable and predictable mooring layouts  
- Reduced risk of localized load amplification due to terrain effects  
- Simplified cable routing with fewer constraints related to steep gradients  

However, depth variability across the site still requires:

- Consistent normalization of mooring configurations (addressed in **morie_mooring**)  
- Alignment of anchor design with local water depth conditions (addressed in **morie_anchor**) 
- Consideration of cable touchdown zones under varying depth profiles (addessed in **morie_cable**)  

This bathymetric characterization defines the **geometric boundary conditions** for all downstream engineering modules.

---

## Seabed Characterization 

### Initial Mapping

<div align="center">
  <img src="/img/posts/morie_site/2dfarm_soil_2_folk7.png" 
       alt="Initial seabed classification map showing raw sediment distribution prior to EMODnet alignment for offshore wind site analysis" 
       width="500">
</div>
*Figure 3 – Initial soil classification used for validation of processing steps.*

### EMODnet Classification Alignment

<div align="center">
  <img src="/img/posts/morie_site/seabed_legend.PNG" 
       alt="EMODnet Folk-7 classification legend showing sediment categories used for seabed mapping in offshore wind studies" 
       width="500">
</div>
*Figure 4 – EMODnet Folk 7 classification legend.*

The EMODnet seabed dataset provides sediment classification at multiple levels of resolution:

- **Folk-16** → highly detailed classification including mixed sediment types  
- **Folk-7** → intermediate engineering-relevant grouping  
- **Folk-5** → simplified classification for large-scale screening  

In this workflow, the **Folk-7 classification** is selected as a balance between:

- Spatial resolution (soil horizontal variability)
- Engineering interpretability  
- Compatibility with anchor and cable design models  

This level preserves key distinctions (e.g., sand vs mud vs coarse material) while avoiding excessive fragmentation of sediment classes.

### Engineering Mapping

<div align="center">
  <img src="/img/posts/morie_site/2dfarm_soil_2_folk7_EMOD.png" 
       alt="Seabed classification map aligned with EMODnet Folk-7 system showing sediment distribution for anchor and cable design assessment" 
       width="500">
</div>
*Figure 5 – Soil classification aligned with EMODnet standards.*

The processed map shows a **predominance of sandy sediments** across the selected Celtic Sea region, with localized variations including:

- Finer materials (mud-dominated zones)  
- Coarser sediments and transitional layers  

### Engineering Significance

Seabed classification supports:

- Anchor concept screening (e.g., suction piles vs driven solutions)  
- Soil-structure interaction assumptions (strength, stiffness, friction)  
- Cable burial feasibility and protection requirements  

From an engineering perspective, the dominance of sand suggests:

- Favorable conditions for **predictable installation behavior**  
- Strong dependence on **relative density and friction angle**  
- Suitability for **drag-embedded or driven anchor concepts**, depending on depth and variability  

At the same time, localized heterogeneity highlights the need for:

- Site-specific soil reconstruction (addressed in **morie_soil**)  
- Robust design envelopes for mixed conditions    

---

## Regional Context Verification

<div align="center">
  <img src="/img/posts/morie_site/celtic_sea_map_EMOD.jpg" 
       alt="Regional seabed map of the Celtic Sea showing large-scale sediment distribution across offshore wind development areas" 
       width="500">
</div>
*Figure 6 – Regional seabed conditions across the Celtic Sea.*

---

## Local-to-Regional Validation

<div align="center">
  <img src="/img/posts/morie_site/celtic_sea_map_EMODnet.png" 
       alt="Comparison of lease-scale seabed classification against regional EMODnet dataset to validate spatial consistency" 
       width="500">
</div>
*Figure 7 – Verification of lease-scale results within regional context.*

### Engineering Significance

Ensures:

- Spatial accuracy  
- Classification consistency  
- Traceability to source datasets  

---

## Outputs Generated

For each lease area:

- bathymetry grids (`.txt`)  
- soil classification grids (`.txt`)  
- spatial plots (`.png`)  
- structured CSV summaries  

These outputs are directly usable in downstream engineering workflows.

---

## Engineering Applications

The outputs support:

- Lease-to-lease comparison 
- Anchor concept screening  
- Mooring system feasibility  
- Cable routing strategy  
- Installation planning  
 
This transforms raw geospatial data into **engineering decision inputs**.

---

## Relationship to Other Morie Study Cases

This study is the **entry point of the Morie Analytics workflow**.

### Feeds into:

- **morie_layout** → spatial layout optimization  
- **morie_soil** → localized soil modeling  
- **morie_mooring** → depth-informed system geometry  
- **morie_anchor** → preliminary anchor feasibility  
- **morie_cable** → seabed-aware routing constraints  

It provides the **baseline environmental context** for all downstream modules.

---

## Why It Matters Commercially

- Reduces reliance on manual GIS workflows  
- Enables rapid multi-site screening  
- Improves consistency across projects  
- Accelerates early-stage decision making  
- Provides scalable data infrastructure for developers  

This is where **data becomes engineering leverage**.

---

## Aspects to Improve

- Incorporation of higher-resolution bathymetry datasets  
- Integration of geotechnical CPT data  
- Inclusion of metocean conditions  
- Automated constraint mapping (exclusion zones, cables, shipping)  

These extensions would move the workflow closer to **FEED-level site characterization**.

---

## Design Philosophy

This study reflects the Morie Analytics approach:

- Modular  
- Reproducible  
- Data-driven  
- Rngineering-focused  
- Scalable to full wind farm design  

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
python morie_site.py
```