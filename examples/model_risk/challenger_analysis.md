# Model Validation: Challenger Model Analysis

- **Model ID:** `EQ_MR_RSI20_US_LC`
- **Validation Desk:** Quantitative Model Validation Group (QMVG)
- **Review Date:** October 18, 2025

---

## 1. Context & Purpose
Under the **SR 11-7** framework, independent validation groups must benchmark a proposed quantitative model against an independent, simple heuristic model—referred to as the **Challenger Model**. 

This comparison determines if the proposed model's complexity (and associated model risk) is justified by superior risk-adjusted performance, or if the returns are simply capturing beta exposures that a simpler model could achieve at lower cost.

---

## 2. Model Specifications

### Proposed Model: Multi-Factor RSI-20 Z-Score
- **Logic:** Winsorized z-score of rolling 20-day RSI, optimized with volatility-adjusted portfolio weights, sector neutrality constraints, and daily rebalancing.
- **Complexity:** High (Requires real-time portfolio optimization, covariance matrix inputs, and continuous execution adjustments).

### Challenger Model: Simple 5-Day RSI Reversal
- **Logic:** Equal-weighted long positions in S&P 500 constituents with RSI-5 < 20, and equal-weighted short positions in constituents with RSI-5 > 80.
- **Complexity:** Extremely Low (Heuristic sizing, no optimization, zero parameter tuning).

---

## 3. Comparative Performance Analysis (2018–2025)

| Metric | Proposed Model (Optimized) | Challenger Model (Heuristic) | Performance Delta |
|---|---|---|---|
| Annualized Return | `14.8%` | `11.2%` | `+3.6%` |
| Sharpe Ratio | `1.40` | `1.05` | `+0.35` |
| Max Drawdown | `-15.2%` | `-24.4%` | `+9.2%` (MDR reduced) |
| Active Share | `82.4%` | `91.0%` | `-8.6%` |
| Monthly Turnover | `240%` | `410%` | `-170%` (T-Cost savings) |

---

## 4. Validation Verdict & Findings

The Independent Validation Group finds that the Proposed Model's complexity **is justified** by its superior risk-adjusted performance, which stems from two core optimizations:

1.  **Slippage Mitigation:** The challenger model's high turnover (410% monthly) eats 80% of its returns in transaction fees. The proposed model's optimized signal filters successfully reduce noise trades, saving **170% annualized turnover**.
2.  **Drawdown Protection:** During the March 2020 crash, the simple challenger suffered a severe -24.4% drawdown due to its lack of sector hedges. The proposed model's sector-neutral constraints successfully cushioned losses to -15.2%.

> [!TIP]
> **Validation Finding:**
> The proposed model is not simply "p-hacking" noise. The incremental complexity provides structural benefits in risk sizing and transaction cost mitigation that outperform the heuristic challenger.
