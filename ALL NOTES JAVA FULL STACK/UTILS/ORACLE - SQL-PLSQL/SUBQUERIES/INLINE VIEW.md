## INLINE VIEW

A subquery placed in the **FROM clause** — Oracle treats its result as a temporary, unnamed table that the outer query can then filter/select from.

```sql
SELECT *
FROM (
    SELECT * FROM emp
    ORDER BY esal DESC
)
WHERE ROWNUM <= 3;
```

```text
EID  ENAME   ESAL    DEPTNO
104  Kiran   60000   20
106  David   55000   NULL
102  Raja    52000   20
```

Top 3 highest earners.

Why you can't just write WHERE ROWNUM <= 3 directly with ORDER BY in one query — this is the actual reason inline views exist for this pattern:

```sql
-- ❌ This does NOT give top 3 by salary

SELECT * FROM emp
WHERE ROWNUM <= 3
ORDER BY esal DESC;
```

**Oracle assigns ROWNUM before sorting happens — it numbers rows as they're first retrieved (often insertion order), filters to the first 3 *of that unsorted set*, and only then sorts those 3. So you'd get "3 random-ish early rows, sorted" — not the actual top 3 by salary. Classic gotcha, this trips up a lot of people.**

**Why "inline" — the naming makes sense once you see it:** it's like a view (a saved query treated as a table), except you're not saving it anywhere with CREATE VIEW — it exists only inline, for the duration of this one query, then disappears.

**Other common uses beyond pagination:** aggregating first, then filtering on the aggregate result without needing a separate step:

**Why "inline" — the naming makes sense once you see it:** it's like a view (a saved query treated as a table), except you're not saving it anywhere with CREATE VIEW — it exists only inline, for the duration of this one query, then disappears.

**Other common uses beyond pagination:** aggregating first, then filtering on the aggregate result without needing a separate step:

```sql
SELECT * FROM (
    SELECT deptno, AVG(esal) AS avg_sal
    FROM emp
    GROUP BY deptno
)
WHERE avg_sal > 45000; -- departments where average salary is greater than 45k
```
