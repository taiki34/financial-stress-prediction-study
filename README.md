# Financial Stress Prediction from Mobile Money Activity

This project began with my participation in the Zindi AI4EAC Liquidity Stress Early Warning Challenge, where I placed **12th on the final leaderboard** in a field of about 270 participants.

The task was to estimate the probability that a customer would experience liquidity stress within 30 days from six months of mobile-money activity. After the competition, I extended the work into an independent study of validation, feature engineering, model comparison, and calibration. Because the evaluation combines log loss and ROC-AUC, the analysis treats ranking and probability calibration as separate problems.

**Project status:** complete competition project and retrospective study  
**Main notebook:** [`financial_stress_prediction_report.ipynb`](financial_stress_prediction_report.ipynb)

## Competition context and scope

The challenge's prizes were restricted to students enrolled at universities in the East African Community, so my leaderboard placement was not eligible for a prize. This was not professor-supervised coursework.

After the competition, I used the publicly released first-place workflow as a reference for the self-directed extension documented here. The later analysis focuses on validation, feature testing, model comparison, and calibration.

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
