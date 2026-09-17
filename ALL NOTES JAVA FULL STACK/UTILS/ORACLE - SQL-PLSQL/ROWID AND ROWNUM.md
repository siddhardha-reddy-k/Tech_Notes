## ROWID

ROWID identifies the physical location of a row in an Oracle heap-organized table.

Example:

```sql
SELECT ROWID,eid,ename,esal FROM emp;
```

It can be useful for fast row identification.

## ROWNUM

ROWNUM is a pseudocolumn that assigns numbers to rows as they are returned by a query.

```sql
SELECT ROWNUM,eid,ename FROM emp;
```

Typical values:

1  
2  
3  
4  
...

## FIRST N ROWS

```sql
SELECT *
FROM emp
WHERE ROWNUM<=3;
```

Modern row limiting:

```sql
SELECT *
FROM emp
FETCH FIRST 3 ROWS ONLY;
```

## LAST N ROWS

One approach:

```sql
SELECT *
FROM (
    SELECT *
    FROM emp
    ORDER BY eid DESC
)
WHERE ROWNUM<=3;
```

Using row limiting:

```sql
SELECT *
FROM emp
ORDER BY eid DESC
FETCH FIRST 3 ROWS ONLY;
```

## FOURTH RECORD

Using OFFSET:

```sql
SELECT *
FROM emp
ORDER BY eid
OFFSET 3 ROWS
FETCH NEXT 1 ROW ONLY;
```

This means:

Skip first 3 rows  
Return next 1 row
