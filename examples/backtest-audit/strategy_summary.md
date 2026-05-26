# Strategy Summary: Equity Mean Reversion (RSI-20)

This document provides a detailed architectural summary of the proposed Equity Mean Reversion strategy prior to independent validation and backtest audit.

---

## 1. Strategy Identity & Parameters
- **Strategy ID:** `EQ_MR_RSI20_US_LC`
- **Investment Universe:** S&P 500 Constituents (US Large-Cap Equities)
- **Primary Hypothesis:** Assets exhibiting short-term extreme price momentum (measured by a 20-period Relative Strength Index) tend to mean-revert over a 1-week horizon, driven by institutional block-rebalancing flows and liquidity provider compensation.
- **Trading Style:** Statistical Arbitrage / Mean Reversion
- **Rebalance Frequency:** Weekly on Friday close

---

## 2. Signal Generation & Mathematical Model
The strategy generates cross-sectional signals by calculating a 20-period Relative Strength Index (RSI-20) on daily close prices $P_{i,t}$.

### Signal Steps:
1. **RSI Calculation:**
   
   $$\text{RSI}_{i,t} = 100 - \frac{100}{1 + \text{RS}_{i,t}}$$
   
   where $\text{RS}_{i,t} = \frac{\text{EMA}(\text{U}, 20)}{\text{EMA}(\text{D}, 20)}$; $\text{U}$ is the daily upward price change and $\text{D}$ is the downward change.

2. **Cross-Sectional Normalization:**
   To establish a relative value ranking across the index constituents, raw RSI values are converted into cross-sectional Z-Scores:
   
   $$Z_{i,t} = \frac{\text{RSI}_{i,t} - \mu_{\text{RSI}, t}}{\sigma_{\text{RSI}, t}}$$
   
   where $\mu_{\text{RSI}, t}$ and $\sigma_{\text{RSI}, t}$ represent the cross-sectional mean and standard deviation of all active index constituents at time $t$.

3. **Winsorization:**
   Z-Scores are winsorized at $\pm 3.0$ standard deviations to prevent outliers from dominating capital allocations:
   
   $$\hat{Z}_{i,t} = \min(\max(Z_{i,t}, -3.0), 3.0)$$

4. **Target Sizing:**
   Target long positions are assigned to constituents where $\hat{Z}_{i,t} \le -1.5$ (oversold), and target short positions where $\hat{Z}_{i,t} \ge 1.5$ (overbought). Sizing is linear relative to the Z-score deviation.

---

## 3. Flawed Execution Assumptions
In the original backtest submitted by the model developer, the following execution rules were assumed:
- **Instant Fills:** Fills are assumed at Friday's closing price $P_{i,t}$ at the exact millisecond the weekly signal is generated.
- **Linear Slippage:** Slippage and fees are modeled as a flat, constant cost of **1.0 basis point** per trade, regardless of trade size relative to Average Daily Volume (ADV).
- **Index Universe:** Static indexing S&P 500 constituents as of October 2025 were used retrospectively back to 2018.
