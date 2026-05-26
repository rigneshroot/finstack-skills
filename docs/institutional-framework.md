# Institutional Governance & Regulatory Framework

FinStack Skills is designed to mirror the actual operational structures and regulatory compliance workflows mandated across Tier 1 financial institutions.

---

## 1. Federal Reserve SR 11-7 / OCC 2011-12
The **Supervisory Guidance on Model Risk Management (SR 11-7)** is the global gold standard for quantitative model governance. FinStack Skills replicates this via:
- **Separation of Duties:** The research phase (`/quant-research-director`) is structurally decoupled from the independent validation phase (`/model-risk-officer`).
- **Conceptual Soundness Review:** Interrogating mathematical formulations, data lineage, and underlying assumptions.
- **Ongoing Monitoring Plan:** Setting dynamic limits for model drift and defining strict triggers for recalibration or automated deactivation.

---

## 2. Basel III Capital Accord (G-SIB Standards)
For investment banking trading desks, portfolio management must align with international banking standards:
- **Capital Adequacy & RWAs:** Under `/ccar-stress-tester`, trading books are stress-tested against Federal Reserve CCAR/DFAST "Severely Adverse" macroeconomic shocks to calculate drawdown impact on Risk-Weighted Assets (RWAs) and Tier 1 Capital ratios.
- **Bilateral Margin Rules (UMR):** OTC derivative desks utilize `/counterparty-risk-officer` to audit Uncleared Margin Rules (UMR) and ensure appropriate Initial Margin (IM) posting via the Standard Initial Margin Model (SIMM).

---

## 3. UCITS & GIPS Standards
For traditional Asset Managers, fiduciary duty requires strict compliance with client mandates and disclosure standards:
- **UCITS 5/10/40 Rule:** Audited via `/benchmark-tracking-auditor` to ensure single-issuer concentration never breaches the regulatory limits for European-regulated mutual funds.
- **Active Share Integrity:** Preventing "closet indexing" (charging active fees for index-matching portfolios) by enforcing minimal Active Share targets.
- **GIPS returns compliance:** Aligning performance metrics with Global Investment Performance Standards.

---

## 4. SEC Rule 15c3-5 (The Market Access Rule)
For proprietary trading desks and electronic market makers:
- **Bypassing Risk Checks Banned:** Enforced via `/algorithmic-trader-validator` by requiring pre-trade capital and credit limits at the gateway layer.
- **Fat-finger & Erroneous Order Blocks:** Mandating Single Order Limits (SOL) and price collar band filters.
- **Loop Kill Switches:** Requiring cancel-on-disconnect (COD) heartbeats and order throttling to prevent cascade failures.

---

## 5. Alternative Data & Compliance
For systematic hedge funds:
- **Material Non-Public Information (MNPI):** Checked via `/alternative-data-auditor` to ensure data ingestion workflows comply with SEC insider trading misappropriation frameworks.
- **Point-in-Time Integrity:** Auditing data delivery timestamps to eliminate target leakage and lookahead bias.