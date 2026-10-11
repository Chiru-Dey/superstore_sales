# Superstore Sales — E-Commerce Analytics & Customer Churn Prediction

## Project Overview
An end-to-end, AI-assisted data analytics pipeline on the Superstore Sales dataset.
It follows the full business-intelligence workflow:
**Raw Data → Cleaning → Exploratory Data Analysis → Insights → Leakage-safe Churn Prediction → Customer Risk Table → Strategic Actions.**

Key outputs:
- Cleaned dataset: `data/processed/superstore_clean.csv`
- 5 EDA visualisations (revenue trend, category, segment, region, sub-category)
- Trained churn model: `models/churn_logreg.joblib`
- Customer risk table: `data/processed/customer_risk_table.csv`
- Business narrative (risks, opportunities, actions): `reports/executive_summary.md`

There is no web front-end; the Jupyter notebook is the interface, and all outputs/charts are reproduced in the submitted project report.

## Dataset
<https://www.kaggle.com/datasets/rohitsahoo/sales-forecasting>
(Raw file stored at `data/raw/train.csv` — never modified, per the golden rule.)

## Tech Stack
- Python 3.12 (managed with `uv`; plain `pip` also supported)
- pandas / numpy — data manipulation
- matplotlib / seaborn — visualisation
- scikit-learn — logistic regression pipeline
- joblib — model persistence

## How the Model Works
1. **Cleaning** — mixed-format dates parsed (`dayfirst=True`), Kaggle columns renamed to the workbook schema (`Sales → Revenue`, etc.), invalid/negative rows dropped, duplicates removed, text hygiene applied. Raw file untouched.
2. **EDA** — monthly revenue trend, category & sub-category revenue, customer segment mix, regional performance.
3. **Leakage-safe churn setup** — RFM features (Recency, Frequency, Monetary, Avg Order Value) are computed **only** from orders before `2018-01-01`; the target is "no purchase in the following 180-day window" (2018-01-01 → 2018-06-30). No future information leaks into the features.
4. **Model** — `LogisticRegression` + `StandardScaler` inside a scikit-learn `Pipeline`; stratified 75/25 train-test split. Baseline metrics: Accuracy 52.0%, Precision 44.7%, Recall 18.9% (limitations discussed honestly in the report).
5. **Risk scoring** — churn probability per customer → risk bands (Low < 40%, Medium 40–70%, High ≥ 70%) → sorted customer risk table.

## Project Structure
superstore_sales/
├── data/
│   ├── raw/train.csv                       # original Kaggle file (never modified)
│   └── processed/
│       ├── superstore_clean.csv            # cleaned + enriched data
│       └── customer_risk_table.csv         # final churn-risk output
├── models/
│   └── churn_logreg.joblib                 # trained pipeline
├── notebooks/
│   └── ChirantanDey_SuperstoreSales.ipynb  # single code file: cleaning → EDA → model → risk table
├── reports/
│   └── executive_summary.md                # source text of the submitted report
├── README.md
└── requirements.txt

## How to Run
### Option A — uv (recommended, Windows PowerShell)
```powershell
cd superstore_sales
uv sync
```
Then open `notebooks/ChirantanDey_SuperstoreSales.ipynb` in VS Code, select the `.venv` kernel and **Run All**.

### Option B — pip
```powershell
python -m venv .venv
.venv\Scripts\Activate
pip install -r requirements.txt
pip install ipykernel
```
jupyter notebook notebooks/ChirantanDey_SuperstoreSales.ipynb

> **Note:** run the notebook with kernel working directory = `notebooks/` (the VS Code default), because all file paths are relative (`../data/raw/train.csv`).

## Headline Business Insights
- Revenue grows 2015→2018 with strong Q4 seasonality; Technology (Phones) is the revenue engine.
- West region leads; South and Central lag → diagnostic follow-up recommended.
- The baseline RFM model separates risk weakly (recall 18.9%), so retention spend should target **high-Monetary "Medium Risk"** customers (e.g. SM-20320, $24.5k lifetime revenue) rather than blanket campaigns.

Full narrative: `reports/executive_summary.md` and the submitted project report.