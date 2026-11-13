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

**Cooling Riyadh** examines how urban heat, vegetation, population, and the built environment vary across Riyadh, Saudi Arabia.

The project combines satellite imagery, population estimates, building footprints, spatial analysis, machine learning, and interactive mapping. The main objective is to identify parts of Riyadh where high surface temperatures, limited vegetation, population exposure, and urban development overlap.

> **Research Question:**  
> Where are the hottest and least vegetated populated areas in Riyadh, and which areas could be prioritized for further evaluation of urban greening interventions?

---

## Study Area

The study focuses on the urban area of **Riyadh, Saudi Arabia**.

The study boundary was derived from the **Copernicus Global Human Settlement Urban Centre Database (GHS-UCDB)** and was used to clip and organize the spatial datasets used throughout the project.

---

## Data Sources

| Dataset | Purpose | Source |
|---|---|---|
| Landsat Collection 2 Level-2 | Land Surface Temperature and NDVI | U.S. Geological Survey |
| WorldPop 2026 | Estimated population distribution | WorldPop |
| Microsoft Building Footprints | Building count, footprint area, and coverage | Microsoft |
| GHS Urban Centre Database | Riyadh study boundary | Copernicus / European Commission |

The datasets were processed and integrated using a common **500 m × 500 m analysis grid** so that variables from different sources could be compared at the same spatial scale.

---

## Analysis Workflow

The analysis was completed in five main stages: data preparation, satellite processing, built-environment analysis, population integration, and spatial modeling.

### 1. Data Preparation

Spatial datasets were cleaned, checked, reprojected where necessary, and clipped to the Riyadh study boundary.

### 2. Satellite Processing

Landsat Collection 2 Level-2 imagery was used to calculate:

- **Land Surface Temperature (LST)**
- **Normalized Difference Vegetation Index (NDVI)**

Quality Assessment information was used to exclude invalid pixels and reduce the effect of clouds.

### 3. Built Environment Analysis

Microsoft Building Footprints were clipped to Riyadh and summarized within the 500 m analysis grid.

For each grid cell, the following variables were calculated:

- Building count
- Total building footprint area
- Building coverage percentage

### 4. Population Exposure

WorldPop population estimates were summarized within the same 500 m grid.

This makes it possible to compare population exposure with heat, vegetation, and building conditions using one consistent spatial unit.

### 5. Final Spatial Dataset

After integrating the different datasets, the final analysis contained approximately:

**4,700 valid 500 m grid cells**

Each valid cell includes information on:

- Surface temperature
- Vegetation
- Population
- Building intensity

---

## Machine Learning

### K-Means Urban Clustering

K-Means clustering was used to explore whether grid cells with similar environmental and urban characteristics could be grouped together.

Four standardized variables were included in the clustering:

1. Mean Land Surface Temperature
2. Mean NDVI
3. Population
4. Building Coverage Percentage

Several cluster counts were examined before selecting a final model with **five urban profiles**.

The five profiles were interpreted as:

- **Hot Dense Built-Up**
- **Dense Populated Urban**
- **Hot Low-Density Peripheral**
- **Greener Cooler Areas**
- **Cooler Lower-Density**

These names were assigned after reviewing the characteristics of each cluster. They are descriptive labels rather than official land-use classifications.

---

## Greening Priority Screening

A separate priority score was calculated to identify grid cells where several conditions occur together:

- Higher surface temperature
- Lower vegetation
- Higher population
- Greater building coverage

The weighting framework used in the project is:

| Indicator | Weight |
|---|---:|
| High Land Surface Temperature | 35% |
| Low Vegetation | 30% |
| Population Exposure | 25% |
| Building Coverage | 10% |

The final score was divided into five relative priority classes:

- Very Low
- Low
- Moderate
- High
- Very High

### Interpretation

The priority score is intended as a **screening tool**.

It does not mean that every high-priority grid cell should automatically receive new trees or other greening interventions.

The weights were selected for this project and were not statistically estimated. The results are therefore most useful for identifying areas that may deserve additional investigation.

---

## AI-Assisted Priority Interpretation

The K-Means clusters were compared with the independently calculated priority classes to examine whether particular urban profiles were more frequently associated with high-priority areas.

The largest shares of **High** and **Very High** priority cells occurred within:

- **Hot Dense Built-Up**
- **Dense Populated Urban**

K-Means was used only to identify recurring urban profiles.

The priority score was calculated separately using the weighted indicators described above.

The clustering therefore helps interpret the priority results, but it does not generate or predict the priority score.

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

A Quarto website was developed to present the main maps, results, and methods from the project.

### Urban Heat

Shows the spatial distribution of Landsat-derived Land Surface Temperature across Riyadh.

### Vegetation & Buildings

Includes interactive maps of NDVI and building coverage.

### Population Exposure

Shows estimated population within the 500 m analysis grid.

### AI & Priority Areas

Includes interactive maps of:

- K-Means urban profiles
- Cluster-priority associations
- Greening priority levels

### Methods & Data

Documents the data sources, workflow, assumptions, machine-learning approach, weighting framework, and main limitations.

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
├── .gitignore
└── README.md
```

---

## Main Analytical Notebooks

### `01_data_setup_and_building_footprints.ipynb`

This notebook contains the main data-preparation workflow, including:

- Riyadh boundary preparation
- Microsoft Building Footprint processing
- Population integration
- Landsat processing
- NDVI calculation
- Land Surface Temperature calculation
- 500 m grid construction
- Dataset integration
- Exploratory spatial analysis

### `02_ai_clustering_and_priority_analysis.ipynb`

This notebook contains:

- Variable preparation
- Standardization
- K-Means evaluation
- Final five-cluster model
- Cluster interpretation
- Weighted priority calculation
- Priority classification
- Static analytical maps

### `03_interactive_web_maps.ipynb`

This notebook creates interactive maps for:

- Land Surface Temperature
- Vegetation
- Building coverage
- Population
- K-Means clusters
- Greening priority

### `04_ai_assisted_priority_analysis.ipynb`

This notebook compares the K-Means urban profiles with the final priority classes and examines how strongly each profile is associated with High and Very High priority areas.

---
## Technology Stack

### Geospatial Analysis

- **Python** — primary programming language for the geospatial data science workflow.
- **GeoPandas** — used for vector spatial data, including the Riyadh boundary, the 500 m analysis grid, building footprints, and spatial operations.
- **Rasterio** — used to read and process raster datasets, including Landsat imagery, NDVI, Land Surface Temperature, and WorldPop population data.
- **QGIS** — used to inspect spatial datasets, review coordinate systems and layers, visualize intermediate results, and perform quality checks on spatial outputs.

### Data Analysis & Machine Learning

- **Pandas** — used for tabular data preparation, integration, summary statistics, and CSV outputs.
- **NumPy** — used for numerical calculations and array operations throughout the analysis.
- **Scikit-learn** — used for StandardScaler and K-Means clustering to identify recurring urban profiles across Riyadh.

### Visualization

- **Matplotlib** — used to create static analytical figures and maps within the notebooks.
- **Folium** — used to create the interactive maps presented on the project website.

### Development & Workflow

- **Jupyter Notebook** — used to organize and run the main analytical workflow across the project notebooks.
- **Quarto** — used to build and render the bilingual project website.
- **GitHub / GitHub Desktop** — used for version control, repository management, project documentation, and deployment through GitHub Pages.

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

The notebooks are organized in the following order:

```text
01 → Data preparation and integration
02 → Machine learning and priority analysis
03 → Interactive maps
04 → Cluster-priority interpretation
```

The Quarto website can be rendered from the `website` directory using:

```bash
quarto render
```

For a local preview:

```bash
quarto preview
```

---

## Limitations

### Satellite Timing

The Land Surface Temperature results represent conditions observed during the selected Landsat scenes rather than a continuous or long-term record of urban heat.

### Spatial Resolution

The 500 m grid provides a common unit for combining several datasets, but it also generalizes smaller variations that may occur within individual cells.

### Population Estimates

WorldPop provides modeled population estimates rather than official neighborhood-level census counts.

### Building Footprints

Building footprint coverage represents the horizontal area occupied by mapped buildings. It does not account for building height, occupancy, construction materials, or energy use.

### Priority Weights

The priority weights were selected for this project and were not estimated from observed intervention outcomes.

### Intervention Suitability

A High or Very High priority score does not automatically mean that a location is suitable for tree planting.

Additional information would be needed before any intervention, including land ownership, utilities, water availability, street design, infrastructure constraints, and implementation feasibility.

---

## Academic Context

This project was developed for:

**MUSA 5500 — Geospatial Data Science in Python**  
Master of Urban Spatial Analytics  
Weitzman School of Design  
University of Pennsylvania

The project applies several methods covered in geospatial data science, including:

- Raster processing
- Vector analysis
- Integration of multiple spatial datasets
- Machine learning
- Spatial prioritization
- Interactive web mapping
- Reproducible notebook workflows

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

This repository contains code and derived project outputs developed for academic purposes.

The original datasets remain subject to the terms and licensing conditions of their respective providers:

- U.S. Geological Survey
- WorldPop
- Microsoft
- Copernicus / European Commission

Source datasets should be obtained from the original providers where required.