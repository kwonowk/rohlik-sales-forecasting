***
# Rohlik Sales Forecasting
Predicting future sales value with CatBoost
***

<br>

## 📖 Overview

This project aims to forecast sales for a grocery delivery platform that operates 11 warehouses across five European countries (Czechia, Germany, Austria, Hungary, and Romania). Using the `CatBoost` model, the objective is to leverage `Optuna` for hyperparameter fine-tuning. This challenge is part of a Kaggle competition.

## ❓ Key questions

**Model selection**
- Does the sales data exhibit seasonality?
- Is the dataset complete or are there missing values?
**Feature selection**
- What feature engineering techniques can be applied based on the existing features?
- Which features play a significant rolw in explaining the sales data?

## 💾 Dataset

**Description**
- Sales data for selected inventory across 11 warehouses from August 1st 2020 to June 2nd 2024. Note that the values have been modified by the company for confidentiality.

**Source**
- [Rohlik group](https://www.kaggle.com/competitions/rohlik-sales-forecasting-challenge-v2/data)

**Size (after merging, date filtering and feature engineering)**
- 2,499,004 rows * 36 columns

**Structure**
```
data
├── calendar.csv
├── inventory.csv
├── sales_train.csv
├── sales_test.csv
└── test_weights.csv
```

## 🧭 Methodology

*Tools highlighted with `pre-formatting` for clarity. Relevant steps from the Jupyter Notebook are indicated within parentheses.

- [Step 0-2] Exploratory Data Analysis and Feature Engineering
  - Utilize `pandas` for data manipulation and `matplotlib`, along with `seaborn` and `plotly` to analyze the seasonality of sales data.
  - Rule out the use of time-dependent algorithms such as SARIMA and Prophet, as some products are missing up to 95% of sales records
  - Generate date-related features suitable for gradient boost algorithms from the calendar table, including cyclical encodings of the day of the week, day of the month, and day of the year.
- [Step 3-4] Baseline Model Evaluation and Time Period Selection
  - Split the two years of data into different time series to determine the optimal time span for analysis.
  - Use a naive model with average sales as the prediction as baseline (WMAE 29.95)
- [Step 5-7] Feature selection and model hyperparamter tuning

  | Process | WMAE | Improvement compared to baseline |
  |:-------|:----|:-----------|
  | Train `CatBoost` model with default setting| 31.00 | -3.39% |
  | Feature selection with permutation importance | 30.75 | -2.60% |
  | Hyperparameter fine-tuning using `Optuna`| 26.69 | 12.21% |

## ⏭️ Next steps

- Study winners' solutions: Analyze top Kaggle solutions to understand best practices and approaches
- Continue exploring various time-series forecasting models : Such as LSTMs, XGBoost, and other hybrid models
