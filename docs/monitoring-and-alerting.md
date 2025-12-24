# Monitoring & Alerting (Pipelines)

Monitoring is what makes pipelines production-grade.

---

## 1) What to monitor
- Job success/failure
- runtime duration and regressions
- throughput (records per run / per minute)
- data freshness (last successful ingestion time)
- error rate and error categories
- resource usage (CPU/memory/IO if available)

---

## 2) Operational metrics
Suggested metrics:
- `run_status` (success/fail)
- `run_duration_seconds`
- `records_processed`
- `records_failed`
- `last_success_time`
- `sla_breach_flag`

---

## 3) Logging levels
- INFO: lifecycle events (start/end)
- WARN: recoverable issues (retries, partial skips)
- ERROR: failures requiring intervention

Keep logs structured (machine-readable) when possible.

---

## 4) Alerting rules (examples)
Alert when:
- consecutive failures exceed threshold
- runtime spikes beyond baseline
- data freshness crosses SLA
- error rate crosses threshold
- critical dataset missing

---

## 5) Dashboards
A simple dashboard should show:
- pipeline health (success trend)
- runtime trend
- throughput trend
- top error categories
- SLA compliance

---

## 6) Incident workflow
- Alert → Triage → Mitigation → Root cause → Prevention
- Track incidents and preventive actions
