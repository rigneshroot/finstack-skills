# Model Assumptions Audit: Equity Mean Reversion Model

- **Model ID:** `EQ_MR_RSI20_US_LC`
- **Audit Date:** October 19, 2025
- **Assumptions Validator:** Lead Challenger Model Reviewer

This document details the mathematical and statistical audits conducted on the core assumptions of the RSI-20 Mean Reversion strategy.

---

## 1. Stationarity & Cointegration Audit (ADF Test)
The strategy assumes that the cross-sectional winsorized RSI-20 Z-scores ($\hat{Z}_{i,t}$) are stationary and mean-reverting. We tested this assumption by running an **Augmented Dickey-Fuller (ADF)** unit root test on the signal timeseries across a representative sample of 50 liquid large-caps:

$$\Delta \hat{Z}_{t} = \alpha + \beta \hat{Z}_{t-1} + \sum_{j=1}^{p} \delta_j \Delta \hat{Z}_{t-j} + \epsilon_t$$

### Results:
- **Average ADF t-Statistic:** `-3.82` (1% Critical Value: `-3.43`, 5% Critical Value: `-2.86`)
- **Average p-Value:** `0.0024`
- **Audit Verdict:** **PASS.** We reject the null hypothesis of a unit root at the $99\%$ confidence level. The signals exhibit strong, stationary mean-reverting behavior, confirming that the statistical basis for mean-reversion is sound.

---

## 2. Residual Normality Audit (Jarque-Bera Test)
The portfolio construction model assumes that residual tracking errors and daily strategy returns are normally distributed. We tested the normality of daily residual returns using the **Jarque-Bera (JB)** test for skewness ($S$) and excess kurtosis ($K$):

$$\text{JB} = \frac{n}{6} \left( S^2 + \frac{(K-3)^2}{4} \right)$$

### Results:
- **Calculated Skewness ($S$):** `-0.84` (Negative skewness indicates left-tail risk)
- **Calculated Kurtosis ($K$):** `6.45` (Excess kurtosis indicates heavy fat tails)
- **Calculated JB Statistic:** `482.4` (Critical Value at 1%: `9.21`)
- **p-Value:** `< 0.0001`
- **Audit Verdict:** **FAIL.** We reject the null hypothesis of normal distribution at the $99\%$ confidence level. The residuals exhibit significant negative skewness and leptokurtic fat tails, which violates standard linear regression assumptions.
- **Remediation Mandate:** The risk desk must replace standard Value-at-Risk (VaR) models with **99% Expected Shortfall (ES)** to account for left-tail fat-tail events.

---

## 3. Constant Covariance & Correlation Stability Audit
The strategy utilizes a historical 90-day covariance matrix $\Sigma_t$ for risk budgeting. We tested whether this matrix remains stable during periods of high market stress using the **Box's M** test for covariance homogeneity.

### Results:
- **Chi-Square Approximation:** `1,280.4`
- **p-Value:** `< 0.0001`
- **Audit Verdict:** **FAIL.** Covariance matrices are highly non-stationary and exhibit extreme "correlation clumping" during market drawdowns (e.g. all stock correlations spike toward 1.0 during liquidity crashes).
- **Remediation Mandate:** Implement a dynamic correlation multiplier ($1.5\text{x}$) to scale down portfolio gross leverage when realized index volatility exceeds **20.0%**.
