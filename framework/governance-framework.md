# Model Risk Governance & Segregation of Duties

This document establishes the formal organizational governance and audit trail standards required to manage model risk across our systematic trading desks.

---

## 1. Segregation of Duties (Separation of Powers)
To prevent cognitive bias, front-running, and self-validation conflicts, the firm enforces a strict **Separation of Duties** covenant:
*   **The Research Desk (Model Developer):** Responsible for thesis formulation, backtest coding, and signal generation.
*   **The Validation Desk (Model Validator):** A completely independent department (Model Risk Management) responsible for auditing the backtest (`/backtest-auditor`), validating conceptual soundness (`/model-risk-officer`), and issuing model approvals. **Validators do not report to the trading or research desk heads.**
*   **The Risk Management Desk (Risk Controller):** Independent portfolio risk managers responsible for setting sizing ceilings (`/portfolio-risk-manager`) and managing stress buffers.

---

## 2. Review Committee Roles & Commands

```
Research Director  ──>  Backtest Auditor  ──>  Model Risk Officer  ──>  Risk Committee
```

### 1. Quantitative Research Director
- **Role:** Evaluates signal conceptual validity.
- **Command:** `/quant-research-director`
- **Output:** Research validation score & pass/fail thesis check.

### 2. Backtest Auditor
- **Role:** Forensic data-leakage and timing auditor.
- **Command:** `/backtest-auditor`
- **Output:** Forensic bias audit report & PR-Score component.

### 3. Model Risk Officer
- **Role:** Regulatory SR 11-7 validation officer.
- **Command:** `/model-risk-officer`
- **Output:** Independent validation report & model card schema.

### 4. Portfolio Risk Manager
- **Role:** Exposure and liquidity controller.
- **Command:** `/portfolio-risk-manager`
- **Output:** Position concentration, stressed ES, and ADV limits.

---

## 3. Model Lineage & Audit Trails
Every model in the firm's inventory must maintain a complete **Audit Lineage**:
- **Metadata Card:** Every model must have an active `model_card.yaml` detailing mathematical specifications, inputs, and boundaries.
- **Validation Log:** A complete record of all validation iterations, including failed backtest audits and challenger benchmark comparisons, must be permanently archived.
- **Version Control:** Shifting any parameter or variable in a live trading model automatically triggers a *Major Revision*, requiring a full re-validation by the independent validation desk.
