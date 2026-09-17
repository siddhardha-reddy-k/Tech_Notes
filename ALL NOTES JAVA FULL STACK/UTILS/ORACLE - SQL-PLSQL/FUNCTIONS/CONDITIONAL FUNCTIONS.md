## CONDITIONAL FUNCTIONS

Conditional functions return different values based on conditions.

Main functions:

CASE  
DECODE  
COALESCE  
NVL  
NVL2  
NULLIF

### CASE Simple CASE

```sql
CASE expression
  WHEN value1 THEN result1
  WHEN value2 THEN result2
  ELSE result_default
END
```

Example:

```sql
SELECT eid, ename, job,
  CASE job
    WHEN 'Manager' THEN 'Senior'
    WHEN 'Clerk' THEN 'Junior'
    ELSE 'Mid-Level'
  END AS level
FROM emp;
```

### CASE Searched CASE

```sql
CASE
  WHEN condition1 THEN result1
  WHEN condition2 THEN result2
  ELSE result_default
END
```

Example:

```sql
SELECT eid, ename, esal,
  CASE
    WHEN esal > 40000 THEN 'High'
    WHEN esal > 25000 THEN 'Medium'
    ELSE 'Low'
  END AS salary_grade
FROM emp;
```

### COALESCE

Returns the first non-NULL value in a list.

Syntax: COALESCE(expr1, expr2, expr3, ...)

Example:

```sql
SELECT eid, ename, COALESCE(commission, 0) AS comm FROM emp;
```

If commission is NULL, returns 0.

Multiple arguments:

```sql
SELECT COALESCE(col1, col2, col3, 'No value') FROM table1;
```

### NVL

Returns a substitute value if the expression is NULL.

Syntax: NVL(expr1, substitute_value)

Example:

```sql
SELECT eid, ename, NVL(commission, 0) AS comm FROM emp;
```

Similar to COALESCE but takes only 2 arguments.

### NVL2

Returns different values based on whether expr1 is NULL.

Syntax: NVL2(expr1, if_not_null, if_null)

Example:

```sql
SELECT eid, ename,
  NVL2(commission, 'Has Commission', 'No Commission') AS comm_status
FROM emp;
```

### NULLIF

Returns NULL if two expressions are equal, otherwise returns the first expression.

Syntax: NULLIF(expr1, expr2)

Example:

```sql
SELECT eid, ename,
  NULLIF(esal, 25000) AS modified_sal
FROM emp;
```

If esal = 25000, returns NULL; otherwise returns esal.

### DECODE

Compares an expression to a list of values and returns a result.

Syntax:

```sql
DECODE(expr, search_value1, result1, search_value2, result2, ..., default_result)
```

Example:

```sql
SELECT eid, ename, deptno,
  DECODE(deptno,
    10, 'HR',
    20, 'IT',
    30, 'Sales',
    'Unknown') AS dept_name
FROM emp;
```

### CASE vs DECODE

CASE is ANSI SQL standard (portable).

DECODE is Oracle-specific.

CASE is more readable for complex conditions.

Both achieve similar results.
