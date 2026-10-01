# Financial Stress Prediction from Mobile Money Activity

This project was my submission for  the Zindi AI4EAC Liquidity Stress Early Warning Challenge, where I placed **12th on the final leaderboard** out of about 270 participants.

The task was to estimate the probability that a customer would experience liquidity stress within 30 days from six months of mobile money activity. After the competition, I created this project to go a bit more in depth and study  validation, feature engineering, model comparison and calibration. Because the evaluation combines log loss and ROC-AUC, the analysis treats ranking and probability calibration as separate problems.


**Main notebook:** [`financial_stress_prediction_report.ipynb`](financial_stress_prediction_report.ipynb)


## Dataset summary

- 40,000 training observations
- 30,000 test observations
- Binary target with an approximately 15% positive rate
- Six months of inflows, withdrawals, balances, merchant payments, bill payments, and account engagement


## Method

- Built recent-versus-older behavioural comparisons, cash-flow pressure measures, balance drawdown features and stable transformations for skewed monetary variables.
- Used five-fold stratified validation.
- Generated target encodings out of fold.
- Compared CatBoost, XGBoost, LightGBM, neural, ranking, and stacking variants.
- Tested monotonic rank-preserving calibration because the metric weights log loss more heavily than ROC-AUC.

## Main result

The final locally selected candidate achieved an out-of-fold ROC-AUC of **0.922525**, an improvement of **0.000093** over its reference prediction, with positive gains in all five folds. That gain did not transfer to the hidden test data, once tested on hidden data the model scored slightly lower compared with the public data. 


## Repository structure

```text
.
├── financial_stress_prediction_report.ipynb
├── results
│   └── aggregate_metrics.csv
├── .gitignore
└── requirements.txt
```




## Attribution

- [Zindi Liquidity Stress Early Warning Challenge](https://zindi.world/competitions/liquidity-stress-early-warning-challenge)

