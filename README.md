# FDA AI-Enabled Medical Devices: Data Wrangling and Exploratory Analysis with Python

**An end-to-end Python analysis of FDA AI-enabled medical device authorizations, regulatory review timelines, medical specialties, and linked recall records.**

## Project overview

Artificial intelligence is increasingly represented in medical devices, but authorization counts alone do not describe the regulatory landscape or the post-market issues recorded for these products. This project explores three related datasets: device authorizations, product-code classifications, and linked recalls, to examine trends, concentration, review timelines, and recorded recall reasons.

The project follows a reproducible **gather → assess → clean → analyze → interpret** workflow in a Jupyter Notebook. Its emphasis is on practical data wrangling, exploratory data analysis (EDA), and careful interpretation of observational data.

## Business and analytical questions

1. How have annual FDA AI-enabled medical device authorizations changed?
2. Which medical specialties account for the most authorizations?
3. How do observed receipt-to-decision timelines vary across authorization pathways?
4. Which recall root-cause categories appear most often in linked records?
5. Is radiology's share of annual authorizations changing?
6. Which product codes are most common among authorizations from 2023 onward?
7. Which submission numbers have the most linked recall records?
8. How does limited follow-up time affect interpretation of recent recall data?

## Tech stack

| Technology | Application |
| --- | --- |
| Python | Data processing and analysis |
| Pandas | DataFrames, cleaning, grouping, aggregation, and merging |
| NumPy | Numerical analysis support |
| Matplotlib | Charts and visual customization |
| Seaborn | Statistical and categorical visualizations |
| Jupyter Notebook | Interactive analysis and documentation |

## Data

**Source:** [FDA AI Medical Devices Authorizations and Recalls](https://www.kaggle.com/datasets/kylefengkfeng209/fda-ai-medical-devices-authorizations-and-recalls)

The notebook loads three CSV files:

- `fda_ai_medical_devices.csv`: authorization records (1,524 rows; 44 columns).
- `fda_ai_product_codes.csv`: product-code classifications used to enrich the authorization analysis.
- `fda_ai_device_recalls.csv`: linked recall records (313 rows; 29 columns).

The recall table contains 313 records linked to 102 distinct submission numbers. **Recall records are not interchangeable with distinct recalled devices or device-level recall probabilities.** The data extend through March 30, 2026; 2026 is therefore a partial year.

## Methodology and Python skills demonstrated

### 1. Data ingestion and assessment

- Imported multiple CSV files into Pandas DataFrames.
- Inspected records using `.head()` and `.info()`.
- Checked full-row duplicates using `.duplicated().sum()`; none were found in the three tables.
- Identified date fields stored as strings and structural categories stored as object types.

### 2. Data cleaning and preparation

- Created working copies of the source DataFrames before transformation.
- Converted date strings to `datetime64` using `pd.to_datetime()`.
- Converted selected classification fields to Pandas `category` dtype.
- Verified the resulting data types.

### 3. Exploratory data analysis

- Used Boolean filtering, `.value_counts()`, `.groupby()`, and `.describe()` to profile the datasets.
- Compared authorization counts across years, specialties, and regulatory pathways.
- Computed radiology's annual percentage of authorizations.
- Joined authorization product codes to classification descriptions using `DataFrame.merge()`.
- Examined recall root-cause categories and repeated submission numbers.
- Visualized distributions and patterns using bar charts, line charts, violin plots, and scatterplots with a fitted regression line.

### 4. Interpretation and limitations

Distinguished descriptive patterns from causal explanations, identified unresolved recall investigations, and considered the effect of unequal observation periods when comparing time to first recall.

## Key findings

| Area | Finding | Interpretation |
| --- | --- | --- |
| Authorization growth | 65 authorizations in 2018 versus 333 in 2025 | Strong growth in annual counts in the dataset |
| Specialty concentration | Radiology: 1,160 of 1,524 (76.1%) | Radiology dominates the recorded authorization landscape |
| Regulatory pathway | 510(k): 1,466 of 1,524 (96.2%) | Most listed authorizations use the 510(k) pathway |
| Review duration | Median: 135 days (510(k)), 293 (De Novo), 353 (PMA) | Observed review spans differ by pathway; no causal claim is made |
| Recall categories | Under investigation: 108; Software design: 90; Device design: 41 | Software design leads among these categories once unresolved investigations are set aside |
| Product classifications | QIH: 217 authorizations from 2023 onward | Automated Radiological Image Processing Software is the leading listed product code in that period |
| Radiology over time | 86.8% share in 2020; 75.0% in partial 2026 | Concentration appears lower in the latest partial year |

**Important:** The 92 authorization records for 2026 only cover part of the year, so 2026 counts should not be directly compared with complete calendar years.

## Visualizations

The notebook includes:

1. Annual FDA AI-device authorizations - bar chart.
2. Leading medical specialties - horizontal bar chart.
3. Review-day distributions by pathway - violin plot.
4. Recall root-cause frequencies - horizontal bar chart.
5. Radiology's share of annual authorizations - line chart.
6. Authorization year versus days to first linked recall - scatterplot with regression line.

Open [`Solution.ipynb`](Solution.ipynb) to explore the charts, calculations, and accompanying explanations.

## How to run the project

1. Clone this repository and navigate to its folder.
2. Install Python 3 and Jupyter Notebook.
3. Install the dependencies:

   ```bash
   pip install pandas numpy matplotlib seaborn notebook
   ```

4. Download the three CSV files from the [dataset source](https://www.kaggle.com/datasets/kylefengkfeng209/fda-ai-medical-devices-authorizations-and-recalls) and place them in the same directory as `Solution.ipynb` (or adjust the file paths in the notebook).
5. Start Jupyter:

   ```bash
   jupyter notebook
   ```

6. Open `Solution.ipynb` and run the cells in order.

## Limitations

- The dataset is a curated collection of FDA-related records; its coverage and linking logic affect interpretation.
- Missingness and source accuracy were not comprehensively validated.
- Review-day comparisons are descriptive and do not control for differences between submissions or pathways.
- A recall record does not directly represent a unique device or a probability of recall.
- Some recall causes remain under investigation.
- More recently authorized devices have had less time to accumulate recalls; the time-to-first-recall plot cannot establish that newer devices are safer.
- 2026 authorization figures are partial through March 30.


## Project takeaway

This project demonstrates how I use Python to transform multiple related datasets into interpretable evidence: inspecting data quality, preparing analysis-ready fields, joining classifications, calculating metrics, creating informative visualizations, and communicating conclusions with appropriate caveats.

## Author

**Adaeze Obasi**  
Python • Data Analysis • Data Visualization
