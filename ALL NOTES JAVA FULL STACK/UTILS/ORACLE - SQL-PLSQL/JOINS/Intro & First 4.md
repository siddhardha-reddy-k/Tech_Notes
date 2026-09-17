## JOINS

### JOIN :

A join combines data from multiple tables based on a relationship or condition.

- Table Alias

- **Cartesian Product**
- **Equi Join (old syntax)**
- **Inner Join (ANSI)**
- **Non-Equi Join**
- **Self Join**
- **Left Outer Join**
- **Right Outer Join**
- **Full Outer Join**

- Cross Join
- Natural Join
- USING clause
- ON vs USING vs NATURAL — final comparison

### Exmaple Data for Joins:

```sql
-- DEPT table (Parent)

CREATE TABLE dept (
    deptno NUMBER PRIMARY KEY,
    dname  VARCHAR2(50),
    dloc   VARCHAR2(50)
);
```

```sql
-- EMP table (Child)

CREATE TABLE emp (
    eid    NUMBER PRIMARY KEY,
    ename  VARCHAR2(50),
    esal   NUMBER,
    deptno NUMBER
);
```

```sql
-- DEPT data (Sales dept 40 has NO employees -> tests RIGHT/FULL join)

INSERT INTO dept VALUES (10, 'HR', 'Hyderabad');
INSERT INTO dept VALUES (20, 'IT', 'Bangalore');
INSERT INTO dept VALUES (30, 'Finance', 'Chennai');
INSERT INTO dept VALUES (40, 'Sales', 'Mumbai');
```

```sql
-- EMP data (David has NO deptno -> tests LEFT/FULL join)

INSERT INTO emp VALUES (101, 'Alan', 45000, 10);
INSERT INTO emp VALUES (102, 'Raja', 52000, 20);
INSERT INTO emp VALUES (103, 'Priya', 41000, 10);
INSERT INTO emp VALUES (104, 'Kiran', 60000, 20);
INSERT INTO emp VALUES (105, 'Meena', 38000, 30);
INSERT INTO emp VALUES (106, 'David', 55000, NULL);
```

```sql
COMMIT;
```

### TABLE ALIAS

A temporary name given to a table for that query only. Doesn't persist, doesn't rename the actual table.

```sql
SELECT e.eid, e.ename, d.dname
FROM emp e, dept d;
```


## CARTESIAN PRODUCT

Every row from table1 combined with every row from table2. No matching condition applied.

```sql
SELECT * FROM emp, dept;
```

If EMP has 6 rows, DEPT has 4 rows → result = **6 × 4 = 24 rows**.  
its accidental.

## Equi Join (old syntax)

Tables joined using an **equality condition** (=) in the WHERE clause. This is the "old style" join syntax (pre-ANSI), but conceptually it's the foundation everything else builds on.

```sql
SELECT e.eid, e.ename, e.esal, d.dname, d.dloc
FROM emp e, dept d
WHERE e.deptno = d.deptno;
```

Simply -> it will show all records where emp dept no and dept deptno matches.

- David (deptno = NULL) → dropped. NULL never equals anything, not even another NULL, so e.deptno = d.deptno fails for him.
- Sales (deptno 40) → dropped. No emp row has deptno 40, so no match.

**-- Equi join (old style, comma + WHERE)**

```sql
FROM emp e, dept d WHERE e.deptno = d.deptno;
```

**-- Inner join (ANSI, next topic) — same output**

```sql
FROM emp e INNER JOIN dept d ON e.deptno = d.deptno;
```

## Inner Join (ANSI)

Same result as equi join, but written with explicit JOIN...ON — this is the modern, standard syntax you should default to.

```sql
SELECT e.eid, e.ename, e.esal, d.dname, d.dloc
FROM emp e
INNER JOIN dept d
ON e.deptno = d.deptno;
```

Same as Equi Join ->join both tables where the conditon matches. Simply we get employee details with depart name and location in department table.

## NON-EQUI JOIN

any join other than =

```sql
CREATE TABLE salgrade (
    grade  NUMBER, --1,2,3
    losal  NUMBER,
    hisal  NUMBER
);
```

```sql
INSERT INTO salgrade VALUES (1, 30000, 40000);
INSERT INTO salgrade VALUES (2, 40001, 50000);
INSERT INTO salgrade VALUES (3, 50001, 60000);
```

```sql
COMMIT;
```

```sql
SELECT e.ename, e.esal, s.grade
FROM emp e
JOIN salgrade s
ON e.esal BETWEEN s.losal AND s.hisal;
```

What join does here is -> it will take Each record of emp.  
ON e.esal BETWEEN s.losal AND s.hisal -> by this condition  
it will compare

- Is 45000 between 30000–40000? No.
- Is 45000 between 40001–50000? **Yes → Alan gets GRADE 2.**
- Is 45000 between 50001–60000? No (doesn't even need to check, already matched).

it will join s.grade to each emp record.
