# AI-Assisted Framework Skills System Layer & Scorecard Mapping

This document maps all 21 validator skills to their respective **System Layer** parameters, including **PR-Score** components, **Primary Escalation Triggers**, **Key Evidence Requirements**, and **Severe Severity Deficiencies**.

---

## 1. Core Governance Pipeline

| Slash Command | Specialist Role | PR-Score Component | Key Escalation Trigger | Required Evidence |
|---|---|---|---|---|
| `/quant-research-director` | **Research Director** | Validation Quality | Reported gross Sharpe $> 4.0$ or OOS window $< 20\%$ | Walks-forward Purged/Embargoed cross-validation logs |
| `/backtest-auditor` | **Backtest Auditor** | Data Integrity & Execution Assumptions | Same-Bar execution lookahead bias | Full trade execution logs, point-in-time constituent sources |
| `/challenger-model-reviewer` | **Challenger Model Reviewer** | Governance Evidence (SR 11-7) | Zero challenger comparisons or extreme parametric sensitivity | Documented primary `model_card.yaml`, parameter sensitivity test results |
| `/model-risk-officer` | **Model Risk Officer** | Governance Evidence | Missing independent challenger heuristic | Signed validation certificate, model assumptions matrix |
| `/portfolio-risk-manager` | **Portfolio Risk Manager** | Risk Controls | Sector concentration $> 25\%$ or single stock $> 5\%$ | 99% Stressed Expected Shortfall modeling data |
| `/stress-testing-officer` | **Stress Testing Officer** | Risk Controls | Stressed loss exceeding Tier 1 capital buffers | Historical crisis replay and macro volatility shock outputs |
| `/factor-exposure-reviewer` | **Factor Exposure Reviewer** | Risk Controls | Unintended style factor tilts ($>2.0$ standard deviations) | Time-varying factor regression tracking charts |
| `/production-readiness-reviewer` | **Production Readiness Reviewer** | Operational & Telemetry | PR-Score $< 80$ or missing automated rollback | Automated rollback script logs, Prometheus/Grafana dashboard setups |
| `/quant-red-team` | **Red Team Adversary** | Composite Haircut | Strategy factor co-movement $> 0.75$ with crowded indexes | P&L outlier check (Top-3 day exclusion checks) |
| `/research-governance-chair` | **Governance Committee Chair** | Final Approval State | Governance bypass or unresolved high-severity risk failures | Signed validator checklist logs, documented capital restriction limits |

---

## 2. Hedge Fund Vertical (`skills/hedge-funds/`)

| Slash Command | Specialist Role | PR-Score Component | Key Escalation Trigger | Required Evidence |
|---|---|---|---|---|
| `/alpha-decay-monitor` | **Decay Specialist** | Execution Assumptions | Expected trade execution size $> 10\%$ ADV | Forward-returns correlation decay curves |
| `/market-microstructure-analyst` | **Market Microstructure Analyst** | Execution Assumptions | Instant limit order fills assumed or VPIN toxicity $> 0.80$ | Calibrated Almgren-Chriss TCM, VPIN time-series logs |
| `/liquidity-risk-officer` | **Liquidity Risk Officer** | Risk Controls | Stressed TTL $> 10$ business days or position $> 15\%$ ADV | Stressed TTL (5% ADV Limit) model output, concentration HHI |
| `/alpha-decay-reviewer` | **Alpha Decay Reviewer** | Execution Assumptions | Zero residual alpha ($p > 0.05$) or capacity collapse under $10M | Fama-French 5-Factor regression outputs, IC decay curves |
| `/execution-optimizer` | **Microstructure Analyst** | Execution Assumptions | Hard-to-Borrow fee $> 8\%$ or SPAN margins $> 50\%$ | SPAN/TIMS margin requirement calculations |
| `/alternative-data-auditor` | **Alt-Data Auditor** | Data Integrity | Unverified delivery timestamps or MNPI insider risk | Vendor due diligence audit consent records |

---

## 3. Asset Manager Vertical (`skills/asset-managers/`)

| Slash Command | Specialist Role | PR-Score Component | Key Escalation Trigger | Required Evidence |
|---|---|---|---|---|
| `/portfolio-allocation-committee` | **Allocation Committee Chair** | Risk Controls | Sizing exceeds Half-Kelly limit or correlation clumping $> 0.75$ | Risk Contribution Parity weighting model, marginal risk contribution |
| `/factor-decomposer` | **Factor Analyst** | Governance Evidence | 90-day Style Drift Index (SDI) $> 0.25$ | Time-varying factor regression t-statistics |
| `/benchmark-tracking-auditor` | **Mandate Auditor** | Risk Controls | Realized Active Share $< 60\%$ (closet indexing) | UCITS 5/10/40 concentration checklists |
| `/esg-mandate-reviewer` | **ESG Integration Officer** | Governance Evidence | Any exclusion list violation (weapons, coal, etc.) | Signed carbon WACI Scope 1/2 calculations |

---

## 4. Investment Bank Vertical (`skills/investment-banks/`)

| Slash Command | Specialist Role | PR-Score Component | Key Escalation Trigger | Required Evidence |
|---|---|---|---|---|
| `/ccar-stress-tester` | **Stress Specialist** | Risk Controls | Stressed capital loss breaches Tier 1 capital buffer | Stressed SLR under CCAR Severely Adverse shock |
| `/counterparty-risk-officer` | **Counterparty Analyst** | Governance Evidence | Unenforceable close-out netting in bankruptcy jurisdiction | Bilateral CSA parameters, Peak exposure (PFE 95%) |
| `/algorithmic-trading-validator` | **Algo Validator** | Risk Controls | Bypassable gateway pre-trade SOL bounds or missing COD | Sandbox simulation UAT order-entry FIX logs |
| `/regulatory-controls-reviewer` | **Regulatory Controls Reviewer** | Risk Controls | Missing pre-trade SOL limits or bypassable risk gates | Pre-trade SOL price collars config, CAT event log records |