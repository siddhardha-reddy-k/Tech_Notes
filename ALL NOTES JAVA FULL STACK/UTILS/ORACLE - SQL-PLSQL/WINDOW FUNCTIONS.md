## — Core Concept

Unlike GROUP BY (which **collapses** rows into one row per group), window functions calculate across a group of related rows **without collapsing anything** — every original row stays visible, with an extra calculated column added.

```sql
function_name() OVER (PARTITION BY col ORDER BY col)
```

- PARTITION BY = groups rows (like GROUP BY, but doesn't hide individual rows)
- ORDER BY = decides row order *within* each partition (needed for ranking/running totals)

**This distinction is the one thing to really lock in:** GROUP BY gives you "1 row per department." Window functions give you "every employee row, but with department-level info attached alongside."

## ROW_NUMBER(), RANK(), DENSE_RANK()

All three number rows based on order — differ only in how they handle **ties**.

```sql
SELECT eid, ename, esal,
  ROW_NUMBER() OVER (ORDER BY esal DESC) AS row_num,
  RANK()       OVER (ORDER BY esal DESC) AS rnk,
  DENSE_RANK() OVER (ORDER BY esal DESC) AS dense_rnk
FROM emp;
```

Using our data (no actual ties, but here's the behavior rule to remember):

|  | **Ties get** | **Numbers skip after tie?** |
| --- | --- | --- |
| ROW_NUMBER() | different numbers, always unique | n/a — always sequential |
| RANK() | same rank | **Yes** — 1,1,3 (skips 2) |
| DENSE_RANK() | same rank | **No** — 1,1,2 (no skip) |

**If two people both earned 60000 (highest):** RANK gives both rank 1, next person gets rank 3 (2 is "used up" by the tie). DENSE_RANK gives both rank 1, next person gets rank 2 (no gap). ROW_NUMBER ignores the tie entirely and just assigns 1, 2 arbitrarily between them.

**Classic interview use — Nth highest salary, cleaner than the nested MAX() subquery approach we did earlier:**

```sql
SELECT * FROM (
    SELECT eid, ename, esal,
      DENSE_RANK() OVER (ORDER BY esal DESC) AS rnk
    FROM emp
)
WHERE rnk = 2;
```

This is the inline-view pattern (topic 5 from subqueries) combined with a window function — genuinely cleaner than nested MAX() WHERE esal < (SELECT MAX...) for 2nd, 3rd, 4th highest, etc. **This is worth remembering — it directly replaces that clunky nested-subquery pattern.**

**Top N per group — very common pattern:**

```sql
SELECT * FROM (
    SELECT eid, ename, esal, deptno,
      ROW_NUMBER() OVER (PARTITION BY deptno ORDER BY esal DESC) AS row_num
    FROM emp
)
WHERE row_num <= 2;
```

"Top 2 earners per department" — PARTITION BY resets the numbering for each department separately, so numbering starts fresh at 1 for HR, fresh at 1 for IT, etc.

## LAG() / LEAD()

Pulls a value from a **previous** (LAG) or **next** (LEAD) row, based on the specified order — without needing a self-join.

```sql
SELECT eid, ename, esal,
  LAG(esal, 1, 0) OVER (ORDER BY eid) AS prev_sal
FROM emp;
```

For each row, shows the previous row's esal (ordered by eid). First row has no "previous," so it falls back to the default value (0, the 3rd argument).

**Real use case:** month-over-month comparisons, "salary increased/decreased from previous record," gap analysis — anywhere you'd normally need a self-join just to compare "this row vs the row before it."

## SUM()/AVG()/MAX() OVER — Running Totals

```sql
SELECT eid, ename, esal,
  SUM(esal) OVER (ORDER BY eid) AS running_total
FROM emp;
```

Each row shows the cumulative sum of esal, from the first row up through the current one — a "running total," not a single grand total repeated (that would be a plain scalar subquery, topic 3 earlier).

Add PARTITION BY deptno and the running total resets per department instead of running across the whole table.

**What I'm deliberately keeping light, per your priority level:** NTILE (grouping into buckets), FIRST_VALUE/LAST_VALUE, and the FRAME clause (ROWS BETWEEN...) — know they exist, know roughly what they do, but don't grind deep practice here. If you get an interview question on them, the pattern will feel familiar since it's the same OVER (PARTITION BY... ORDER BY...) shape as everything above.

**One-line summary to keep in your notes:**

Window functions = calculations across related rows, without collapsing rows like GROUP BY does. ROW_NUMBER/RANK/DENSE_RANK for ranking, LAG/LEAD for row-to-row comparison, SUM/AVG OVER for running totals.
