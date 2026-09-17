## MULTIPLE-COLUMN SUBQUERY

A subquery that returns **more than one column** — compared against a matching set of columns from the outer query, as a **tuple** (grouped pair/set), not individually.

**Better example than the book's self-referential one — let's use something that actually makes sense with our data.** Suppose you want employees whose (deptno, esal) combination matches any (deptno, esal) pair found among employees earning above 50000:

```sql
SELECT *
FROM emp
WHERE (deptno, esal) IN
(
    SELECT deptno, esal
    FROM emp
    WHERE esal > 50000
);
```

**Step by step:**

1. Inner query finds employees earning > 50000: Raja (20, 52000), Kiran (20, 60000), David (NULL, 55000).
2. Inner query returns **pairs**, not single values: (20, 52000), (20, 60000), (NULL, 55000).
3. Outer query checks: does this row's **(deptno, esal) pair, as a whole**, match any pair in that list?

**Output:**

```text
EID  ENAME   ESAL    DEPTNO
102  Raja    52000   20
104  Kiran   60000   20
106  David   55000   NULL
```

**Why tuple matching matters — what makes this different from checking columns separately:** the pair (20, 52000) must match **both** deptno=20 AND esal=52000 together on the same row, not deptno=20 matching one row while esal=52000 matches a different row. This is genuinely different from writing two separate IN conditions:

```sql
-- NOT the same thing — checks each column independently

WHERE deptno IN (SELECT deptno FROM emp WHERE esal > 50000)
AND esal IN (SELECT esal FROM emp WHERE esal > 50000)
```

That version would incorrectly match, say, an employee in dept 20 earning exactly 60000 even if no *single row* actually has that combination — because it's checking column membership separately, not as a linked pair. Multi-column subquery keeps the relationship intact.

**David and NULL, gotcha:** technically, NULL comparisons in tuples behave the same as regular NULL rules — (NULL, 55000) won't reliably match via = comparison logic, so depending on Oracle version/context, David's own row might not even match itself in strict tuple comparison. Not something to worry deeply about for interviews — just know NULL + tuple comparisons is an edge case, not a core scenario they'd test heavily.

**Real-world use case:** commonly used for comparison-style row matching, e.g., "find rows in table A that exactly match a row in table B across multiple key columns" — useful in data validation/reconciliation.
