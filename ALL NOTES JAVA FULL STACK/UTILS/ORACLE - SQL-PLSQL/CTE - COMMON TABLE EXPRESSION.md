## CTE — Common Table Expression

A **named temporary result set**, defined at the top of a query using WITH, then referenced like a table in the main query. Basically: a subquery, but named and readable instead of nested and buried.

```sql
WITH high_earners AS (
    SELECT eid, ename, esal
    FROM emp
    WHERE esal > 40000
)
SELECT * FROM high_earners;
```

```text
EID  ENAME   ESAL
101  Alan    45000
102  Raja    52000
104  Kiran   60000
106  David   55000
```

Functionally, this is identical to an inline view / subquery version:

```sql
SELECT * FROM (
    SELECT eid, ename, esal FROM emp WHERE esal > 40000
);
```

**Same result, same execution — CTE is purely a readability/structure upgrade, not a different mechanism.**

**Why it actually helps — the real reason to use it:** once queries get complex (multiple joins, multiple filtering steps), nesting subqueries inside subqueries becomes unreadable fast. CTE lets you name each logical step, so the final query reads top-to-bottom like a story instead of inside-out.

**Multiple CTEs, chained together — this is where it earns its keep:**

```sql
WITH dept_total AS (
    SELECT deptno, SUM(esal) AS total_sal
    FROM emp GROUP BY deptno
),
dept_avg AS (
    SELECT deptno, AVG(esal) AS avg_sal
    FROM emp GROUP BY deptno
)
SELECT dt.deptno, dt.total_sal, da.avg_sal
FROM dept_total dt
JOIN dept_avg da ON dt.deptno = da.deptno;
```

Two named "sub-tables," each built once, then joined together. Writing this as nested subqueries would be far messier — this is the genuine advantage over subqueries: **each piece has a name, is reusable within the same query, and reads cleanly.**

**CTE vs Subquery — the practical difference to remember:**

|  | **CTE** | **Subquery** |
| --- | --- | --- |
| Named | Yes | No (anonymous) |
| Reference multiple times in same query | Yes | No, re-typed each time |
| Readability at scale | Better | Gets messy when nested deep |
| Underlying execution | Same result either way | Same result either way |

**CTE with INSERT/UPDATE/DELETE** — same idea, just feeding the CTE's result into a DML statement instead of a plain SELECT. Not fundamentally different from what you already know from subqueries in DML (topic 11 from our subquery session) — just wrapped with a name first.

**RECURSIVE CTE** — a CTE that references itself, used for hierarchical data (org charts, category trees). Real syntax:

```sql
WITH RECURSIVE numbers AS (
    SELECT 1 AS num              -- anchor/base case
    UNION ALL
    SELECT num + 1 FROM numbers  -- recursive case
    WHERE num < 10                -- stop condition
)
SELECT * FROM numbers;
```

Produces 1 through 10. **Honestly:** know this exists and roughly how it works (anchor + recursive part + stop condition) — actual hands-on recursive CTE writing is rare for fresher-level interviews, don't over-invest here.

**Skip for now, deliberately:** the "Complex CTE with RANK()/ROW_NUMBER()" examples in your doc — those use window functions, which is the next topic. We'll circle back to those exact patterns once window functions themselves make sense; right now they'd just be confusing syntax with unexplained pieces.
