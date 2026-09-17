## EXISTS OPERATOR

Checks **whether a subquery returns any rows at all** — doesn't care about the actual values, just: does at least one row come back? Returns TRUE or FALSE.

```sql
SELECT * FROM emp e
WHERE EXISTS (
    SELECT 1 FROM dept d
    WHERE e.deptno = d.deptno
);
```

**What's different here — notice e.deptno inside the subquery.** The inner query references a column from the **outer** query (e.deptno). This makes it a **correlated subquery** — the inner query isn't a fixed, standalone thing anymore; it depends on which outer row Oracle is currently looking at. We'll properly define "correlated" as its own topic right after this, but you need to see it in action first to understand EXISTS.

**Step by step, row by row (this is the part that matters):**

- Oracle takes Alan (deptno 10) → runs the inner query **specifically for Alan**: SELECT 1 FROM dept WHERE deptno = 10 → dept 10 (HR) exists → subquery returns 1 row → EXISTS is TRUE → **Alan kept**.
- Takes Raja (deptno 20) → inner query checks deptno 20 → IT exists → TRUE → **kept**.
- ...same for Priya, Kiran, Meena — all their depts exist.
- Takes David (deptno **NULL**) → inner query: SELECT 1 FROM dept WHERE deptno = NULL → NULL never equals anything, not even in this context → returns 0 rows → EXISTS is FALSE → **David excluded**.

Output:

```text
EID  ENAME   ESAL    DEPTNO
101  Alan    45000   10
102  Raja    52000   20
103  Priya   41000   10
104  Kiran   60000   20
105  Meena   38000   30
```

Same result as our INNER JOIN from earlier, actually — EXISTS here is functioning like a filter version of a join.

**Why SELECT 1 and not SELECT * or SELECT deptno?** This is a genuinely important habit, not just style. EXISTS **never looks at what values come back** — it only checks *if any row comes back at all*. So selecting actual column data is wasted work — Oracle would fetch real values it's just going to throw away. SELECT 1 (or any constant) tells Oracle "I don't need the data, just tell me if a row exists" — this is a real performance habit, not just convention.
