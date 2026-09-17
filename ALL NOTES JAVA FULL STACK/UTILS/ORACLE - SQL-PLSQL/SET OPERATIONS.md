## SET OPERATIONS

Set operations combine results from multiple SELECT statements.

Four main operations:

UNION  
UNION ALL  
INTERSECT  
MINUS  

### UNION

Combines result sets from two or more queries and removes duplicates.

Syntax:

```sql
SELECT col1, col2 FROM table1
UNION
SELECT col1, col2 FROM table2;
```

Example:

```sql
SELECT ename FROM emp WHERE deptno=10
UNION
SELECT ename FROM dept WHERE deptno=10;
```

Returns unique names from both queries.

**Important**

Both SELECT statements must have the same number of columns.

Column datatypes must be compatible.

UNION removes duplicate rows.

Result is sorted by default (performance consideration).

### UNION ALL

Combines results and KEEPS duplicates.

Syntax:

```sql
SELECT col1, col2 FROM table1
UNION ALL
SELECT col1, col2 FROM table2;
```

Example:

```sql
SELECT esal FROM emp WHERE deptno=10
UNION ALL
SELECT esal FROM emp WHERE deptno=20;
```

Returns all salaries, including duplicates.

Performance: UNION ALL is faster than UNION (no duplicate check).

### INTERSECT -

Returns only rows that appear in BOTH queries.

Syntax:

```sql
SELECT col1, col2 FROM table1
INTERSECT
SELECT col1, col2 FROM table2;
```

Example:

```sql
SELECT deptno FROM emp
INTERSECT
SELECT deptno FROM dept;
```

Returns department numbers present in both tables.

Practical Use: Find common values between two datasets.

### MINUS

Returns rows from first query that do NOT appear in second query. Removes rows from first row

Syntax:

```sql
SELECT col1, col2 FROM table1
MINUS
SELECT col1, col2 FROM table2;
```

Example:

```sql
SELECT eid FROM emp
MINUS
SELECT eid FROM emp WHERE deptno=10;
```

Returns employee IDs NOT in department 10.

Practical Use: Find differences between two datasets.

### ORDER BY with Set Operations

ORDER BY applies to the entire result.

Syntax (Oracle):

```sql
SELECT ename FROM emp WHERE deptno=10
UNION
SELECT ename FROM emp WHERE deptno=20
ORDER BY ename;
```

Important: ORDER BY must be at the end of the entire statement.

Example: Three-way UNION

```sql
SELECT eid FROM emp WHERE deptno=10
UNION
SELECT eid FROM emp WHERE deptno=20
UNION
SELECT eid FROM emp WHERE deptno=30;
```
