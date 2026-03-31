---
layout: post
title: Lease Area Site Characterization - Celtic Sea
image: "/posts/morie_site/celtic_sea_lease_areas.png"
tags: [Offshore Wind, Site Characterization, GEBCO, EMODnet, GIS, Python]
---

# Celtic Sea Floating Offshore Wind – Site Characterization & Spatial Intelligence

This project develops a structured Python workflow to transform publicly available marine geospatial datasets into **engineering-ready inputs** for floating offshore wind development in the Celtic Sea.

Using lease boundary data, **GEBCO 2025 bathymetry**, and **EMODnet seabed classification**, the workflow converts raw regional datasets into standardized spatial products suitable for:

- lease-scale screening  
- floater layout definition  
- mooring system planning  
- anchor concept selection  
- cable routing strategy  
- early geotechnical interpretation  

The objective is to formalize public marine data ingestion into a reproducible computational pipeline that connects **regional site intelligence** with downstream offshore engineering workflows.

---

## Project Scope

- **5 Celtic Sea lease areas** screened at regional level  
- Public bathymetry processed from **GEBCO 2025**  
- Public seabed classification processed from **EMODnet Folk 7**  
- Lease-scale bathymetry and soil maps generated in projected coordinates  
- Validation of local lease plots against regional seabed mapping  

This workflow transforms raw public datasets into **decision-ready offshore site intelligence**.

<pre>
Public Marine Data → Spatial Processing → Site Constraints → Engineering Inputs
                                      ↓
               Layout → Mooring → Anchor → Cable → Installation
</pre>

---

## 1. Regional Lease Context

The first step is to position the project within the broader Celtic Sea development area.

At regional scale, multiple lease areas are identified and screened as candidate zones for floating offshore wind deployment.

<div align="center">
  <img src="/img/posts/morie_site/celtic_sea_lease_areas.png" width="700">
</div>
*Figure 1 – Celtic Sea lease areas of interest used as the regional screening context for the workflow.*

### Engineering Significance

Regional framing is important because offshore design does not start from a single polygon in isolation. It starts from a broader marine system where:

- lease areas compete for feasible seabed conditions  
- bathymetry varies across the region  
- sediment environments shift spatially  
- design assumptions must remain consistent from regional screening to local engineering  

---

## 2. Lease Area Definition

Following regional screening, the selected lease area is converted into a computational polygon for local analysis.

### Methodology

- import boundary coordinates  
- transform from geographic to projected metric coordinates  
- generate a closed lease polygon  
- validate spatial consistency  

### Outputs

- projected lease boundary  
- analysis-ready coordinate system  
- masking domain  

### Engineering Significance

Defines the **valid engineering domain** for:

- floater placement  
- mooring footprint  
- anchor positioning  
- cable routing  

---

## 3. Bathymetry Integration – GEBCO 2025

<div align="center">
  <img src="/img/posts/morie_site/2farm_bathy_2_folk7.png" width="500">
</div>
*Figure 2 – Lease-scale bathymetry map.*

### Processing Steps

- load GEBCO data  
- clip to lease  
- interpolate grid  
- generate contours  

### Outputs

- depth map  
- contour lines  
- depth statistics  

### Engineering Significance

Bathymetry informs:

- mooring geometry  
- anchor radius  
- floater feasibility  
- cable routing  
- installation constraints  

---

## 4. Seabed Characterization – Initial Soil Mapping

<div align="center">
  <img src="/img/posts/morie_site/2dfarm_soil_2_folk7.png" width="500">
</div>
*Figure 3 – Initial soil map (generic colors).*

### Purpose

Verification of:

- clipping  
- alignment  
- classification mapping  

---

## 5. EMODnet Folk 7 Legend Alignment

<div align="center">
  <img src="/img/posts/morie_site/seabed_legend.PNG" width="380">
</div>
*Figure 4 – EMODnet Folk 7 legend.*

### Engineering Significance

Ensures:

- consistency with source datasets  
- correct interpretation  
- cross-project comparability  

---

## 6. Seabed Characterization – EMODnet Color Mapping

<div align="center">
  <img src="/img/posts/morie_site/2dfarm_soil_2_folk7_EMOD.png" width="500">
</div>
*Figure 5 – Soil map using EMODnet colors.*

### Engineering Significance

Supports:

- anchor screening  
- seabed interaction understanding  
- cable burial feasibility  

---

## 7. Regional Soil Context

<div align="center">
  <img src="/img/posts/morie_site/celtic_sea_map_EMOD.jpg" width="700">
</div>
*Figure 6 – Regional seabed map.*

### Engineering Significance

Provides large-scale sediment context.

---

## 8. Embedded Verification

<div align="center">
  <img src="/img/posts/morie_site/celtic_sea_map_EMODnet.jpg.png" width="700">
</div>
*Figure 7 – Local vs regional verification.*

### Engineering Significance

Ensures:

- spatial accuracy  
- classification consistency  
- dataset traceability  

---

## 9. Integrated Python Workflow

```python
import xarray as xr
import geopandas as gpd
import numpy as np
import matplotlib.pyplot as plt

lease_gdf = gpd.read_file('lease_area.geojson')
gebco = xr.open_dataset('gebco_2025.nc')
soil_gdf = gpd.read_file('emodnet_folk7.shp')

lease_proj = lease_gdf.to_crs(target_crs)
soil_proj = soil_gdf.to_crs(target_crs)