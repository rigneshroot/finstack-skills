# FinStack: The AI Operating System for Quantitative Research Governance

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Governance Standard: SR 11-7](https://img.shields.io/badge/Governance-SR%2011--7-red.svg)](https://www.federalreserve.gov/supervisionreg/srletters/sr1107.htm)
[![Market Integrity: SEC 15c3-5](https://img.shields.io/badge/Compliance-SEC%2015c3--5-green.svg)](https://www.sec.gov/rules/final/2010/34-63241.pdf)

> "The best quant strategies don't die in production because of bad math. They die because nobody stress-tested the assumptions, nobody audited the backtest, and nobody asked 'what kills this trade?'" — Every Portfolio Manager who lost money on a crowded factor.

Wall Street runs on independent review committees, risk sign-offs, and adversarial challenge. A systematic strategy doesn't touch a single dollar of live capital until a research director evaluates the economic thesis, a backtest auditor checks for statistical biases, a model risk officer signs the governance review, a portfolio risk manager sizes the exposure, and a red team tries to kill it. 

**FinStack is that entire institutional review pipeline, automated.** It is an **AI Operating System for Quantitative Research Governance** — a suite of 14 specialized, role-based AI agents that interrogate systematic strategies, audit backtests, enforce regulatory constraints, and prevent capital destruction.

---

## Why FinStack Exists: The Multi-Strat Wedge

Traditional AI coding assistants focus on **strategy generation** (writing more backtests, fitting more parameters, scraping more data). **FinStack focuses on the high-value institutional bottlenecks:**
*   **Preventing Bad Research & False Alpha** — Exposing target leakage, lookahead bias, and survivorship anomalies before they burn capital.
*   **Accelerating Regulatory Validation** — Automating model risk documentation in compliance with the Federal Reserve **SR 11-7** and UK PRA **SS 1/23** frameworks.
*   **Standardizing Audit Lineage** — Generating standardized, machine-readable validation reports and findings for risk committees.
*   **Enforcing Microstructure Realism** — Auditing slippage models, short borrow constraints (HTB), and market-access risk gates (**SEC Rule 15c3-5**).

---

## Inspiration

FinStack is inspired by Y Combinator CEO Garry Tan's [gstack](https://github.com/garrytan/gstack), which structures AI agents into a virtual engineering team (CEO, designer, EM, QA, release engineer). FinStack applies this same paradigm to **institutional quantitative finance** — turning your AI coding assistant into a virtual investment committee and model risk validation desk.

*   `gstack` asks: _"Does this code ship?"_
*   `FinStack` asks: _"Does this strategy survive?"_

---

## Repository Structure

The framework decouples cross-cutting core risk reviews from specialized vertical portfolios:

```
finstack-skills/
├── skills/
│   ├── core/                           # Cross-Cutting Governance Pipeline
│   │   ├── quant-research-director/    # Economic thesis & validation design
│   │   ├── backtest-auditor/           # Forensic bias & leakage check (PR-Score)
│   │   ├── model-risk-officer/         # SR 11-7 model risk validation
│   │   ├── portfolio-risk-manager/     # Sizing, Expected Shortfall, & drawdowns
│   │   └── quant-red-team/             # Adversarial stress & hard kill criteria
│   │
│   ├── hedge-funds/                    # Vertical: Signal, Execution & Alt-Data
│   │   ├── alpha-decay-monitor/        # Half-life decay curves & AUM capacity
│   │   ├── execution-optimizer/        # TCM, spread crossing, & SPAN margins
│   │   └── alternative-data-auditor/   # Point-in-time integrity & MNPI compliance
│   │
│   ├── asset-managers/                 # Vertical: Purity, Mandates & Benchmarks
│   │   ├── factor-decomposer/          # Fama-French systematic style drift
│   │   ├── benchmark-tracking-auditor/ # Active Share & UCITS 5/10/40 limits
│   │   └── esg-mandate-reviewer/       # Carbon WACI Scope 1/2 & exclusions
│   │
│   └── investment-banks/               # Vertical: Macro Stress & Clearing Risk
│       ├── ccar-stress-tester/         # CCAR/DFAST macro stress shock replays
│       ├── counterparty-risk-officer/  # Peak Exposure, Wrong-Way Risk, & CVA
│       └── algorithmic-trader-validator/ # SEC Rule 15c3-5 pre-trade bounds
│
├── docs/
│   ├── workflow-diagrams/              # Mermaid visualizations of the Quant Lifecycle
│   ├── institutional-framework.md      # Regulatory alignments (Basel III, SR 11-7)
│   └── skill-map.md                    # Full skill-to-role responsibility matrix
│
├── examples/                           # Real Institutional Example Artifacts (JSON/YAML/CSV)
│   ├── backtest_audit/                 # Strategy report, audit output, & findings.json
│   ├── model_risk/                     # YAML model cards & validation reports
│   └── portfolio_review/               # Real CSV positions & stressed ES reports
│
└── README.md
```

---

## Standardized Production Readiness Scoring (PR-Score)

FinStack evaluates systematic models using a unified, institutional scoring system. Each validation agent grades the model on a scale of `[0-100]`, generating a composite **PR-Score**:

$$\text{PR-Score} = \text{Data Integrity} \times 0.20 + \text{Validation Quality} \times 0.20 + \text{Risk Controls} \times 0.20 + \text{Execution Assumptions} \times 0.20 + \text{Governance Evidence} \times 0.20$$

*   **PR-Score >= 80:** Approved for production capital allocation.
*   **PR-Score 60-79:** Approved with conditional limits (remediation required).
*   **PR-Score < 60:** Model Rejected. Do Not Deploy.

---

## Quick Start

1. Clone `finstack-skills` into your AI agent's local skills directory (e.g., `~/.claude/skills/finstack-skills` or vendor it directly).
2. Point your AI agent to the workspace and invoke the **Core Governance Pipeline**:
   ```bash
   /quant-research-director   # Evaluate the economic thesis & OOS validation design
   /backtest-auditor          # Run forensic checks for lookahead & survivorship bias
   /model-risk-officer        # Conduct regulatory SR 11-7 independent validation
   /portfolio-risk-manager    # Model tail risk, Expected Shortfall, and ADV sizing
   /quant-red-team            # Run adversarial attacks and define hard kill criteria
   ```
3. Run specialized audits as needed:
   * **Hedge Funds:** `/alpha-decay-monitor` or `/execution-optimizer`
   * **Asset Managers:** `/factor-decomposer` or `/benchmark-tracking-auditor`
   * **Investment Banks:** `/ccar-stress-tester` or `/algorithmic-trader-validator`

---

## Credits

Inspired by [garrytan/gstack](https://github.com/garrytan/gstack). FinStack takes the concept of multi-agent role-playing and scaling loops and applies it directly to the rigorous world of quantitative finance, model governance, and capital risk management.

---

## License

MIT