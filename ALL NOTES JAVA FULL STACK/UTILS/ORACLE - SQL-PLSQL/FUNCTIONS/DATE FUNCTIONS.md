## DATE FUNCTIONS

ADD_MONTHS  
MONTHS_BETWEEN  
NEXT_DAY  
LAST_DAY

### ADD_MONTHS

Adds months to a date.

```sql
SELECT ADD_MONTHS(SYSDATE,4) FROM dual;
```

### MONTHS_BETWEEN

Returns the number of months between two dates.

```sql
SELECT MONTHS_BETWEEN(
    DATE '2026-04-01',
    DATE '2026-01-01'
)
FROM dual;
```

### NEXT_DAY

Returns the date of the next specified weekday.

```sql
SELECT NEXT_DAY(SYSDATE,'SUNDAY') FROM dual;
```

### LAST_DAY

Returns the last day of a month.

```sql
SELECT LAST_DAY(SYSDATE) FROM dual;
```
