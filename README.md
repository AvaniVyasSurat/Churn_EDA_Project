# Telco Customer Churn — Exploratory Data Analysis

An EDA project on the Telco Customer Churn dataset (7,043 customers) using **Python**, **Pandas**, **Matplotlib**, and **Seaborn**, exploring tenure, contract type, payment methods, and which add-on services are most strongly associated with churn.

## 📊 About the Dataset

File: `Telco-Customer-Churn.csv` — 7,043 rows × 21 columns (22 after feature engineering).

| Column | Description |
|---|---|
| customerID | Unique customer identifier |
| gender | Customer's gender |
| SeniorCitizen | Whether the customer is a senior citizen (0/1) |
| Partner | Whether the customer has a partner |
| Dependents | Whether the customer has dependents |
| tenure | Number of months the customer has stayed |
| PhoneService | Whether the customer has phone service |
| MultipleLines | Whether the customer has multiple lines |
| InternetService | Type of internet service |
| OnlineSecurity | Whether the customer has online security add-on |
| OnlineBackup | Whether the customer has online backup add-on |
| DeviceProtection | Whether the customer has device protection add-on |
| TechSupport | Whether the customer has tech support add-on |
| StreamingTV | Whether the customer has streaming TV |
| StreamingMovies | Whether the customer has streaming movies |
| Contract | Contract type (Month-to-month, One year, Two year) |
| PaperlessBilling | Whether billing is paperless |
| PaymentMethod | Payment method used |
| MonthlyCharges | Monthly charge amount |
| TotalCharges | Total amount charged |
| Churn | Whether the customer churned (target variable) |

**Engineered column:** `tenure_bin` — tenure grouped into bins (0–20, 20–35, 35–50, 50–100 months).

**Missing values:** None — all 21 original columns are fully populated.

## 🎯 Purpose

To explore which customer attributes and subscribed services are most associated with churn, and to practice a complete analysis workflow: target encoding, binning, grouped aggregation, and correlation analysis.

## 🛠️ Approach

1. **Load and inspect** the dataset — shape, dtypes, `info()`, missing value check.
2. **Demographic exploration** — value counts for `SeniorCitizen`, `gender`, `PaymentMethod`, `Dependents`, visualized with pie charts.
3. **Target encoding** — convert `Churn` from Yes/No to a binary `1`/`0` column.
4. **Feature engineering** — bin `tenure` into four groups using `pd.cut()`.
5. **Churn by tenure** — group churn counts by `tenure_bin` to see how loyalty changes over time.
6. **Churn by contract type** — group churn counts by `Contract` (Month-to-month, One year, Two year).
7. **Service impact analysis** — group `OnlineSecurity` and `TechSupport` by `Churn` to compare uptake between churned and retained customers.
8. **Correlation analysis** — map six Yes/No add-on service columns (`OnlineSecurity`, `OnlineBackup`, `DeviceProtection`, `TechSupport`, `StreamingTV`, `StreamingMovies`) to numeric flags and correlate each with `Churn`, visualized as heatmaps.

## ❓ Questions Answered

- What does the dataset look like, and what is its shape and structure?
- What are the data types of each column, and are there any missing values?
- How many senior citizens are in the customer base?
- Which payment methods are most commonly used?
- What is the gender split of customers?
- What proportion of customers have dependents?
- How is customer tenure distributed across bins?
- How does churn rate change across different tenure groups?
- How does churn differ by contract type (Month-to-month vs. One year vs. Two year)?
- Does having Online Security reduce the likelihood of churn?
- Does having Tech Support reduce the likelihood of churn?
- Which add-on services are most strongly correlated (positively or negatively) with churn?

## 🗄️ Tech Stack

- **Python**
- **Pandas**
- **NumPy**
- **Matplotlib**
- **Seaborn**
- **Jupyter Notebook**

## 📁 Repository Structure

```
├── Telco_Customer_Churn.ipynb   # Notebook with code, outputs, and visualizations
├── Project_Report.docx          # Full project report
└── README.md
```

## 🚀 How to Run

1. Install the requirements:
   ```
   pip install pandas numpy matplotlib seaborn jupyter
   ```
2. Place `Telco-Customer-Churn.csv` in the working directory (update the file path in the notebook if needed — the original path points to a Google Drive mount).
3. Open and run the notebook:
   ```
   jupyter notebook Telco_Customer_Churn.ipynb
   ```

**Note:** An early version of the service-correlation cell tried to re-map the already-binary `Churn` column back from `'Yes'/'No'` strings (`churn['Churn'].map({'Yes': 1, 'No': 0})`), which returned all `NaN` since `Churn` had already been encoded as `0`/`1` earlier in the notebook. This was identified and corrected later in the notebook by using the existing binary `Churn` column directly — both the broken attempt and the fix are kept in the notebook for reference.

## 📌 Key Findings

- The dataset covers **7,043 customers**, fully clean with **no missing values**.
- **1,142 customers (16.2%)** are senior citizens.
- **Electronic check** is the most common payment method (2,365 customers), followed by mailed check, bank transfer, and credit card.
- Churn is heavily concentrated among **short-tenure customers**: of customers with 0–20 months tenure, **1,251 out of 2,867 (43.6%)** churned, compared to just **188 out of 2,105 (8.9%)** among customers with 50–100 months tenure.
- **Contract type strongly predicts churn**: Month-to-month customers churn at roughly **43%**, One-year contract customers at about **11%**, and Two-year contract customers at just **2.8%**.
- **OnlineSecurity** (r ≈ -0.17) and **TechSupport** (r ≈ -0.16) show the strongest negative correlation with churn — customers with these add-ons are notably less likely to leave.
- **StreamingTV** (r ≈ 0.06) and **StreamingMovies** (r ≈ 0.06) show a small positive correlation with churn, unlike the protective services above.

---
*An exploratory data analysis project on Telco customer churn drivers.*
