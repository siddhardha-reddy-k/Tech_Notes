## SELF JOIN -

A table joined **with itself**. Since it's the same table, you must alias it twice — Oracle needs two "copies" to compare rows against each other.

```sql
SELECT e1.ename AS emp1, e2.ename AS emp2, e1.deptno
FROM emp e1
JOIN emp e2
ON e1.deptno = e2.deptno
AND e1.eid < e2.eid;
```

Output:

```text
EMP1    EMP2    DEPTNO
Alan    Priya   10
Raja    Kiran   20
```

it takes one record from table 1 and it tried to check condition is true with every other record in table 2

Order--

**The comparison order Oracle conceptually follows:** row-by-row from e1 (outer loop), and for *each* e1 row, scan through **all** of e2 (inner loop) — top to bottom, in whatever order the rows physically exist in the table (which is usually insertion order, unless you sort).

FOR each row in e1 (Alan, Raja, Priya, Kiran, Meena, David — in that insert order): FOR each row in e2 (Alan, Raja, Priya, Kiran, Meena, David — same order): check condition if true → keep the pair

**One more thing — result order isn't guaranteed** unless you use ORDER BY. Never assume SQL output order without it, even if it "looks" ordered in practice.
