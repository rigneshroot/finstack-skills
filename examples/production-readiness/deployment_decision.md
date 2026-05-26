# Governance Approval & Deployment Decision Memorandum

- **Strategy ID:** `EQ_MR_RSI20_US_LC`
- **Authorized Capital:** **$100 Million AUM**
- **Sizing Buffer:** Half-Kelly limit active
- **Approval Date:** October 24, 2025
- **Signed:** Research Governance Committee & Model Risk Officer

---

## 1. Executive Verdict

Following a rigorous audit of the **Equity Mean Reversion (RSI-20)** strategy, the **Research Governance Committee** hereby issues an official **PRODUCTION APPROVED** status. The model developer (Dr. Alan Vance) has successfully remediated all timing lookahead, survivorship, and transaction cost biases flagged during the initial forensic audit. 

The composite **Production Readiness Score (PR-Score)** is certified at **84.8 / 100**, satisfying the firm's strict $\ge 80$ threshold for production capital deployment.

---

## 2. Certified PR-Score Breakdown

$$\text{PR-Score} = 85 \times 0.20 + 92 \times 0.20 + 82 \times 0.20 + 80 \times 0.20 + 85 \times 0.20 = 84.8$$

- **Data Integrity:** `85 / 100` (CRSP Point-in-time constituent list active)
- **Validation Quality:** `92 / 100` (Purged/Embargoed walk-forward cross-validation active)
- **Risk Controls:** `82 / 100` (99% ES active, single-stock cap <= 4%, sector cap <= 20%)
- **Execution Assumptions:** `80 / 100` (Almgren-Chriss TCM active, GC borrow fee schedule)
- **Governance Evidence:** `85 / 100` (SR 11-7 validation certified, model card filed)

---

## 3. Authorized Sizing and Capital Limits
- **Initial Capital Allocation:** **$100 Million AUM**.
- **Leverage Ceiling:** Capped at **1.50x Gross Exposure** (Net exposure must remain within $\pm 10.0\%$ to maintain market-neutrality).
- **Position Sizing Buffer:** Sizing is capped at **50% of the calculated Kelly Criterion limit** (Half-Kelly) to protect against parameter estimation errors and market regimes shifts.

---

## 4. Hard Operational Controls & Kill Switch
The Order Management System (OMS) gateway has hardcoded the following pre-trade controls:
- **Maximum Daily Loss (Drawdown) Stop-Out:** **-3.0% realized daily loss** on intraday NAV. If breached, the kill-switch deactivates the strategy, cancels all active orders, and liquidates positions.
- **Trailing Drawdown Stop-Out:** **-12.0% trailing peak drawdown**.
- **Liquidity Restriction Ceiling:** Order size is capped at **10% of 30-day Average Daily Volume (ADV)** for daily execution.
