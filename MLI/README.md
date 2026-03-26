# Mali EACI and EAC-I Survey Data Processing Documentation

## Overview
The Mali MultiCropping R script processes data from two waves of agricultural surveys in Mali, harmonizing them into a standardized format for cross-wave and cross-country analysis.

## Folder Structure
- **/data** → Raw LSMS survey data per wave (CSV/Excel)
- **/metadata** → Generated metadata files per wave
- **/out** → Final harmonized output files
- **/scripts** → Processing scripts (Mali_MultiCropping.R)

---

## Wave 1: 2014-2015 (EACI - Enquête Communautaire)

### Survey Information
- **Survey Name**: EACI (Enquête Communautaire d'Evaluation de l'Investissement Agricole)
- **Dataset ID**: MLI_2014_EACI_v03_M
- **DOI**: https://doi.org/10.48529/qqam-mn86

### Input Files (in `/data` folder)
- **eaciculture_p1.csv** - Planting module with crop & planting dates
- **eacis3a_p2.csv** - Harvest module with harvest information
- **eaciexploi_p1.csv** - Household & farm exploitation data
- **eaci_geovariables_2014.csv** - GPS coordinates
- **adm_conversion_2014.csv** - Administrative conversion codes
- **mli_crop_code.xlsx** - Mali crop code mappings

### Processing Steps

#### 1. Administrative Division Harmonization
Create lookup tables from adm_conversion_2014.csv:
- **adm1** (Region): Regional names
- **adm2** (Circle): District/circle names
- **adm3** (Commune): Commune names
- Link using Adm_Level codes

#### 2. Household Identification
- Household ID: `hhID = paste(grappe, menage, sep="_")`
- grappe = enumeration area
- menage = household within EA

#### 3. Planting Data (from eaciculture_p1.csv)
- fieldID (s1cq01), plotID (s1cq02)
- crop_code (s1cq03), crop_area_share (s1cq06)
- planting_month (s1cq11b)
- Link crop codes to names using mli_crop_code.xlsx

#### 4. Plot Area (from eaciexploi_p1.csv)
- plot_area_measured (s1bq05a)
- plot_area_reported (s1bq10)
- Convert to hectares

#### 5. Harvest Data (from eacis3a_p2.csv)
- fieldID (s3aq01), plotID (s3aq02)
- harvest_month_begin (s3aq04b)
- harvest_month_end (s3aq07b)

#### 6. Data Consolidation
- Merge planting + harvest by (hhID, fieldID, plotID)
- Merge with household & admin data
- Merge GPS coordinates

### Wave 1 Output
- **out/MLI_2014_2015.csv** - Wave 1 harmonized data
- **out/mali_w1.csv** - Alternative naming

---

## Wave 2: 2017-2018 (EAC-I - Updated Version)

### Survey Information
- **Survey Name**: EAC-I (updated EACI version)
- **Dataset ID**: MLI_2017_EAC-I_v03_M
- **DOI**: https://doi.org/10.48529/0v50-h966

### Input Files (in `/data` folder)
- **eaci17_s11cp1.csv** - Planting module (updated variable names)
- **eaci17_s7fp2.csv** - Harvest module
- **eaci17_s00p1.csv** - Household identification
- **eaci_geovariables_2017.csv** - GPS coordinates (updated)
- **adm_conversion.csv** - Updated administrative codes
- **mli_crop_code.xlsx** - Crop code mappings

### Processing Steps (Wave 2 Specific)

#### 1. Administrative Division Harmonization
- Use updated adm_conversion.csv
- Create lookup tables for region/circle/commune
- Apply using lapply and plyr::join_all

#### 2. Household Identification
- Household ID: `hhID = paste(grappe, exploitation, sep="_")`
- Note: "exploitation" replaces "menage" in Wave 2

#### 3. Planting Data (from eaci17_s11cp1.csv)
- fieldID (s11cq01), plotID (s11cq02)
- crop_code (s11cq03)
- crop_area_share (s11cq07)
- planting_month (s11cq14b)

#### 4. Plot Area (from eaci17_s11bp1.csv)
- plot_area_measured (s11bq07) - already in hectares
- plot_area_reported (s11bq11a)
- Unit flag (s11bq11b): 1=hectares, other=sq meters
- **Conversion**: If >10,000 sq m → divide by 10,000

#### 5. Harvest Data (from eaci17_s7fp2.csv)
- fieldID (s7fq01), plotID (s7fq02)
- harvest_month_begin (s7fq05b), harvest_year_begin (s7fq05c)
- harvest_month_end (s7fq12b), harvest_year_end (s7fq12c)

#### 6. Planting Year Inference
- If planting_month >= 10: planting_year = harvest_year - 1
- Otherwise: planting_year = harvest_year

### Wave 2 Output
- **out/MLI_2017-2018.csv** - Wave 2 harmonized data
- **out/mali_w2.csv** - Alternative naming

---

## Consolidated Output Files

### Combined Outputs
- **out/MLI_allWaves.csv** - All waves consolidated
- **out/mali.csv** - Alternative naming

### Output Columns (All Files)
country, adm1, adm2, adm3, adm4, lat, lon, GPS_level, hhID, fieldID, plotID, crop, season, plot_area_measured_ha, plot_area_reported_ha, plot_area_reported_localUnit, localUnit_area, crop_area_share, planting_year, planting_month, harvest_month, harvest_year, harvest_month_begin, harvest_month_end, harvest_year_begin, harvest_year_end, dataset_name, dataset_doi

---

## Key Data Processing Features

### Area Unit Handling
- **Standard unit**: Hectares
- **Conversions**: 
  - Sq meters → hectares (÷ 10,000)
  - Timad → hectares (÷ 4, if applicable)

### Administrative Hierarchy
- 3-level: Region (adm1) → Circle (adm2) → Commune (adm3)
- Names linked via conversion files
- Consistent across waves

### Crop Processing
- Crop codes → standardized names
- Crop area share as percentage of plot
- Handles multiple crops per plot

### Temporal Data
- Separate begin/end harvest months
- Year inference for planting/harvest
- Seasonal markers

## Dependencies

The Mali_MultiCropping.R script requires:
- R packages: dplyr, tidyverse, readxl, haven, plyr
- Input files placed in `/data` folder
- Reference files: mli_crop_code.xlsx, adm_conversion_*.csv
- Output directories (`/out`, `/metadata`) writable

## Notes for Users

- Ensure all input files match expected naming and format
- Administrative codes must match conversion files
- Cross-wave consolidation requires both waves processed first
- GPS_level = 3 indicates household-level coordinates
- Missing harvest year handled appropriately for each wave
