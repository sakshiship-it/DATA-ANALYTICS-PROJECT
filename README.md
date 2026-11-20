# Hospital Data Analytics Project

A data analytics project focused on exploring and cleaning hospital patient data using Python and Jupyter notebooks (developed and run in Google Colab).

## Project Overview

This project works with a hospital dataset to practice and perform:
- Data loading and inspection
- Data exploration and summary statistics
- Filtering, grouping, and sorting records
- Data cleaning and preprocessing
- Feature creation (age groups, BMI categories, admission year/month)
- Analysis of hospital admission patterns, patient indicators, and hospital stay duration
- Visual presentation of findings through charts and a PowerPoint report

The final cleaned dataset is saved as `cleaned_health_data.csv`.

## Folder Structure

```text
Data Analytics Project/
│
├── data/
│   ├── raw/
│   │   └── hospital.csv                 # Original/raw dataset
│   │
│   └── processed/
│       └── cleaned_hospital.csv          # Cleaned dataset (final output)
│
├── notebook/
│   ├── draft1.ipynb                   # Initial dataset loading and file operations
│   ├── draft2.ipynb                   # NumPy/Pandas exploration and analysis practice
│   ├── final cleaning.ipynb            # Data cleaning, feature creation, summaries
│   ├── hospital.csv                   # Raw data copy used by notebooks
│   └── clean hospital.csv              # Cleaned data copy used by notebooks
│
├── images/
│   └── charts/                          # Charts generated for analysis/presentation
│
├── documents/
│   ├── SRS.doc / SRS.docx              # Software Requirements Specification
│   └── PPT/                              # Project presentation
│
└── README.md
```

> File names shown above are based on the described folder setup. Adjust the names in this README if your actual files use slightly different names (for example, `cleaned_health_data.csv` instead of `cleaned_hospital.csv`).

## Dataset

### Raw Data

- Location: `data/raw/hospital.csv`
- Contains the original hospital records before cleaning.

### Processed Data

- Location: `data/processed/cleaned_hospital.csv`
- Contains the cleaned and prepared data used for analysis.

The notebooks may also contain copies of the raw and cleaned CSV files so they can be accessed easily while running notebooks in Google Colab.

## Tools and Technologies

- **Python**
- **Google Colab**
- **Jupyter Notebook (`.ipynb`)**
- **Pandas** — data loading, cleaning, filtering, grouping, and analysis
- **NumPy** — numerical operations and conditional transformations
- **Matplotlib** — chart generation (where used)
- **CSV** — dataset storage and exchange

## Notebooks

### `draft1.ipynb` — Data Loading and File Handling
Introduces reading CSV data with Pandas, inspecting rows and dataset dimensions, checking column names and data types, selecting columns and rows, and exporting sample data to CSV and Excel.

### `draft2.ipynb` — Pandas and NumPy Exploration
Practices NumPy arrays and calculations alongside Pandas operations, including:
- Selecting rows and columns
- Filtering using conditions
- Summary statistics
- Value counts
- Grouped averages
- Sorting records
- Creating BMI categories and a high-blood-sugar indicator
- Checking missing values, duplicates, and suspicious age values

### `final cleaning.ipynb` — Data Cleaning and Preparation
Performs the final cleaning/preparation workflow:
1. Loads and inspects the dataset.
2. Checks missing values, duplicate rows, city values, and invalid ages.
3. Removes duplicate records.
4. Standardizes city names by trimming whitespace and applying title case.
5. Converts invalid ages (below 0 or above 110) to missing values.
6. Fills missing numeric values in Age, BMI, Fasting Blood Sugar, and Distance to Hospital using each column's median.
7. Fills missing Insurance Type values using the most frequent category (mode).
8. Converts Admission Date to a datetime type and Age to integer.
9. Creates `Age_Group`, `BMI_Category`, `Admission_Year`, and `Admission_Month` features.
10. Produces descriptive statistics, grouped hospital-stay summaries, category counts, and numeric correlations.
11. Saves the prepared dataset to CSV.

## Data Cleaning Details

The final cleaning notebook applies these transformations:

| Field / Issue | Cleaning method |
|---|---|
| Duplicate rows | Removed |
| City names | Trimmed and standardized to title case |
| Invalid Age values | Values below 0 or above 110 set to missing |
| Missing Age | Filled with median |
| Missing BMI | Filled with median |
| Missing Fasting Blood Sugar | Filled with median |
| Missing Distance to Hospital | Filled with median |
| Missing Insurance Type | Filled with mode |
| Admission Date | Converted to datetime |
| Age | Converted to integer after imputation |

### Feature Engineering

- **Age_Group:** Child/Teen, Young Adult, Middle Aged, Senior
- **BMI_Category:** Underweight, Normal, Overweight, Obese
- **Admission_Year:** Year extracted from Admission Date
- **Admission_Month:** Month extracted from Admission Date

## Analysis Areas

The project explores patient and hospital data such as:
- Patient demographics (including age and gender)
- City-wise patient distribution
- Admission type (Emergency, Planned, Referral)
- Insurance type
- BMI categories
- Fasting blood sugar
- Medication count
- Distance to hospital
- Hospital stay duration
- Grouped statistics and numeric correlations

## Charts and Presentation

Chart images are stored in the `images/` folder. They are used to communicate findings visually, including patient distributions and hospital admission/length-of-stay summaries.

The PowerPoint presentation and SRS document are stored in the `documents/` folder.

## Running the Notebooks

### Option 1 — Google Colab

1. Open Google Colab.
2. Upload the notebook from the `notebook/` folder.
3. Upload the required CSV file(s), or mount Google Drive and use the correct file path.
4. Update the notebook's `pd.read_csv(...)` path if the CSV is not in the current Colab working directory.
5. Run the notebook cells in order.

### Option 2 — VS Code

1. Install Python and VS Code.
2. Install the VS Code Python and Jupyter extensions.
3. Open the project folder.
4. Create and activate a Python environment if desired.
5. Install the dependencies listed below.
6. Open a notebook from `notebook/` and select the Python kernel.
7. Make sure the CSV file path used in the notebook points to the correct file.

Install the main packages:

```bash
pip install pandas numpy matplotlib openpyxl jupyter
```

## Notes on File Paths

The notebooks were developed in Google Colab, so some cells may use simple paths such as:

```python
pd.read_csv("hospital.csv")
```

That works only if the CSV is in the notebook's current working directory. In VS Code, either place the file in the working directory or use a relative path, for example:

```python
pd.read_csv("../data/raw/hospital.csv")
```

The correct relative path depends on where the notebook is located and the actual filename.

## Project Status

- [x] Raw dataset organized
- [x] Exploratory notebook work
- [x] Data cleaning and preprocessing
- [x] Cleaned dataset generated
- [x] Charts prepared
- [x] Project presentation prepared
- [ ] Final review of paths and filenames
- [ ] Add project-specific findings/limitations from the SRS

## Disclaimer

This project is for educational and data-analysis purposes. The dataset and analysis should not be used to make clinical decisions about real patients.

## Author

**Project Author:** *Add your name here*
