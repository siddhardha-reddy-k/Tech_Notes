## SCALAR SUBQUERY

A subquery that returns **exactly one value** (one row, one column) — used directly in the SELECT list, not just WHERE. It runs once per outer row and inserts that single value as a computed column.

```sql
SELECT ename, esal,
       (SELECT AVG(esal) FROM emp) AS avg_salary
FROM emp;
```

```text
ENAME   ESAL    AVG_SALARY
Alan        45000        48500
Raja        52000        48500
Priya        41000        48500
Kiran        60000        48500
Meena        38000        48500
David        55000        48500
```

**What's happening:** the inner query (AVG(esal) = 48500) is a fixed value here — it doesn't depend on which row it's next to, so it just repeats on every row. This lets you show each employee's salary **alongside** a company-wide reference value, in one query, instead of running two separate queries and combining them yourself.
