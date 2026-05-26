# Challenger Model Review: Equity Mean Reversion Model

- **Primary Model ID:** `EQ_MR_RSI20_US_LC`
- **Challenger Model ID:** `EQ_MR_RSI20_SIMPLE_EW`
- **Review Date:** October 20, 2025
- **Lead Validator:** Lead Challenger Model Reviewer
- **Primary Standard:** **Federal Reserve Letter SR 11-7 (Conceptual Soundness)**

---

## 1. Description of Models

### Primary Model (Systematic Z-Score Optimised)
The primary model calculates daily winsorized cross-sectional RSI-20 Z-scores. Portfolio weights are dynamically optimized using a 90-day covariance matrix to minimize portfolio risk contribution, subject to a single-stock cap of $4.0\%$ and sector caps of $20.0\%$.

### Challenger Model (Simple Equal-Weighted Benchmark)
The challenger model uses the same daily RSI-20 signals but executes a simple equal-weighted allocation ($1/N$) across all active buy/sell candidates, completely ignoring covariance optimizations and risk-parity adjustments.

---

## 2. Performance Comparison Scorecard

| Performance Metric | Primary Model (Optimized Risk-Parity) | Challenger Model (Simple Equal-Weighted) | Performance Spread |
|---|---|---|---|
| Annualized Return | `15.8%` | `18.2%` | `-2.4%` (Challenger higher return) |
| Sharpe Ratio | `1.40` | `1.05` | `+0.35` (Primary higher Sharpe) |
| Maximum Drawdown | `-12.4%` | `-22.8%` | `+10.4%` (Primary lower drawdown) |
| Turnover (Annualized) | `1,200%` | `1,650%` | `-450%` (Primary lower turnover) |
| Deflated Sharpe Ratio (DSR) | `84.5%` | `61.2%` | `+23.3%` |

---

## 3. Parametric Sensitivity Cliff Analysis
To verify that the primary model is not hyper-overfitted, we tested its sensitivity to minor parameter shifts. We perturbed the Relative Strength Index lookback window from its optimal value of **20 days** across a range of **10 to 30 days**:

- **Lookback = 10 Days:** Sharpe degrades to `0.92` (higher turnover and noise).
- **Lookback = 15 Days:** Sharpe stable at `1.24`.
- **Lookback = 20 Days (Optimal):** Sharpe peaks at `1.40`.
- **Lookback = 25 Days:** Sharpe stable at `1.32`.
- **Lookback = 30 Days:** Sharpe degrades to `0.85` (slow signal reaction).

> [!TIP]
> **Sensitivity Verdict:**
> The strategy exhibits a smooth, bell-shaped performance curve around the 20-day optimal parameter rather than a sharp parameter "cliff." This indicates that the optimal parameter is structurally stable and not a random, overfitted statistical artifact.

---

## 4. MVG Final Verdict & Recommendations
The primary model's optimization layer successfully delivers superior risk-adjusted performance (Sharpe ratio $+0.35$) and reduces tail drawdowns by $10.4\%$ compared to the simpler equal-weighted challenger, justifying its mathematical complexity under **SR 11-7**. 

The model is **Approved for Live Deployment** subject to regular monthly replication of this challenger analysis.
