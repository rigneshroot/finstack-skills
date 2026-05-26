# Standardized Production Readiness Scoring (PR-Score)

All systematic strategies are graded using the standardized **Production Readiness Score (PR-Score)**. This metric ensures that no strategy is allocated live capital without passing rigorous, multi-desk quantitative gates.

---

## 1. The PR-Score Formula

The composite PR-Score is calculated across five independent dimensions, each weighted equally:

$$\text{PR-Score} = \text{Data Integrity} \times 0.20 + \text{Validation Quality} \times 0.20 + \text{Risk Controls} \times 0.20 + \text{Execution Assumptions} \times 0.20 + \text{Governance Evidence} \times 0.20$$

---

## 2. Validation Pillars & Grading Standards

### A. Data Integrity (20%)
- **Auditor:** `/backtest-auditor` & `/alternative-data-auditor`
- **90-100:** Point-in-Time constituent list CRSP integrated, delisted stock bankruptcies modeled correctly, absolute zero lookahead timestamps.
- **70-89:** Static index universe with minor delisting bias, 1-day timestamp lag verified.
- **<70:** Static index universe, missing delisting returns, or unverified data timestamps.

### B. Validation Quality (20%)
- **Auditor:** `/quant-research-director` & `/factor-decomposer`
- **90-100:** Walks-forward Purged/Embargoed cross-validation (de Prado), stationary-winsorized features, DSR adjusted, outperforms independent challenger by >0.30 Sharpe.
- **70-89:** Walk-forward cross-validation with basic parameters, winsorized features.
- **<70:** standard k-fold cross-validation, unadjusted Sharpe, or failure to outperform challenger.

### C. Risk Controls (20%)
- **Auditor:** `/portfolio-risk-manager` & `/ccar-stress-tester` & `/algorithmic-trading-validator`
- **90-100:** 99% Expected Shortfall limit active, single-position weight <= 4.0%, sector gross exposure <= 20%, Time-to-Liquidate < 1.0 day under 40% volume shock.
- **70-89:** VaR limits active, single-position weight <= 5.0%, sector exposure <= 25%, Time-to-Liquidate < 2.0 days.
- **<70:** Sizing unconstrained, missing tail-risk limits, or exit horizon exceeds 2 days.

### D. Execution Assumptions (20%)
- **Auditor:** `/execution-optimizer` & `/alpha-decay-monitor`
- **90-100:** Non-linear square-root market impact model (Almgren-Chriss), daily locate inventory integration for short borrows, margin volatility shocks modeled.
- **70-89:** Constant bid-ask spread crossed, GC borrow rates applied, standard TIMS margin assumptions.
- **<70:** Assuming mid-price executions, zero slippage, flat borrow fees, or unlimited liquidity.

### E. Governance Evidence (20%)
- **Auditor:** `/model-risk-officer` & `/counterparty-risk-officer` & `/esg-mandate-reviewer`
- **90-100:** Complete model card `model_card.yaml` filed, SR 11-7 independent validation certificate signed, daily Zero-Threshold CSAs active, SFDR Article 8/9 DNSH compliance verified.
- **70-89:** Basic model card, signed validation document, monthly CSA netting agreements.
- **<70:** Missing validation card, uncollateralized OTC exposure, or unverified ESG exclusions.

---

## 3. Capital Allocation Covenants

The final composite PR-Score dictates the strategy's capital allocation ceiling:

| Composite PR-Score | Capital Allocation Status | Maximum Allocated AUM | Leverage Limit |
|---|---|---|---|
| **$\ge 80$** | **PRODUCTION APPROVED** | `$100 Million` | Up to `2.0x Gross` |
| **$60 - 79$** | **LIMITED DEPLOYMENT** (Shadow Trading) | `$10 Million` | Capped at `1.0x Gross` (No long leverage) |
| **$< 60$** | **REJECTED** | `$0.00` | Deactivated |
