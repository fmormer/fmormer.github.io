---
layout: post
title: Lease Area Site Characterization - Celtic Sea
image: "img/posts/celtic_sea_map.jpg"
tags: [Offshore Wind, Site Characterization, GEBCO, EMODnet, Python]
---

# Celtic Sea Floating Offshore Wind – Site Characterization

This project presents a structured site characterization workflow for a floating offshore wind lease area in the **Celtic Sea**. The objective is to define the lease boundary, extract bathymetric data, and integrate regional soil information to support early-stage engineering assessments for anchors, moorings, and infrastructure layout.

---

## 1. Lease Area Definition

The lease area contour is defined using geospatial boundary coordinates and converted into a computational polygon for spatial analysis. The workflow includes:

- Importing geographic coordinates (WGS84)
- Converting to projected metric coordinates
- Generating a closed lease polygon
- Visual validation of boundary consistency

This contour forms the spatial reference for all subsequent bathymetric and geotechnical data extraction.

---

## 2. Bathymetry – GEBCO Integration

Bathymetric data is sourced from **GEBCO (General Bathymetric Chart of the Oceans)**.

Processing steps:

- Load GEBCO raster dataset
- Subset data within lease polygon
- Convert depth reference to project datum
- Generate depth contours and gradient maps
- Compute statistics (min, max, mean depth)

Outputs:

- Lease-area bathymetry map
- Depth distribution histogram
- Slope estimation for mooring footprint assessment

Bathymetry directly informs:

- Anchor feasibility
- Mooring line length estimation
- Installation logistics
- Cable routing constraints

---

## 3. Soil Properties – EMODnet Integration

Seabed geotechnical characterization is derived from **EMODnet Geology & Seabed Habitat datasets**.

Processing steps:

- Import sediment classification layers
- Intersect with lease boundary
- Extract dominant soil types
- Map spatial variability

Where available, the following parameters are interpreted:

- Sediment type (sand, clay, mixed sediments)
- Relative density (for sands)
- Undrained shear strength proxies (for clays)
- Rock presence indicators

This data supports early-stage screening for:

- Suction anchor feasibility
- Driven or drilled pile suitability
- Drag-embedment anchor potential

---

## 4. Integrated Spatial Framework (Python Workflow)

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
