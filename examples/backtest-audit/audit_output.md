# Forensic Backtest Audit Report: RSI Mean Reversion Strategy

- **Audit Date:** October 14, 2025
- **Auditor Desk:** Independent Model Validation & Backtest Audit Desk
- **Target Strategy:** Equity Mean Reversion (RSI-20)
- **Status:** **REJECTED - DO NOT DEPLOY**

---

## 1. Executive Summary

A comprehensive forensic audit of the proposed RSI-20 Mean Reversion strategy was conducted. While the strategy's reported Sharpe of **2.45** is mathematically impressive, our audit revealed three critical structural biases that render the simulation invalid. 

After adjusting the backtest engine for lookahead timing, survivorship bias, and realistic transaction costs, the strategy's Sharpe collapses from **2.45 to 0.54**, with a maximum drawdown widening from **-11.2% to -34.8%**.

---

## 2. Production Readiness Score (PR-Score)

The strategy was evaluated using the **PR-Score** framework:

```
Composite PR-Score: 36 / 100 [CRITICAL REJECT]
```

- **Data Integrity:** `45 / 100` (Degraded due to survivorship constituent bias)
- **Validation Quality:** `20 / 100` (Failed due to critical lookahead timing logic)
- **Risk Controls:** `50 / 100` (Concentration caps missing)
- **Execution Assumptions:** `15 / 100` (Flat 1bp transaction cost is highly optimistic)
- **Governance Evidence:** `50 / 100` (Incomplete out-of-sample data partitioning)

---

## 3. Forensic Bias Breakdown

### Bias 1: Critical Lookahead Timing Bias (Timing Lag)
> [!CAUTION]
> **Lookahead Execution:**
> The backtest engine calculates the RSI-20 signal using Friday's close price $P_{i,t}$ and executes the trade at that exact same price $P_{i,t}$ on the same Friday. This assumes the trading desk possesses instant, zero-latency execution capabilities at 4:00 PM without information leakage. 
> 
> *Impact:* Applying a standard 1-day execution lag (calculating signals at Friday close and executing at Monday VWAP) reduces the strategy's annualized return from 22.4% to 9.2%.

### Bias 2: Constituent Survivorship Bias
- **Finding:** The backtest used the static constituent list of the S&P 500 index from October 2025 retrospectively back to 2018. This excludes companies that defaulted, went bankrupt, or were acquired (e.g., SVB, Signature Bank, First Republic) over the backtest window.
- **Impact:** Survivorship bias overstates the annualized return by **+2.4%** across the 7-year period.

### Bias 3: Optimistic Slippage and Transaction Cost Models
- **Finding:** The backtest assumed a flat 1.0 bp transaction fee. However, the strategy trades heavily in the bottom quintile of S&P 500 market caps (mid-caps). At the target $100M allocation, trades would regularly exceed **12% of the constituent ADV**, causing substantial market impact.
- **Impact:** Applying the non-linear **Almgren-Chriss** square-root impact model:
  
  $$\text{Slippage (bps)} = \text{Spread (bps)} + \gamma \times \sigma_{\text{daily}} \times \left(\frac{\text{Trade Size}}{\text{ADV}}\right)^{0.5}$$
  
  reveals that execution costs actually average **6.8 bps**, consuming over 60% of gross alpha.

---

## 4. Adjusted Performance Comparison

| Performance Metric | Reported Backtest | Auditor Restated |
|---|---|---|
| Annualized Return | `22.4%` | `5.8%` |
| Sharpe Ratio | `2.45` | `0.54` |
| Maximum Drawdown | `-11.2%` | `-34.8%` |
| Turnover (Annualized) | `1,200%` | `1,200%` |
| Est. Slippage Cost | `1.0 bp` | `6.8 bps` |

---

## 5. Audit Recommendation
The strategy is **Rejected** for live capital allocation. The reported returns are a mathematical artifact of lookahead timing and constituent selection biases. The research desk is directed to implement the remediation plan detailed in the `findings.json` audit log before resubmission.
