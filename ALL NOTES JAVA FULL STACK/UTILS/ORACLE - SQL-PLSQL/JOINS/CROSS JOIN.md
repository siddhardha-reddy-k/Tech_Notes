	## CROSS JOIN

The **intentional** version of the cartesian product. Every row from table1 paired with every row from table2 — no condition at all, on purpose.

```sql
SELECT e.ename, d.dname
FROM emp e
CROSS JOIN dept d;
```

**Output:** 6 emp rows × 4 dept rows = **24 rows total.** Every employee shown against every department, including nonsensical pairs (Alan against Sales, even though Alan isn't in Sales).

**Difference from topic 2's accidental cartesian product:** mechanically **identical** — same 24 rows either way. The only difference is *intent*:

- FROM emp, dept with no WHERE → looks like a mistake, someone forgot the join condition.
- FROM emp CROSS JOIN dept → explicitly signals "I want every combination, this is deliberate," so anyone reading the query knows it's not a bug.

Real use case — generating combinations, not filtering real relationships:

```sql
-- Example: every color with every size (product catalog)

SELECT c.color, s.size
FROM colors c
CROSS JOIN sizes s;
```
