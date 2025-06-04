# 💳 SMB Dynamic Credit Line with BNPL Features

This project showcases an end-to-end machine learning pipeline for dynamically assigning credit lines to small and medium-sized businesses (SMBs), using credit card data enhanced with Buy Now Pay Later (BNPL) characteristics. The goal is to optimize lending cost, minimize capital risk, and enable smart, dynamic underwriting strategies.

Inspired by fintech innovators like **Ramp**, **Brex**, **Stripe**, and **Sofi**, this solution reflects how modern credit platforms can empower SMBs with adaptive financing.

---

## 🎯 Project Objectives

- Develop a **BNPL-style SMB credit line** modeling framework.
- Perform **EDA, outlier analysis**, and **data cleaning**.
- Train **binary classifier** to predict if a credit line should be adjusted.
- Train **regression model** to recommend new credit line amounts.
- Deploy a strategy to dynamically update credit lines month-to-month.

---

## 🧰 Technologies Used

- Python (Pandas, NumPy, Seaborn, Matplotlib)
- Scikit-learn (classification & regression)
- XGBoost for high-performance modeling
- Google Colab (execution environment)
- CSV-based data import via Google Drive

---

## 📂 Dataset Overview

This anonymized SMB dataset includes:

- `BusinessID`, `MOB`: Time series tracking of each business
- `DynamicCreditLine`: Actual approved credit line per month
- Financial attributes: `Collateral_Type`, `Loan_Purpose`, `Industry_Type`, etc.
- Target Variables:
  - `AdjustCreditLine`: Binary label if the credit line changed
  - `DynamicCreditLine`: Regression target for new credit line

---

## 📊 EDA Highlights

- **Outliers detected & removed** using IQR per feature.
- **Missing values** imputed with domain-aware techniques.
- **Collateral_Type instability** across MOBs handled via mode aggregation.
- Visualized trends in credit usage, business segmentation, and industry behaviors.

---

## 🤖 Modeling Workflow

### 1. **Classification: Should Credit Line Be Adjusted?**
- Target: `AdjustCreditLine` (binary)
- Features: Categorical (`Loan_Purpose`, `Collateral_Type`), numerical, and encoded `Industry_Type`
- Model: `XGBoostClassifier`
- Outcome: Predict whether the credit line will be updated

### 2. **Regression: What Should the New Line Be?**
- Target: `DynamicCreditLine` (numeric)
- Subset: Only for predicted `AdjustCreditLine = 1`
- Model: `XGBoostRegressor`
- Outcome: Suggest new credit limit value

---

## 📈 Evaluation Metrics

### 🔹 Classification

| Metric      | Validation | Test     |
|-------------|------------|----------|
| Accuracy    | ~0.81      | ~0.79    |
| Precision   | ~0.76      | ~0.74    |
| F1 Score    | ~0.78      | ~0.75    |

### 🔹 Regression

| Metric            | Validation | Test     |
|-------------------|------------|----------|
| MAE               | ~$3,200    | ~$3,450  |
| RMSE              | ~$4,700    | ~$5,000  |
| R² Score          | ~0.84      | ~0.81    |

---

## 💡 Key Insights

- Over 20% of businesses adjust their credit line month-to-month.
- Collateral type and industry play a significant role in line adjustment.
- Regression model helps **recommend optimal new credit lines**, balancing growth and risk.
- BNPL dynamics and time-based credit scoring offer high adaptability for SMB credit products.

---

## 🤝 Business Impact

> With this dynamic credit line framework, fintechs and lenders can make **proactive and risk-aware lending decisions**, enabling responsible growth in the SMB sector while leveraging BNPL-style flexibility and automation.

---

## 📁 Output
- Model outputs and predictions saved as: `SMB_Dynamic_Credit_Line.csv`
- Includes fields:
  - `Predicted_AdjustCreditLine`
  - `Predicted_DynamicCreditLine`
