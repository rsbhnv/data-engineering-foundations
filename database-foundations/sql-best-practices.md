# SQL Best Practices

This document summarizes practical SQL practices for reliability, performance, and maintainability.

---

## 1) Write for clarity first
- Use consistent naming and formatting
- Prefer explicit column lists (avoid `SELECT *`)
- Break complex logic into readable CTEs
- Add comments where business logic is not obvious

---

## 2) Filter early, return less
- Apply filters as early as possible
- Return only required rows and columns
- Avoid doing heavy transformations on the full dataset if unnecessary

---

## 3) Be intentional with joins
- Confirm join keys and cardinality
- Avoid accidental many-to-many joins
- Prefer `INNER JOIN` when rows must exist in both sides
- Use `LEFT JOIN` only when nulls are meaningful

---

## 4) Aggregations and grouping
- Aggregate only after filtering and joining correctly
- Ensure grouping columns match the business grain
- Be careful with duplicated rows introduced by joins

---

## 5) NULL handling
- Be explicit with NULL logic
- Avoid assumptions like `NULL = NULL` (it is not true)
- Use `COALESCE` / `NVL` for defaults when appropriate

---

## 6) Dates and time filtering
- Prefer range filters over function-wrapped columns
  - ✅ `where created_at >= :from and created_at < :to`
  - ❌ `where trunc(created_at) = trunc(sysdate)`
- Ensure time zones are handled consistently across systems

---

## 7) Avoid non-sargable predicates (when possible)
Non-sargable predicates prevent efficient index usage.
Examples:
- Functions on the column side (`UPPER(col)`, `TRUNC(date_col)`)
- Calculations on indexed columns (`col + 1 = ...`)

Prefer transforming the input parameter instead of the column.

---

## 8) Parameterization
- Use bind variables / parameters
- Avoid string concatenation for dynamic SQL
- Protect against SQL injection
- Improve plan stability (especially on Oracle)

---

## 9) Performance troubleshooting checklist
- Identify the slow part (scan, join, sort, aggregation)
- Review execution plan
- Check indexes and statistics
- Validate data volume changes
- Confirm query grain and join uniqueness
- Consider partition pruning (if partitioned)

---

## 10) Maintainability
- Keep queries deterministic (stable ordering only when required)
- Avoid hidden logic in deeply nested statements
- Extract reusable transformations to views (or upstream layers) when appropriate

