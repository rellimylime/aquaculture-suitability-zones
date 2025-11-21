# Prioritizing Marine Aquaculture Locations on the US West Coast

## About

This repository contains a geospatial analysis identifying optimal locations for marine aquaculture development along the US West Coast. The analysis evaluates Exclusive Economic Zones (EEZs) based on species-specific sea surface temperature and depth requirements to determine which areas are most suitable for oyster farming and other marine aquaculture operations.

**Analysis Objectives:**
- Identify suitable marine aquaculture locations based on sea surface temperature and depth criteria
- Calculate total suitable area within each West Coast EEZ
- Rank EEZs by their aquaculture potential for multiple species
- Create a generalizable workflow for assessing suitability for different species

## Repository Structure
```
aquaculture-suitability-zones/
│
├── README.md
├── .gitignore
├── aquaculture-suitability-zones.Rproj
├── aquaculture_analysis.qmd
│
└── data/
    ├── wc_regions_clean.shp
    ├── depth.tif
    ├── average_annual_sst_2008.tif
    ├── average_annual_sst_2009.tif
    ├── average_annual_sst_2010.tif
    ├── average_annual_sst_2011.tif
    └── average_annual_sst_2012.tif
```

**Note:** The `data/` folder is included in `.gitignore` and is not tracked by version control due to file size. See below for data access instructions.

## Data

### Access

1. Download the data folder from [this link](https://drive.google.com/file/d/1u-iwnPDbe7ZG1F_wPM8xyD85q6XD1CKY/view?usp=sharing)
2. Unzip the downloaded folder
3. Place the unzipped data into a `data/` folder in the root directory of this repository
4. Verify the folder structure matches the Repository Structure shown above

### Data Sources

**Sea Surface Temperature (SST)**
- Average annual sea surface temperature data from 2008-2012
- Source: NOAA 5km Daily Global Satellite Sea Surface Temperature Anomaly v3.1
- Files: `average_annual_sst_2008.tif` through `average_annual_sst_2012.tif`
- Units: Kelvin (converted to Celsius in analysis)
- Resolution: ~5km

**Bathymetry (Depth)**
- Global ocean depth measurements
- Source: General Bathymetric Chart of the Oceans (GEBCO) 2022 Grid
- File: `depth.tif`
- Citation: GEBCO Compilation Group (2022) GEBCO_2022 Grid (doi:10.5285/e0f0bb80-ab44-2739-e053-6c86abc0289c)
- Units: Meters below sea level

**Exclusive Economic Zones (EEZ)**
- Maritime boundaries for US West Coast
- Source: MarineRegions.org
- File: `wc_regions_clean.shp`
- Region: West Coast United States (California, Oregon, Washington)

### Species Requirements

**Oysters** *(Crassostrea spp.)*
- Sea surface temperature: 11-30°C
- Depth range: 0-70 meters below sea level
- Source: SeaLifeBase

**Black Abalone** *(Haliotis cracherodii)*
- Sea surface temperature: 12.2-18.6°C
- Depth range: 0-6 meters below sea level
- Source: SeaLifeBase

## Methodology

The analysis workflow includes:

1. **Data Preparation:** Load and harmonize SST, bathymetry, and EEZ data to consistent coordinate reference systems
2. **SST Processing:** Calculate mean SST from 2008-2012 and convert from Kelvin to Celsius
3. **Spatial Alignment:** Resample depth data to match SST resolution and extent using nearest neighbor interpolation
4. **Suitability Analysis:** Reclassify SST and depth layers based on species-specific requirements
5. **Site Identification:** Apply map algebra to identify locations meeting both temperature and depth criteria
6. **Area Calculation:** Determine total suitable area within each EEZ
7. **Ranking:** Prioritize EEZs based on total suitable aquaculture area

The analysis is implemented as a generalizable function that accepts species-specific parameters (temperature range, depth range, species name) and produces ranked suitability maps.

## Author

Emily Miller

[GitHub](https://github.com/rellimylime)

## Course Information

This analysis was completed for **EDS 223: Geospatial Analysis and Remote Sensing** at the Bren School of Environmental Science & Management, UC Santa Barbara.

- **Instructor:** Annie Adams
- **Assignment:** Homework 4 - Prioritizing Potential Aquaculture
- **Date:** November 2025

## References

- Gentry, R. R., Froehlich, H. E., Grimm, D., Kareiva, P., Parke, M., Rust, M., Gaines, S. D., & Halpern, B. S. (2017). Mapping the global potential for marine aquaculture. *Nature Ecology & Evolution*, 1, 1317-1324.
- Hall, S. J., Delaporte, A., Phillips, M. J., Beveridge, M. & O'Keefe, M. (2011). *Blue Frontiers: Managing the Environmental Costs of Aquaculture*. The WorldFish Center, Penang, Malaysia.
- Assignment instructions: [EDS 223 Course Website](https://eds-223-geospatial.github.io/assignments/HW4.html)
