# Expected Shortfall & Extreme Tail Risk Analysis

- **Strategy ID:** `EQ_MR_RSI20_US_LC`
- **Analysis Date:** October 25, 2025
- **Validator Desk:** Portfolio Risk Manager

This document provides a detailed tail-risk and Value-at-Risk (VaR) audit of the proposed RSI-20 Mean Reversion strategy.

---

## 1. 99% Value-at-Risk (VaR) vs. Expected Shortfall (ES)
Due to the non-normal, fat-tailed distribution of residual returns (Jarque-Bera test failed at $p < 0.0001$), standard linear Value-at-Risk (VaR) models severely underestimate extreme tail loss. We calculated the **99% Expected Shortfall (ES)** (Conditional VaR)—measuring the average expected loss in the worst $1\%$ of return outcomes—using a 1,000-trial historical simulation:

### Risk Metrics ($100M Portfolio Scale):
- **95% Daily VaR:** `-1.24%` (Potential daily capital loss: `$1.24 Million`)
- **99% Daily VaR:** `-2.38%` (Potential daily capital loss: `$2.38 Million`)
- **99% Expected Shortfall (ES):** `-3.85%` (Potential daily capital loss: **`$3.85 Million`**)

> [!WARNING]
> **Tail-Loss Indicator:**
> The Expected Shortfall is **1.6x higher** than the 99% VaR, confirming a highly leptokurtic distribution. The portfolio risk manager mandates that the desk's unencumbered cash buffer be set at a minimum of **$4.0 Million** to guarantee survival of a 99% ES event without forced liquidation.

---

## 2. Multi-Strategy Correlation & Contagion Spikes
Mean reversion strategies are highly vulnerable to systematic factor co-movements during liquidity panics. We modeled the correlation of the RSI-20 strategy against our active systematic portfolios across different market regimes:

- **Standard Market Correlation:** `0.08` (Highly diversified, zero factor overlap)
- **High Volatility Regime (VIX > 25):** `0.34` (Moderate co-movement)
- **Extreme Liquidity Freeze Regime (VIX > 40):** `0.78` (Severe correlation clumping)

### Contagion Risk Mitigations:
To prevent systemic drawdown contagion, the risk gateway will enforce a **leverage contraction trigger**: if the rolling 10-day cross-strategy correlation coefficient exceeds **0.50**, target gross leverage is automatically scaled down from **1.50x to 1.0x**.
