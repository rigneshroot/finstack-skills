# Quantitative Research Lifecycle & Governance Workflow

This document visualizes the institutional validation workflow implemented by **FinStack**. In elite financial institutions, no strategy is allowed to trade until it successfully runs this linear gauntlet.

---

## Workflow Diagram

```mermaid
graph TD
    classDef core fill:#e1f5fe,stroke:#03a9f4,stroke-width:2px;
    classDef HF fill:#e8f5e9,stroke:#4caf50,stroke-width:2px;
    classDef AM fill:#fff3e0,stroke:#ff9800,stroke-width:2px;
    classDef IB fill:#fce4ec,stroke:#e91e63,stroke-width:2px;
    classDef gate fill:#efebe9,stroke:#795548,stroke-width:3px;

    %% Steps
    A[Idea Generation & Thesis] -->|/quant-research-director| B(Research Review)
    B -->|PR-Score < 70 / Reject| A
    B -->|PR-Score >= 70 / Pass| C(Forensic Backtest Audit)
    
    C -->|/backtest-auditor| D{Bias & Leakage Audit}
    D -->|Lookahead / Survivorship Bias Detected| A
    D -->|Clean Audit| E(Model Risk Governance)
    
    E -->|/model-risk-officer| F{SR 11-7 validation}
    F -->|Conceptual Soundness Deficiencies| E
    F -->|Validation Approved| G(Portfolio Sizing & Risk)
    
    G -->|/portfolio-risk-manager| H{Tail Risk & Liquidity Review}
    H -->|Drawdown or ADV Bounds Breached| G
    H -->|Sizing Approved| I(Execution & Microstructure)
    
    %% Verticals
    I -->|/execution-optimizer| J{Slippage & TCM Audit}
    J -->|optimistic assumptions| I
    J -->|TCM Validated| K(Investment Committee)
    
    K -->|/quant-red-team| L{Adversarial Challenge}
    L -->|Regime Limits Breached / Fragile| K
    L -->|Approved with Kill Criteria| M[Production Capital Allocation]

    %% Applying Classes
    B:::core
    C:::core
    E:::core
    G:::core
    I:::core
    K:::core
    D:::gate
    F:::gate
    H:::gate
    J:::gate
    L:::gate
    M:::core
```

---

## Detailed Phase Breakdown

### 1. Research Thesis Evaluation (`/quant-research-director`)
- **Objective:** Interrogate the economic foundation.
- **Goal:** Ensure the model is exploiting a structural market anomaly, not overfitting historical noise.
- **Key Metric:** Economic intuition score.

### 2. Forensic Backtest Audit (`/backtest-auditor`)
- **Objective:** Search for data-snooping, lookahead bias, and constituent survivorship anomalies.
- **Goal:** Eliminate the mathematical lies that make backtests look perfect in simulation.
- **Key Metric:** Deflated Sharpe Ratio (DSR) & Haircut Sharpe.

### 3. Model Governance Validation (`/model-risk-officer`)
- **Objective:** Independent review complying with the Federal Reserve **SR 11-7** framework.
- **Goal:** Establish mathematical boundaries, identify data dependencies, and set drift limits.
- **Key Metric:** SR 11-7 compliance scorecard.

### 4. Portfolio Sizing & Tail Risk (`/portfolio-risk-manager`)
- **Objective:** Size positions based on liquidity limits and extreme tail behavior.
- **Goal:** Prevent single-strategy models from introducing systemic liquidity freezes.
- **Key Metric:** 99% Expected Shortfall (ES) & 10% ADV Time-to-Liquidate bounds.

### 5. Execution Optimization (`/execution-optimizer`)
- **Objective:** Apply non-linear market impact models (Almgren-Chriss) and locate/borrow parameters.
- **Goal:** Ensure gross alpha is not entirely consumed by spread-crossing or borrow fees.
- **Key Metric:** Stressed transaction cost model (TCM) haircut.

### 6. Adversarial Red-Teaming (`/quant-red-team`)
- **Objective:** Actively stress-test the model for factor crowding and structural regime failure.
- **Goal:** Define strict, quantitative **kill criteria** for deactivating the model in production.
- **Key Metric:** Maximum drawdown limit & Signal-to-P&L divergence thresholds.
