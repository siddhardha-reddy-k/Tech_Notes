## USING CLAUSE -

The explicit, safer version of NATURAL JOIN — **you** name which column(s) to join on, instead of letting Oracle guess by matching all same-named columns.

```sql
SELECT * FROM emp
JOIN dept USING (deptno);
```

Output — same as NATURAL JOIN:

```text
DEPTNO  EID  ENAME   ESAL    DNAME     DLOC
10        101        Alan        45000        HR        Hyderabad
20        102        Raja        52000        IT        Bangalore
10        103        Priya        41000        HR        Hyderabad
20        104        Kiran        60000        IT        Bangalore
30        105        Meena        38000        Finance        Chennai
```

deptno still shows once (not duplicated) — that behavior carries over from NATURAL JOIN. David and Sales still excluded (inner-join behavior).

**Why this fixes NATURAL JOIN's danger:** even if emp and dept *also* shared a created_date column, USING only joins on what you explicitly listed — deptno. That phantom second match-condition problem from topic 11 simply can't happen here, because you control exactly which column(s) get used.

**Important restriction — this is a common gotcha:** with USING, you **cannot alias the join column** in the SELECT list with a table prefix:

```sql
-- ❌ ERROR — deptno is ambiguous with USING, can't prefix it

SELECT e.deptno FROM emp e
JOIN dept d USING (deptno);
```

```sql
-- ✅ Correct — reference deptno without table prefix

SELECT deptno FROM emp
JOIN dept USING (deptno);
```

This is because USING merges deptno into a single shared column — Oracle won't let you call it e.deptno or d.deptno anymore, since technically it no longer "belongs" to just one side.

Multiple columns:

```sql
SELECT * FROM emp
JOIN dept USING (deptno, company_id);
```

Only works if both column names match exactly and you want to join on all of them together.

**Where USING fits in the hierarchy:** shorter than full ON syntax, safer than NATURAL JOIN, but still less flexible than ON — can't join on columns with *different* names (e.g., emp.deptno = dept.department_id), which ON can do.
