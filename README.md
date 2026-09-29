# Financial Stress Prediction from Mobile Money Activity

This repository documents an independent, post-competition study of liquidity-stress prediction using data and model artefacts released after a Zindi challenge.

The aim is to estimate the probability that a customer will experience liquidity stress in the next 30 days from six months of mobile-money activity. Because the evaluation combines log loss and ROC-AUC, the work treats ranking and probability calibration as separate problems.

**Project status:** complete retrospective study  
**Main notebook:** [`financial_stress_prediction_report.ipynb`](financial_stress_prediction_report.ipynb)

## Provenance and scope

This was not professor-supervised coursework and should not be presented as an eligible prize entry. The starting raw data and reference workflow came from a publicly released first-place solution repository. The analysis here is a self-directed extension focused on validation, feature testing, model comparison, and calibration.

No code from the reference solution is included in this portfolio package. The challenge data and large model-ready matrices are also excluded.

## Dataset summary

- 40,000 training observations
- 30,000 test observations
- Binary target with an approximately 15% positive rate
- Six months of inflows, withdrawals, balances, merchant payments, bill payments, and account engagement
- 694 numeric model features in the saved modelling matrices

## Method

- Built recent-versus-older behavioural comparisons, cash-flow pressure measures, balance drawdown features, and stable transformations for skewed monetary variables.
- Used five-fold stratified validation with `SEED = 42`.
- Generated target encodings out of fold.
- Compared CatBoost, XGBoost, LightGBM, neural, ranking, and stacking variants.
- Kept public leaderboard evidence separate from local cross-validation.
- Tested monotonic rank-preserving calibration because the metric weights log loss more heavily than ROC-AUC.

## Main result

The final locally selected candidate achieved an out-of-fold ROC-AUC of **0.922525**, an improvement of **0.000093** over its reference prediction, with positive gains in all five folds. That gain did not transfer to the hidden test data: its public and revealed private competition scores were lower than the earlier calibrated candidate.

This negative result is part of the analysis rather than something removed from it. It shows why small improvements among highly correlated predictions can fail under train-test shift, even when every validation fold improves.

## Repository structure

```text
.
├── financial_stress_prediction_report.ipynb
├── results
│   └── aggregate_metrics.csv
├── .gitignore
└── requirements.txt
```

The notebook is an executed report. Re-running the full workflow requires the original challenge files, saved model matrices, and intermediate experiment summaries, which are not redistributed here. The committed outputs allow the modelling decisions and results to be reviewed without those files.

## Limitations

- The original raw-data audit cannot be reproduced from this public package.
- The public leaderboard covered only part of the hidden test set.
- Many candidate predictions were highly correlated, increasing the risk of leaderboard overfitting.
- Feature importance is not causal and can be unstable across correlated variables.

## Attribution

- [Zindi Liquidity Stress Early Warning Challenge](https://zindi.world/competitions/liquidity-stress-early-warning-challenge)
- Public first-place reference repository: `Mouhamadmm466/FinancialStress_Solution_Zindi`
