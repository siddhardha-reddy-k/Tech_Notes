## NATURAL JOIN -

Automatically joins two tables on **any column(s) with the same name** — no ON or WHERE needed, Oracle figures out the join column itself.

```sql
SELECT * FROM emp
NATURAL JOIN dept;
```

Since emp and dept both have a column called deptno, Oracle automatically joins on it — equivalent to:

```sql
SELECT * FROM emp e
JOIN dept d ON e.deptno = d.deptno;
```

```text
DEPTNO  EID  ENAME   ESAL    DNAME     DLOC
10        101        Alan        45000        HR        Hyderabad
20        102        Raja        52000        IT        Bangalore
10        103        Priya        41000        HR        Hyderabad
20        104        Kiran        60000        IT        Bangalore
30        105        Meena        38000        Finance        Chennai
```

Notice: **deptno appears only once** (not duplicated as e.deptno and d.deptno separately) — that's a genuine difference from regular JOIN...ON, where you'd see both if you did SELECT *.

David and Sales are excluded — behaves like INNER JOIN by default (no OUTER variant of NATURAL JOIN in standard use).

**Why this is risky — the real gotcha:** it matches on **every** shared column name, not just the one you intend.

Suppose both tables also happened to have a created_date column (common in real schemas — audit columns). NATURAL JOIN would silently join on deptno AND created_date together — meaning a valid deptno match could get *rejected* just because created_date differs. You wouldn't get an error, just silently wrong/missing results. That's the dangerous part: it fails quietly, not loudly.
