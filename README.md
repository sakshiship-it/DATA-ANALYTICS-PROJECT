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
- Visual presentation of findings through Matplotlib charts and a PowerPoint report

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
│   ├── 04_matplotlib_charts.ipynb      # Matplotlib charts for the four business questions
│   ├── hospital.csv                   # Raw data copy used by notebooks
│   └── clean hospital.csv              # Cleaned data copy used by notebooks
│
├── images/
│   └── charts/                          # Chart images (PNG) created by 04_matplotlib_charts.ipynb
│       ├── q1_stay_histogram.png
│       ├── q1_stay_boxplot.png
│       ├── q2_correlation.png
│       ├── q2_medications_vs_stay.png
│       ├── q2_age_vs_stay.png
│       ├── q2_sugar_vs_stay.png
│       ├── q3_stay_by_groups.png
│       ├── q4_long_stay_count.png
│       ├── q4_long_stay_rate.png
│       ├── q4_long_stay_profile.png
│       └── extra_patients_per_city.png
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
- **Matplotlib** — all charts (histogram, box plot, bar, line and scatter charts)
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

### `04_matplotlib_charts.ipynb` — Charts with Matplotlib
Reads `cleaned_health_data.csv` and draws the charts that answer the four business questions:
- **Question 1:** histogram (with mean and median lines) and box plot of `Hospital_Stay_Days`.
- **Question 2:** correlation bar chart, average stay by number of medications, and scatter plots with trend lines for `Age` and `Fasting_Blood_Sugar`.
- **Question 3:** four bar charts of average stay by `Admission_Type`, `City`, `Insurance_Type` and `Gender`.
- **Question 4:** creates the `Long_Stay` column (10 or more days) and charts the Long Stay count, the Long Stay rate by age group and admission type, and the average age and medications of Long Stay patients.
- **Extra:** number of patients per city.

Every chart is saved as a PNG file in a `charts` folder, and the last cell downloads them all as `charts.zip` in Google Colab.

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

## Questions to Answer

All answers below use the cleaned dataset (`cleaned_health_data.csv`, 250 patients). The numbers can be reproduced with the pandas code shown under each question.

### 1. What does `Hospital_Stay_Days` look like overall?

| Measure | Value |
|---|---|
| Typical stay (mean) | 6.86 days |
| Typical stay (median) | 7 days |
| Most common stay (mode) | 5 days (40 patients) |
| Spread (standard deviation) | 2.38 days |
| Middle half of patients (25th to 75th percentile) | 5 to 9 days |
| Shortest stay | 1 day (5 patients) |
| Longest stay | 12 days (4 patients) |

**Summary:** A typical patient stays about a week. The mean (6.86) and median (7) are close, so the stays are spread fairly evenly around the middle, with no extreme outliers. Stays of 5 to 9 days cover 180 of the 250 patients (72%).

```python
clean["Hospital_Stay_Days"].describe()
clean["Hospital_Stay_Days"].mode()
clean["Hospital_Stay_Days"].value_counts().sort_index()
```

![Distribution of hospital stay](images/charts/q1_stay_histogram.png)

![Hospital stay box plot](images/charts/q1_stay_boxplot.png)

### 2. Do `Age` and `Medications_Count` affect `Hospital_Stay_Days`? Does `Fasting_Blood_Sugar` matter as much?

| Column | Correlation with stay | Pattern in the averages |
|---|---|---|
| `Medications_Count` | 0.51 (strongest) | 5.49 days with 1 medicine, 7.28 with 3, 9.18 with 6, 9.80 with 8 |
| `Age` | 0.40 | Child/Teen 4.92, Young Adult 6.31, Middle Aged 6.84, Senior 8.44 days |
| `Fasting_Blood_Sugar` | 0.15 (weak) | 6.46 days at 100 or below, 7.10 at 101 to 125, 7.24 above 125 |

**Summary:** Yes, both `Age` and `Medications_Count` clearly affect the stay: older patients and patients on more medicines stay longer. Patients who are over 60 and take 5 or more medicines average 10.25 days (only 4 patients, so treat this as a hint). `Fasting_Blood_Sugar` matters much less: patients with sugar above 125 stay 7.24 days on average, against 6.78 for the rest, a gap of only about half a day. A correlation shows a relationship, not a cause.

```python
cols = ["Age", "Medications_Count", "Fasting_Blood_Sugar"]
clean[cols + ["Hospital_Stay_Days"]].corr()["Hospital_Stay_Days"]
clean.groupby("Medications_Count")["Hospital_Stay_Days"].mean().round(2)
clean.groupby("Age_Group")["Hospital_Stay_Days"].mean().round(2)
```

![Correlation with hospital stay](images/charts/q2_correlation.png)

![Average stay by number of medications](images/charts/q2_medications_vs_stay.png)

![Age vs hospital stay](images/charts/q2_age_vs_stay.png)

![Fasting blood sugar vs hospital stay](images/charts/q2_sugar_vs_stay.png)

### 3. Does `Hospital_Stay_Days` differ by `Admission_Type`, `City`, `Insurance_Type` and `Gender`?

| Group | Category | Patients | Average stay (days) |
|---|---|---|---|
| `Admission_Type` | Emergency | 121 | 7.27 |
| | Referral | 40 | 7.15 |
| | Planned | 89 | 6.17 |
| `City` | Kolkata | 27 | 7.59 |
| | Chennai | 43 | 7.16 |
| | Mumbai | 63 | 6.86 |
| | Delhi | 63 | 6.62 |
| | Bengaluru | 54 | 6.54 |
| `Insurance_Type` | Uninsured | 75 | 6.91 |
| | Private | 81 | 6.86 |
| | Government | 94 | 6.82 |
| `Gender` | Female | 103 | 7.03 |
| | Male | 147 | 6.74 |

**Summary:**
- **Admission type matters most:** Emergency and Referral stays are about one day longer than Planned stays.
- **City shows a difference** of about one day between Kolkata (longest) and Bengaluru (shortest), but Kolkata has only 27 patients, so this is less reliable.
- **Insurance type makes almost no difference** (6.82 to 6.91 days).
- **Gender shows a small gap** (0.29 days).

```python
for col in ["Admission_Type", "City", "Insurance_Type", "Gender"]:
    print(clean.groupby(col)["Hospital_Stay_Days"].agg(["count", "mean"]).round(2))
```

![Average stay by admission type, city, insurance type and gender](images/charts/q3_stay_by_groups.png)

### 4. Which records need attention? ("Long Stay" = 10 or more days)

**How many:** 35 of 250 patients (14.0%) are Long Stay patients.

```python
clean["Long_Stay"] = np.where(clean["Hospital_Stay_Days"] >= 10, "Long Stay", "Normal")
print(clean["Long_Stay"].value_counts())
long_stay = clean[clean["Long_Stay"] == "Long Stay"]
```

The `Long_Stay` column is created in `04_matplotlib_charts.ipynb`. Add the same line to `final cleaning.ipynb` if you want it saved in the cleaned file.

![Long Stay vs Normal patients](images/charts/q4_long_stay_count.png)

**What they have in common** (compared with the other 215 patients):

| Feature | Long Stay patients | Other patients |
|---|---|---|
| Average age | 57.3 years | 43.4 years |
| Seniors (over 60) | 17 of 35 (49%) | 14% |
| Average medications | 4.4 | 2.9 |
| Taking 5 or more medicines | 15 of 35 | n/a |
| Average fasting blood sugar | 114.7 | 103.9 |
| Emergency admission | 22 of 35 (63%) | 46% |
| Referral admission | 9 of 35 (26%) | 14% |
| Planned admission | 4 of 35 (11%) | 40% |
| Overweight BMI category | 21 of 35 (60%) | 40% |

**Where the Long Stay rate is highest:**
- **By age group:** Seniors 35% (17 of 48), Middle Aged 12%, Young Adults 7%, Child/Teen 0%.
- **By admission type:** Referral 22.5%, Emergency 18.2%, Planned 4.5%.

**What they do not have in common:** insurance type (the mix matches the other patients) and gender (51% male, 49% female). City differences are small.

**Summary:** Records that need attention are typically older patients on several medicines who were admitted as Emergency or Referral cases. The 35 Long Stay patient IDs are:

![Long Stay rate by age group and admission type](images/charts/q4_long_stay_rate.png)

![Average age and medications of Long Stay patients](images/charts/q4_long_stay_profile.png)

```text
P1167, P1171, P1077, P1205, P1013, P1172, P1140, P1154, P1151, P1221,
P1186, P1086, P1149, P1119, P1069, P1073, P1183, P1085, P1076, P1201,
P1111, P1163, P1157, P1021, P1116, P1199, P1226, P1007, P1238, P1102,
P1026, P1091, P1146, P1240, P1244
```

> The dataset is synthetic, so these patterns describe this data only and not real hospital patients.

## Charts and Presentation

All charts are made with Matplotlib in `04_matplotlib_charts.ipynb` and saved as PNG images in `images/charts/`.

| Chart file | Question | What it shows |
|---|---|---|
| `q1_stay_histogram.png` | 1 | Number of patients for each hospital stay length, with mean (6.86) and median (7) |
| `q1_stay_boxplot.png` | 1 | Spread of stays: middle half is 5 to 9 days, range 1 to 12 |
| `q2_correlation.png` | 2 | Correlation with stay: medications 0.51, age 0.40, fasting blood sugar 0.15 |
| `q2_medications_vs_stay.png` | 2 | Average stay rises from 5.49 days (1 medicine) to 9.80 days (8 medicines) |
| `q2_age_vs_stay.png` | 2 | Each patient as a dot, with a trend line: older patients stay longer |
| `q2_sugar_vs_stay.png` | 2 | Each patient as a dot, with a flatter trend line: sugar has a weaker effect |
| `q3_stay_by_groups.png` | 3 | Average stay by admission type, city, insurance type and gender |
| `q4_long_stay_count.png` | 4 | 35 Long Stay patients against 215 Normal patients |
| `q4_long_stay_rate.png` | 4 | Long Stay rate by age group (Seniors 35%) and admission type (Referral 22.5%) |
| `q4_long_stay_profile.png` | 4 | Long Stay patients are older (57.3 vs 43.4) and take more medicines (4.4 vs 2.9) |
| `extra_patients_per_city.png` | Extra | Number of patients in each city |

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

For `04_matplotlib_charts.ipynb`, upload `cleaned_health_data.csv` (the output of `final cleaning.ipynb`), because the charts use columns such as `Age_Group` that are created during cleaning.

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
- [x] Charts prepared with Matplotlib (`04_matplotlib_charts.ipynb`, images in `images/charts/`)
- [x] Project presentation prepared
- [ ] Final review of paths and filenames
- [ ] Add project-specific findings/limitations from the SRS

## Disclaimer

This project is for educational and data-analysis purposes. The dataset and analysis should not be used to make clinical decisions about real patients.

## Author

**Project Author:** *Add your name here*
