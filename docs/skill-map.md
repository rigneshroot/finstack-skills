# FinStack Skills Responsibility Map

This document defines the roles, primary responsibilities, and key checklists for the entire FinStack Skills catalog.

---

## Core Skills (Cross-Cutting)

| Slash Command | Specialist Role | Primary Responsibility | Key Checklist focus |
|---|---|---|---|
| `/quant-research-director` | **Research Director** | Evaluates economic thesis and out-of-sample validation design | Stationarity, economic anomaly, parameter sensitivity |
| `/backtest-auditor` | **Backtest Auditor** | Forensic check for data leaks, survivorship, and lookahead biases | Target leakage, timing lag, delisting bias, p-hacking |
| `/model-risk-officer` | **Model Risk Officer** | Regulatory governance in compliance with **SR 11-7** framework | Conceptual soundness, drift monitoring, model bounds |
| `/portfolio-risk-manager` | **Portfolio Risk Manager** | Portfolio concentration, leverage, tail-risk, and liquidity caps | Expected Shortfall (ES), 10% ADV limits, stress replays |
| `/quant-red-team` | **Red Team Adversary** | Adversarial stress-testing to break strategy assumptions | Factor crowdedness, regime shift failure, kill criteria |

---

## Hedge Fund Vertical (`skills/hedge-funds/`)

*Focused on speed, capacity constraints, execution microstructure, and alternative datasets.*

| Slash Command | Specialist Role | Primary Responsibility | Key Checklist focus |
|---|---|---|---|
| `/alpha-decay-monitor` | **Decay & Capacity Specialist** | Monitors alpha half-life and capacity-AUM scaling elasticity | Predictive decay curve, ADV scaling, crowded factor co-movement |
| `/execution-optimizer` | **Microstructure Analyst** | TCM audits, spread-crossing, borrow rates, and leverage | Non-linear market impact, HTB borrow locate costs, SPAN margins |
| `/alternative-data-auditor` | **Alt-Data Auditor** | Point-in-time database integrity and MNPI compliance | Creation timestamps, web-scraping legality, panel attrition |

---

## Asset Manager Vertical (`skills/asset-managers/`)

*Focused on mandate compliance, style purity, and environmental/social scoring.*

| Slash Command | Specialist Role | Primary Responsibility | Key Checklist focus |
|---|---|---|---|
| `/factor-decomposer` | **Factor Attribution Analyst** | Systematic return decomposition and style drift auditing | Fama-French 5-Factor loadings, Style Drift Index (SDI) |
| `/benchmark-tracking-auditor` | **Benchmark Mandate Auditor** | Portfolio Active Share and tracking error constraints | UCITS 5/10/40 rule, tracking error bounds, closet indexing |
| `/esg-mandate-reviewer` | **ESG Integration Officer** | Sustainability metric compliance and exclusion checking | Weighted average carbon intensity (WACI), SFDR Article 8/9 |

---

## Investment Bank Vertical (`skills/investment-banks/`)

*Focused on macro stress-testing, counterparty pricing adjustments (XVA), and electronic safety controls.*

| Slash Command | Specialist Role | Primary Responsibility | Key Checklist focus |
|---|---|---|---|
| `/ccar-stress-tester` | **Stress-Testing Specialist** | Replaying portfolios under CCAR/DFAST stress scenarios | Severely Adverse shocks, Tier 1 capital RWA drawdowns |
| `/counterparty-risk-officer` | **Counterparty & XVA Analyst** | Netting, CSA term audits, and CVA pricing adjustments | Peak Forward Exposure (PFE), Wrong-Way Risk (WWR), Zero CSAs |
| `/algorithmic-trader-validator` | **Algo Compliance Officer** | Pre-trade risk controls and market manipulation detection | SEC Rule 15c3-5, infinite loop throttle, spoofing patterns |