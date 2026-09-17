## SINGLE-ROW SUBQUERY

A subquery that returns **exactly one row** (one value). Used with single-row comparison operators: =, >, <, >=, <=, <>.

```sql
SELECT *
FROM emp
WHERE esal >
      (SELECT esal FROM emp WHERE ename = 'Meena');
```

### Multi-Column Single Row Example -

```sql
SELECT * FROM employees WHERE (manager_id, department_id) = (SELECT manager_id, department_id FROM employees WHERE employee_id = 100);
```

It will get the esal from table with meena ename, only one record.

**The critical gotcha — this is THE most common runtime error with subqueries:** if the inner query accidentally returns **more than one row**, Oracle throws: ORA-01427: single-row subquery returns more than one row

We must make sure the inner query returns only one record.
