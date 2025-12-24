# Error Handling Patterns (Data Engineering)

This document describes common patterns to make pipelines reliable and observable.

---

## 1) Error taxonomy
Typical categories:
- Connectivity failures (DB/API/network)
- Data quality issues (missing fields, invalid formats)
- Logic failures (unexpected joins, duplicates)
- Resource/scale failures (timeouts, memory, throttling)
- External dependencies (API changes, vendor outages)

---

## 2) Retry with backoff (when appropriate)
Use retry for transient failures:
- network timeouts
- rate limits
- temporary service unavailability

Avoid retry for deterministic errors:
- invalid schema
- missing mandatory fields
- authentication failures (unless token refresh is expected)

---

## 3) Fail fast vs. quarantine
Two common strategies:
- **Fail fast**: stop the pipeline and alert (for critical correctness)
- **Quarantine**: isolate bad records and continue (for high-throughput ingestion)

Choose per domain and business requirements.

---

## 4) Structured error logging
Capture:
- process/job name
- stage/step
- file/key identifiers
- timestamps
- error category
- exception message (sanitized)
- correlation id / run id

This enables fast triage and analytics.

---

## 5) Idempotency patterns
Avoid duplicates by design:
- write using deterministic keys
- upsert/merge
- checkpoint offsets for streaming
- record processed file names / hashes

---

## 6) Human-friendly alerts
A good alert includes:
- what failed
- where it failed
- impact (how many records, which dataset)
- suggested next action
- links to logs/monitoring
