# E-Commerce Analytics & Churn Prediction Pipeline

## Project Overview
This project performs an end-to-end data analytics pipeline on a retail e-commerce dataset. It covers data preprocessing, exploratory data analysis (EDA) to uncover business insights, and predictive modeling to identify customers at risk of churning.

## Tech Stack
- **Python 3.12** (Managed via `uv`)
- **Pandas & NumPy** (Data manipulation)
- **Matplotlib & Seaborn** (Data visualization)
- **Scikit-Learn** (Predictive modeling)

## Project Structure
```text
superstore_sales/
├── data/
│   ├── raw/            # Original Kaggle dataset (never modified)
│   └── processed/      # Cleaned data and final customer risk tables
├── notebooks/
│   ├── 01_data_preprocessing.ipynb
│   ├── 02_exploratory_data_analysis.ipynb
│   └── 03_predictive_modeling_churn.ipynb
├── models/             # Saved machine learning models (.joblib)
├── reports/            # Executive summary and business insights
└── README.md
```
## How to Run
```code
pip install uv
```
```code
uv sync
```

