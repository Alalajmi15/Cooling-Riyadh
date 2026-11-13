<p align="center">
  <img src="website/assets/images/cooling-riyadh-logo.png" alt="Cooling Riyadh Logo" width="520">
</p>

<h1 align="center">Cooling Riyadh</h1>

<p align="center">
  <strong>Mapping Urban Heat and Greening Priorities in Riyadh</strong><br>
  A Geospatial Data Science Approach
</p>

---

## Project Overview

**Cooling Riyadh** is a geospatial data science project examining the spatial relationship between urban heat, vegetation, population exposure, and the built environment across Riyadh, Saudi Arabia.

The project integrates satellite imagery, population estimates, building footprints, spatial analytics, machine learning, and interactive web mapping to identify areas that may warrant further evaluation for urban greening and heat-mitigation interventions.

> **Research Question:**  
> Where are the hottest and least vegetated populated areas in Riyadh, and which areas could be prioritized for further evaluation of urban greening interventions?

---

## Study Area

The project focuses on the urban area of **Riyadh, Saudi Arabia**.

A Riyadh urban boundary derived from the **Copernicus Global Human Settlement Urban Centre Database (GHS-UCDB)** is used to define the study extent and spatially constrain the analysis.

---

## Data Sources

| Dataset | Purpose | Source |
|---|---|---|
| Landsat Collection 2 Level-2 | Land Surface Temperature and NDVI | U.S. Geological Survey |
| WorldPop 2026 | Estimated population distribution | WorldPop |
| Microsoft Building Footprints | Building count, footprint area, and coverage | Microsoft |
| GHS Urban Centre Database | Riyadh study boundary | Copernicus / European Commission |

All datasets were transformed, clipped, standardized, and spatially integrated for analysis at the **500 m × 500 m grid-cell level**.

---

## Analytical Framework

The project follows a complete geospatial data science workflow.

### 1. Data Preparation

Raw spatial datasets were cleaned, validated, reprojected, and clipped to the Riyadh study boundary.

### 2. Satellite Processing

Landsat Collection 2 Level-2 imagery was processed to derive:

- **Land Surface Temperature (LST)**
- **Normalized Difference Vegetation Index (NDVI)**

Quality Assessment information was used to reduce the influence of clouds and invalid pixels.

### 3. Built Environment Analysis

Microsoft Building Footprints were spatially filtered to Riyadh and aggregated to the analysis grid.

For each 500 m cell, the analysis calculated:

- Building count
- Total building footprint area
- Building coverage percentage

### 4. Population Exposure

WorldPop population estimates were integrated into the same spatial grid to estimate the population represented within each analysis cell.

### 5. Spatial Data Integration

The final analytical dataset contains approximately:

**4,700 valid 500 m grid cells**

with integrated measurements for:

- Surface temperature
- Vegetation
- Population
- Building intensity

---

## Machine Learning

### K-Means Urban Clustering

K-Means clustering was used as the project's primary unsupervised machine-learning component.

Four standardized variables were used:

1. Mean Land Surface Temperature
2. Mean NDVI
3. Population
4. Building Coverage Percentage

After evaluating alternative cluster counts, the final model uses **five urban cluster profiles**:

- **Hot Dense Built-Up**
- **Dense Populated Urban**
- **Hot Low-Density Peripheral**
- **Greener Cooler Areas**
- **Cooler Lower-Density**

The clustering is used to identify recurring urban environmental profiles rather than predefined administrative or land-use categories.

---

## Greening Priority Screening

A spatial multicriteria priority score was developed to identify locations combining environmental heat, limited vegetation, population exposure, and built-environment intensity.

### Priority Weights

| Indicator | Weight |
|---|---:|
| High Land Surface Temperature | 35% |
| Low Vegetation | 30% |
| Population Exposure | 25% |
| Building Coverage | 10% |

The resulting score was classified into five relative priority levels:

- Very Low
- Low
- Moderate
- High
- Very High

### Important Interpretation

The priority score is a **spatial screening framework**, not a direct tree-planting recommendation.

The weights are analyst-defined rather than statistically estimated and should therefore be interpreted as a transparent decision-support framework for identifying locations requiring additional investigation.

---

## AI-Assisted Priority Interpretation

The machine-learning clusters and the independently calculated priority score were compared to evaluate how strongly different urban profiles are associated with high-priority areas.

The strongest associations were observed within:

- **Hot Dense Built-Up**
- **Dense Populated Urban**

This step supports interpretation of the spatial priority results.

It does **not** replace, predict, or recalculate the priority score.

This distinction is important because the K-Means model represents the project's machine-learning component, while the priority index represents a separate weighted spatial decision-support framework.

---

## Key Project Metrics

| Metric | Value |
|---|---:|
| Core Data Sources | 4 |
| Final Analysis Cells | 4,700 |
| Spatial Analysis Grid | 500 m |
| Urban Cluster Profiles | 5 |
| Mean LST | ~51.1 °C |
| Observed LST Range | ~40.7–57.7 °C |
| Estimated Population Represented | ~6.28 million |

---

## Interactive Web Visualization

The project includes an interactive web-based visualization platform developed with **Quarto**.

The website contains the following sections:

### Urban Heat

Interactive visualization of Landsat-derived surface temperature patterns across Riyadh.

### Vegetation & Buildings

Exploration of NDVI and building coverage across the city.

### Population Exposure

Spatial visualization of estimated population within the 500 m analysis grid.

### AI & Priority Areas

Interactive exploration of:

- K-Means urban cluster profiles
- AI-assisted priority associations
- Greening priority screening

### Methods & Data

Documentation of datasets, workflow, weighting assumptions, machine-learning methods, and study limitations.

**Live Website:** GitHub Pages link will be added after deployment.

---

## Repository Structure

```text
Final Project/
│
├── Data/
│   ├── boundary/
│   ├── landsat/
│   ├── Population/
│   └── building_footprints/
│
├── notebooks/
│   ├── 01_data_setup_and_building_footprints.ipynb
│   ├── 02_ai_clustering_and_priority_analysis.ipynb
│   ├── 03_interactive_web_maps.ipynb
│   └── 04_ai_assisted_priority_analysis.ipynb
│
├── outputs/
│   ├── rasters/
│   ├── Riyadh_500m_Final_Analysis_Grid.gpkg
│   ├── Riyadh_500m_Final_Analysis_Table.csv
│   ├── Riyadh_500m_Clustering_and_Greening_Priority.gpkg
│   └── Riyadh_500m_Clustering_and_Greening_Priority.csv
│
├── scripts/
│
├── website/
│   ├── assets/
│   │   ├── images/
│   │   └── maps/
│   ├── index.qmd
│   ├── urban-heat.qmd
│   ├── vegetation-buildings.qmd
│   ├── population.qmd
│   ├── priority.qmd
│   ├── methods.qmd
│   ├── styles.css
│   └── _quarto.yml
│
└── README.md
```

---

## Main Analytical Notebooks

### `01_data_setup_and_building_footprints.ipynb`

Primary geospatial data pipeline:

- Riyadh boundary preparation
- Microsoft Building Footprint processing
- Population integration
- Landsat processing
- NDVI calculation
- Land Surface Temperature calculation
- 500 m analysis-grid construction
- Final dataset integration
- Exploratory spatial analysis

### `02_ai_clustering_and_priority_analysis.ipynb`

Contains:

- Variable preparation
- Standardization
- K-Means evaluation
- Five-cluster model
- Urban-profile interpretation
- Weighted priority framework
- Priority classification
- Final analytical maps

### `03_interactive_web_maps.ipynb`

Produces interactive web maps for:

- Land Surface Temperature
- Vegetation
- Building coverage
- Population
- K-Means clusters
- Greening priority

### `04_ai_assisted_priority_analysis.ipynb`

Evaluates the relationship between machine-learning-derived urban profiles and the spatial priority framework.

---

## Technology Stack

### Spatial Analysis

- Python
- GeoPandas
- Rasterio
- Shapely
- PyProj
- Rasterstats

### Data Analysis & Machine Learning

- Pandas
- NumPy
- Scikit-learn
- SciPy

### Visualization

- Matplotlib
- Folium
- Branca

### Web Development

- Quarto
- HTML
- CSS

### Spatial Data Formats

- GeoPackage
- GeoTIFF
- CSV

---

## Reproducibility

The project uses a dedicated Conda environment:

```bash
conda activate cooling-riyadh
```

The analytical workflow should be executed in notebook order:

```text
01 → Data preparation and integration
02 → Machine learning and priority analysis
03 → Interactive maps
04 → AI-assisted interpretation
```

The Quarto website can then be rendered from the `website` directory using:

```bash
quarto render
```

For local preview:

```bash
quarto preview
```

---

## Methodological Limitations

Several limitations should be considered when interpreting the project results.

### Satellite Timing

Land Surface Temperature represents conditions captured by selected Landsat observations rather than continuous long-term thermal conditions.

### Spatial Resolution

The 500 m analysis grid improves cross-dataset integration but generalizes fine-scale variation within individual cells.

### Population Estimates

WorldPop represents modeled population estimates rather than official neighborhood-level census counts.

### Building Footprints

Building coverage represents mapped footprint geometry and does not directly account for building height, occupancy, materials, or energy use.

### Priority Weights

The weighting framework is analyst-defined and intended for transparent spatial screening rather than causal inference.

### Intervention Suitability

High-priority cells do not automatically represent suitable locations for tree planting or other interventions. Local land ownership, infrastructure, water availability, urban design, utilities, and implementation feasibility require additional investigation.

---

## Academic Context

This project was developed as part of:

**MUSA 5500 — Geospatial Data Science in Python**  
Master of Urban Spatial Analytics  
Weitzman School of Design  
University of Pennsylvania

The project demonstrates a complete geospatial data science workflow integrating:

- Raster analysis
- Vector analysis
- Multiple spatial datasets
- Machine learning
- Spatial decision-support analysis
- Interactive web mapping
- Reproducible analytical notebooks

---

## Author

### Alhaylam Fahad Alajmi

**Civil Engineer · Urban Spatial Analytics Graduate Student**

Master of Urban Spatial Analytics  
University of Pennsylvania

B.S. Civil Engineering  
Texas A&M University

Professional background:

- WSP — Green Riyadh
- Bechtel — NEOM

Professional certifications:

- PMP
- PMI-RMP
- P3O Foundation

Areas of interest:

**Smart Cities · GIS · Urban Analytics · Geospatial Data Science · AI-Enabled Urban Decision-Making**

---

## Project Status

- **Analysis:** Complete
- **Interactive Maps:** Complete
- **Web Visualization:** Complete
- **Final Deployment:** In preparation
- **Academic Presentation & Report:** In preparation

---

## Data Attribution

This repository contains analytical code and project outputs developed for academic purposes.

Original third-party datasets remain subject to the terms and licensing conditions of their respective providers, including:

- U.S. Geological Survey
- WorldPop
- Microsoft
- Copernicus / European Commission

Users should consult the original data providers before redistributing source datasets.