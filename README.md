# Automatated-Data-Cleaning-and-Validation-script-using-Python


An interactive Python command-line tool powered by `pandas` designed to automate foundational data preprocessing workflows. This script handles file path validation, dynamic format parsing (.csv and .xlsx), duplicate extraction/removal, and datatype-specific missing value imputation.

## Project Overview

In data analytics, clean data is a prerequisite for accurate modeling and reporting. This project provides an automated, repeatable data cleaning solution that accepts raw, messy files and outputs an analysis-ready dataset. It eliminates manual spreadsheet scrubbing by enforcing objective data-cleaning rules programmatically.

## Automated Pipeline Workflow

The script executes a sequential 15-step processing pipeline:
1. **Interactive Ingestion:** Prompts the user for a local data path and a project name identifier.
2. **Path Verification:** Validates environment paths via `os.path.exists()` to prevent runtime crashes.
3. **Dynamic Format Detection:** Sniffs out the file extension to dynamically use the correct reader engine (`pd.read_csv` vs `pd.read_excel`).
4. **Structural Audit (Pre-Cleaning):** Evaluates and outputs the baseline dimensions (`shape`) of the raw dataset.
5. **Duplicate Risk Mitigation:** Scans the dataframe for identical rows, isolates the duplicate records, exports them to a secondary `*_duplicates.csv` audit file for transparency, and cleanly drops them from the primary dataset.
6. **Null Profile Evaluation:** Scans all dimensions and prints a column-by-column breakdown of missing value counts.
7. **Positioned Imputation Strategy:**
   * **Numerical Columns (`int`, `float`):** Preserves data volume by programmatically filling missing values using the column's calculated mathematical average (`mean`).
   * **Categorical/Non-Numerical Columns (`object`):** Maintains categorical integrity by dropping rows where textual identifiers are missing.
8. **Final Pipeline Export:** Verifies that the remaining missing values equal zero, prints the newly optimized dimensions, and saves the pristine file as `*_Clean_data.csv`.

## Tech Stack & Libraries

* **Python 3.x** – Core execution scripting
* **Pandas** – High-performance vector operations, logical filtering, and missing data interpolation
* **Numpy** – Foundation mathematical representations
* **OS & Time** – Environment interaction, system safety locks, and system feedback control
* **Openpyxl & Xlrd** – Behind-the-scenes storage engines for Excel workbook parsing

## Script Demonstration & Sample Log Output

When executed in a standard shell, the program runs interactively as follows:

```text
Welcome!
Please enter dataset path : data/raw_delivery_logs.xlsx
Please enter dataset name : logistics_performance

Thank you for providing the details!
Please wait for 4 seconds...Checking file path
Dataset is an excel file!

Please wait for 4 seconds...Checking total columns and rows
Dataset contains total rows: 29 
Total Columns: 5

Please wait for 4 seconds...Checking total duplicates
Datasets has total duplicates records : 0

Please wait for 3 seconds! Saving total duplicates rows
Please wait for 4 seconds...Checking for missing values
Datasets Total missing value: 14
Datasets missing values by each column:
delivery_id        0
order_id           3
delivery_status    3
delivery_time      5
rider_id           3
dtype: int64

Please wait for 6 seconds...Cleaning datasets
Please wait for 4 seconds...Exporting datasets
Congrats! Dataset is cleaned! 
Number of Rows: 24 | Number of columns: 5
Dataset is saved!
