# Quantitative Model Validation Standards

This document establishes the mathematical and statistical validation rules mandated for all systematic trading models.

---

## 1. Out-of-Sample (OOS) Data Partitioning
Using the same dataset to train a model and evaluate its performance is strictly banned. 
*   **Purged & Embargoed Combinatorial Cross-Validation (de Prado):** Standard time-series cross-validation leaks information from the training set to the validation set due to overlapping data. 
    *   **Purging:** All training samples whose labels overlap with the validation set must be removed.
    *   **Embargoing:** Since returns are serially correlated, training samples immediately following the validation set must be embargoed (removed) by a window proportional to the signal's decay.

```
[ Train Block ] ──> [ Purge Gap ] ──> [ Validation Block ] ──> [ Embargo Gap ] ──> [ Train Block ]
```

*   **OOS Data Ratio:** Out-of-sample testing must represent at least **25.0%** of the total historical data window.

---

## 2. Statistical Robustness & Overfitting Tests
- **Deflated Sharpe Ratio (DSR):** The reported Sharpe ratio must be deflated to adjust for selection bias and the number of parameter configurations tested during the optimization phase.
- **augmented Dickey-Fuller (ADF) Test:** All features, signals, and spread relationships must pass the ADF unit-root test ($p < 0.01$) to verify mathematical stationarity. Non-stationary variables are strictly banned from direct inclusion in pricing models.
- **Outlier Sensitivity:** The validation desk will run the "Top-3 Outlier Exclusion Check." If removing the top 3 trading days of the backtest drops the Sharpe ratio by more than 30%, the strategy is rejected as non-robust.

---

## 3. Challenger Model Benchmarking
Every quantitative model must be evaluated against an independent **Challenger Model**:
*   **The Challenger Definition:** A simple, non-parameterized baseline heuristic (e.g., equal-weighted constituent indexes, simple momentum rules, or flat buy-and-hold benchmarks).
*   **Validation Requirement:** If the proposed model does not outperform the challenger model's Sharpe ratio by at least **0.25** or fails to reduce maximum drawdown by at least **5.0%**, the model's complexity is deemed unjustified and the strategy is rejected.
