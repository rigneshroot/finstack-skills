# Model Risk Governance: Independent Validation Report (SR 11-7 Compliant)

- **Model ID:** `EQ_MR_RSI20_US_LC`
- **Validation Date:** October 16, 2025
- **Validation Authority:** Chief Model Risk Officer & Independent Validation Committee
- **Rating:** **APPROVED WITH CONDITIONS (MEDIUM RISK)**

---

## 1. Executive Summary
This document serves as the regulatory-grade Independent Validation Report for the *S&P 500 Short-Term RSI Reversal Model* in compliance with the Federal Reserve **SR 11-7** guidelines. 

The validation team reviewed the conceptual soundness, validation evidence, and ongoing monitoring frameworks. The model's theoretical basis is **Conceptually Sound**, but it is highly sensitive to regime shifts and liquidity drops. The model is **Approved with Conditions** subject to the implementation of the mandated boundaries and circuit breakers.

---

## 2. Validation Scorecard

| SR 11-7 Pillar | Assessment | Score (1-5) |
|---|---|---|
| **Conceptual Soundness** | The mathematical signal formulation utilizes winsorized cross-sectional z-scores. Stationarity is preserved. However, the distribution of RSI-20 remains slightly non-normal at the tails. | `4.0 / 5.0` |
| **Out-of-Sample Validation** | The research desk utilized a proper walk-forward combinatorial cross-validation with a 20% purged out-of-sample block. Overfitting has been successfully mitigated. | `4.5 / 5.0` |
| **Ongoing Monitoring** | The monitoring plan incorporates daily tracking error checks and Population Stability Index (PSI) drift alerts. | `4.0 / 5.0` |
| **Limitations Control** | Circuit breakers are active, but they fail to account for systemic margin spikes during extreme market deleveraging. | `3.0 / 5.0` |

---

## 3. Detailed Technical Review

### 3.1 Conceptual Soundness & Assumptions
The model assumes that short-term stock deviations (RSI deviations) are temporary and driven by liquidity imbalances. 
- *Mathematical Critique:* RSI-20 is mathematically bounded between 0 and 100. Calculating standard normal z-scores on bounded variables is technically flawed near extremes. The validation team requires mapping raw RSI to a cumulative distribution function (CDF) to preserve normal tail scaling.
- *Stationarity:* Augmented Dickey-Fuller (ADF) test confirms the z-score series is stationary ($p < 0.01$), mitigating unit-root risks.

### 3.2 Operational Boundaries & Limitations
> [!CAUTION]
> **Correlation Breakdowns in Volatile Regimes:**
> During systemic market liqudiation events (e.g. VIX > 40), the historical cross-sectional relationships between stock returns break down. Assets that are normally uncorrelated correlate heavily, rendering the long/short hedge ineffective.

---

## 4. Mandated Conditions for Approval

To achieve full operational approval, the trading desk must implement these three controls:

### Condition 1: Volatility Circuit Breaker
- **Trigger:** If the realized 5-day annualized portfolio volatility exceeds **25.0%**, the strategy must automatically liquidate 50% of outstanding gross exposure.
- **Goal:** Neutralize leverage during systemic market selloffs.

### Condition 2: Short Borrow Limits (GC Only)
- **Trigger:** The algorithm must query the prime broker's daily locate inventory. Any stock requiring a Hard-to-Borrow (HTB) fee exceeding **5.0% annualized** must be automatically blacklisted from shorts.

### Condition 3: Regular Recalibration Check
- **Trigger:** If the rolling 30-day realized tracking error vs. the benchmark index exceeds **3.5%**, the model must pause trading and trigger an automatic parameter recalibration.
