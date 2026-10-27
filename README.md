# Credit Risk – Probability of Default Modeling

> 🚧 **Work in progress.** This repository is being built step by step; results will be added as each stage is validated.

## Objective

Estimate the **probability of default (PD)** of borrowers and compare an interpretable baseline (logistic regression) with more flexible machine learning models (Random Forest, Gradient Boosting).

The goal is not only to rank borrowers by risk, but to produce **calibrated, explainable PDs** that could support credit decisions, provisioning and stress testing.

This project extends my undergraduate thesis in Actuarial Science (University of Buenos Aires).

## Questions this project answers

1. How much predictive power do ML models add over logistic regression?
2. Are the estimated probabilities well calibrated, so they can be read as PDs?
3. Which drivers explain default risk, and do the models agree on them?
4. How does the portfolio's PD change under adverse scenarios?

## Methodology

| Stage | Notebook | Status |
|---|---|---|
| Exploratory data analysis | `01_EDA.ipynb` | ⬜ |
| Data preparation & feature engineering | `02_Data_Preparation.ipynb` | ⬜ |
| Logistic regression baseline | `03_Logistic_Regression.ipynb` | ⬜ |
| Model comparison (Random Forest, Gradient Boosting) | `04_Model_Comparison.ipynb` | ⬜ |
| Calibration & interpretability (Brier score, SHAP) | `05_Calibration_Interpretability.ipynb` | ⬜ |
| Portfolio stress testing | `06_Stress_Testing.ipynb` | ⬜ |

**Evaluation:** ROC-AUC, Gini, precision/recall, calibration curves and Brier score.

## Data

*To be documented:* source, horizon, target definition and data dictionary.

## Repository structure

```
credit-risk-pd-modeling/
├── data/
│   ├── raw/          # original data (not tracked)
│   └── processed/    # cleaned datasets
├── notebooks/        # analysis, step by step
├── src/              # reusable functions
├── reports/figures/  # charts used in this README
└── requirements.txt
```

## Results

*Coming soon.*

## Limitations and next steps

*Coming soon.*

## Author

**Ramiro López** · Actuarial Science, University of Buenos Aires · ramalopez1510@gmail.com
