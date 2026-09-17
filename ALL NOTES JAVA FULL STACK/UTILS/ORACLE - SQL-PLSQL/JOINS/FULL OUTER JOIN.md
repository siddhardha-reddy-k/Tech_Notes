## FULL OUTER JOIN

Returns matching rows + leftovers from **both** left and right tables. It's LEFT OUTER JOIN + RIGHT OUTER JOIN combined, with duplicates removed.

```sql
SELECT e.eid, e.ename, e.deptno, d.dname, d.dloc
FROM emp e
FULL OUTER JOIN dept d
ON e.deptno = d.deptno;
```

```text
EID   ENAME   DEPTNO  DNAME     DLOC
101        Alan        10        HR        Hyderabad
102        Raja        20        IT        Bangalore
103        Priya        10        HR        Hyderabad
104        Kiran        20        IT        Bangalore
105        Meena        30        Finance        Chennai
106        David        null        null        null
null        null        null        Sales        Mumbai
```

**Mental model, tying together everything so far:**

| Join type | What survives |
| --- | --- |
| INNER JOIN | Only matches |
| LEFT OUTER JOIN | Matches + left leftovers |
| RIGHT OUTER JOIN | Matches + right leftovers |
| FULL OUTER JOIN | Matches + left leftovers + right leftovers |
