## EXISTS with UPDATE/DELETE

EXISTS isn't limited to SELECT — it's just as common inside UPDATE/DELETE WHERE clauses, to conditionally act on rows based on some related condition.

**Example — give a raise to everyone in the IT department:**

```sql
UPDATE emp e
SET esal = esal * 1.1
WHERE EXISTS (
    SELECT 1 FROM dept d
    WHERE e.deptno = d.deptno
    AND d.dname = 'IT'
);
```

**Step by step:**

- For each emp row, correlated subquery checks: does a dept row exist matching this employee's deptno **AND** having dname = 'IT'?
- Raja (deptno 20) → dept 20 is IT → EXISTS true → **gets updated**: 52000 × 1.1 = 57200
- Kiran (deptno 20) → same → **updated**: 60000 × 1.1 = 66000
- Everyone else (HR, Finance, NULL) → EXISTS false → **untouched**

**Why EXISTS here instead of a plain join-style filter?** UPDATE/DELETE can't use a JOIN clause in Oracle the way SELECT does — you can't write UPDATE emp e JOIN dept d ON.... EXISTS (or IN) is how you bring in a **related table's condition** into an UPDATE/DELETE without a join syntax. This is genuinely important — it's the standard pattern for "update/delete rows in table A based on a condition in table B."

**Example — delete departments with zero employees (using our earlier NOT EXISTS logic, now as a DELETE):**

```sql
DELETE FROM dept d
WHERE NOT EXISTS (
    SELECT 1 FROM emp e
    WHERE e.deptno = d.deptno
);
```

This would delete Sales (deptno 40) — the only dept with no employees. Same NOT EXISTS logic as the SELECT version from topic 9, just wrapped in DELETE instead.

**Practical caution, genuinely important:** always **test the logic as a SELECT first**, then convert to UPDATE/DELETE once you're sure it targets the right rows. Once you run DELETE, there's no undo without a ROLLBACK (and only if you haven't committed yet). This is standard practice, not just caution for caution's sake — accidentally deleting the wrong rows because your WHERE EXISTS logic was slightly off is a very real, very common mistake.

```sql
-- Safe habit: check first

SELECT * FROM dept d WHERE NOT EXISTS (SELECT 1 FROM emp e WHERE e.deptno = d.deptno);
```

```sql
-- Then convert to DELETE once confirmed

DELETE FROM dept d WHERE NOT EXISTS (SELECT 1 FROM emp e WHERE e.deptno = d.deptno);
```
