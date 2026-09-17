## CORRELATED SUBQUERY

A subquery that **references a column from the outer query** — which means the inner query can't run once and be done; it has to **re-run separately for every single row** the outer query processes.

You already saw this in action in EXISTS last topic — now let's define it properly on its own.

```sql
SELECT e.ename, e.esal, e.deptno
FROM emp e
WHERE e.esal > (
    SELECT AVG(e2.esal)
    FROM emp e2
    WHERE e2.deptno = e.deptno
);
```

**Goal:** find employees earning more than the **average salary of their own department** — not the company-wide average like topic 1.

**Step by step — this is the important part, how it actually executes:**

- Take **Alan** (deptno 10) → inner query runs *just for dept 10*: AVG(esal) WHERE deptno=10 → average of Alan(45000) + Priya(41000) = **43000** → is Alan's 45000 > 43000? **Yes → kept.**
- Take **Priya** (deptno 10) → inner query runs *again*, same dept 10 → average still 43000 → is 41000 > 43000? **No → excluded.**
- Take **Raja** (deptno 20) → inner query runs *again*, now for dept 20 → average of Raja(52000)+Kiran(60000) = **56000** → is 52000 > 56000? **No → excluded.**
- Take **Kiran** (deptno 20) → same dept 20, avg 56000 → is 60000 > 56000? **Yes → kept.**
- Take **Meena** (deptno 30) → only employee in dept 30, avg = her own 38000 → is 38000 > 38000? **No → excluded** (not strictly greater than herself).
- Take **David** (deptno NULL) → inner query: AVG(esal) WHERE deptno = NULL → matches nothing → returns NULL → esal > NULL is always **unknown/false → excluded.**

**Output:**

```text
ENAME   ESAL    DEPTNO
Alan    45000   10
Kiran   60000   20
```

**This is the core distinction to lock in — non-correlated vs correlated:**

|  | **Non-correlated (topic 1)** | **Correlated (this topic)** |
| --- | --- | --- |
| Inner query references outer table? | No | Yes (e.g., e2.deptno = e.deptno) |
| How many times inner query runs | **Once**, total | **Once per outer row** |
| Result | Fixed single value used for all rows | Different result per row, depending on that row's context |

**Why "correlated" is the right name:** the inner query's outcome is *correlated with* — tied to, dependent on — whichever outer row is currently being evaluated. It's not an independent calculation anymore; it's contextual per row.

**Performance note (matters for interviews):** correlated subqueries can be slower on large tables since the inner query conceptually re-executes for every outer row — Oracle's optimizer often rewrites these internally for efficiency, but conceptually, that's the model to reason with.
