## Right Outer Join -

Returns **all rows from the right table**, plus matching rows from the left. Unmatched left-table columns show NULL. It's the mirror image of LEFT OUTER JOIN.

Outer - leftover(include rows even if they're outside the matching zone.)

```sql
SELECT e.eid, e.ename, d.deptno, d.dname, d.dloc
FROM emp e
RIGHT OUTER JOIN dept d
ON e.deptno = d.deptno;
```

**Output:**

```text
EID  ENAME   DEPTNO  DNAME     DLOC
101        Alan        10        HR        Hyderabad
102        Raja        20        IT        Bangalore
103        Priya        10        HR        Hyderabad
104        Kiran        20        IT        Bangalore
105        Meena        30        Finance        Chennai
null        null        40        Sales        Mumbai
```

**Important practical note:** RIGHT OUTER JOIN is really just LEFT OUTER JOIN with the tables swapped. In real codebases, most people avoid RIGHT JOIN entirely and just rewrite it as a LEFT JOIN by flipping the FROM order — easier to read consistently:

```sql
-- This RIGHT JOIN...

FROM emp e RIGHT OUTER JOIN dept d ON e.deptno = d.deptno;
```

```sql
-- ...is identical to this LEFT JOIN (swap table order)

FROM dept d LEFT OUTER JOIN emp e ON e.deptno = d.deptno;
```

Same output either way. Good practice: pick ONE style (usually LEFT) and stick to it everywhere for consistency, rather than mixing LEFT and RIGHT across a codebase.
