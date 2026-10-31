# Credit Risk – Probability of Default Modeling

> 🚧 **Work in progress.** This repository is being built step by step; results are added as each stage is validated.

## Objective

Estimate the **probability of default (PD)** of borrowers and compare an interpretable baseline (logistic regression) with more flexible machine learning models (Random Forest, Gradient Boosting).

The goal is not only to rank borrowers by risk, but to produce **calibrated, explainable PDs** that could support credit decisions, provisioning and stress testing.

This project extends my undergraduate thesis in Actuarial Science (University of Buenos Aires).

## Key finding so far: SMOTE breaks PD calibration

In my thesis, all models were trained on a SMOTE-balanced dataset and every calibration curve sat below the diagonal. To test whether SMOTE was the cause, I ran a controlled experiment: same data, same split, same logistic regression, with and without SMOTE.

| Model | AUC | Brier score | Average PD |
|---|---|---|---|
| Logistic regression **with** SMOTE | 0.812 | 0.155 | 36.9% |
| Logistic regression **without** SMOTE | 0.807 | 0.052 | 6.5% |
| Naive benchmark (everyone gets the observed default rate) | 0.500 | 0.062 | 6.6% |

*Observed default rate in the test set: 6.6%.*

- **Ranking is unchanged:** AUC is almost identical with or without SMOTE.
- **Probabilities are not:** SMOTE inflates the average PD more than 5×, and its Brier score is worse than the naive benchmark.
- **Why:** SMOTE moves the training default rate from 6.6% to 50%, which shifts every predicted log-odds upward. The order of borrowers is preserved; the level of their PDs is not.
- **Why it matters:** an overestimated PD inflates IFRS 9 provisions and Basel capital, and prices good borrowers out of credit.

👉 Full experiment: [`notebooks/smote_calibration_experiment.ipynb`](notebooks/smote_calibration_experiment.ipynb)

## Questions this project answers

1. How much predictive power do ML models add over logistic regression?
2. Are the estimated probabilities well calibrated, so they can be read as PDs?
3. Which drivers explain default risk, and do the models agree on them?
4. How does the portfolio's PD change under adverse scenarios?

## Methodology

| Stage | Notebook | Status |
|---|---|---|
| SMOTE and calibration experiment | `smote_calibration_experiment.ipynb` | ✅ |
| Exploratory data analysis | `01_EDA.ipynb` | ✅ |
| Data preparation & feature engineering | `02_Data_Preparation.ipynb` | ✅ |
| Logistic regression baseline | `03_Logistic_Regression.ipynb` | ⬜ |
| Model comparison (Random Forest, Gradient Boosting) | `04_Model_Comparison.ipynb` | ⬜ |
| Calibration & interpretability (Brier score, SHAP) | `05_Calibration_Interpretability.ipynb` | ⬜ |
| Portfolio stress testing | `06_Stress_Testing.ipynb` | ⬜ |

**Evaluation:** ROC-AUC, Gini, KS, precision/recall, calibration curves and Brier score, always compared against a naive benchmark.

## Data

[Give Me Some Credit](https://www.kaggle.com/c/GiveMeSomeCredit) (Kaggle): 150,000 borrowers, 10 features, target = serious delinquency (90+ days past due) within 2 years.

The data is not included in this repository (Kaggle's terms do not allow redistribution). To reproduce: download `cs-training.csv` and place it in `data/raw/`.

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

## Next steps

1. Treat outliers in `RevolvingUtilizationOfUnsecuredLines` and the `DebtRatio` distortion when income is missing.
2. Retrain all models without SMOTE and evaluate post-hoc calibration (Platt / isotonic) for tree-based models.
3. Stratified cross-validation.
4. Portfolio stress testing of aggregate PD.

## Author

**Ramiro López** · Actuarial Science, University of Buenos Aires · ramalopez1510@gmail.com
