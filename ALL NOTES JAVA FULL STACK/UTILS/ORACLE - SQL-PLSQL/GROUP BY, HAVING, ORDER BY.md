## GROUP BY, HAVING, ORDER BY

### GROUP BY

### My explanation -

Name      Null?    Type        

--------- -------- ------------

ID        NOT NULL NUMBER      

NAME               VARCHAR2(50)

DEPT               VARCHAR2(50)

JOB_TITLE          VARCHAR2(50)

SALARY             NUMBER(10,2)



FOR THIS TABLE - QUERY -

```sql
SELECT dept, COUNT(*) AS staff_count
FROM staff
GROUP BY dept;
```

```sql
-- FIRST group by creates separate tables for each dept and add those records in that table. And then SELECT DEPT, COUNT(*) will show table dept name and count will tell total records in that table nothing but total no of employees.
```

```sql
SELECT dept, MAX(salary) AS highest_salary
FROM staff
GROUP BY dept;
```

grouped by dept, and max will be applied to to find the cell with max salary and it will show dept and the max salary in that dept. no other details.  

USING WHERE with group by -

```sql
SELECT dept, MAX(salary) FROM STAFF WHERE salary<=50000 GROUP BY dept;
```

it will olly pick records with salary greater than 50000 to from the groups by dept.  

GROUP BY divides rows into groups.

Example:

```sql
SELECT deptno, SUM(esal) FROM emp GROUP BY deptno;
```

Result conceptually:

DEPTNO    SUM(SALARY)

------    -----------

10        ...

20        ...

30        ...

### Average Salary Per Department

```sql
SELECT deptno, AVG(esal) FROM emp GROUP BY deptno;
```

### Maximum Salary Per Job

```sql
SELECT job, MAX(esal) FROM emp GROUP BY job;
```

### GROUP BY with WHERE

```sql
SELECT deptno, SUM(esal) FROM emp WHERE deptno<>10 GROUP BY deptno;
```

### Important Order

FROM  
WHERE  
GROUP BY

### HAVING

### Explnation

```sql
SELECT dept, COUNT(*) AS staff_count
FROM staff
GROUP BY dept
HAVING COUNT(*) > 2;
```

```sql
-- create groups by dept and then show dept and its count() - total reocrds in that table. And then finally if its having more than 2 only it will show.
```

so, having is performed on the final output of the query. And where keyword is used to pick records to from groups tables.  

HAVING filters groups.

Example:

```sql
SELECT deptno, SUM(esal) FROM emp GROUP BY deptno HAVING SUM(esal)>40000;
```

### WHERE vs HAVING

| WHERE | HAVING |
| --- | --- |
| Filters rows | Filters groups |
| Applied before grouping | Applied after grouping |
| Usually used with normal conditions | Commonly used with aggregate results |

### ORDER BY

Used to sort query results.

### Ascending

```sql
SELECT * FROM emp ORDER BY esal;
```

ASC is the default.

Explicit:

```sql
SELECT * FROM emp ORDER BY esal ASC;
```

### Descending

```sql
SELECT * FROM emp ORDER BY esal DESC;
```

### Multiple Columns

```sql
SELECT * FROM emp ORDER BY deptno ASC, esal DESC;
```

```sql
SELECT * FROM EMP;

select deptno, AVG(esal)
FROM emp
WHERE deptNO IS NOT NULL
GROUP BY deptno
HAVING AVG(ESAL) > 40000
ORDER BY AVG(ESAL) DESC;
```

### SQL CLAUSE ORDER

A useful logical order to remember:

FROM  
WHERE  
GROUP BY  
HAVING  
SELECT  
ORDER BY

A common written query:

```sql
SELECT deptno, SUM(esal)
FROM emp
WHERE deptno<>10
GROUP BY deptno
HAVING SUM(esal)>30000
ORDER BY deptno;
```
