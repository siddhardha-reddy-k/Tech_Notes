## MULTIPLE-ROW SUBQUERY

A subquery that returns **more than one row** — needs different operators since =, >, < can't handle multiple values. Three operators: IN, ANY, ALL.

### IN

Checks if the outer value matches **any one** value in the list returned by the subquery — like checking membership in a set.

```sql
SELECT *
FROM emp
WHERE esal IN
(
    SELECT esal FROM emp WHERE deptno = 10 -- will return single column with esal of dept 10. and the outer will compare one record with all rows of inner.
);
```

Inner query returns: 45000, 41000 (Alan's and Priya's salaries — dept 10).

Output:

```text
EID  ENAME   ESAL    DEPTNO
101  Alan    45000   10
103  Priya   41000   10
```

Only rows whose esal **exactly equals one of** 45000 or 41000 survive — a direct match check against the list.

### ANY

esal > ANY (subquery) means: greater than **at least one** value in the list — effectively, greater than the **minimum** of the subquery's results.

```sql
SELECT *
FROM emp
WHERE esal > ANY
(
    SELECT esal FROM emp WHERE deptno = 10
);
```

Subquery list: 45000, 41000. > ANY succeeds if esal beats **at least one** of these — so effectively esal > 41000 (the smaller one) is enough to qualify.

Output:

```text
EID  ENAME   ESAL    DEPTNO
101  Alan    45000   10
102  Raja    52000   20
104  Kiran   60000   20
106  David   55000   NULL
```

Alan (45000) qualifies because he beats 41000 (Priya's), even though he doesn't beat his own 45000. Priya herself doesn't qualify — 41000 isn't greater than either 45000 or 41000.

### ALL

esal > ALL (subquery) means: greater than **every single** value in the list — effectively, greater than the **maximum**.

```sql
SELECT *
FROM emp
WHERE esal > ALL
(
    SELECT esal FROM emp WHERE deptno = 10
);
```

Subquery list: 45000, 41000. Must beat **both** — effectively esal > 45000 (the larger one).

Output:

```text
EID  ENAME   ESAL    DEPTNO
102  Raja    52000   20
104  Kiran   60000   20
106  David   55000   NULL
```

Alan is excluded now — 45000 is not greater than 45000 (his own value is in the list).

**Memory trick, plain and simple:**

- ANY = easier to satisfy → compares against the **weakest** condition (min for >, max for <)
- ALL = harder to satisfy → compares against the **strongest** condition (max for >, min for <)
