# Model Risk Validation Report: Equity Mean Reversion Model

- **Model ID:** `EQ_MR_RSI20_US_LC`
- **Validation Date:** October 18, 2025
- **Validation Desk:** Independent Model Validation Group (MVG)
- **Primary Standard:** **Federal Reserve Letter SR 11-7**
- **Validation Status:** **CONDITIONALLY APPROVED** (Subject to challenger monitoring covenants)

---

## 1. Governance Scorecard

| Governance Pillar | MVG Rating (0-100) | Findings / Remediations | Status |
|---|---|---|---|
| Conceptual Soundness | `88 / 100` | Satisfactorily defends the economic thesis. Rebalance changed from Weekly to Daily to prevent signal half-life decay. | **Approved** |
| Data Integrity | `85 / 100` | CRSP point-in-time pricing databases are active, eliminating historical constituent survivorship bias. | **Approved** |
| Outcomes Analysis | `82 / 100` | Out-of-sample purged/embargoed walk-forward cross-validation has been executed successfully. | **Approved** |
| Ongoing Monitoring | `78 / 100` | Population Stability Index (PSI) alerts are configured, but require real-time execution slip variance tracking. | **Conditional** |
| **Composite Score** | **83.2 / 100** | **The model meets the minimum threshold of 80 for production deployment under conditional controls.** | **PASS** |

---

## 2. Mathematical Soundness & Lineage
The model uses relative value cross-sectional winsorized Z-scores on a 20-period RSI to assign long/short portfolio weights. 
- **Conceptual Soundness:** Explicits institutional block rebalancing imbalances.
- **Formulation:** Linear scaling based on winsorized Z-scores provides a proportional, bounded allocation schema, limiting concentration risk.

---

## 3. Data Inputs and Lineage
- **Primary Prices:** CRSP point-in-time daily adjusted close prices, eliminating lookahead and survivorship biases.
- **Volume Metrics:** Reuters Equity Microstructure API 30-day Average Daily Volume (ADV), ensuring accurate liquidity caps.
- **Linage Flow:** Standard pricing database $\rightarrow$ Signal generator module $\rightarrow$ Order Management System (OMS) gateway.

---

## 4. Model Boundaries & Hard Limits
To mitigate extreme tail risk and leverage interactions, the following hard limits have been validated and integrated into the execution gateway:
- **Single-Stock Cap:** Maximum long or short position capped at **4.0%** of total portfolio capital.
- **Sector Cap:** Aggregated exposure to any single GICS sector capped at **20.0%** of total capital.
- **Execution Collar:** Orders are rejected if the limit price drifts by $>0.50\%$ from the prevailing mid-point.
- **Volatility Kill Switch:** If the portfolio realized 5-day annualized volatility exceeds **25.0%**, the algorithm is suspended, and all outstanding orders are canceled.
