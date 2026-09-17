## FUNCTIONS 
Functions perform operations and return results.

Two major categories:

1. Group / Multiple-Row Functions -  Ex- add all the values of a column.  
2. Single-Row / Scalar Functions - Ex - uppercase and return all rows.

The repository covers both categories.
## GROUP FUNCTIONS

Group functions process Multiple rows and return one result per group, or one result for the entire input if no GROUP BY is used.

Main functions:

SUM()
AVG()
MAX()
MIN()
COUNT()

### SUM

```sql
SELECT SUM(esal) FROM emp;
```

Returns total salary.

### AVG

```sql
SELECT AVG(esal) FROM emp;
```

Returns average salary.

### MAX

```sql
SELECT MAX(esal) FROM emp;
```

Returns highest salary.

### MIN

```sql
SELECT MIN(esal) FROM emp;
```

Returns lowest salary.

### COUNT(*)

```sql
SELECT COUNT(*) FROM emp;
```

Counts rows.

### COUNT(column)

```sql
SELECT COUNT(comm) FROM emp;
```

Counts non-NULL values in comm.
