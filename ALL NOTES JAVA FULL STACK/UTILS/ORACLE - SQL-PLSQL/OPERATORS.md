## OPERATORS

Common comparison.

=
>
<
>=
<=
<> anyvalue other than 10
!=

Examples:

```sql
SELECT * FROM emp WHERE esal=25000;
SELECT * FROM emp WHERE esal>25000;
SELECT * FROM emp WHERE esal<25000;
SELECT * FROM emp WHERE esal>=25000;
SELECT * FROM emp WHERE esal<=25000;
```

Not equal:

```sql
SELECT * FROM emp WHERE deptno<>10; -- anyvalue tother than 10
```

## AND

Combines conditions(all conditions must be true.

```sql
SELECT * FROM emp WHERE eid=201 AND ename='Alan';
```

Another:

```sql
SELECT * FROM emp WHERE esal=42000 AND deptno=30;
```

## OR

At least one condition must be TRUE.

```sql
SELECT * FROM emp WHERE eid=201 OR ename='Alan';
```

Multiple:

```sql
SELECT * FROM emp WHERE deptno=10 OR deptno=20 OR deptno=30;
```

## NOT

Reverses a condition.

```sql
SELECT * FROM emp WHERE NOT deptno=10;
```

Alternative:

```sql
SELECT * FROM emp WHERE deptno<>10;
```

## BETWEEN

Used to select values within a range.

```sql
SELECT * FROM emp WHERE esal BETWEEN 10000 AND 30000;
```

Equivalent conceptually to:

```sql
SELECT * FROM emp WHERE esal>=10000 AND esal<=30000;
```

**Important**

BETWEEN is inclusive: lower value included, upper value included

It can be used with numeric, date and character expressions where appropriate—not only numbers.

## IN

Used to compare a value against a list.

```sql
SELECT * FROM emp WHERE deptno IN(10,20,30);
```

Equivalent:

```sql
SELECT * FROM emp WHERE deptno=10 OR deptno=20 OR deptno=30;
```

Character values:

```sql
SELECT * FROM emp WHERE job IN('Clerk','HR','Manager');
```

## IS NULL

NULL cannot be compared using =.

Wrong:

```sql
WHERE comm=NULL
```

Correct:

```sql
SELECT * FROM emp WHERE comm IS NULL;
```

## IS NOT NULL

```sql
SELECT * FROM emp WHERE comm IS NOT NULL;
```

## LIKE

LIKE is used for pattern matching.

There are two important wildcards:

%  → zero or more characters
_  → exactly one character

### Starts With

```sql
SELECT * FROM emp WHERE ename LIKE 'A%';
```

Meaning:

A
Alan
Alice
Andrew
...

### Ends With

```sql
SELECT * FROM emp WHERE ename LIKE '%n';
```

### Contains

```sql
SELECT * FROM emp WHERE ename LIKE '%l% ';
```

### Second Character

```sql
SELECT * FROM emp WHERE ename LIKE '_l%';
```

Meaning:

first character = anything
second character = l
remaining characters = anything

### Third Character

```sql
SELECT * FROM emp WHERE ename LIKE '__r%';
```

### Second Last Character

```sql
SELECT *FROM emp WHERE ename LIKE '%i_';
```
