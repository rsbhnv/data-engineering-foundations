# Indexes & Partitions – Concepts and Practical Guidance

This document summarizes practical guidance for indexes and partitioning strategies.

---

## 1) Index types (conceptual)
- B-Tree index: best for selective lookups and range filters
- Bitmap index: useful for low-cardinality columns (mostly DW, not OLTP)
- Composite index: multiple columns in one index

---

## 2) When indexes help
- Highly selective filters
- Join keys frequently used in joins
- Range filters on ordered data (date ranges)

---

## 3) When indexes don’t help (or hurt)
- Very low selectivity columns (unless bitmap in DW)
- Queries returning a large percentage of the table
- Heavy write workloads (index maintenance overhead)
- Function-wrapped predicates that prevent index usage

---

## 4) Composite indexes: ordering matters
General guidance:
- Put the most selective column first (often)
- Align with common query predicates (WHERE conditions)
- Consider additional columns for “covering” access if it reduces table lookups

---

## 5) Partitioning: why it’s useful
Partitioning can improve:
- Performance via pruning (only scanning relevant partitions)
- Manageability (drop old partitions, load new partitions)
- Parallel operations on large datasets

---

## 6) Common partition strategies
- Range partition by date (most common in data platforms)
- List partition by category (less common)
- Hash partition by key (for distribution)

Often:
- Range(date) + Subpartition(hash/business_key)

---

## 7) Partition pruning checklist
Pruning works best when:
- Filters are on the partition key
- Predicates are sargable
- Query uses range filtering (`>=` and `<`)

Avoid:
- Applying functions to the partition key column in WHERE clause

---

## 8) Maintenance patterns
- Rolling window retention: drop old partitions
- Bulk loads: exchange partition / load into new partition
- Stats refresh per partition when needed
