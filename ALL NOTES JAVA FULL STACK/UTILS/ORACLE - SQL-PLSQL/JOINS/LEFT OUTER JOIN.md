## LEFT OUTER JOIN-

Returns **all rows from the left table**, plus matching rows from the right table. If no match exists, right table's columns show as NULL.

Outer - leftover(include rows even if they're outside the matching zone.)

```sql
SELECT e.eid, e.ename, e.deptno, d.dname, d.dloc
FROM emp e
LEFT OUTER JOIN dept d
ON e.deptno = d.deptno;
```

```text
EID  ENAME   DEPTNO  DNAME     DLOC
101        Alan        10        HR        Hyderabad
103        Priya        10        HR        Hyderabad
102        Raja        20        IT        Bangalore
104        Kiran        20        IT        Bangalore
105        Meena        30        Finance        Chennai
106        David        null        null        null
```

**What changed vs INNER JOIN:** David is back. emp is the **left** table here (FROM emp e LEFT OUTER JOIN dept d), so LEFT OUTER JOIN guarantees every emp row survives — matched or not. Since David's deptno is NULL, there's no dept match, so dname and dloc just show NULL instead of dropping his row entirely.

**Sales dept (40)?** Still missing — it's on the right side, and LEFT OUTER JOIN doesn't guarantee right-side rows, only left-side ones.

**Mental model — think of it as INNER JOIN + leftovers:**

1. First, do the normal inner join (5 matching rows, same as topic 4).
2. Then, add back any left-table rows that had zero matches, filling right-side columns with NULL.

**Left table = whichever table is written first / before "LEFT OUTER JOIN".** This is critical — swap emp and dept in the FROM clause and the result changes completely (that becomes RIGHT join territory, coming next).
