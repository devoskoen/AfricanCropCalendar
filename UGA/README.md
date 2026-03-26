# Uganda Crop Calendar Scripts

This directory contains R scripts for processing survey data from Uganda across multiple waves for the UNPS (Uganda National Panel Survey). The scripts extract and harmonize agricultural data in preparation for analysis.

## Scripts Overview

### Wave-Specific Scripts

1. **UgandaMulti11.R**
   - Processes the first wave of survey data.
   - Extracts household information and GPS coordinates from the geovariables file.
   - Handles first and second visit data related to agricultural seasons.
   - Merges planting and harvesting information.
   - Creates seasonal identifiers to standardize data across agricultural seasons.
   - Converts plot areas from acres to hectares.
   - Generates a harmonized CSV with:
     - Administrative divisions
     - Household and plot identifiers
     - Crop information
     - Planting and harvest dates
     - Plot areas

2. **UgandaMulti13.R**
   - Processes the second wave of survey data (similar functionalities as above).

3. **UgandaMulti15.R**
   - Processes the third wave of survey data (similar functionalities as above).

4. **UgandaMulti18.R**
   - Processes the fourth wave of survey data (similar functionalities as above).

5. **UgandaMulti19.R**
   - Processes the fifth wave of survey data (similar functionalities as above).

### Consolidation Script

- **UGA_create_allwaves.R**
   - Consolidates all the waves and associated metadata files into single output files.
   - Facilitates cross-country merging of data, ensuring uniformity and compatibility for further analysis.

## Usage

To run the scripts, ensure you have the required R packages installed. The workflow follows:
1. Download the corresponding UNPS data files.
2. Run the wave-specific scripts in sequence to prepare the data for a unified output.
3. Use the `UGA_create_allwaves.R` script to consolidate all outputs into a single dataset suitable for cross-country analysis.

### Note

Ensure to check file paths and required input data formats when using the scripts. Each script is designed to handle specific versions of the UNPS survey data, and their output should be verified for correctness and completeness after execution.
