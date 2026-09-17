## NOT EXISTS

The opposite of EXISTS — returns TRUE if the subquery returns **zero rows**, FALSE if it returns any rows.

```sql
SELECT * FROM emp e
WHERE NOT EXISTS (
    SELECT 1 FROM dept d
    WHERE e.deptno = d.deptno
);
```

**Step by step — mirroring the EXISTS trace from topic 7, but flipped:**

- Alan (deptno 10) → inner query finds dept 10 (HR) exists → subquery returns 1 row → EXISTS is TRUE → **NOT EXISTS is FALSE → Alan excluded.**
- Same logic excludes Raja, Priya, Kiran, Meena — all have valid, existing departments.
- David (deptno **NULL**) → inner query: WHERE deptno = NULL → matches nothing, 0 rows → EXISTS is FALSE → **NOT EXISTS is TRUE → David kept.**

Output:

```text
EID  ENAME   ESAL    DEPTNO
106  David   55000   NULL
```

Only David — the one employee whose department doesn't actually exist (well, technically his deptno is NULL, so there's nothing to match against in dept at all).

**A more realistic/common NOT EXISTS use case — the reverse direction, checking dept instead of emp:**

```sql
SELECT dname FROM dept d
WHERE NOT EXISTS (
    SELECT 1 FROM emp e
    WHERE e.deptno = d.deptno
);
```

This flips perspective: for each **department**, check if any employee exists in it.

- HR (10) → Alan, Priya exist → EXISTS true → NOT EXISTS false → excluded.
- IT (20) → Raja, Kiran exist → excluded.
- Finance (30) → Meena exists → excluded.
- Sales (40) → **no employee has deptno 40** → EXISTS false → NOT EXISTS true → **kept.**

Output:

```text
DNAME
Sales
```

This is the genuinely common real-world pattern: "find departments/categories/products with **zero** related records" — e.g., "find customers who never placed an order," "find products never sold." You'll see this exact shape in interviews a lot.

**Quick mental shortcut:** EXISTS = "has at least one match." NOT EXISTS = "has zero matches." Both are almost always used as correlated subqueries (referencing the outer row), since a non-correlated EXISTS/NOT EXISTS would just return the same TRUE/FALSE for every row — not very useful.
