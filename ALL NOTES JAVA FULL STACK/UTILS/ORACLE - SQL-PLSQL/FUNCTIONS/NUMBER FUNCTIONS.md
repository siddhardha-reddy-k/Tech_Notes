## NUMBER FUNCTIONS

### ABS

Returns absolute value.

```sql
SELECT ABS(-10)
FROM dual;
```

Result:

10

### POWER

Returns a number raised to a power.

```sql
SELECT POWER(5,3) FROM dual;
```

Result:

125

### SQRT

Returns square root.

```sql
SELECT SQRT(25) FROM dual;
```

Result:
5

### CEIL

Returns the smallest integer greater than or equal to the number.

```sql
SELECT CEIL(10.6) FROM dual; --10.1 10.2 SAME 11 result
```

Result:
11

### FLOOR

Returns the largest integer less than or equal to the number.

```sql
SELECT FLOOR(10.6) FROM dual;
```

Result:
10

### ROUND

Rounds a number.

```sql
SELECT ROUND(10.5) FROM dual;
```

Result:
11

### TRUNC

Truncates without rounding.

```sql
SELECT TRUNC(10.56) FROM dual;
```

Result:
10

### GREATEST

Returns the greatest value.

```sql
SELECT GREATEST(9,2,7,1) FROM dual;
```

Result:
9

### LEAST

Returns the smallest value.

```sql
SELECT LEAST(9,2,7,1) FROM dual;
```

Result:
1
