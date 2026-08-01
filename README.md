# Invoice Payment Risk Regression

An end-to-end regression project that predicts invoice **days past due (`dpd_target`)** using customer, invoice, payment-history, and behavioural features.

## Business objective

Accurately estimating payment delay can help collections and finance teams prioritise follow-ups, forecast cash flow, and identify invoices that may require early intervention.

## Modelling approaches

This project compares two approaches:

### Approach A — Original target

Models are trained directly on `dpd_target`.

Models evaluated:

- Linear Regression
- LightGBM
- XGBoost
- Random Forest

### Approach B — Yeo–Johnson transformed target

The target is transformed using Yeo–Johnson before modelling. The transformer is fitted on the training target and applied to the test target.

Models evaluated:

- Linear Regression
- LightGBM

## Project workflow

- Data loading and inspection
- Target analysis
- Identifier and date-variable removal
- High-missing-variable removal
- Low-variance filtering
- Correlation analysis
- VIF analysis
- Feature selection
- Missing-value treatment
- Outlier treatment
- Linear Regression baseline
- LightGBM regression
- XGBoost regression
- Random Forest regression
- Yeo–Johnson target transformation
- Model comparison

## Recorded performance

### Original target

| Model | Test MAE | Test RMSE | Test R² |
|---|---:|---:|---:|
| Linear Regression | 15.26 | 25.75 | 0.375 |
| LightGBM | 12.71 | 22.89 | 0.506 |
| XGBoost | 12.93 | 23.14 | 0.495 |
| Random Forest | 12.79 | 23.24 | 0.490 |

### Transformed target

| Model | Test MAE | Test RMSE | Test R² |
|---|---:|---:|---:|
| Linear Regression | 0.51 | 0.75 | 0.442 |
| LightGBM | 0.43 | 0.68 | 0.546 |

The transformed-target metrics are measured in transformed space. Predictions should be inverse-transformed before MAE and RMSE are interpreted in days.

## Technologies used

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

## Repository structure

```text
invoice-payment-risk-regression/
├── Invoice_Payment_Risk_Regression.ipynb
├── README.md
├── requirements.txt
├── .gitignore
├── data/
├── images/
└── outputs/
```

## Dataset

The source datasets are not included.

Place the original files at:

```text
data/train_data_shuffle.csv
data/test_data_shuffle.csv
```

The second modelling approach reads prepared datasets from:

```text
outputs/df_train_shuffle_data.csv
outputs/df_test_shuffle_data.csv
```

Do not upload these files if they are proprietary or confidential.

## Key finding

The recorded LightGBM R² increased from approximately **0.506** on the original target to **0.546** after Yeo–Johnson transformation. A complete comparison should inverse-transform predictions and calculate errors on the original days-past-due scale.

## Future improvements

- Inverse-transform predictions for business-readable metrics
- Build a leakage-safe preprocessing pipeline
- Add cross-validation
- Perform systematic hyperparameter tuning
- Add SHAP explainability
- Segment residual analysis
- Streamlit deployment
