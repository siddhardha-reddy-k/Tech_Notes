## EXISTS vs IN

Both can achieve similar filtering results, but they work differently under the hood, and this difference matters at scale.

**Same goal, two ways — employees who have a valid department:**

```sql
-- Using IN

SELECT * FROM emp e
WHERE e.deptno IN (SELECT deptno FROM dept);
```

```sql
-- Using EXISTS

SELECT * FROM emp e
WHERE EXISTS (SELECT 1 FROM dept d WHERE d.deptno = e.deptno);
```

Both give the same 5 rows (everyone except David). So why does it matter which you pick?

**How IN actually works:** Oracle runs the inner query **completely first**, builds the **full list** of all dept's deptno values (10, 20, 30, 40), holds that entire list in memory, and *then* checks each emp row against that full list.

**How EXISTS actually works (with correlated subquery):** for each emp row, Oracle runs the inner query and **stops the moment it finds ONE matching row** — it doesn't care if there are more matches, one is enough to confirm TRUE. No need to build or scan a full separate list.

**Why this matters at scale — the actual performance reasoning:**

- If dept has **millions of rows**, IN has to materialize that entire result set first, before doing any comparison — expensive in memory and time.
- EXISTS, being correlated, checks row-by-row and **short-circuits** — the moment it finds a match for the current emp row, it moves on. It never needs the "full list" concept at all.

**Rule of thumb, genuinely useful for interviews:**

- **EXISTS** → better for correlated checks against **large** subquery result sets, since it stops early.
- **IN** → fine, often simpler to read, for **small, static lists** — especially non-subquery lists like WHERE deptno IN (10, 20, 30).

One more real difference — NULL handling, a classic gotcha:

```sql
WHERE deptno NOT IN (SELECT deptno FROM emp)  -- risky
```

If the subquery's result **contains even one NULL**, NOT IN mysteriously returns **zero rows for everything** — because comparing against NULL with <> (which NOT IN uses internally) is always NULL/unknown, poisoning the entire list. NOT EXISTS doesn't have this problem — it's immune to NULLs in the subquery, since it's just checking row-existence, not literal value comparison.

**This NULL trap is a very common real bug people hit** — always prefer NOT EXISTS over NOT IN when the subquery column could contain NULLs (deptno on our emp table, for instance, given David).

**Summary table:**

|  | **EXISTS** | **IN** |
| --- | --- | --- |
| Returns | TRUE/FALSE | TRUE/FALSE/**NULL** (unknown) |
| Stops early on match? | Yes | No, builds full list first |
| Safe with NULLs in subquery (NOT variant) | Yes | **No — silently breaks NOT IN** |
| Best for | Correlated, large datasets | Small static/simple lists |
