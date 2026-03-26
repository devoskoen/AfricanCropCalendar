# Malawi LSMS Data Processing Pipeline

This document outlines the workflow for processing multi-wave Malawi LSMS data using the `main_Mw_allWaves.py` Python script. The process includes several key stages:

## Overview

The processing pipeline incorporates the following steps:
1. **DTA to CSV Conversion:**  Using Stata 18, raw .DTA files are transformed into .CSV format for easier ingestion and processing.
2. **LSMS CSV Ingestion:** The CSV files generated from the previous step are ingested into the system for further analysis.
3. **Data Cleaning:** This stage ensures that the data is accurate and usable by removing inconsistencies and handling missing values.
4. **Variable Harmonization:** Different variables from multiple waves are standardized to ensure uniformity across datasets.
5. **Household-level Aggregation:** Data is aggregated at the household level for more manageable analysis.
6. **Metadata Generation:** Metadata files are created to provide context about the data, ensuring better understanding and usability.

## Modular Folder Structure

The script executes in a defined folder structure:
- `ingest_Stata_files`: Contains raw Stata files for ingestion.
- `ingest_csv_files`: Holds the final CSV files after conversion from Stata.
- `processing`: Where data cleaning, harmonization, and aggregation are conducted.
- `out`: The directory where processed outputs are copied for final review.

## Usage

To run the `main_Mw_allWaves.py` script, ensure all necessary dependencies are installed and execute the script from the command line. The script will automatically navigate the folder structure and perform all tasks sequentially as outlined in the pipeline.

## Conclusion

This pipeline facilitates a streamlined approach to processing and analyzing multi-wave LSMS data for Malawi, ensuring data accuracy and consistency for further research and analysis.

---

**Date of Documentation:** 2026-03-26 08:42:47 (UTC)

**Author:** koendvos