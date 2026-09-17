## SELECT - retrieves data from ta table.

```sql
SELECT * FROM tablename; -- all columns.
```

## PROJECTION - selecting specific columns.

```sql
SELECT roll,name,address FROM student;
```

## WHERE filter rows according to condition.

```sql
SELECT * FROM tablename WHERE condition;

SELECT * FROM student WHERE sno=101;
SELECT * FROM student WHERE sname='Ravi';
SELECT * FROM emp WHERE esal>35000;
```
