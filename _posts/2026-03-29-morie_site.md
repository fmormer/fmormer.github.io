---
layout: post
title: Site Intelligence & Spatial Characterization
image: "/img/posts/morie_site/morie_site.png"
tags: [Offshore Floating Wind, Site Characterization, GEBCO, EMODnet, GIS, Python]
---

# Celtic Sea Floating Offshore Wind – Site Intelligence & Spatial Characterization

## Executive Summary

This study establishes the **site intelligence layer** of Morie Analytics by transforming heterogeneous public offshore datasets into **standardized engineering resources** for floating offshore wind development.

Using Celtic Sea lease areas together with **GEBCO 2025 bathymetry**, **EMODnet seabed classification**, **ERA5 atmospheric reanalysis** and **Copernicus Marine wave and ocean physics products**, the workflow converts raw environmental information into reproducible resources describing bathymetry, seabed conditions, terrain, wind climate, wave climate and ocean currents.

The result is a **reproducible Python-based workflow** that replaces fragmented GIS and metocean preprocessing with a scalable and transparent environmental characterization pipeline.

Rather than operating directly on heterogeneous public datasets, the workflow establishes a common environmental representation that can be consumed directly by downstream engineering modules throughout the Morie ecosystem.

This article is the first study case within the Morie Analytics portfolio, introducing the environmental foundation upon which subsequent engineering workflows are built:

> **Site intelligence** → Layout generation → Soil reconstruction → Mooring physics → Anchor verification → Cable optimization

Each module transforms standardized engineering resources into progressively more detailed design decisions, enabling a modular and reproducible approach to floating offshore wind engineering.


## Project Scope

- Screening of **5 Celtic Sea lease areas**
- Processing of **GEBCO 2025 bathymetry**
- Integration of **EMODnet Folk-7 seabed classification**
- Characterization of **ERA5 wind resources**
- Characterization of **Copernicus Marine wave and current resources**
- Generation of standardized environmental engineering resources
- Validation of lease-scale results against regional datasets

This study transforms **public offshore environmental data into standardized engineering resources** for downstream floating offshore wind analyses.


## Engineering Context

Early-stage floating offshore wind development requires the rapid and consistent integration of multiple environmental datasets to support engineering decision-making, including:

- Water depth and bathymetric variability
- Seabed slope and terrain complexity
- Seabed geology and engineering soils
- Wind climate and directional energy resource
- Wave climate and environmental loading
- Ocean current conditions

Traditionally, these assessments rely on independent GIS workflows, multiple software platforms and manually processed environmental datasets, often leading to duplicated effort, inconsistent assumptions and limited reproducibility between projects.

This workflow introduces a **structured computational approach**, where heterogeneous public datasets are transformed into **standardized engineering resources** that provide a common environmental foundation for downstream floating offshore wind analyses.


## Inputs and Data Sources

This study integrates multiple publicly available environmental datasets that collectively describe the physical characteristics of floating offshore wind lease areas:

- Celtic Sea lease area boundaries
- **GEBCO 2025** global bathymetry
- **EMODnet Folk-7** seabed classification
- **ERA5** atmospheric reanalysis
- **Copernicus Marine** wave reanalysis
- **Copernicus Marine** ocean physics reanalysis

The EMODnet classification is used as a regional sediment screening dataset and should not be interpreted as a substitute for site-specific geotechnical investigation.

All datasets are automatically:

- Harmonized into a common geographic reference framework
- Spatially aligned with the lease geometry
- Processed into standardized engineering resources

This establishes a **common environmental foundation** that can be directly consumed by downstream Morie Analytics modules.


## System Flow

**Public Environmental Data** → **Environmental Characterization** → **Standardized Engineering Resources**

This modular workflow transforms heterogeneous offshore datasets into a consistent environmental representation, ensuring **reproducibility, transparency and scalability** across floating offshore wind projects.

### Processing Workflow

For each lease area:

1. Import the lease boundary and establish the engineering reference geometry
2. Transform geographic coordinates into a consistent projected coordinate system
3. Process GEBCO bathymetry and derive seabed slopes
4. Classify seabed sediments using EMODnet geological data
5. Characterize the wind climate from ERA5 atmospheric reanalysis
6. Characterize the wave climate from Copernicus Marine wave products
7. Characterize ocean currents from Copernicus Marine physics products
8. Generate standardized engineering resources and visualizations

This workflow transforms **heterogeneous public environmental datasets into standardized engineering resources** that can be directly consumed by downstream floating offshore wind engineering modules.


## Regional Lease Context

<div align="center">
  <img src="/img/posts/morie_site/celtic_sea_lease_areas.png"
       alt="Map of Celtic Sea lease areas showing spatial distribution of candidate zones for floating offshore wind development"
       width="500">
</div>
_Figure 1 – Regional lease areas used as the screening context for floating offshore wind development._

### Engineering Significance

Environmental characterization begins at the regional scale, where:

- Lease areas present different environmental conditions
- Bathymetry, seabed properties and metocean resources vary spatially
- Engineering assumptions must remain consistent across candidate sites

Establishing a common environmental baseline enables objective site screening and provides a reproducible foundation for downstream floating offshore wind engineering analyses.


## Bathymetry Characterization

<div align="center">
  <img src="/img/posts/morie_site/2farm_bathy_2_folk7.png"
       alt="Lease-scale bathymetry map showing water depth variations across Celtic Sea offshore wind lease areas"
       width="500">
</div>
_Figure 2 – Lease-scale bathymetry used to characterize water depth across the selected lease areas._

The processed bathymetric dataset reveals water depths across the selected Celtic Sea lease areas typically ranging between:

- **~85 m to 100 m**
- Gentle regional gradients with gradual depth transitions

These characteristics define a **bathymetrically smooth offshore environment**, well suited for floating offshore wind development.

### Engineering Significance

Bathymetry provides the geometric framework for several downstream engineering activities, including:

- Floating platform concept selection
- Mooring system geometry and footprint definition
- Anchor layout and horizontal offsets
- Cable routing and touchdown assessment

From an engineering perspective, the observed depth range indicates that:

- **Floating wind solutions are preferred**, as fixed-bottom foundations are generally not economically viable at these water depths.
- Mooring systems operate within an **intermediate-depth floating wind regime**, where line compliance and seabed footprint become key design considerations.
- Anchor layouts must accommodate **significant horizontal offsets** between floating platforms and seabed foundations.

The relatively mild seabed gradients support:

- Stable and predictable mooring configurations
- Reduced potential for terrain-induced load amplification
- Simplified cable routing with fewer constraints associated with steep seabed gradients

Nevertheless, spatial variations in water depth remain important for downstream engineering analyses, including:

- Consistent normalization of mooring system configurations (addressed in `morie_mooring`)
- Preliminary anchor sizing and verification under site-specific depth conditions (addressed in `morie_anchor`)
- Assessment of cable touchdown behaviour along variable bathymetric profiles (addressed in `morie_cable`)

Overall, bathymetry defines the **geometric boundary conditions** that underpin subsequent floating offshore wind engineering analyses throughout the Morie Analytics workflow.

## Seafloor Slope Characterization

<div align="center">
  <img src="/img/posts/morie_site/2dfarm_slope_2.png"
       alt="Seafloor slope map derived from GEBCO bathymetry showing slope distribution across the Celtic Sea lease area"
       width="500">
</div>
_Figure 3 – Seafloor slope map derived from the processed bathymetric dataset._

The seafloor slope map was derived directly from the processed bathymetric grid to characterize terrain variability across the selected lease area.

The results indicate a relatively smooth seabed morphology, with gentle regional gradients and limited occurrence of localized steep terrain.

### Engineering Significance

Seafloor slope provides an additional terrain constraint that influences several downstream engineering activities, including:

- Mooring line touchdown behaviour
- Anchor loading conditions at the mudline
- Cable routing and touchdown configuration
- Installation accessibility and marine operations

Even in relatively smooth environments, localized slope variations can affect:

- Horizontal and vertical load transfer at the seabed
- Mooring system equilibrium geometry
- Cable free-span potential
- Spatial variability of installation conditions

Although bathymetry defines the overall geometric framework of the site, seafloor slope provides complementary information on local terrain variability, supporting more robust engineering assessments throughout the Morie Analytics workflow.


## Seabed Characterization

### Initial Mapping

<div align="center">
  <img src="/img/posts/morie_site/2dfarm_soil_2_folk7.png"
       alt="Initial seabed classification map showing raw sediment distribution prior to EMODnet alignment for offshore wind site analysis"
       width="500">
</div>
_Figure 4 – Initial seabed classification generated during the environmental processing workflow._

### EMODnet Classification Alignment

<div align="center">
  <img src="/img/posts/morie_site/seabed_legend.PNG"
       alt="EMODnet Folk-7 classification legend showing sediment categories used for seabed mapping in offshore wind studies"
       width="500">
</div>
_Figure 5 – EMODnet Folk-7 engineering sediment classification._

The EMODnet seabed dataset provides sediment classification at multiple levels of detail:

- **Folk-16** → detailed sediment classification including mixed sediment types
- **Folk-7** → intermediate engineering-oriented grouping
- **Folk-5** → simplified classification for regional screening

Within this workflow, the **Folk-7 classification** is selected as a balance between:

- Spatial resolution
- Engineering interpretability
- Compatibility with downstream engineering workflows

This level preserves the principal engineering distinctions between sand-, mud-, and coarse-dominated seabeds while avoiding unnecessary fragmentation of sediment classes.

### Engineering Mapping

<div align="center">
  <img src="/img/posts/morie_site/2dfarm_soil_2_folk7_EMOD.png"
       alt="Seabed classification map aligned with EMODnet Folk-7 system showing sediment distribution for anchor and cable design assessment"
       width="500">
</div>
_Figure 6 – Lease-scale engineering seabed classification derived from the EMODnet Folk-7 dataset._

The processed seabed map indicates a **predominance of sandy sediments** across the selected Celtic Sea lease areas, together with localized occurrences of:

- Mud-dominated sediments
- Coarser materials and transitional sediment classes

### Engineering Significance

Seabed characterization provides the geological context required for several downstream engineering activities, including:

- Preliminary anchor concept screening
- Soil–structure interaction assumptions
- Cable burial feasibility and protection assessment

From an engineering perspective, the predominance of sandy sediments suggests favourable conditions for suction-assisted or driven anchor concepts, subject to confirmation through site-specific geotechnical investigations.

At this stage, the Folk-7 classification should be interpreted as a **regional sediment screening layer**, rather than a direct indicator of engineering soil properties such as strength, stiffness, relative density, installation feasibility, or anchor capacity.

At the same time, the observed spatial variability highlights the need for:

- Site-specific soil reconstruction from geotechnical investigations (addressed in `morie_soil`)
- Detailed anchor design and verification under representative soil conditions (addressed in `morie_anchor`)
- Site-specific cable burial and protection assessments 

This environmental characterization transforms regional geological information into a standardized engineering resource that supports the downstream Morie Analytics workflow.


## Metocean Resource Characterization

In addition to the static characteristics of the offshore environment, floating offshore wind engineering requires a quantitative description of the dynamic environmental conditions that govern energy production, structural loading, installation planning and long-term system performance.

The workflow therefore characterizes the regional wind, wave, and current climate using publicly available atmospheric and oceanographic reanalysis datasets. These environmental resources complement the bathymetric and geological characterization presented previously, providing a consistent environmental foundation for downstream engineering analyses.

### Wind Climate

<div align="center">
  <img src="/img/posts/morie_site/wind_rose_Celtic_2.png"
       alt="Directional wind climate characterized from ERA5 atmospheric reanalysis"
       width="500">
</div>
_Figure 7 – Directional wind resource characterized from ERA5 atmospheric reanalysis._

The processed wind resource summarizes the directional distribution of wind speed across the selected lease area together with representative Weibull parameters used for offshore wind resource assessment.

### Engineering Significance

Wind characterization provides the primary environmental input for:

- Wind farm layout optimization
- Wake modelling and energy yield assessment
- Turbine loading studies
- Early-stage energy production estimates

Within the Morie Analytics workflow, the standardized wind resource is consumed directly by `morie_layout`, where it supports wake modelling and annual energy production (AEP) assessment.

### Wave Climate

<div align="center">
  <img src="/img/posts/morie_site/wave_rose_Celtic_2.png"
       alt="Directional wave climate characterized from Copernicus Marine wave reanalysis"
       width="500">
</div>
_Figure 8 – Directional wave climate characterized from Copernicus Marine wave reanalysis._

The wave resource summarizes the directional occurrence of sea states together with representative significant wave heights and peak periods across the lease area.

### Engineering Significance

Wave characterization supports:

- Environmental loading assessment
- Mooring system design
- Dynamic cable analysis
- Installation planning and operability studies

These environmental conditions provide essential inputs for downstream engineering workflows, particularly `morie_mooring` and `morie_cable`.

### Current Climate

<div align="center">
  <img src="/img/posts/morie_site/current_rose_Celtic_2.png"
       alt="Directional ocean current characterization from Copernicus Marine physics reanalysis"
       width="500">
</div>
_Figure 9 – Directional ocean current resource characterized from Copernicus Marine physics reanalysis._

The current resource describes the prevailing ocean current regime across the lease area, including directional occurrence and representative current velocities.

### Engineering Significance

Ocean current characterization contributes to:

- Dynamic cable behaviour
- Marine operations and installation planning
- Environmental loading assessments
- Future integrated offshore system studies

Although generally secondary to wind and waves for floating wind design, ocean currents remain an important component of the offshore environmental characterization and complete the standardized environmental resource package generated by `morie_site`.


## Geological Validation

<table align="center">
  <tr>
    <th>Regional EMODnet reference</th>
    <th>Lease-scale engineering classification</th>
  </tr>
  <tr>
    <td align="center">
      <img src="/img/posts/morie_site/celtic_sea_map_EMOD.jpg"
           alt="Regional seabed map of the Celtic Sea showing large-scale sediment distribution across offshore wind development areas"
           width="380">
    </td>
    <td align="center">
      <img src="/img/posts/morie_site/celtic_sea_map_EMODnet.png"
           alt="Comparison of lease-scale seabed classification against regional EMODnet dataset to validate spatial consistency"
           width="380">
    </td>
  </tr>
</table>

_Figure 10 – Comparison between the regional EMODnet seabed dataset and the lease-scale engineering seabed classification generated by the workflow._

### Engineering Significance

The lease-scale engineering seabed classification is verified against the original regional EMODnet dataset to ensure that the environmental processing workflow preserves the spatial distribution of sediment classes while transforming geological information into engineering-ready resources.

This validation confirms:

- Consistency with the original EMODnet geological dataset
- Spatial fidelity throughout the processing workflow
- Traceability from engineering resources back to their public data sources

Although the workflow standardizes environmental information for engineering applications, the resulting seabed characterization remains directly linked to the underlying regional geological observations.


## Outputs Generated

For each lease area, the workflow automatically generates a standardized environmental characterization package comprising:

- Lease boundary and engineering reference geometry
- Bathymetry and seabed slope resources
- Engineering seabed classification
- Wind, wave, and current resource datasets
- Engineering visualizations and directional resource roses
- Standardized MORIE engineering resource files

These outputs establish a **common environmental foundation** that can be consumed directly by downstream Morie Analytics modules without additional preprocessing.


## Engineering Applications

The standardized environmental resources generated by this workflow support a wide range of early-stage floating offshore wind engineering activities, including:

- Multi-site comparison and lease screening
- Wind farm layout optimization and wake assessment
- Mooring system engineering
- Preliminary anchor concept screening
- Cable routing and corridor assessment
- Installation feasibility and marine operations planning
- Environmental baseline studies

By transforming heterogeneous public environmental datasets into **standardized engineering resources**, the workflow establishes a common environmental foundation for engineering decision-making across the Morie Analytics ecosystem.


## Relationship to Other Morie Study Cases

This study establishes the **environmental intelligence layer** of the Morie Analytics workflow by generating standardized engineering resources that are shared across downstream engineering modules.

### Provides environmental resources for:

- **morie_layout** → wind resource, bathymetry, and lease geometry for layout optimization and wake assessment
- **morie_soil** → seabed classification as the regional foundation for localized soil reconstruction
- **morie_mooring** → water depth and metocean conditions for mooring system engineering
- **morie_anchor** → bathymetry and seabed characterization for preliminary anchor concept selection and verification
- **morie_cable** → bathymetry, seabed conditions, slopes, waves, and currents for routing and touchdown assessment

Rather than supplying independent datasets to each study case, `morie_site` establishes a **common environmental foundation** that ensures all downstream engineering core workflows operate from the same validated site characterization.


## Why It Matters Commercially

- Reduces reliance on fragmented GIS and metocean preprocessing workflows
- Enables rapid multi-site environmental characterization and lease screening
- Establishes a consistent environmental baseline across engineering disciplines
- Accelerates early-stage engineering decision-making
- Improves reproducibility and traceability throughout project development
- Provides scalable environmental intelligence for developers, consultants, and researchers

This is where **public environmental data becomes standardized engineering knowledge**.


## Aspects to Improve

- Integration of site-specific geotechnical investigations (CPTs and boreholes)
- Support for higher-resolution bathymetric and terrain datasets
- Automated environmental constraint mapping (shipping lanes, subsea infrastructure, protected areas, and exclusion zones)
- Geohazard characterization, including slope instability, seabed mobility, and liquefaction susceptibility
- Environmental uncertainty quantification and confidence mapping
- Multi-site automated environmental characterization at regional scale

These extensions would further strengthen the environmental intelligence layer, moving the workflow closer to **FEED-level site characterization** while providing an increasingly comprehensive foundation for downstream engineering analyses.


## Design Philosophy

The objective of this study is not to replace detailed site investigations, but to establish a transparent, reproducible, and scalable environmental characterization workflow that transforms heterogeneous public offshore datasets into standardized engineering resources for early-stage floating offshore wind development.

Rather than exposing downstream engineering workflows to raw environmental datasets, `morie_site` establishes a common environmental foundation that can be shared consistently across layout optimization, soil reconstruction, mooring engineering, anchor verification, cable routing, and future engineering analyses.

The study reflects the Morie Analytics approach:

- **Resource-oriented** – Standardized engineering resources provide a common interface between environmental characterization and downstream engineering workflows.
- **Physics-informed** – Environmental characterization is guided by engineering relevance rather than purely geospatial representation.
- **Modular** – Independent processing components enable straightforward maintenance, extension, and reuse.
- **Traceable** – Every engineering resource remains linked to publicly available environmental datasets.
- **Engineering-focused** – Outputs are designed for direct integration into floating offshore wind engineering workflows.
- **Scalable** – The same workflow can be applied consistently across multiple lease areas, offshore regions, and future environmental datasets.

Ultimately, the objective is not simply to process environmental data, but to transform publicly available offshore information into standardized engineering knowledge that accelerates floating offshore wind development.  

