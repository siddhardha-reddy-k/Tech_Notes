## ON vs USING vs NATURAL — Final Comparison

Three ways to specify the same join, ranked by control and safety.

### ON Clause — most explicit, most flexible

```sql
SELECT e.eid, e.ename, d.dname
FROM emp e
JOIN dept d ON e.deptno = d.deptno;
```

- Works even if column names **differ** between tables (e.g. emp.deptno = dept.department_id)
- Both e.deptno and d.deptno remain separately accessible
- Standard SQL, portable across databases
- **Default choice for production code**

### USING Clause — shorter, still explicit

```sql
SELECT deptno, ename, dname
FROM emp
JOIN dept USING (deptno);
```

- Only works when column names are **identical** on both sides
- Merges the join column into one — can't prefix it with a table alias
- Good middle ground: safe, but less flexible than ON

### NATURAL JOIN — implicit, riskiest

```sql
SELECT * FROM emp
NATURAL JOIN dept;
```

- Auto-matches **every** same-named column — no control over which ones
- Silent failure risk if an unexpected shared column exists (e.g. created_date)
- Not recommended for production

### Side-by-side summary

| Feature | ON | USING | NATURAL |
| --- | --- | --- | --- |
| Join column stated explicitly | ✅ Yes | ✅ Yes (named) | ❌ No (auto) |
| Works with differently-named columns | ✅ Yes | ❌ No | ❌ No |
| Column appears once or twice in output | Twice (e.deptno, d.deptno) | Once | Once |
| Risk of unintended extra matches | None | None | High |
| Recommended for production | ✅ Best | ✅ OK | ❌ Avoid |

**Interview-ready one-liner:** *"NATURAL JOIN implicitly matches all same-named columns, which is risky if unexpected columns overlap. USING is the explicit, safer alternative when column names match. ON is the most flexible — it works regardless of naming and is standard practice in production."*
