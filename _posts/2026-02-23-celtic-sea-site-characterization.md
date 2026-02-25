---
layout: post
title: Lease Area Site Characterization - Celtic Sea
image: "/posts/celtic_sea_map.jpg"
tags: [Offshore Wind, Site Characterization, GEBCO, EMODnet, Python]
---

# Celtic Sea Floating Offshore Wind – Public Data Site Characterization

This project demonstrates how publicly available marine geospatial datasets can be transformed into structured, engineering-ready inputs for floating offshore wind development.

Using lease boundary shapefiles, GEBCO 2025 bathymetry (15 arc-second resolution), and EMODnet seabed classification, a modular Python workflow was developed to process five Celtic Sea lease areas and generate standardized outputs suitable for early-stage offshore engineering assessments.

The objective is to formalize public data ingestion into a reproducible offshore analytics pipeline that replaces fragmented GIS workflows with scalable and transparent processing.

---

## Project Scope

- **5 lease areas processed**
- ~**316,800 regional bathymetric grid points**
- ~**25,000–60,000 masked nodes per lease**
- EMODnet sediment classification at **1:250k resolution**
- Automated batch generation of structured output files and spatial plots

The workflow transforms raw public datasets into engineering-grade inputs for feasibility screening.

---

## 1. Lease Area Definition

The lease area contour is defined using geospatial boundary coordinates and converted into a computational polygon for spatial analysis.

Processing steps:

- Import geographic coordinates (WGS84)
- Transform to projected metric CRS
- Generate closed lease polygon
- Validate spatial consistency

The lease polygon forms the spatial mask for all subsequent bathymetric and seabed extraction.

---

## 2. Bathymetry Integration – GEBCO 2025

Bathymetric data is sourced from the **GEBCO 2025 global elevation grid** (15 arc-second resolution).

![Celtic Sea Bathymetry]("/img/posts/2dfarm_bathy_lease_2.png")
*Figure 1 – Masked GEBCO 2025 bathymetry within lease boundary.*

Depth variations across the lease area directly influence mooring system configuration, anchor embedment requirements, and installation vessel selection.

Processing steps:

- Load netCDF bathymetry raster
- Mask bathymetry within lease boundary
- Convert depth reference to project datum
- Generate contour maps and slope estimation
- Compute statistical depth metrics

Outputs:

- Lease-area bathymetry maps
- Depth distribution analysis
- Slope estimation relevant to mooring footprint behavior and cable routing

Bathymetry directly informs:

- Anchor feasibility
- Mooring line length estimation
- Installation planning
- Cable routing constraints

---

## 3. Seabed Characterization – EMODnet Integration

Seabed classification is derived from **EMODnet Geology & Seabed Habitat datasets**.

![Celtic Sea Seabed Classification](/img/posts/2dfarm_soil_2.png)
*Figure 2 – EMODnet sediment classification intersected with lease polygon.*

Spatial sediment variability informs anchor concept selection and early-stage geotechnical feasibility screening.

Processing steps:

- Import sediment classification shapefiles
- Intersect seabed layers with lease polygon
- Extract dominant sediment types
- Map spatial variability

Where available, the following indicators are interpreted:

- Sediment type (sand, clay, mixed sediments)
- Relative density proxies
- Undrained shear strength proxies
- Rock presence indicators

This supports early-stage screening of:

- Suction anchor suitability
- Driven or drilled pile feasibility
- Drag-embedment anchor potential

---

## 4. Integrated Spatial Workflow (Python)

All datasets are processed using Python-based geospatial tools:

```python
import xarray as xr
import geopandas as gpd
import numpy as np

# Load lease polygon
lease = gpd.read_file("lease_area.geojson")

# Load GEBCO bathymetry
gebco = xr.open_dataset("gebco_subset.nc")

# Spatial masking example
bathymetry_subset = gebco.where(
    (gebco.lon >= lease.bounds.minx) &
    (gebco.lon <= lease.bounds.maxx)
)
