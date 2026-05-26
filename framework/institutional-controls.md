# Institutional Risk & Operational Controls

This document establishes the pre-trade, post-trade, and clearing-house level operational risk controls mandated for all trading systems.

---

## 1. SEC Rule 15c3-5 Compliance (Market Access controls)
All automated order routing systems and high-frequency algorithms must connect through our **Central Risk Gateway**. Risk controls cannot be bypassed by any trading desk:
- **Single Order Limits (SOL):** Hard-coded limits that reject any order exceeding **4.0% of constituent ADV** or **$5 Million notional** value.
- **Price Collar Bands (Fat-Finger Prevention):** The gateway blocks buy orders priced >2.0% above the National Best Offer (NBO) and sell orders priced >2.0% below the National Best Bid (NBB).
- **Message Rate Limiters (Throttles):** If an algorithm submits more than **100 orders per second (OPS)**, the gateway automatically suspends the algorithm, cancels all active orders, and alerts the compliance officer (preventing Knight Capital-style infinite looping).

---

## 2. Clearing Margin & Leverage Buffers
Traditional margin requirements (Reg T) are insufficient under Basel III standards. We enforce dynamic portfolio-margining:
- **TIMS/SPAN Margining:** Clearing brokers calculate margin daily based on portfolio-level risk offsets.
- **Stressed Margin Cushion:** Trading desks must maintain a cash reserve buffer of at least **20.0% of gross capital allocation** to prevent forced de-leveraging during extreme volatility spikes.

---

## 3. Emergency Kill Switches & Circuit Breakers
Any strategy trading live capital must have active, programmatic **Kill Switches**:
- **Intraday Drawdown Stop-Out:** If the strategy's realized P&L drops below **-3.0% of allocated capital** in a single trading day, all open positions must be instantly liquidated via market-neutral TWAP, and the algorithm is deactivated.
- **Trailing Peak Drawdown Stop-Out:** If the strategy's trailing peak-to-trough drawdown exceeds **-12.0%**, the strategy is permanently stopped out and its validation certificate is revoked.
- **Connection Heartbeat Fail-safe:** If network latency between the trading desk and the exchange gateway exceeds **500ms** or drops entirely, the gateway triggers **Cancel-on-Disconnect (COD)** to pull all passive orders.
