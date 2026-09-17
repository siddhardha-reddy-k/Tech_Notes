## ARITHMETIC OPERATORS

### + - * /

```sql
SELECT esal+1000 FROM emp;
SELECT esal-1000 FROM emp;
SELECT esal*12 FROM emp;
SELECT esal/12 FROM emp;
```

Annual salary:

```sql
SELECT eid, ename, esal, esal*12 FROM emp;
```

## COLUMN ALIAS

Temporary column name while the ouput the result.

### Using AS

```sql
SELECT esal*12 AS annual_sal FROM emp;
```

### Without AS

```sql
SELECT esal*12 annual_sal FROM emp;
```

Multiple aliases:

```sql
SELECT roll AS roll_no, name AS studentname, address AS city FROM student;
```

## DUAL

DUAL is Oracle's special one-row table commonly used to evaluate expressions and functions without selecting from a user table.

Examples:

```sql
SELECT 10+20 FROM dual; - 10+20 col with 30 as row.
SELECT 10*20 FROM dual;
SELECT SYSDATE FROM dual;
SELECT CURRENT_DATE FROM dual;
```

## COPY TABLE -

### CREATE TABLE AS SELECT

Used to create a new table using the result of a query.

### Copy Everything

```sql
CREATE TABLE employees AS SELECT * FROM emp;
```

### Copy Selected Columns

```sql
CREATE TABLE employees AS SELECT eid,ename,esal FROM emp;
```

### Copy Selected Rows

```sql
CREATE TABLE employees AS SELECT * FROM emp WHERE deptno=10;
```

### Copy Using LIKE

```sql
CREATE TABLE employees AS SELECT * FROM emp WHERE ename LIKE 'A%';
```
