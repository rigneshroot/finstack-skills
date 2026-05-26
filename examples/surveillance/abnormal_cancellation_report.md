# Abnormal Cancellation Compliance Report

- **Report ID:** `COMP_AN_20251025_12`
- **Audit Date:** October 25, 2025
- **Compliance Officer:** Lead Regulatory Controls Reviewer
- **Target Strategy:** Equity Mean Reversion (RSI-20)
- **Status:** **WARNING ISSUED - DESTRUCTIVE THROTTLING IMMINENT**

---

## 1. Regulatory Warning Summary
The NASDAQ Exchange Market Operations group has issued a formal warning regarding the trading behavior of the firm's algorithmic routing gateway. The proposed **Equity Mean Reversion (RSI-20)** strategy exhibits an **Abnormal Cancel-to-Fill Ratio** on several large-cap symbols. 

Excessive cancellation messages strain exchange matching engines without contributing to genuine liquidity, violating exchange fair-access rules and triggering high surcharge fees.

---

## 2. Cancellation and Messaging Statistics

The following table displays the daily message metrics across the most active symbols:

| Traded Symbol | Total Messages Routed | Total Fills (Executions) | Total Cancellations | Cancel-to-Fill Ratio (OTR) | Exchange Limit | Compliance Status |
|---|---|---|---|---|---|---|
| `TSLA` | `482,450` | `240` | `482,210` | **2,009 : 1** | 100 : 1 | **BREACH (CRITICAL)** |
| `NVDA` | `320,150` | `185` | `319,965` | **1,729 : 1** | 100 : 1 | **BREACH (CRITICAL)** |
| `MSFT` | `98,420` | `350` | `98,070` | **280 : 1** | 100 : 1 | **BREACH (HIGH)** |
| `JPM` | `12,800` | `140` | `12,660` | **90 : 1** | 100 : 1 | **PASS (WARNING)** |

---

## 3. Financial Surcharge Penalty
Under NASDAQ Commission Rule Section 118, OTRs (Order-to-Trade Ratios) exceeding **100:1** are penalized under a progressive surcharge structure:
- **Ratio 101 - 500:** `$0.005` per excess cancellation message.
- **Ratio > 500:** `$0.01` per excess cancellation message.
- **Estimated Daily Penalty:**
  - *TSLA Excess Cancels:* $482,210 - (240 \times 100) = 458,210$ messages $\times \$0.01 = \$4,582.10$ per day.
  - *NVDA Excess Cancels:* $319,965 - (185 \times 100) = 301,465$ messages $\times \$0.01 = \$3,014.65$ per day.
  - *Total Cumulative Daily Penalty:* **`$7,596.75`** (entirely consuming strategy profits).

---

## 4. Compliance Directive & Throttling Remediations
The high OTR is a result of the algorithm "quote chasing"—cancelling and re-entering limit orders at every microsecond tick change of the spread.
- **Mandate:** The model developer must immediately implement a **Minimum Order Life (MOL)** gate of **50 milliseconds** at the execution handler. This prevents order updates from being routed to the exchange until the resting order has resided in the book for at least 50 milliseconds, reducing the OTR to $< 40:1$.
