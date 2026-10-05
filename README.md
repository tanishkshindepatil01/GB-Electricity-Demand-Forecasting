# Great Britain Electricity Demand: Forecasting and Variance Analysis

**Tanishk Nanasaheb Shinde** · NESO historic demand data · 2023–2025

This project explores half-hourly electricity demand, compares a previous-week forecast with two machine learning models, and investigates forecast errors. The Jupyter notebook contains the data preparation, exploratory analysis, models, plots, and a single Tableau-ready CSV export. The Tableau workbook contains 13 worksheets across three dashboards.

## Repository contents

```text
GB-Electricity-Demand-Forecasting/
├── README.md
├── requirements.txt
├── data/
│   ├── demanddata_2023.csv
│   ├── demanddata_2024.csv
│   ├── demanddata_2025.csv
│   └── GB_Electricity_Demand_Tableau.csv
├── notebook/
│   └── GB_Electricity_Demand_Analysis.ipynb
├── tableau/
│   └── GB_Electricity_Demand.twb
├── dashboards/
│   ├── Dashboard_1_Demand_Overview.png
│   ├── Dashboard_2_Forecast_Performance.png
│   └── Dashboard_3_Variance_and_Data_Quality.png
└── sheets/
    └── 01_Demand_Over_Time.png … 13_Data_Quality_Coverage.png
```

The `data/GB_Electricity_Demand_Tableau.csv` file is the one combined dataset used by the workbook. Each row represents a half-hourly settlement interval. It includes calendar and quality fields, actual demand, model predictions, signed and absolute errors, and evaluation flags. The three annual CSVs are the notebook inputs; they are included so the analysis can be rerun.

## Open and rerun

1. Extract this repository, install the Python dependencies with `python -m pip install -r requirements.txt`, and launch Jupyter from the repository root with `jupyter notebook`.
2. Open `notebook/GB_Electricity_Demand_Analysis.ipynb` and run all cells. It discovers the three annual CSVs in `data/`. By default, `OUTPUT_DIR = Path.cwd()`, so launching Jupyter from the repository root rewrites the combined CSV in `data/` **only if** you change `OUTPUT_DIR` to `Path.cwd() / 'data'` first. Otherwise the new CSV is written to the repository root. The provided combined CSV is already generated and does not require a rerun to use Tableau.
3. Open `tableau/GB_Electricity_Demand.twb` in Tableau Desktop. If Tableau asks for the text file, use **Data → [data source] → Edit Connection** and select `data/GB_Electricity_Demand_Tableau.csv`. Then refresh the data source. The workbook is a `.twb` definition with its CSV supplied separately. To make a self-contained Tableau file in Tableau Desktop, use **File → Save As** and choose **Tableau Packaged Workbook (`.twbx`)**.

The workbook's connection path has been changed to a repository-relative hint (`../data`), but Tableau may still request a connection edit after download or relocation. The packaged `.twbx` step should be done in Tableau Desktop after reconnecting.

## Analysis and results

The target is NESO **National Demand (`ND`)**, measured in MW. The notebook checks settlement coverage and duplicate/missing records, explores daily/weekly/seasonal patterns, creates calendar and historical lag features, and compares a same-time previous-week baseline with ridge regression and histogram gradient boosting. It uses 2023 for training, 2024 for validation and selection, and 2025 as the held-out test. Ridge was selected on validation MAE before the test results were examined. Errors are **forecast minus actual**, so positive bias means overforecasting.

| Model | 2025 test MAE (MW) | 2025 test RMSE (MW) |
| --- | ---: | ---: |
| Previous-week seasonal baseline | 2,177.5 | 2,920.1 |
| Ridge regression, selected model | 1,565.3 | 2,068.4 |
| Histogram gradient boosting | 1,568.0 | 2,059.4 |

Ridge reduced test MAE by **28.1%** against the previous-week baseline. Its full-year mean signed error was about **−45 MW**, although bias and error magnitude vary over time. The source coverage checks found 17,520, 17,568, and 17,520 intervals for 2023, 2024, and 2025 respectively, with no missing settlement periods or actual-demand values in these supplied files. The additional 2024 intervals reflect the leap year.

The results are an evaluation of models built from the supplied historic demand data, not a comparison with NESO's issued operational forecasts. The notebook's availability assumptions and feature timing are part of its model interpretation. A small mean signed error does not imply that individual intervals were accurate, and large errors should not be assigned a cause without external evidence.

## Tableau views

| Dashboard | Worksheets |
| --- | --- |
| 1 · Demand Overview | `01_Demand_Over_Time`, `02_Intraday_Demand`, `03_Weekday_Weekend`, `04_Monthly_Demand` |
| 2 · Forecast Performance | `05_Actual_vs_Forecast`, `06_Model_MAE`, `07_Model_RMSE`, `08_Forecast_Error_Distribution`, `09_Monthly_MAE` |
| 3 · Variance and Data Quality | `10_Daily_Error_Calendar`, `11_Largest_Errors`, `12_Forecast_Bias_By_Time`, `13_Data_Quality_Coverage` |

The `dashboards/` and `sheets/` folders contain PNG snapshots of the workbook views. The title of worksheet 11 has been corrected to **Top 10 Largest Forecast Errors (2025 Test Set)** in the editable workbook. The supplied `sheets/11_Largest_Errors.png` and `dashboards/Dashboard_3_Variance_and_Data_Quality.png` were exported before that correction and still show the old title. Re-export those two images from Tableau if publishing the screenshots independently.

## Sources and attribution

- [NESO Historic Demand Data](https://www.neso.energy/data-portal/historic-demand-data) and the [2025 dataset page](https://www.neso.energy/data-portal/historic-demand-data/historic_demand_data_2025) supply the annual source files.
- The analysis and dashboard are an independent portfolio project and are not endorsed by NESO.

To publish as a navigable GitHub repository, **extract the ZIP and upload its contents** (or push the folder with Git). Uploading the ZIP alone to a repository leaves it as a single downloadable file.
