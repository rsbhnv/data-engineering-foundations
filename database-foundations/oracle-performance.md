# Oracle Performance – Practical Notes

This document captures practical Oracle performance principles commonly used in data engineering environments.

---

## 1) The usual bottlenecks
- Full table scans on large tables (sometimes expected, often not)
- Poor join order or join method (nested loops vs hash joins)
- Large sorts (ORDER BY / GROUP BY) spilling to disk
- Missing or stale statistics
- High concurrency contention (locks, latches, hot blocks)

---

## 2) Execution plans: what to look for
When a query is slow, focus on:
- Access path (index range scan / full scan)
- Join method (hash join / nested loop)
- Estimated vs actual rows (cardinality mismatch)
- Sort operations and temp usage
- Partition pruning (when partitioned)

---

## 3) Statistics matter
- Stale statistics can lead to wrong plans
- High data churn tables need more frequent stats updates
- Histograms can help for skewed data distributions (use carefully)

---

## 4) Bind variables and plan stability
- Bind variables help performance and reduce parse overhead
- However, in some cases they can lead to suboptimal generic plans
- If performance is unstable, check:
  - bind peeking / adaptive plans
  - data skew
  - plan changes over time

---

## 5) Index usage principles
- Indexes help selective predicates
- Indexes may hurt heavy write workloads
- Composite indexes should match common filter patterns
- Avoid over-indexing: each additional index has a cost

---

## 6) Partitioning basics (for large tables)
Partitioning helps with:
- Partition pruning for time-based filtering
- Faster maintenance (drop/truncate partitions)
- Parallel execution opportunities

Common pattern:
- Range partition by date
- Optional subpartition by business key

---

## 7) Common tuning actions (high-level)
- Reduce scanned data (filters, partition pruning)
- Fix join logic (grain, uniqueness, correct join keys)
- Create or adjust indexes (based on real predicates)
- Refresh statistics
- Consider materialization / staging for repeated heavy transformations
- Use parallelism carefully (avoid “parallel everywhere”)

---

## 8) Operational discipline
- Track query runtimes over time
- Detect regressions early
- Keep change history (index changes, stats policies)
- Use a performance baseline for critical workloads
