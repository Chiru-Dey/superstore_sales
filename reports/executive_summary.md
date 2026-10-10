# E-Commerce Analytics & Customer Churn Prediction
## Executive Summary

### 1. Exploratory Data Analysis (What Happened?)
**Observations:**
*   **Revenue Growth & Seasonality:** Revenue shows a clear upward trend from 2015 to 2018, with consistent seasonal spikes occurring in the final months of each year (Q4).
*   **Category Dominance:** Technology drives the highest revenue, followed by Furniture and Office Supplies. At the sub-category level, Phones, Chairs, and Storage are the top performers.
*   **Customer Base:** The customer base is predominantly Consumer (51.6%), followed by Corporate (29.8%) and Home Office (18.7%).
*   **Regional Performance:** The West region generates the highest revenue, while the South and Central regions lag behind.

**Insights & Hypotheses:**
*   **Insight:** The business relies heavily on Q4 seasonal spikes and the Technology category to drive annual revenue.
*   **Hypothesis:** The Q4 spikes *may* be driven by holiday shopping and end-of-year corporate budget spending. The dominance of Phones *could* indicate a high average order value for electronics compared to office supplies.
*   **Insight:** The West region significantly outperforms other regions, suggesting either higher population density, better marketing penetration, or more efficient logistics in that area.

### 2. Predictive Modeling (What Might Happen?)
**Model Performance (Baseline Logistic Regression):**
*   **Accuracy:** 52.0%
*   **Precision:** 44.7%
*   **Recall:** 18.9%

**Interpretation & Association vs. Causation:**
The baseline model identified that **high Recency** (e.g., >500 days since last purchase) and **low Frequency** (1-2 orders) are *associated with* a higher probability of churn. For example, customer MW-18235 (956 days recency) was flagged as High Risk (81.2% probability).

However, the model struggled to confidently separate churners from retained customers, resulting in the vast majority of customers being classified as "Medium Risk" (probabilities between 55% - 68%). 

*Crucial Analyst Note:* The low recall (18.9%) indicates that basic RFM (Recency, Frequency, Monetary) features alone are insufficient to predict e-commerce churn. Many customers with recent purchases still did not buy in the subsequent 180-day window. We observe *associations* in the data, not *causations*. The model cannot prove *why* customers leave, only that certain historical behaviors correlate with future inactivity.

### 3. Strategic Recommendations (What Should We Do?)
1.  **Target High-Value "Medium Risk" Customers:** Since the baseline model cannot perfectly separate risk, the marketing team should prioritize "Medium Risk" customers who have high historical **Monetary** value (e.g., customer SM-20320 with $24,508 lifetime revenue but high recency). Sending win-back discounts to high-value customers yields a better ROI than blanketing all medium-risk users.
2.  **Capitalize on Q4 & Technology:** Allocate the majority of the Q4 marketing budget to the Technology/Phones sub-categories, as they are the proven revenue engines of the business.
3.  **Investigate Regional Disparities:** Conduct a diagnostic analysis on the South and Central regions to understand why they underperform compared to the West. This *might* reveal logistics bottlenecks or untapped market potential.
4.  **Data Science Next Steps:** The data team must iterate on the churn model. Future models should incorporate categorical preferences, discount usage, and shipping times to improve the 18.9% recall rate and reduce the "fence-sitting" Medium Risk bucket.