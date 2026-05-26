# Prometheus & Grafana Telemetry Alerting Requirements

- **Strategy ID:** `EQ_MR_RSI20_US_LC`
- **Audit Date:** October 23, 2025
- **Lead Validator:** Lead Production Readiness Reviewer

The following telemetry alert bounds must be active on the Grafana production dashboard. Any breach of these thresholds will trigger instant escalations to the Infrastructure Operations and Compliance desks.

---

## 1. System Infrastructure Metrics

| Metric | Prometheus Collector | Warning Threshold | Critical Threshold (Auto Kill-Switch) |
|---|---|---|---|
| CPU Utilization | `node_cpu_seconds_total` | $> 75\%$ | $> 90\%$ sustained for 30s |
| Memory Leak indicator | `node_memory_Active_bytes` | $> 12 \text{GB}$ | $> 15 \text{GB}$ (OOM Protection) |
| Logging Disk Space | `node_filesystem_free_bytes` | $< 20\%$ | $< 5\%$ |

---

## 2. Low-Latency Venue Telemetry

| Metric | Prometheus Collector | Warning Threshold | Critical Threshold (Auto Kill-Switch) |
|---|---|---|---|
| Broker Round-Trip Time | `gateway_rtt_latency_microseconds` | $> 5,000 \mu s$ | $> 25,000 \mu s$ sustained for 5s |
| FIX Session Reconnects | `gateway_session_reconnect_total` | 1 reconnect / hr | $\ge 3$ reconnects / hr |
| Order Reject Rate | `gateway_order_rejections_total` | $> 1.5\%$ of fills | $> 5.0\%$ of fills (Immediate Halting) |
| Feed Handler Lag | `market_data_feed_handler_lag_ms` | $> 15 \text{ms}$ | $> 100 \text{ms}$ (Price stale protection) |

---

## 3. Risk & Compliance Telemetry

| Metric | Prometheus Collector | Warning Threshold | Critical Threshold (Auto Kill-Switch) |
|---|---|---|---|
| Single-Stock Weight | `portfolio_symbol_weight_pct` | $> 3.5\%$ | $> 4.0\%$ (Hard Gateway Collar) |
| Realized Daily Loss | `portfolio_realized_drawdown_pct` | $-2.0\%$ | $-3.0\%$ (Hard Capital Halting) |
| Network PTP Clock Drift | `ptp_clock_offset_nanoseconds` | $> 25,000 \text{ns}$ | $> 50,000 \text{ns}$ (FINRA CAT breach) |

---

## 4. Alert Routing Playbook
- **Level 1 (Warning):** Routes immediately to the **Trading Desk Operations (Tops)** via PagerDuty.
- **Level 2 (Critical):** Triggers the automated **Execution Venue Kill Switch** (hard cancels all outstanding orders at the broker, sets strategy trade size limit to 0), and escalates to the **Chief Compliance Officer** and **Head of Systematic Trading**.
