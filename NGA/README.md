# Nigeria GHS Processing Pipelines

This repository contains scripts and resources for processing Nigeria's GHS (General Household Survey) data across multiple survey waves.

## Description
This provides a detailed overview of the processing done for Nigeria's multi-wave GHS data.

## Main Entry Points
The main Stata scripts for executing the processing are located at:
- `/NGA/Nigeria_GHS_W3.do` - Processing script for Wave 3 data
- `/NGA/Nigeria_GHS_W4.do` - Processing script for Wave 4 data

These scripts handle the data processing, harmonization, and analysis for each survey wave.

## Contents
- **/rawData-wave3/**: Directory containing raw GHS Wave 3 datasets
- **/rawData-wave4/**: Directory containing raw GHS Wave 4 datasets
- **/temp**: Temporary directory for intermediate processing files
- **Nigeria_GHS_W3.do**: Main processing script for Wave 3
- **Nigeria_GHS_W4.do**: Main processing script for Wave 4
- **NGA_2016_metadata.csv**: Metadata for 2016 wave
- **NGA_2018_metadata.csv**: Metadata for 2018 wave
- **Nigeria_GHS_W4_metadata.xlsx**: Metadata for Wave 4
- **Nigeria_GHS_W3_results.csv**: Output results from Wave 3 processing
- **Nigeria_GHS_W4_results.csv**: Output results from Wave 4 processing

## Usage
1. Clone the repository:  
   `git clone https://github.com/koendvos/AfricanCropCalendar.git`  
2. Change directory:  
   `cd AfricanCropCalendar/NGA`  
3. Ensure raw data files are in the appropriate `rawData-wave*` directories  
4. Run the main processing script:  
   `stata -b do Nigeria_GHS_W3.do` or `stata -b do Nigeria_GHS_W4.do`