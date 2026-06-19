---
layout: post
title: Geohazard-Aware Planning for Floating Offshore Wind
image: "/img/posts/morie_geohazard/morie_geohazard.png"
tags: [Offshore Floating Wind, Geohazards, Site Characterization, Seabed Engineering, Offshore Planning, Bathymetry, Python]
---

# Celtic Sea Floating Offshore Wind – Geohazard-Aware Planning Workflow


## Executive Summary

This study establishes the **geohazard intelligence layer** of Morie Analytics by extending the existing offshore engineering workflow toward lease-scale geohazard awareness and planning support.

The workflow evaluates how slope conditions, mobile seabed sediments and shallow subsurface susceptibility influence engineering suitability across the offshore domain. 
Building directly on the outputs of the following case studies:

* `morie_site`
* `morie_layout`
* `morie_soil`
* `morie_seismic`

Rather than treating geohazards as isolated events assessed late in the design process, the workflow introduces a framework capable of identifying potentially sensitive sectors before detailed engineering begins.

Within the unified offshore planning framework this study combines:

* Bathymetric interpretation
* Morphological analysis
* Shallow subsurface susceptibility indicators
* Synthetic seabed scenarios
* Spatial geohazard screening

The result is a reproducible workflow that transforms site characterization data into geohazard intelligence layers capable of supporting future layout optimization, anchor planning and risk-informed engineering decisions.

This study represents the transition from:

> Site characterization

toward:

> Geohazard-aware offshore planning.

> Site intelligence → Layout generation → Soil reconstruction → Mooring physics → Anchor verification → Seismic intelligence → **Geohazard-aware planning**

<div align="center">
  <img src="/img/posts/morie_geohazard/morie_geohazard.png"
       alt="Integrated geohazard-aware planning workflow for floating offshore wind"
       width="1000">
</div>

*Figure 1 – Integrated geohazard workflow linking bathymetry, morphology, subsurface susceptibility and spatial screening within the Morie ecosystem.*


## Project Scope

* Bathymetric interpretation
* Morphological variability assessment
* Synthetic seabed scenario generation
* Shallow subsurface susceptibility mapping
* Geohazard screening
* Spatial classification of sensitive areas
* Lease-scale geohazard visualization

This study converts:

**Seabed conditions → Geohazard awareness → Planning intelligence**


## Engineering Context

Floating offshore wind developments interact with the seabed through a distributed network of:

* Anchors
* Mooring systems
* Dynamic power cables

Unlike fixed-bottom developments, engineering interactions are not concentrated around a single foundation location.
Instead, seabed conditions influence large portions of the lease area simultaneously.

This creates an important challenge. Even within apparently uniform offshore environments, variations in seabed morphology and shallow subsurface structure can create zones that 
deserve additional engineering attention.

The key question therefore becomes:

> How can geohazard awareness be incorporated into offshore planning before detailed engineering decisions are made?

Traditional workflows often assess geohazards after layouts have already been selected.
This study explores an alternative approach. Rather than evaluating individual hazards independently, multiple seabed indicators are integrated into a spatial screening framework capable of highlighting potentially sensitive sectors across the engineering domain.

Within this study, geohazard sensitivity is explored through three representative categories:

* Slope instability
* Mobile seabed sediments
* Liquefaction susceptibility

Together, these categories capture both static and dynamic aspects of the offshore environment. 
While slope-related conditions primarily reflect persistent terrain characteristics, mobile sediments introduce the possibility of seabed evolution through dune migration and morphological change. 
Liquefaction susceptibility provides an additional view of how shallow subsurface conditions may influence infrastructure performance under cyclic loading conditions.

The objective is not to model individual failure mechanisms directly, but to provide a spatial framework capable of highlighting areas where these geohazard influences may deserve additional engineering attention.


## Inputs and Data Sources

This study builds directly on upstream Morie Analytics outputs.

### From `morie_site`

* Bathymetry grids
* Terrain characteristics
* Local engineering domain

### From `morie_layout`

* Floating wind layout
* Anchor locations
* Spatial engineering context

### From `morie_soil`

* Reconstructed subsurface geometry
* Layer-boundary information
* Spatial soil variability

### From `morie_seismic`

* Liquefaction-related susceptibility indicators
* Degradation-aware geohazard concepts
* Screening concepts associated with cyclic soil behavior and post-event seabed sensitivity

These inputs complement the bathymetric and morphological information by introducing a shallow subsurface perspective into the geohazard assessment workflow.

### Additional Inputs

* Synthetic seabed scenarios
* Morphological interpretation layers
* Geohazard classification criteria

All workflows remain tied to the same cropped Celtic Sea engineering domain used throughout the Morie ecosystem.
This preserves continuity across:

* Site characterization
* Soil reconstruction
* Anchor engineering
* Seismic assessment
* Geohazard screening


## System Flow

Bathymetry → Morphological Interpretation → Subsurface Susceptibility Assessment → Geohazard Screening → Planning Intelligence

Throughout the workflow, this architecture preserves:

* Engineering traceability
* Spatial consistency
* Reproducibility
* Integration with previous Morie modules

### Processing Workflow

1. Import bathymetry and reconstructed soil information
2. Evaluate seabed morphology
3. Assess terrain variability
4. Generate geohazard screening layers
5. Introduce synthetic seabed scenarios
6. Recompute geohazard sensitivity
7. Classify engineering suitability
8. Generate lease-scale geohazard maps
9. Support planning interpretation

This converts:

**Site information → Geohazard intelligence**


## Baseline Seabed Characterization

The workflow begins with interpretation of the cropped Celtic Sea engineering domain.

<div align="center">
  <img src="/img/posts/morie_geohazard/bathy_cropped_before_synthetic.png"
       alt="Baseline bathymetry used for geohazard assessment"
       width="850">
</div>

*Figure 2 – Baseline bathymetry used as the starting point for geohazard assessment.*

Bathymetry provides more than water depth.
It also contains information regarding:

* Terrain variability
* Morphological transitions
* Potential seabed complexity

These characteristics influence how engineering systems interact with the offshore environment and therefore provide an important foundation for geohazard screening.


## Synthetic Seabed Scenarios

One of the challenges of offshore planning is uncertainty.
Future seabed conditions may not perfectly match the conditions observed during a site investigation campaign.

To explore this uncertainty, the workflow introduces controlled synthetic seabed scenarios inspired by realistic dune-field behavior and mobile sediment environments commonly encountered offshore.

<div align="center">
  <img src="/img/posts/morie_geohazard/bathy_cropped_after_synthetic.png"
       alt="Synthetic seabed scenario used for geohazard sensitivity assessment"
       width="850">
</div>

*Figure 3 – Example synthetic seabed scenario used to evaluate sensitivity to evolving morphological conditions.*

These synthetic scenarios are not intended as predictions of future seabed evolution.
Instead, they act as controlled stress tests that allow the workflow to evaluate how changes in morphology may influence geohazard sensitivity.
This introduces an important planning capability:

> Evaluating not only current conditions, but also sensitivity to plausible future seabed states.


## Geohazard Screening Framework

The workflow integrates multiple geohazard indicators into a unified spatial screening layer.
The objective is to identify sectors where combinations of seabed characteristics may warrant additional engineering investigation.

Examples of influencing factors include:

* Morphological variability
* Local terrain gradients
* Shallow subsurface structure
* Susceptibility-related indicators

The resulting maps should be interpreted as relative screening tools rather than deterministic design criteria.

They help answer questions such as:

* Which sectors appear consistently favorable?
* Which sectors exhibit elevated sensitivity?
* Where should additional investigation be prioritized?


## Geohazard Sensitivity Mapping

The combined screening framework generates a lease-scale geohazard sensitivity map.

<div align="center">
  <img src="/img/posts/morie_geohazard/geohazard_index_map_synthetic_dunes.png"
       alt="Lease-scale geohazard sensitivity map"
       width="900">
</div>

*Figure 4 – Lease-scale geohazard sensitivity map generated from the integrated screening workflow.*

Several observations emerge:

* Geohazard sensitivity is not uniformly distributed across the site.
* Mobile sediment environments create distinct spatial corridors of elevated sensitivity.
* Areas of increased terrain variability tend to coincide with higher screening scores.
* Shallow subsurface susceptibility introduces additional differentiation between sectors that would otherwise appear similar based on bathymetry alone.

This highlights the importance of moving beyond simple bathymetric screening toward more integrated spatial assessment approaches.


## Geohazard Classification

For planning purposes, continuous geohazard sensitivity values are translated into engineering-oriented classes.

<div align="center">
  <img src="/img/posts/morie_geohazard/geohazard_index_map_synthetic_dunes_classes.png"
       alt="Geohazard classification map"
       width="900">
</div>

*Figure 5 – Geohazard classification map highlighting relative suitability across the engineering domain.*

The objective is to create a practical mechanism for comparing different sectors of the site and identifying areas where additional engineering attention may be warranted.

### Engineering Interpretation

The results demonstrate that:

* Large portions of the site remain broadly suitable for development.
* Geohazard sensitivity tends to cluster spatially rather than appearing randomly.
* Localized sectors may justify additional investigation before final layout decisions are made.
* Relative differences across the lease area can be visualized and communicated effectively.


## Understanding the Drivers

A key objective of the workflow is maintaining interpretability.
Rather than producing a single black-box map, the workflow preserves visibility of the underlying contributors to geohazard sensitivity.

<div align="center">
  <img src="/img/posts/morie_geohazard/gi_partial_bedform_driver_synthetic_dunes.png"
       alt="Bedform contribution to geohazard sensitivity"
       width="850">
</div>

*Figure 6 – Example bedform-related contribution to geohazard sensitivity.*

<div align="center">
  <img src="/img/posts/morie_geohazard/gi_partial_slope_driver_synthetic_dunes.png"
       alt="Slope contribution to geohazard sensitivity"
       width="850">
</div>

*Figure 7 – Example slope-related contribution to geohazard sensitivity.*

<div align="center">
  <img src="/img/posts/morie_geohazard/gi_partial_liquefaction_driver_synthetic_dunes.png"
       alt="Liquefaction susceptibility contribution to geohazard sensitivity"
       width="850">
</div>

*Figure 8 – Example shallow-subsurface susceptibility contribution to geohazard sensitivity.*

This enables engineers to understand whether elevated sensitivity is associated primarily with:

* Morphological variability
* Terrain gradients
* Liquefaction-related susceptibility

The ability to decompose geohazard sensitivity into individual contributors improves traceability and supports more informed engineering interpretation.


## Relationship with Layout Planning

One of the most important concepts introduced by this study is that geohazards become part of the planning workflow rather than a downstream verification exercise.
The framework therefore becomes:

Layout Planning → Geohazard Screening → Engineering Review → Detailed Design

This creates opportunities for:

* Improved site utilization
* Early identification of sensitive sectors
* Reduced redesign risk
* Better alignment between engineering disciplines

The different geohazard categories may influence offshore infrastructure in different ways.
For example:

* Mobile sediments may affect anchor embedment conditions.
* Seabed evolution may influence mooring-line touchdown behavior.
* Morphological variability may affect cable burial, exposure or free-span development.
* Shallow subsurface susceptibility may influence long-term soil-structure interaction.

Integrating geohazard awareness into planning therefore helps identify where additional engineering assessment may provide the greatest value.


## Outputs Generated

The workflow produces:

* Bathymetric interpretation maps
* Synthetic seabed scenarios
* Geohazard sensitivity maps
* Engineering suitability classifications
* Spatial driver decomposition layers
* Lease-scale visualization products

These outputs are directly usable within future planning and decision-support workflows.


## Engineering Applications

The workflow supports:

* Early-stage site screening
* Layout planning studies
* Geohazard-informed anchor positioning
* Investigation campaign planning
* Risk-informed engineering reviews
* Future optimization workflows

This enables:

**Geohazard Awareness → Planning Intelligence → Better Engineering Decisions**


## Relationship to Other Morie Study Cases

This study establishes the geohazard planning extension of the Morie ecosystem.

### Receives from

* **morie_site** → bathymetry and engineering domain
* **morie_layout** → spatial infrastructure context
* **morie_soil** → reconstructed subsurface framework
* **morie_seismic** → degradation-aware geohazard concepts

### Feeds into

* Future layout and cable routing optimization workflows
* Risk-informed engineering studies
* Geohazard-aware design strategies
* Lease-scale planning frameworks
* Future anchor suitability mapping

It provides the transition from:

> Site characterization

toward:

> Geohazard-aware offshore planning.


## Why It Matters Commercially?

* Introduces geohazard awareness earlier in the project lifecycle
* Supports risk-informed planning decisions
* Improves visibility of spatial variability across the lease
* Helps prioritize future investigation efforts
* Preserves interoperability with integrated engineering workflows
* Bridges site characterization and planning intelligence

This is where:

* Site characterization becomes actionable
* Geohazard assessment becomes spatial
* Planning becomes engineering-informed


## Aspects to Improve

* Integration of measured geohazard inventories
* Time-dependent seabed evolution scenarios
* Dynamic sediment transport representations
* Anchor suitability mapping
* Geohazard-aware layout constraints and masks
* Coupled geohazard–layout optimization
* Probabilistic uncertainty assessment
* Multi-hazard interaction frameworks
* Full-domain lease-scale deployment

These developments would progressively transform geohazard screening into engineering decision layers capable of supporting anchor placement, cable routing and future layout optimization studies.


## Design Philosophy

This study reflects the Morie Analytics approach:

* **Physics-informed**: screening layers remain grounded in engineering interpretation of seabed conditions.
* **Mechanism-aware**: the workflow preserves links between morphology, subsurface variability and engineering consequence.
* **Interpretable**: sensitivity maps can be decomposed into their contributing drivers.
* **Reproducible**: all workflows are configuration-driven and traceable.
* **Scalable**: the methodology can be extended to larger offshore domains and future planning studies.
* **Site-conditioned**: all analyses remain tied to the reconstructed Celtic Sea engineering environment.
