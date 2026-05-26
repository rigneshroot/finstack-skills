# Portfolio Sizing & Stress-Testing Report

- **Report Date:** October 19, 2025
- **Portfolio ID:** `EQ_MR_RSI20_PORT`
- **Allocated Capital:** $100 Million
- **Risk Desk:** Portfolio Risk Management & Stress-Testing Desk

---

## 1. Tail-Risk Metrics (Value-at-Risk & Expected Shortfall)

We conducted a portfolio-level tail-risk assessment utilizing a historical simulation method with a rolling 250-day lookback.

- **99% Value-at-Risk (1-day VaR):** `-$1.85 Million` (`-1.85%` of AUM). Under normal market conditions, there is a 1% probability the portfolio loses more than $1.85M in a single trading day.
- **99% Expected Shortfall (1-day ES):** `-$2.45 Million` (`-2.45%` of AUM). If a tail event occurs, the expected average loss is $2.45M.
- **Current Leverage:** `1.40x Gross` (0.23x Long, -0.17x Short, net market exposure: +0.06x).

---

## 2. Historical Crisis Scenario Stress Replay

We replayed the current portfolio weights against historical macroeconomic crisis periods to evaluate capital drawdown risks.

| Stress Scenario | Historical Dates | Macro Shock | Simulated Portfolio Loss | Capital Cushion Status |
|---|---|---|---|---|
| **2020 COVID Liquidity Crisis** | March 9-20, 2020 | S&P 500 fell -30%; VIX spiked to 82. Correlations converged to 1.0. | `-$18.2 Million` (`-18.2%`) | **PASS** (Within -20% allocation buffer) |
| **2011 Euro Debt Crisis** | July-August 2011 | European credit spreads spiked. High-beta US stocks crashed. | `-$8.5 Million` (`-8.5%`) | **PASS** |
| **2018 Volpocalypse** | Feb 5, 2018 | XIV inverse-vol ETF collapsed. VIX spiked 100% intraday. | `-$6.2 Million` (`-6.2%`) | **PASS** |
| **1987 Black Monday** | Oct 19, 1987 | Single-day US equity crash of -22.6%. Systemic liquidity freeze. | `-$28.4 Million` (`-28.4%`) | **FAIL** (Tier 1 stress limit breached) |

---

## 3. Correlation Breakdown Risk Analysis
> [!IMPORTANT]
> **Correlation Convergence Hazard:**
> Under standard economic regimes, the strategy's long technology stocks are hedged by short energy and consumer staple positions. However, during systemic liquidity crises (like March 2020), this hedge disintegrates. Investors liquidate all assets to raise cash, causing correlations to spike to +1.0. The longs collapse while the shorts experience severe squeezes, causing double losses on both sides of the book.

---

## 4. Operational Risk Allocations & Mandates
The portfolio risk committee enforces the following boundaries based on this stress audit:

- **Capital Cap:** The absolute strategy capital allocation is capped at **$50 Million** until realized out-of-sample volatility is audited for 180 days.
- **Leverage Ceiling:** Gross leverage is capped at **1.50x**. Bypassing this limit will trigger an automatic execution halt.
- **Sector Volatility Trigger:** If the realized 5-day sector correlation exceeds **0.85**, gross exposure to that sector must be reduced by 30% within 24 hours.
