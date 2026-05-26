# Portfolio Exposure & Liquidity Concentration Audit

- **Date:** October 20, 2025
- **Portfolio ID:** `EQ_MR_RSI20_PORT`
- **Audit Desk:** Quantitative Risk Analytics Group

---

## 1. Sector Concentration & Risk Allocation

The portfolio was audited for sector concentrations. The investment prospectus mandates a maximum sector exposure ceiling of **25.0%**.

| Sector | Long Weight | Short Weight | Net Weight | Gross Weight | Compliance Status |
|---|---|---|---|---|---|
| **Technology** | `0.093` | `-0.015` | `+0.078` | `0.108` | **COMPLIANT** |
| **Financials** | `0.055` | `0.000` | `+0.055` | `0.055` | **COMPLIANT** |
| **Consumer Staples** | `0.000` | `-0.060` | `-0.060` | `0.060` | **COMPLIANT** |
| **Healthcare** | `0.040` | `-0.025` | `+0.015` | `0.065` | **COMPLIANT** |
| **Consumer Discretionary**| `0.060` | `-0.010` | `+0.050` | `0.070` | **COMPLIANT** |
| **Energy** | `0.000` | `-0.040` | `-0.040` | `0.040` | **COMPLIANT** |
| **Total** | `0.248` | `-0.150` | `+0.098` | `0.398` | **COMPLIANT** |

*Note: The portfolio maintains high sector neutrality. The largest gross exposure is Technology at 10.8%, well below the 25.0% hard limit.*

---

## 2. Marginal Contribution to Risk (MCTR)

We calculated the Marginal Contribution to Risk (MCTR) for each asset class and core factor to determine what bets are driving the portfolio's realized tracking error.

- **Systematic Beta Risk:** `54.2%` of active risk is driven by broad market beta.
- **Technology Factor Loadings:** `32.5%` of active risk is driven by idiosyncratic Technology sector factor exposure (e.g. semiconductor momentum).
- **Idiosyncratic Residual Risk (Alpha):** Only `13.3%` of the risk is driven by actual stock-specific alpha signals.

> [!WARNING]
> **Factor Dominance Risk:**
> A massive 86.7% of the portfolio's active risk is systematic (beta + sector), indicating that the portfolio's returns will be dominated by macro factor movements rather than stock-selection alpha.

---

## 3. Liquidity & Stressed Time-to-Liquidate (TTL)

We audited the liquidity profile of the holdings under both normal and stressed market conditions. We assume an institutional **Participation Rate Cap of 10.0% of 30-day ADV**.

- **Total Portfolio Value:** $100 Million
- **Stressed Market Volume Decline:** -40.0% daily volume shock.

| Asset Ticker | Position Size (Shares) | Normal 30D ADV | TTL Normal (Days) | TTL Stressed (Days) | Liquidity Risk |
|---|---|---|---|---|---|
| **AAPL** | `165,000` | `55,000,000` | `0.03 days` | `0.05 days` | `Negligible` |
| **MSFT** | `105,000` | `28,000,000` | `0.04 days` | `0.06 days` | `Negligible` |
| **PG** (Short) | `-152,000` | `6,500,000` | `0.23 days` | `0.39 days` | `Low` |
| **LLY** | `22,500` | `3,200,000` | `0.07 days` | `0.12 days` | `Low` |
| **XOM** (Short) | `-168,000` | `18,000,000` | `0.09 days` | `0.15 days` | `Low` |

*Note: All positions can be liquidated within less than 0.5 trading days, even under a severe stressed market shock, satisfying our institutional mandate of Time-to-Liquidate < 2.0 days.*
