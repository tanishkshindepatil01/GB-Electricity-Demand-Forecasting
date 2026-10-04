# Great Britain Electricity Demand: Forecasting & Variance Analysis

A planned Python and Tableau portfolio project exploring electricity demand in Great Britain, evaluating demand forecasts, and investigating differences between forecasts and actual outcomes.

**Author:** Tanishk Nanasaheb Shinde  
**Dashboard scope:** 12 Tableau worksheets across 3 interactive dashboards

## Project Overview

This project will use official National Energy System Operator (NESO) data to examine demand patterns, build and evaluate forecasting models, and communicate operational insights through interactive dashboards.

The analysis will focus on reproducible data preparation, chronological forecast evaluation, KPI reporting, and clear explanations of forecast errors. It is designed to demonstrate skills relevant to energy analytics and forecasting roles.

## Objectives

- Identify seasonal, weekly, and intraday electricity demand patterns.
- Prepare and validate a consistent analytical dataset from official CSV files.
- Compare a seasonal baseline with a statistical or machine learning forecasting model.
- Measure forecast accuracy, signed bias, and changes in performance over time.
- Investigate unusually large forecast errors and document possible explanations.
- Communicate findings, assumptions, and limitations through 3 dashboards.

## Data Sources

| Source | Planned use |
| --- | --- |
| [NESO Historic Demand Data 2025](https://www.neso.energy/data-portal/historic-demand-data/historic_demand_data_2025) | Primary CSV source for half-hourly national demand and contextual electricity-system variables. |
| [NESO Historic Demand Data](https://www.neso.energy/data-portal/historic-demand-data) | Additional historical years, if required for model training. |
| [NESO Historic Day Ahead Demand Forecasts](https://www.neso.energy/data-portal/1-day-ahead-demand-forecast/historic_day_ahead_demand_forecasts) | Optional extension comparing published forecasts with corresponding actual outcomes. |

The primary modelling target will be **National Demand (ND), measured in MW**. Estimated embedded wind and solar fields will be treated as contextual variables, rather than total national renewable generation.

Published NESO forecasts cover specific cardinal points and daily peak/trough windows. Any comparison will first align the demand definition, dates, time windows, units, and forecast issue times.

## Tools

- **Python:** pandas, NumPy, scikit-learn, and appropriate time-series libraries.
- **Jupyter Notebook:** data preparation, exploratory analysis, modelling, and evaluation.
- **Tableau:** 12 worksheets and 3 interactive dashboards.
- **GitHub:** documentation and, once available, reproducible analytical code.

## Dashboard Plan

### Dashboard 1: Electricity Demand Overview

| Worksheet | Title | Planned visual |
| --- | --- | --- |
| 01 | National Demand Over Time | Time-series line chart |
| 02 | Average Intraday Demand Profile | Demand by half-hour of day |
| 03 | Weekday vs Weekend Demand | Comparative demand profiles |
| 04 | Monthly and Seasonal Demand Patterns | Monthly summary chart |

### Dashboard 2: Forecast Performance

| Worksheet | Title | Planned visual |
| --- | --- | --- |
| 05 | Actual vs Forecast Demand | Actual and predicted demand lines |
| 06 | Baseline vs Model Accuracy | MAE and RMSE comparison |
| 07 | Forecast Error Distribution | Signed-error histogram |
| 08 | Forecast Accuracy Over Time | Monthly MAE trend |

### Dashboard 3: Variance Investigation & Data Quality

| Worksheet | Title | Planned visual |
| --- | --- | --- |
| 09 | Forecast Error Calendar | Daily error heatmap |
| 10 | Largest Forecast Deviations | Ranked error periods |
| 11 | Forecast Bias by Time of Day | Mean signed error by half-hour |
| 12 | Data Quality & Coverage | Missing-value, duplicate, and coverage scorecard |

Planned dashboard controls include date-range filters, model selection where relevant, linked selections, navigation buttons, and tooltips explaining units and KPI definitions.

## Analytical Approach

1. Download and record the source CSVs, extraction dates, and data definitions.
2. Validate dates, settlement periods, duplicates, missing values, units, and coverage; handle UK daylight-saving clock changes explicitly.
3. Explore demand patterns and prepare historical lag and calendar features.
4. Establish a previous-week, same-time baseline with an explicit clock-change alignment rule.
5. Train a candidate model and evaluate on later dates using chronological splits or rolling validation.
6. Use only inputs available at the forecast issue time; observed future demand, wind, and solar values will not be used as forecast inputs.
7. Export validated actuals, predictions, errors, and KPI summaries for Tableau.
8. Investigate large errors and distinguish observed associations from verified causes.

## Evaluation Metrics

- **MAE (MW):** average absolute forecast error.
- **RMSE (MW):** forecast error measure giving greater weight to large deviations.
- **Mean signed error (MW):** average prediction minus actual demand; positive values indicate overforecasting.
- **Data quality indicators:** missing values, duplicate records, and expected-period coverage.

A demand value in MW measures power. Energy totals in MWh will be calculated using interval duration rather than by directly summing MW values.

## Planned Deliverables

A reproducible Python notebook, validated Tableau-ready data, a Tableau workbook with 12 worksheets and 3 dashboards, dashboard screenshots, and a concise findings summary will be added after completion.

**This initial repository contains only this README. No datasets, code, dashboards, performance results, or completed findings are included yet.**

## Limitations & Attribution

Data revisions, missing records, forecast timing, and demand definitions may affect comparisons. All sources and applicable reuse terms will be acknowledged. This is an independent portfolio project and is not affiliated with or endorsed by NESO or Low Carbon Contracts Company.
