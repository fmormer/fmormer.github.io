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

- water depth distribution  
- seabed conditions  
- anchor feasibility constraints  
- mooring footprint implications  
- installation constraints  

These assessments are often performed manually in GIS environments, leading to inconsistencies across projects.

This workflow introduces a **structured computational alternative**, where public datasets are transformed into standardized engineering inputs.

---

## Inputs and Data Sources

The workflow integrates:

- Celtic Sea lease area boundaries  
- **GEBCO 2025** global bathymetry grid  
- **EMODnet Folk 7** seabed classification  

All datasets are:

- harmonized into a projected coordinate system  
- spatially aligned  
- processed into engineering-ready formats  

---

## Technical Architecture

The workflow is implemented in Python using:

- `geopandas` → spatial data processing  
- `xarray` → bathymetry handling  
- `numpy` → numerical operations  
- `matplotlib` → visualization  

Core modules:

- lease boundary extraction  
- CRS transformation  
- bathymetry masking  
- seabed intersection  

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

![Celtic Sea Lease Areas](/img/posts/morie_site/celtic_sea_lease_areas.png)

*Regional lease areas used as the screening context for floating offshore wind development.*

### Engineering Significance

Offshore design begins at regional scale, where:

- lease areas compete for feasible conditions  
- bathymetry and soils vary spatially  
- design assumptions must remain consistent  

---

## Bathymetry Characterization

![Bathymetry Map](/img/posts/morie_site/2farm_bathy_2_folk7.png)

*Lease-scale bathymetry showing water depth distribution.*

### Engineering Significance

Bathymetry directly informs:

- mooring line geometry  
- anchor radius and footprint  
- floater feasibility  
- cable routing constraints  

---

## Seabed Characterization (Initial Mapping)

![Soil Map Generic](/img/posts/morie_site/2dfarm_soil_2_folk7.png)

*Initial soil classification used for validation of processing steps.*

---

## EMODnet Classification Alignment

![Seabed Legend](/img/posts/morie_site/seabed_legend.PNG)

*EMODnet Folk 7 classification legend.*

---

## Seabed Characterization (Engineering Mapping)

![Soil Map EMOD](/img/posts/morie_site/2dfarm_soil_2_folk7_EMOD.png)

*Soil classification aligned with EMODnet standards.*

### Engineering Significance

Seabed classification supports:

- anchor concept screening  
- soil-structure interaction assumptions  
- cable burial feasibility  

---

## Regional Context Verification

![Regional Soil Map](/img/posts/morie_site/celtic_sea_map_EMOD.jpg)

*Regional seabed conditions across the Celtic Sea.*

---

## Local-to-Regional Validation

![Embedded Verification](/img/posts/morie_site/celtic_sea_map_EMODnet.jpg.png)

*Verification of lease-scale results within regional context.*

### Engineering Significance

Ensures:

- spatial accuracy  
- classification consistency  
- traceability to source datasets  

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

- anchor concept screening  
- mooring system feasibility  
- cable routing strategy  
- installation planning  
- lease-to-lease comparison  

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

- modular  
- reproducible  
- data-driven  
- engineering-focused  
- scalable to full wind farm design  

---

## How to Run

1. Place datasets in `celtic_sea_share/`  
2. Install dependencies:

   - geopandas  
   - xarray  
   - numpy  
   - matplotlib  

3. Execute:

```bash
python lease_area_definition.py