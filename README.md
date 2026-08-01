# 📈 Invoice Payment Risk Regression

An end-to-end regression project that predicts invoice **days past due (`dpd_target`)** using customer, invoice, payment-history, and behavioural features.

---

## 🎯 Business Objective

Accurately estimating invoice payment delay can help collections and finance teams:

- Prioritise follow-ups
- Forecast cash flow more effectively
- Identify invoices that may require early intervention
- Improve collection planning

---

## 📊 Modelling Approaches

### Approach A — Original Target

Regression models are trained directly on the original `dpd_target`.

### Approach B — Yeo–Johnson Transformed Target

A Yeo–Johnson transformation is applied to the target variable before modelling to evaluate whether reducing target skew improves predictive performance.

The transformer is fitted on the training target and then applied to the test target.

---

## 📂 Project Workflow

- Data Loading and Inspection
- Target Analysis
- Identifier Removal
- Date Variable Removal
- High Missing Value Removal
- Low Variance Filtering
- Correlation Analysis
- Variance Inflation Factor (VIF)
- Feature Selection
- Missing Value Treatment
- Outlier Treatment
- Linear Regression Baseline
- LightGBM Regression
- XGBoost Regression
- Random Forest Regression
- Yeo–Johnson Target Transformation
- Model Evaluation
- Model Comparison

---

## 📈 Recorded Performance

### Original Target

| Model | Test MAE | Test RMSE | Test R² |
|---|---:|---:|---:|
| Linear Regression | 15.26 | 25.75 | 0.375 |
| LightGBM | 12.71 | 22.89 | 0.506 |
| XGBoost | 12.93 | 23.14 | 0.495 |
| Random Forest | 12.79 | 23.24 | 0.490 |

### Yeo–Johnson Transformed Target

| Model | Test MAE | Test RMSE | Test R² |
|---|---:|---:|---:|
| Linear Regression | 0.51 | 0.75 | 0.442 |
| LightGBM | 0.43 | 0.68 | 0.546 |

> The transformed-target MAE and RMSE values are measured in transformed space. Predictions should be inverse-transformed before these errors are interpreted in days.

---

## 💡 Key Finding

The recorded LightGBM test R² improved from approximately **0.506** on the original target to **0.546** after applying the Yeo–Johnson target transformation.

This suggests that reducing target skew improved the model's ability to explain variation in invoice payment delay.

For a complete business comparison, transformed predictions should be converted back to the original days-past-due scale before calculating MAE and RMSE.

---

## 🔍 Key Techniques

- Exploratory Data Analysis
- Feature Selection
- Low Variance Filtering
- Correlation Analysis
- Variance Inflation Factor
- Missing Value Treatment
- Outlier Treatment
- Linear Regression
- LightGBM Regression
- XGBoost Regression
- Random Forest Regression
- Yeo–Johnson Target Transformation
- Regression Model Evaluation

---

## 🛠 Technologies Used

- Python
- Pandas
- NumPy
- Scikit-learn
- LightGBM
- XGBoost
- Statsmodels
- Matplotlib
- SciPy
- Jupyter Notebook

---

## 📁 Repository Structure

```text
invoice-payment-risk-regression/
│
├── Invoice_Payment_Risk_Regression.ipynb
├── README.md
├── requirements.txt
├── .gitignore
├── data/
├── images/
└── outputs/
```

---

## 📊 Dataset

The source datasets are not included in this repository.

Place the original files at:

```text
data/train_data_shuffle.csv
data/test_data_shuffle.csv
```

The transformed-target approach reads prepared datasets from:

```text
outputs/df_train_shuffle_data.csv
outputs/df_test_shuffle_data.csv
```

Do not upload these files if they contain proprietary, confidential, or company-provided data.

---

## 🚀 Future Improvements

- Inverse-transform predictions for business-readable error metrics
- Build a leakage-safe preprocessing pipeline
- Add cross-validation
- Perform systematic hyperparameter tuning
- Compare additional regression algorithms
- Add SHAP-based model explainability
- Perform residual analysis across customer and invoice segments
- Deploy the model using Streamlit

---

## 📝 Note

This repository combines two regression approaches in one structured notebook to compare model performance before and after target transformation. The original modelling experiments are preserved to demonstrate the full analysis and decision-making process.
