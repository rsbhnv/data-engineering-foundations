# Procedures & Tuning – Practical Notes

This document summarizes principles for stored procedures, PL/SQL patterns, and tuning approaches.

---

## 1) Procedure design principles
- Keep procedures focused and single-purpose
- Separate orchestration from heavy transformation logic when possible
- Prefer clear parameter contracts and consistent error handling

---

## 2) Transaction control
- Avoid very large transactions when possible
- Commit strategy should match workload characteristics
- Ensure error conditions do not leave partial or inconsistent states

---

## 3) Bulk operations
In data workloads, bulk operations usually outperform row-by-row processing.
Prefer:
- Set-based SQL operations
- Bulk collect / forall patterns (when PL/SQL is required)

Avoid:
- Cursor loops for large datasets unless unavoidable

---

## 4) Error handling & logging
- Capture a clear error message and a process identifier
- Store failure context (job, step, key values, timestamps)
- Avoid swallowing exceptions silently

---

## 5) Performance tuning checklist
- Review SQL inside the procedure (often the real bottleneck)
- Check indexes and statistics
- Validate row counts and join uniqueness
- Reduce repeated computations inside loops
- Minimize context switches between SQL and PL/SQL

---

## 6) Maintainability and change safety
- Version procedures (change history)
- Use consistent naming conventions
- Add small unit-like checks for critical logic
- Document assumptions (grain, keys, expected row volumes)
