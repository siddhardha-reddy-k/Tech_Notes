Remember Things

## REGEXP_SUBSTR

Useful for extracting portions of text using regular expressions.

Example:

```sql
SELECT REGEXP_SUBSTR(name,'\S+',1,1) FROM emp1;
```

First word:

Alan Morries → Alan  
Erick Anderson → Erick  

Syntax decoded -

REGEXP_SUBSTR(name, '\S+', 1, 1):

1. **name — The column being searched.**
2. **'\S+' — The      pattern to match (looks for a continuous block of non-space characters,      i.e., a single word).**
3. **1      (Position) — Where to start searching (starts at the first      character).**
4. **1      (Occurrence) — Which match to extract (grabs the first word found).**

## SUBSTR

Extracts a substring from a string.

Syntax: SUBSTR(string, start_position, [length])

Note: Position starts at 1 (not 0).

Example:

```sql
SELECT SUBSTR('Oracle Training', 1, 6) FROM dual;
```

Result: Oracle

Start position only:

```sql
SELECT SUBSTR('Oracle Training', 8) FROM dual;
```

Result: Training (from position 8 to end)

Negative position (from end):

```sql
SELECT SUBSTR('Oracle Training', -8) FROM dual;
```

Result: Training (8 characters from the end)

## TRUNC

Truncates without rounding.

```sql
SELECT TRUNC(10.56) FROM dual;
```

Result:

10

USED TO COMPARE BETWEEN COLUMNS OF RECORD.

## GREATEST

Returns the greatest value.

```sql
SELECT GREATEST(9,2,7,1) FROM dual;
```

Result:

9

## LEAST

Returns the smallest value.

```sql
SELECT LEAST(9,2,7,1) FROM dual;
```

Result:

1

## CONVERSION FUNCTIONS

Conversion functions convert one datatype/value representation into another.

Important functions:

TO_CHAR  
TO_DATE  
TO_NUMBER

## TO_CHAR — Number

Converts a number to character representation.

```sql
SELECT TO_CHAR(esal,'99,999') FROM emp;
```

Currency formatting:

```sql
SELECT TO_CHAR(esal,'$99,999') FROM emp;
```

## TO_CHAR — Date

```sql
SELECT TO_CHAR(SYSDATE,'DD-MM-YYYY') FROM dual;
```

Other formats:

```sql
SELECT TO_CHAR(SYSDATE,'YYYY-MM-DD') FROM dual;

SELECT TO_CHAR(SYSDATE,'DD-MM-YYYY HH24:MI:SS') FROM dual;

SELECT TO_CHAR(SYSDATE,'YYYY') FROM dual;

SELECT TO_CHAR(SYSDATE,'MONTH') FROM dual;

SELECT TO_CHAR(SYSDATE,'DAY') FROM dual;
```

**Important**

For hours:

HH   → 12-hour clock  
HH24 → 24-hour clock  

For minutes:

MI

# JOINS CHEAT SHEET

## SQL JOINS — Cheat Sheet (dept / emp)

```sql
-- DEPT (parent): 10-HR, 20-IT, 30-Finance, 40-Sales(no emps)
-- EMP (child): eid, ename, esal, deptno (David=106 has deptno NULL)
```

### Cartesian Product

```sql
SELECT e.ename, d.dname
FROM emp e, dept d;
-- no WHERE condition -> rows = 6 x 4 = 24
```

### Equi Join (old syntax)

```sql
SELECT e.ename, d.dname
FROM emp e, dept d
WHERE e.deptno = d.deptno;
```

### Inner Join (ANSI)

```sql
SELECT e.ename, d.dname
FROM emp e
JOIN dept d
  ON e.deptno = d.deptno; - same as equi join
```

### Non-Equi Join

```sql
SELECT e.ename, e.esal, d.dname
FROM emp e
JOIN dept d
  ON e.esal BETWEEN 40000 AND 60000
  AND e.deptno != d.deptno;
```

### Self Join

```sql
-- emp joined to itself (e.g. same dept co-workers)
SELECT e1.ename AS emp1, e2.ename AS emp2, e1.deptno
FROM emp e1
JOIN emp e2
  ON e1.deptno = e2.deptno
  AND e1.eid <> e2.eid;
```

### Left Outer Join

```sql
SELECT e.ename, d.dname
FROM emp e
LEFT JOIN dept d
  ON e.deptno = d.deptno;
-- includes David (deptno NULL)
```

### Right Outer Join

```sql
SELECT e.ename, d.dname
FROM emp e
RIGHT JOIN dept d
  ON e.deptno = d.deptno;
-- includes Sales (40) with no emps
```

### Full Outer Join

```sql
SELECT e.ename, d.dname
FROM emp e
FULL JOIN dept d
  ON e.deptno = d.deptno;
-- includes David AND Sales
```

### Cross Join

```sql
SELECT e.ename, d.dname
FROM emp e
CROSS JOIN dept d;
-- ANSI equivalent of cartesian product, 24 rows
```

### Natural Join

```sql
SELECT e.ename, d.dname
FROM emp e
NATURAL JOIN dept d;
-- auto-joins on ALL identically named columns (here: deptno)
```

### USING clause

```sql
SELECT e.ename, d.dname
FROM emp e
JOIN dept d
  USING (deptno);
-- like natural join but you pick the column; can't prefix deptno with alias
```

# SQL VIEWS — Cheat Sheet (dept / emp)

## Simple View

```sql
-- based on ONE table, no joins/group by/functions -> DML allowed
CREATE VIEW vw_it_emp AS
SELECT eid, ename, esal, deptno
FROM emp
WHERE deptno = 20;
```

## Complex View

```sql
-- multiple tables / group by / functions -> DML mostly NOT allowed
CREATE VIEW vw_dept_salary AS
SELECT d.dname, COUNT(e.eid) AS emp_count, SUM(e.esal) AS total_sal
FROM dept d
LEFT JOIN emp e ON d.deptno = e.deptno
GROUP BY d.dname;
```

## WITH READ ONLY

```sql
-- blocks INSERT/UPDATE/DELETE through the view
CREATE VIEW vw_hr_emp AS
SELECT eid, ename, esal, deptno
FROM emp
WHERE deptno = 10
WITH READ ONLY;

-- any DML attempt fails:
-- ORA-01733: virtual column not allowed here (or)
-- ORA-42399: cannot perform DML on read-only view
```

## WITH CHECK OPTION

```sql
-- allows DML, but blocks rows that would violate the view's WHERE clause
CREATE VIEW vw_it_only AS
SELECT eid, ename, esal, deptno
FROM emp
WHERE deptno = 20
WITH CHECK OPTION;

-- allowed: UPDATE vw_it_only SET esal = 55000 WHERE eid = 102;
-- blocked: UPDATE vw_it_only SET deptno = 30 WHERE eid = 102;
-- (ORA-01402: view WITH CHECK OPTION where-clause violation)
```

## Materialized View

```sql
-- physically stores query result (snapshot), needs refresh; used for performance/reporting
CREATE MATERIALIZED VIEW mv_dept_salary
BUILD IMMEDIATE
REFRESH COMPLETE ON DEMAND
AS
SELECT d.dname, COUNT(e.eid) AS emp_count, SUM(e.esal) AS total_sal
FROM dept d
LEFT JOIN emp e ON d.deptno = e.deptno
GROUP BY d.dname;

-- manual refresh:
EXEC DBMS_MVIEW.REFRESH('MV_DEPT_SALARY');

-- auto refresh every 1 day:
CREATE MATERIALIZED VIEW mv_dept_salary
BUILD IMMEDIATE
REFRESH COMPLETE ON DEMAND
START WITH SYSDATE NEXT SYSDATE + 1
AS
SELECT d.dname, COUNT(e.eid) AS emp_count, SUM(e.esal) AS total_sal
FROM dept d
LEFT JOIN emp e ON d.deptno = e.deptno
GROUP BY d.dname;

-- drop it
DROP MATERIALIZED VIEW mv_dept_salary;
```
