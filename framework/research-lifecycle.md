# Institutional Quantitative Research Lifecycle

This document defines the standard operating procedures (SOP) for the quantitative research lifecycle at our firm. Every systematic trading model must pass through these distinct phases sequentially.

---

## The Six Lifecycle Phases

```
Idea Generation ──> Research Review ──> Forensic Audit ──> Independent Validation ──> Shadow Trading ──> Production Capital Allocation
```

### Phase 1: Idea Generation & Thesis Formulation
- **Objective:** Formulate a robust, economically sound alpha hypothesis.
- **SOP:** Quantitative researchers must document the economic anomaly, behavioral bias, or structural market flow being exploited.
- **Artifact:** [Strategy Proposal Pitch]

### Phase 2: Independent Research Review
- **Objective:** Evaluate the conceptual soundness and mathematical formulation of the alpha signal.
- **Agent Command:** `/quant-research-director`
- **Focus:** Ensure features are properly stationarity-compliant and normal-winsorized.
- **Enforcement:** Research PR-Score must be $\ge 70$.

### Phase 3: Forensic Backtest Audit
- **Objective:** Interrogate the backtest for mathematical biases, timing errors, and over-fitting.
- **Agent Command:** `/backtest-auditor`
- **Focus:** Exposing lookahead timing, constituent survivorship bias, and optimistic transaction costs.
- **Enforcement:** Backtest PR-Score must be $\ge 80$.

### Phase 4: Independent Model Risk Validation
- **Objective:** Regulatory-grade model risk governance in compliance with the Federal Reserve **SR 11-7** framework.
- **Agent Command:** `/model-risk-officer`
- **Focus:** Establish mathematical boundaries, draft model cards, and run simple heuristic challenger benchmarks.
- **Enforcement:** Model Validation PR-Score must be $\ge 80$.

### Phase 5: Sizing & Shadow Trading
- **Objective:** Define portfolio risk constraints and trade the model in a simulated UAT/shadow account.
- **Agent Command:** `/portfolio-risk-manager`
- **Focus:** Size exposure based on 99% Expected Shortfall, sector concentration caps (UCITS), and 10% ADV Time-to-Liquidate bounds.
- **Enforcement:** Realized shadow-trading metrics must not deviate from backtest metrics by more than 20%.

### Phase 6: Production Capital Allocation & Red-Teaming
- **Objective:** Allocate live capital and activate ongoing adversarial stress-testing.
- **Agent Command:** `/quant-red-team`
- **Focus:** Run factor crowdedness checks and establish hard, quantitative **Kill Criteria** (Stop-Outs).
