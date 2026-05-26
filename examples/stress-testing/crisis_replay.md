# Historical Crisis Replay Stress Analysis

- **Strategy ID:** `EQ_MR_RSI20_US_LC`
- **Stress Date:** October 24, 2025
- **Validator Desk:** Independent Stress Testing Desk

This document details the simulated strategy performance and capital decay when replaying actual historical market crises.

---

## 1. 2008 Lehman Collapse (Subprime Crisis)
- **Historical Period:** September 1, 2008 to December 31, 2008
- **Scenario Description:** Extreme equity market liquidations, surging volatility (VIX peak at $80.86$), and tightening short-sale borrow constraints.

### Simulated Performance Metrics:
- **Maximum Intraday Drawdown:** `-24.8%`
- **Cumulative Strategy P&L:** `-15.2%`
- **Short Borrow Fee Spike:** Average borrow rates jumped from General Collateral ($0.50\%$) to Hard-to-Borrow ($12.5\%$) on $18\%$ of portfolio short names.
- **Audit Findings:** The negative skewness of residual returns triggered a severe tail loss. The strategy survived without bankruptcy, but required liquidating $15\%$ of illiquid positions to maintain margin.

---

## 2. 2010 Flash Crash (High-Frequency Liquidity Freeze)
- **Historical Period:** May 6, 2010
- **Scenario Description:** E-Mini S&P futures liquidity collapses, bid-ask spreads widen by $>50\text{x}$ within minutes, and high-frequency cancel-to-fill ratios spike.

### Simulated Performance Metrics:
- **Maximum Intraday Drawdown:** `-8.4%` (primarily due to spread crossing costs)
- **Execution RTT Latency Spike:** Broker matching execution latency surged from $50\mu s$ to $18,000\mu s$ during the primary crash wave.
- **Audit Findings:** Passive limit orders experienced extreme adverse selection (toxic fills right before price collapse). The dynamic **VPIN** throttle successfully deactivated order routing at 2:42 PM, mitigating further losses.

---

## 3. 2020 COVID Liquidity Shock
- **Historical Period:** March 9, 2020 to March 31, 2020
- **Scenario Description:** Extreme global correlation co-movement, consecutive limit-down market circuit breakers, and global capital contagion flows.

### Simulated Performance Metrics:
- **Maximum Intraday Drawdown:** `-18.2%`
- **Cross-Strategy Correlation Spike:** Correlation coefficients between historically uncorrelated stock categories spiked from $0.15$ to $0.88$.
- **Audit Findings:** Correlation clumping completely neutralized the portfolio's market-neutral hedge, exposing it to systematic beta drift. Sizing has been scaled down via the volatility correlation multiplier.
