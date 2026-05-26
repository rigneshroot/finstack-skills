# FinStack Skills Responsibility & Scorecard Mapping

This document maps all 14 FinStack Skills to their respective **PR-Score** components, primary **Common Failure Modes**, and key **Regulatory/Risk Covenants**.

---

## 1. Core Governance Pipeline

| Slash Command | specialist Role | PR-Score component | Primary Failure Mode Checked | Regulatory Covenant |
|---|---|---|---|---|
| `/quant-research-director` | **Research Director** | Validation Quality | Story Bias & CDF Normalization | **SR 11-7** Conceptual Soundness |
| `/backtest-auditor` | **Backtest Auditor** | Data Integrity & Execution Assumptions | Same-Bar execution lookahead bias | **MiFID II** Best Execution |
| `/model-risk-officer` | **Model Risk Officer** | Governance Evidence | Assumption Over-reliance & Drift | **SR 11-7** Model Validation |
| `/portfolio-risk-manager` | **Portfolio Risk Manager** | Risk Controls | Tail correlation convergence & ADV limits | **Basel III** Liquidity & Volatility |
| `/quant-red-team` | **Red Team Adversary** | Composite Haircut | Crowded trades & Outlier dependency | Institutional Risk Covenants |

---

## 2. Hedge Fund Vertical (`skills/hedge-funds/`)

| Slash Command | specialist Role | PR-Score component | Primary Failure Mode Checked | Core Focus |
|---|---|---|---|---|
| `/alpha-decay-monitor` | **Decay Specialist** | Execution Assumptions | Turnover Churn Bleed & ADV scaling | Signal half-life decay elasticity |
| `/execution-optimizer` | **Microstructure Analyst** | Execution Assumptions | Short Locate over-optimism & SPAN Margins | TCM market impact modeling |
| `/alternative-data-auditor` | **Alt-Data Auditor** | Data Integrity | Lookback Delivery Delay (Lookahead) | **SEC MNPI** Insider & PII checks |

---

## 3. Asset Manager Vertical (`skills/asset-managers/`)

| Slash Command | specialist Role | PR-Score component | Primary Failure Mode Checked | Regulatory Covenant |
|---|---|---|---|---|
| `/factor-decomposer` | **Factor Analyst** | Governance Evidence | Unhedged Sector bets (Sector Proxying) | **GIPS** return reporting rules |
| `/benchmark-tracking-auditor` | **Mandate Auditor** | Risk Controls | Closet indexing & cash drag dilutions | **UCITS 5/10/40** concentration bounds |
| `/esg-mandate-reviewer` | **ESG Integration Officer** | Governance Evidence | Greenwashing Derivative Loops | **SFDR Article 8/9** compliance |

---

## 4. Investment Bank Vertical (`skills/investment-banks/`)

| Slash Command | specialist Role | PR-Score component | Primary Failure Mode Checked | Regulatory Covenant |
|---|---|---|---|---|
| `/ccar-stress-tester` | **Stress Specialist** | Risk Controls | Linear Greek assumption breakdowns | **Fed CCAR / DFAST** stress shock |
| `/counterparty-risk-officer` | **Counterparty Analyst** | Governance Evidence | Severe Wrong-Way Risk (WWR) | **Uncleared Margin Rules (UMR)** SIMM |
| `/algorithmic-trader-validator` | **Algo Validator** | Risk Controls | Infinite Message Looping (Knight Capital) | **SEC Rule 15c3-5** Market Access |