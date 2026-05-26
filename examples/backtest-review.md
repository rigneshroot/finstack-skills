# Walkthrough: Institutional Strategy Review (Sample Output)

This document provides a realistic, end-to-end simulation of **finstack-skills** running an equity mean-reversion strategy through the quantitative review gauntlet.

---

## The Strategy: US Large-Cap Equity Mean Reversion
- **Description:** Exploits short-term mean reversion in S&P 500 constituents using rolling z-scores of 5-day RSI.
- **Rebalance Frequency:** Weekly (Every Friday Close).
- **Target AUM:** $150 Million.
- **Assumed Transaction Cost:** Flat 1.0 basis point per trade.

---

```
You:    I have a mean-reversion strategy on US large-cap equities.
        Here's my research notebook and backtest results.
```

---

### Step 1: Research Evaluation
```
You:    /quant-research-director
```

#### [QRD] Quantitative Research Director Review

**Research Readiness Score:** `6.0 / 10`  
**Go/No-Go Recommendation:** `CONDITIONAL PASS`

##### economic & Signal Assessment
| Dimension | Findings | Severity |
|---|---|---|
| Economic Thesis | The strategy exploits short-term liquidity provider compensation (supplying liquidity to institutional block traders). This anomaly is structurally sound but highly commoditized. | `Low` |
| Mathematical Formulation | Signal z-score uses rolling 20-day mean/std of RSI. RSI is bounded [0, 100], making standard normal z-scores mathematically flawed near extremes. Winsorization or CDF mapping is missing. | `Medium` |
| Decay Alignment | **CRITICAL FLAWE:** The alpha signal has an estimated half-life of 1.5 days. However, the rebalance frequency is Weekly. For 3.5 out of 5 trading days, the portfolio is holding stale, decayed signals with zero predictive power. | `High` |

##### Validation Design Critique
> [!WARNING]
> **Signal Churn & Decay Leakage:**
> Rebalancing weekly on a short-term signal introduces severe "alpha leakage." The simulated out-of-sample performance is likely heavily overfitted to capture a few idiosyncratic tail events.

##### Required Action Items
- `[ ]` Shift rebalance frequency to Daily or implement a rolling execution trigger.
- `[ ]` Implement winsorization on the signal boundaries to prevent outliers from distorting sizing.
- `[ ]` Perform parameter sensitivity analysis for the RSI window (vary from 3 to 10 days).

---

### Step 2: Forensic Backtest Audit
```
You:    I have changed the rebalance frequency to Daily. Re-running the backtest.
You:    /backtest-auditor
```

#### [BTA] Forensic Backtest Audit Report

**Production Readiness Score:** `4.0 / 10`  
**Audit Verdict:** `REJECTED`

##### Forensic Findings Table
| Bias Category | Finding & Evidence | Severity |
|---|---|---|
| Lookahead & Timing | **CRITICAL FAIL:** The backtest engine calculates signals using Friday's `close_t` price and executes the trade at the exact same `close_t` price. This assumes instant execution at 4:00 PM without market impact or timing lag. | `Critical` |
| Survivorship & Universe | **SURVIVORSHIP BIAS DETECTED:** The backtest trades the current 2026 constituents of the S&P 500 index retrospectively back to 2018. This excludes companies like Lehman Brothers, Enron, and Sears that went bankrupt, overstating annual returns by ~2.1%. | `High` |
| Transaction Cost Realism | **OPTIMISTIC SLIPPAGE:** Assumed a flat 1.0 bp slippage. The strategy trades mid-caps with wider spreads. At $150M AUM, participation rate in smaller constituents exceeds 15% ADV, requiring a non-linear market impact model. | `High` |

##### Statistical Health Checks
- **Reported Sharpe Ratio:** `2.45`
- **Haircut Sharpe Ratio:** `0.85` (After applying point-in-time universe, 1-day execution lag, and realistic slippage)
- **Deflated Sharpe Ratio (DSR):** `24.5%` (Extremely high probability of backtest overfitting)

##### Remediation Plan
- `[ ]` Force execution lag: Signals calculated at `close_t` must execute at the volume-weighted average price (VWAP) of `t+1`.
- `[ ]` Ingest a Point-in-Time (PIT) constituent database to eliminate survivorship bias.
- `[ ]` Replace flat slippage with an Almgren-Chriss square-root impact model.

---

### Step 3: Sizing & Portfolio Risk Management
```
You:    Lookahead bias fixed (lag added). Point-in-time universe integrated.
        Sharpe is now 1.40. Let's size it.
You:    /portfolio-risk-manager
```

#### [PRM] Portfolio Risk Assessment

**Portfolio Sizing Rating:** `CONSERVATIVE`  
**Drawdown Risk Rating:** `MEDIUM`  
**Recommended AUM Cap:** `$50 Million` (Scaled down from requested $150M due to liquidity bounds)

##### Portfolio Risk Scorecard
| Risk Category | Key Assessment | Recommended Limit | Status |
|---|---|---|---|
| Single Asset Concentration | Max weight is 8.5% in highly volatile tech names. | `Max 4.0% weight` | `Violation` |
| Sector Concentration | The portfolio is heavily clustered in Technology (48% of gross exposure). | `Max 25.0% cap` | `Violation` |
| Tail-Risk (99% ES) | Stressed Expected Shortfall is -3.2% daily. | `Max -2.0% daily ES` | `Violation` |
| Liquidity Exposure | Average exit time is 4.2 trading days under stressed conditions. | `Max 2.0 days exit` | `Violation` |

##### Historical Stress Analysis
> [!IMPORTANT]
> **Worst-Case Stress Scenario (2020 COVID Selloff):**
> Under a replica of the March 2020 liquidity shock, this mean-reversion strategy suffers a **-24.8% max drawdown** in 9 trading days due to correlation spike where all stocks sold off in unison, breaking the long/short hedge.

##### Actionable Risk Controls
- `[ ]` Limit gross exposure of Tech sector to 20%.
- `[ ]` Implement a hard liquidity constraint: No position can exceed 3% of the stock's 30-day ADV.
- `[ ]` Cap maximum single-stock allocation at 4.0%.

---

### Step 4: Adversarial Stress Attack
```
You:    Constraints added. Portfolio rebalanced.
You:    /quant-red-team
```

#### [QRT] Adversarial Stress-Test Report

**Adversarial Assessment:** `MODERATELY FRAGILE`  
**Kill Recommendation:** `CONDITIONAL PASS`

##### The Three Attacks

###### Attack 1: The Crowded Trade & Liquidity Shock
- The strategy trades standard RSI reversal which is a heavily crowded factor. 
- During a market deleveraging event, high-frequency market makers withdraw liquidity. This will cause the bid-ask spreads of the portfolio's mid-cap constituents to widen by 400%, wiping out 100% of the active alpha.

###### Attack 2: The Structural Regime Collapse
> [!CAUTION]
> **Fragile Cointegration Assumption:**
> The strategy assumes that mean reversion is a constant law. In trending bull markets (like 2021), this strategy will continuously sell momentum leaders and buy laggards, leading to a "momentum squeeze" that causes severe capital destruction.

###### Attack 3: Mathematical Outlier Interrogation
- Removing the top 4 trading days (which occurred during extreme high-volatility reversals) drops the portfolio's annualized return from 12.4% to 3.1%. The strategy's profitability is highly dependent on tail events rather than consistent statistical edge.

##### Hard Kill Criteria
- **Drawdown Limit:** Permanent deactivation if realized drawdown exceeds `12.0%` (2x simulated ES).
- **Tracking Deviation:** Kill strategy if live daily tracking error vs. backtest exceeds `3.5%` over any 10-day rolling window.
- **Turnover Drift:** Automatically stop trading if slippage costs consume >40% of realized weekly gross profits.