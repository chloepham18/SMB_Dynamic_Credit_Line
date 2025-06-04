# 💳 Dynamic Credit Limit Assignment Model for SMB

This project implements an end-to-end machine learning pipeline to dynamically assign credit lines to small and medium-sized businesses (SMBs) using credit card data and financial attributes. The goal is to optimize lending costs, minimize capital risk, and enable smart, dynamic underwriting strategies.

Inspired by fintech innovators like Ramp, Brex, Stripe, and Sofi, this solution demonstrates how modern credit platforms can empower SMBs with adaptive financing.

---

## 🎯 Project Objectives

- Develop a dynamic credit limit assignment modeling framework for SMBs.
- Perform Exploratory Data Analysis (EDA), outlier analysis, and data cleaning.
- Train a binary classifier to predict if a credit line should be adjusted.
- Train a regression model to recommend new credit line amounts.
- Deploy a strategy to dynamically update credit lines month-to-month.

---

## 🧰 Technologies Used

- **Python:** Pandas, NumPy, Seaborn, Matplotlib for data processing and visualization.
- **Scikit-learn:** For classification and regression modeling.
- **XGBoost:** High-performance modeling for both classification and regression tasks.
- **Google Colab:** Execution environment for running the pipeline.
- **CSV-based data import:** Via Google Drive for dataset handling.

---

## 📂 Dataset Overview

The anonymized SMB dataset includes the following key features:

- **BusinessID, MOB:** Time-series tracking of each business.
- **DynamicCreditLine:** Actual approved credit line per month.
- **Financial attributes:** Collateral_Type, Loan_Purpose, Industry_Type, etc.

### Target Variables:
- **AdjustCreditLine:** Binary label (0 for no adjustment, 1 for adjustment).
- **DynamicCreditLine:** Regression target for the new credit line amount.

---

## 📊 Exploratory Data Analysis (EDA) Highlights

- **Outlier Detection & Removal:** Used Interquartile Range (IQR) per feature to identify and remove outliers.
- **Missing Values:** Imputed using domain-aware techniques to ensure data integrity.
- **Collateral_Type Stability:** No BusinessID showed changes in Collateral_Type across months, so mode aggregation was applied to handle inconsistencies.

### Visualizations:
- Trends in credit usage, business segmentation, and industry behaviors were visualized.
- Key plots include:
  - Average Dynamic Credit Line by Industry Type.
  - Feature importance for both classification and regression models.
  - Adjustment Rate by Collateral Type.

---

## 🤖 Modeling Workflow

### 1. Binary Classification: Should Credit Line Be Adjusted?

- **Objective:** Predict whether a business (BusinessID) requires a credit line adjustment based on monthly data changes.
- **Target:** AdjustCreditLine (binary: 0 for no adjustment, 1 for adjustment).
- **Features:** Categorical (Loan_Purpose, Collateral_Type), numerical, and encoded Industry_Type.
- **Model:** XGBoostClassifier.
- **Data Preprocessing:**
  - Industry_Type was label-encoded.
  - Other categorical variables (e.g., Loan_Purpose, Collateral_Type) were one-hot encoded.
- **Outcome:** Predict whether the credit line needs adjustment.

### 2. Regression: What Should the New Credit Line Be?

- **Objective:** For businesses predicted to need an adjustment (AdjustCreditLine = 1), predict the new DynamicCreditLine amount.
- **Target:** DynamicCreditLine (numeric).
- **Model:** XGBoostRegressor.
- **Outcome:** Recommend the optimal new credit line value.

---

## 📈 Evaluation Metrics

### 🔹 Classification Model: AdjustCreditLine Prediction

| Metric          | Validation | Test   |
|-----------------|------------|--------|
| Accuracy        | 0.9139     | 0.9121 |
| Precision (0)   | 0.95       | 0.94   |
| Recall (0)      | 0.49       | 0.49   |
| F1-Score (0)    | 0.65       | 0.64   |
| Precision (1)   | 0.91       | 0.91   |
| Recall (1)      | 0.99       | 0.99   |
| F1-Score (1)    | 0.95       | 0.95   |

**Insights:**  
High precision for class 0 indicates reliable predictions when no adjustment is needed, but low recall suggests some missed cases. For class 1, both precision and recall are high, showing effective identification of businesses needing adjustments.

---

### 🔹 Regression Model: DynamicCreditLine Prediction

| Metric                  | Validation | Test    |
|-------------------------|------------|---------|
| Mean Absolute Error (MAE)| 1436.65    | 1441.45 |
| Root Mean Squared Error (RMSE) | 1844.76 | 1854.00 |
| R² Score                | 0.9967     | 0.9968  |

**Insights:**  
MAE of ~$1,441 shows acceptable deviation in predictions. R² close to 1 demonstrates high accuracy in predicting new credit lines.

---

## 💡 Key Insights

### Model Performance
- Over 20% of businesses adjust their credit line month-to-month.
- The classification model excels at identifying businesses needing adjustments (high recall for class 1), though it misses some cases where no adjustment is needed (low recall for class 0).
- The regression model provides precise predictions for new credit lines, balancing growth and risk effectively.

### Feature Importance
- **Classification Model:**  
  Top features include `Current_Max_Monthly_Bank_Balance`, `Has_Collateral`, and `InitialCreditLine`.
- **Regression Model:**  
  Top features include `Current_Avg_Monthly_Bank_Balance`, `InitialCreditLine`, and `Current_Max_Monthly_Bank_Balance`.

### Collateral Type Impact
- Collateral_Type of **Accounts Receivable (AR)** has the highest adjustment rate (95.00%) and significantly influences credit line adjustment decisions.  
- Adjustment rates for other collateral types:  
  - Inventory: 94.88%  
  - Real Estate: 93.88%  
  - Equipment: 93.38%  
  - Intellectual Property: 93.36%  
  - Cash: 91.42%

### Industry Type Analysis
- Lowest average dynamic credit line: **Educational Service** (~$6,800)
- Highest average dynamic credit line: **Wholesale Trade** (~$111,000)

---

## 🤝 Business Impact

This dynamic credit line framework enables fintechs and lenders to:

- Make proactive, risk-aware lending decisions for SMBs.
- Support business growth with adaptive credit limits.
- Automate credit line adjustments, reducing manual overhead while optimizing capital allocation.

By combining classification and regression models, this solution provides a scalable approach to credit underwriting, balancing growth opportunities with risk management.

---

## 📁 Repository Structure

data/ # Raw and processed datasets
images/ # Visualizations and plots (feature importance, industry trends)
outputs/ # Model predictions (SMB_Dynamic_Credit_Line.csv) including Predicted_AdjustCreditLine, Predicted_DynamicCreditLine
notebooks/ # Google Colab notebooks for EDA and modeling
README.md # Project documentation
