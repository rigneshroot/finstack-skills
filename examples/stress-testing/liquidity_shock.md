# Stressed Liquidity Shock & Time-to-Liquidate (TTL) Analysis

- **Strategy ID:** `EQ_MR_RSI20_US_LC`
- **Shock Date:** October 25, 2025
- **Risk Officer:** Chief Liquidity Risk Officer

This document details the portfolio exit horizons and stressed liquidation slippage under a simulated **50% contraction in market Average Daily Volume (ADV)**.

---

## 1. Time-to-Liquidate (TTL) Simulation
We model the number of business days required to liquidate the target **$100 Million** portfolio under standard and stressed liquidity regimes, enforcing a maximum participation ceiling of **10% ADV** per day under normal conditions, and **5% ADV** under stress to prevent severe market impact.

### Portfolio Liquidation Horizon:
- **Normal Liquidity (10% ADV Limit):**
  - $85.0\%$ of the portfolio liquidated within **1 business day**.
  - $98.2\%$ of the portfolio liquidated within **3 business days**.
  - $100\%$ of the portfolio liquidated within **4 business days**.
  - *Verdict:* **PASS.** Satisfies standard capital guidelines.

- **Stressed Liquidity (50% ADV contraction & 5% ADV Limit):**
  - $62.0\%$ of the portfolio liquidated within **1 business day**.
  - $84.5\%$ of the portfolio liquidated within **3 business days**.
  - $94.2\%$ of the portfolio liquidated within **5 business days**.
  - $100\%$ of the portfolio liquidated within **8 business days** (driven by illiquid mid-cap constituents).
  - *Verdict:* **CONDITIONAL PASS.** The portfolio requires a maximum capitalization cap of **$80 Million** for highly volatile mid-cap sub-strategies to maintain a Stressed TTL $< 5$ days.

---

## 2. Stressed Market Impact Slippage
Using the **Almgren-Chriss** square-root impact model, we calculated the expected transaction slippage cost if forced to execute a rapid, emergency exit of the entire portfolio within **48 hours** under a simulated liquidity freeze:

$$\text{Stressed Slippage (bps)} = \text{Stressed Spread (bps)} + \gamma \times \sigma_{\text{stressed}} \times \left(\frac{\text{Trade Size}}{0.5 \times \text{ADV}}\right)^{0.5}$$

### Expected Fire-Sale Impact:
- **Standard Slippage:** `6.8 bps` (Expected portfolio cost: `$68,000`)
- **48-Hour Stressed Liquidation Slippage:** `42.5 bps` (Expected portfolio capital loss: `$425,000`)
- **Stressed Exit Horizon Verdict:** The fire-sale loss is bounded within the firm's maximum allowable loss limit of **0.50% of total capital** ($500,000$), validating the portfolio concentration limits.
