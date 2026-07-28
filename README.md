# RELMS: Green Hydrogen Logistics Hub Feasibility Index for Mexico

This repository contains the data processing, spatial econometrics workflow, and validation framework for constructing a municipal-level **Green Hydrogen Logistics Hub Feasibility Index** in Mexico.

The composite framework evaluates $2,400+$ Mexican municipalities across five core dimensions (**RELMS**): **R**esources, **E**nergy, **L**ogistics, **M**arket, and **S**afety (crime-risk).

### Contact & Support
For questions, collaborations, or suggestions, feel free to contact:

**Franco Josué Patiño Morales, M.Sc.**
- Email: franco.jpm@gmail.com

### Citation
If you use this repository or its data instances in academic work, please cite it as follows:

> Franco Josué Patiño Morales. (2026). Hydrogen Hub Index [GitHub Repository]. https://github.com/FrancoJPM1991/hydrogen-hub-index.git 

*Related journal article:*
- []


## Overview & Methodology

Green hydrogen infrastructure development requires balancing resource availability with logistical accessibility, industrial demand, grid integration, and institutional/operational risk. This project introduces a spatial multi-criteria decision-making framework aggregated via a **Geometric Mean** to prevent full substitutability across dimensions.

$$\text{RELMS}_{i} = \left( R_i \times E_i \times L_i \times M_i \times S_i \right)^{\frac{1}{5}}$$

### The 5 Sub-Indexes

1. **Resources ($R$):** Municipal access to groundwater availability, annual rainfall, wind power density, and photovoltaic potential (PVOUT).
2. **Energy ($E$):** Distance and connection feasibility to the Mexican National Electric Grid (SEN).
3. **Logistics ($L$):** Density of railway and highway networks, along with proximity to strategic infrastructure (Border Crossings, Deepwater Ports, and the **Helax Istmo Green Hydrogen Project** in the CIIT corridor).
4. **Market ($M$):** Density of manufacturing/industrial economic units (DENUE) and net municipal productive economic output.
5. **Safety ($S$):** Incidence of cargo/logistics-related violent and property crimes (evaluating operational risk).



## Core Analytical Pipeline

1. **Spatial Aggregation & Normalization:** Feature extraction from raw geospatial layers (`.shp`, `.tif`, `.csv`) to municipal centroids and boundaries, followed by min-max dimension scoring.
2. **Impact of Crime Integration (Wilcoxon Test):** Evaluated structural rank shifts between non-safety ($RELM$) and safety-inclusive ($RELMS$) formulations using a paired Wilcoxon signed-rank test ($p < 0.05$).
3. **Exploratory Spatial Data Analysis (ESDA):** Calculated Global Moran’s $I$ and Local Indicators of Spatial Association (LISA) to detect spatial clusters ($HH$, $LL$) and spatial outliers ($HL$, $LH$).
4. **Validation Suite:**
   - **Dimensionality:** Principal Component Analysis (PCA) to evaluate variance explained and factor loadings.
   - **Aggregation Sensitivity:** Geometric Mean vs. Arithmetic Mean comparison.
   - **Criterion/Face Validation:** LISA spatial overlay against real-world hydrogen project announcements (e.g., CIIT / Helax).
   - **MCDA Robustness:** Benchmark comparison of Geometric Mean against **TOPSIS** (Technique for Order of Preference by Similarity to Ideal Solution).

## Getting Started

Follow the instructions below to set up your environment, install dependencies, and run the pipeline notebooks in the correct sequence.

### Prerequisites
Make sure you have Python 3.8+ installed on your system.

### Installation
```bash
# Clone the repository
git clone [https://github.com/your-username/hydrogen-hub-index.git]
cd hydrogen-hub-index

# Create and activate a virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install required dependencies
pip install -r requirements.txt
```

### Key Libraries Used
1. **Geospatial Processing:** geopandas, shapely, rasterio, pyproj
2. **Spatial Econometrics & ESDA:** pysal, esda, splot
3. **Data Analysis & MCDA:** pandas, numpy, scikit-learn, scipy
4. **Visualization:** matplotlib, seaborn

### Key Workflow Execution Order
To reproduce the analysis from raw data to validation and figure generation, execute the Jupyter notebooks in \texttt{notebooks/} in the following numerical order:
1. **01_data_cleaning/ (01a through 01g):** Clean raw GIS shapefiles, rasters, and tabular datasets to compute municipal-level metrics (e.g., distances, infrastructure density, resources, and crime counts).
2. **02_transformation_and_merge/:** Join all spatial indicators into a single master dataset (master_merged.csv).
3. **03_dimension_scoring/:** Apply min-max normalization and scale sub-indexes across the five RELMS dimensions.
4. **04_final_index_composition/:** Compute composite $RELM$ and $RELMS$ feasibility scores using the geometric mean.
5. **05_exploratory_spatial_data_analysis/:** Calculate Global Moran’s $I$ and compute Local Indicators of Spatial Association (LISA).
6. **06_visualization_and_maps/:** Render spatial distribution maps, LISA cluster maps, and comparative figures saved to results/maps/.
7. **07_inferential_analysis/:** Run the paired Wilcoxon signed-rank test comparing $RELM$ vs. $RELMS$ to quantify the statistical effect of including crime data.
8. **08_validation/:** Conduct validation tests including PCA variance analysis, geometric vs. arithmetic aggregation sensitivity, spatial face validation, and benchmark comparison against TOPSIS.



## Repository Structure

```text
hydrogen-hub-index/
├── data/
│   ├── raw/                  
│   ├── interim/              
│   └── processed/            
├── notebooks/
│   ├── 01_data_cleaning/     
│   ├── 02_transformation_and_merge/ 
│   ├── 03_dimension_scoring/# Min-max scoring and feature scaling
│   ├── 04_final_index_composition/   
│   ├── 05_exploratory_spatial_data_analysis/ 
│   ├── 06_visualization_and_maps/    
│   ├── 07_inferential_analysis/      
│   └── 08_validation/        
├── results/
│   ├── esda/                 
│   ├── inferential/          
│   ├── maps/                 
│   └── validation/   
├── .gitignore
├── LICENSE        
├── requirements.txt          
└── README.md
```