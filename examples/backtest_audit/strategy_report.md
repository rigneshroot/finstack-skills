# Quantitative Strategy Proposal: Equity Mean Reversion (RSI-20)

- **Date:** October 12, 2025
- **Author:** Dr. Alan Vance, Quantitative Research Desk
- **Target Universe:** S&P 500 Constituents
- **Status:** Draft / Research Phase
- **Target Allocation:** $100 Million
- **Intended Rebalance:** Weekly (Every Friday at Close)

---

## 1. Executive Summary
This proposal outlines a systematic, high-Sharpe short-term mean-reversion strategy trading S&P 500 constituents. By measuring short-term overbought and oversold conditions using a modified 20-period Relative Strength Index (RSI), the strategy captures transient liquidity imbalances. 

In our backtest spanning January 2018 to September 2025, the strategy achieves an annualized return of **22.4%** with a Sharpe Ratio of **2.45** and a maximum drawdown of **11.2%**.

---

## 2. Investment Thesis & Economic Rationale
Short-term stock prices deviate from their fundamental value due to liquidity-driven imbalances (institutional block trading, mutual fund flows, and index rebalancing). Market makers and systematic desks are compensated for providing liquidity to absorb these flows. 

The strategy systematically goes long stocks that are oversold (RSI-20 < 30) and shorts stocks that are overbought (RSI-20 > 70), rebalancing weekly to allow the prices to revert to their historical moving averages.

---

## 3. Mathematical Signal Formulation
Let $P_{i,t}$ be the closing price of stock $i$ on day $t$. The Relative Strength Index ($RSI_{i,t}$) is calculated over a rolling 20-day window:

$$RS_{i,t} = \frac{\text{EMA}_{i,t}(\text{Up}, 20)}{\text{EMA}_{i,t}(\text{Down}, 20)}$$
$$RSI_{i,t} = 100 - \left(\frac{100}{1 + RS_{i,t}}\right)$$

We compute a cross-sectional z-score of the RSI across the investable universe:

$$Z_{i,t} = \frac{RSI_{i,t} - \mu_{t}(RSI)}{\sigma_{t}(RSI)}$$

- **Long Signal:** $Z_{i,t} < -1.5$ (Target weight: Proportional to signal strength)
- **Short Signal:** $Z_{i,t} > 1.5$ (Target weight: Proportional to signal strength)

---

## 4. Backtest Methodology
- **Execution Price:** Friday Close (`close_t`)
- **Transaction Costs:** Flat 1.0 basis point (0.01%) per trade, assuming zero market impact or slippage.
- **Universe:** Current S&P 500 index constituents.
- **Leverage:** 1.0x Gross (Longs offset by shorts to maintain market neutrality).

---

## 5. Performance Statistics (Reported)

| Metric | Value |
|---|---|
| Annualized Return | `22.4%` |
| Annualized Volatility | `9.1%` |
| Sharpe Ratio | `2.45` |
| Maximum Drawdown | `-11.2%` |
| Win Rate (Weekly) | `61.2%` |
| Profit Factor | `1.85` |
| Average Trade Duration | `5 days` |
