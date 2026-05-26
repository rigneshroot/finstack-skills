# Trade Surveillance Alert: Potential Spoofing & Layering Activity

- **Alert ID:** `TS_AL_20251025_08`
- **Audit Date:** October 25, 2025
- **Surveillance Desk:** Global Market Integrity & Surveillance Group
- **Target Strategy:** Equity Mean Reversion (RSI-20)
- **Status:** **HIGH SEVERITY - ESCALATED FOR COMPLIANCE AUDIT**

---

## 1. Alert Trigger Summary
Our automated market surveillance systems triggered an alert at **09:42:15.820 EST** on S&P constituent **AAPL** (Apple Inc.). The algorithm exhibited patterns consistent with **Spoofing and Layering**—the entry of non-bona fide orders designed to create a false appearance of market depth, inducing other participants to buy or sell, followed by rapid order cancellations.

---

## 2. Event Timeline & FIX Log Lineage

The following microsecond FIX log audit shows the order entries, layers, executions, and subsequent cancellations:

| Timestamp (EST) | FIX Tag 35 (MsgType) | FIX Tag 55 (Symbol) | FIX Tag 44 (Price) | FIX Tag 38 (Qty) | FIX Tag 54 (Side) | Event Description / Intent |
|---|---|---|---|---|---|---|
| `09:42:15.820452` | `D` (Order Single) | `AAPL` | `$182.42` | `50,000` | `1` (Buy) | **Bona Fide Order:** Resting buy order at bid price, which the algorithm actually intends to execute. |
| `09:42:15.822312` | `D` (Order Single) | `AAPL` | `$182.46` | `100,000` | `2` (Sell) | **Spoof Layer 1:** Large non-bona fide order entered on the offer, designed to create selling pressure. |
| `09:42:15.823154` | `D` (Order Single) | `AAPL` | `$182.47` | `150,000` | `2` (Sell) | **Spoof Layer 2:** Large non-bona fide order entered one tick above offer to amplify selling pressure. |
| `09:42:15.824880` | `D` (Order Single) | `AAPL` | `$182.48` | `200,000` | `2` (Sell) | **Spoof Layer 3:** Deep non-bona fide order entered to mimic heavy institutional selling inventory. |
| `09:42:15.829112` | `8` (Execution Report) | `AAPL` | `$182.42` | `50,000` | `1` (Buy) | **FILLED:** Bona fide resting order executes as market participants react to the massive offer layers. |
| `09:42:15.830420` | `F` (Order Cancel) | `AAPL` | `$182.46` | `100,000` | `2` (Sell) | **CANCEL LAYER 1:** Cancelled immediately after bona fide order was filled. Elapsed time: $8.1 \text{ms}$. |
| `09:42:15.831110` | `F` (Order Cancel) | `AAPL` | `$182.47` | `150,000` | `2` (Sell) | **CANCEL LAYER 2:** Cancelled immediately. Elapsed time: $7.9 \text{ms}$. |
| `09:42:15.832040` | `F` (Order Cancel) | `AAPL` | `$182.48` | `200,000` | `2` (Sell) | **CANCEL LAYER 3:** Cancelled immediately. Elapsed time: $7.1 \text{ms}$. |

---

## 3. Microstructure Impact Analysis
- **Execution Intent:** The algorithm successfully filled **50,000 shares** at a favorable bid price ($182.42$) by creating **450,000 shares of artificial offer depth**, which was cancelled in under **10 milliseconds** post-fill.
- **Toxicity Check:** The trade occurred during a spike in AAPL's **VPIN** ($0.84$), indicating that other participants were forced to trade against toxic flow.
- **Compliance Verdict:** This behavior directly violates exchange anti-manipulation policies and the Dodd-Frank Act's anti-spoofing provisions. The algorithm has been temporarily blocked from routing short/sell orders in AAPL pending review.
