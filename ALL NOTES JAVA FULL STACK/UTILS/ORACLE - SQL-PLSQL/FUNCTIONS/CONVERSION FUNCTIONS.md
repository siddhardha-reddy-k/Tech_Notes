## CONVERSION FUNCTIONS

Conversion functions convert one datatype/value representation into another.

Important functions:

TO_CHAR  
TO_DATE  
TO_NUMBER

### TO_CHAR — Number

Converts a number to character representation.

```sql
SELECT TO_CHAR(esal,'99,999') FROM emp;
```

Currency formatting:

```sql
SELECT TO_CHAR(esal,'$99,999') FROM emp;
```

### TO_CHAR — Date

```sql
SELECT TO_CHAR(SYSDATE,'DD-MM-YYYY') FROM dual;
```

Other formats:

```sql
SELECT TO_CHAR(SYSDATE,'YYYY-MM-DD') FROM dual;
SELECT TO_CHAR(SYSDATE,'DD-MM-YYYY HH24:MI:SS') FROM dual;
SELECT TO_CHAR(SYSDATE,'YYYY') FROM dual;
SELECT TO_CHAR(SYSDATE,'MONTH') FROM dual;
SELECT TO_CHAR(SYSDATE,'DAY') FROM dual;
```

**Important**

For hours:

HH   → 12-hour clock  
HH24 → 24-hour clock  

For minutes:

MI

## TYPE CONVERSION FUNCTIONS (EXTENDED)

Conversion functions convert one datatype/value representation into another.

### TO_DATE

Converts a string to a DATE datatype.

Syntax: TO_DATE(string, format_mask)

Example:

```sql
SELECT TO_DATE('2026-01-15', 'YYYY-MM-DD') FROM dual;
```

Returns: 15-JAN-26

Other formats:

```sql
SELECT TO_DATE('15/01/2026', 'DD/MM/YYYY') FROM dual;
SELECT TO_DATE('January 15, 2026', 'MONTH DD, YYYY') FROM dual;
```

**With WHERE clause:**

```sql
SELECT * FROM emp WHERE hire_date > TO_DATE('2020-01-01', 'YYYY-MM-DD');
```

Common format masks:

YYYY  → 4-digit year  
YY    → 2-digit year  
MM    → Month (01-12)  
DD    → Day (01-31)  
HH24  → Hour (00-23)  
MI    → Minutes (00-59)  
SS    → Seconds (00-59)

### TO_NUMBER

Converts a string to a NUMBER datatype.

Syntax: TO_NUMBER(string, format_mask)

Example:

```sql
SELECT TO_NUMBER('12345') FROM dual;
```

Returns: 12345 (as number)

With format mask:

```sql
SELECT TO_NUMBER('1,234.56', '9,999.99') FROM dual;
```

Returns: 1234.56

Currency format:

```sql
SELECT TO_NUMBER('$1,000', '$9,999') FROM dual;
```

Important: String must represent a valid number.

Invalid: TO_NUMBER('ABC') will cause error.

### CAST

Generic type conversion function (ANSI SQL standard).

Works across different databases.

Syntax: CAST(expression AS target_datatype)

Examples:

```sql
SELECT CAST('12345' AS NUMBER) FROM dual;
SELECT CAST(12345 AS VARCHAR2(10)) FROM dual;
SELECT CAST('2026-01-15' AS DATE) FROM dual;
SELECT CAST(123.456 AS INTEGER) FROM dual;
```

Common datatypes:

VARCHAR2, CHAR, NUMBER, INTEGER, DATE, FLOAT

CAST is often preferred over TO_* functions for portability.

### Conversion Implicit vs Explicit

Implicit: Oracle automatically converts (may cause errors or unexpected results).

Example:

```sql
SELECT * FROM emp WHERE eid = '101';
```

Oracle converts '101' to 101, but risky.

Explicit: You specify the conversion (safer, clearer).

Example:

```sql
SELECT * FROM emp WHERE eid = TO_NUMBER('101');
```

Always use explicit conversion in production code.

### Common Conversion Scenarios

String to Date: TO_DATE() or CAST()  
String to Number: TO_NUMBER() or CAST()  
Date to String: TO_CHAR()  
Number to String: TO_CHAR()

### Order of Conversion Priority

TO_CHAR for dates/numbers (format control)  
TO_DATE for strings to dates  
TO_NUMBER for strings to numbers  
CAST for generic conversions (portability)

Example: Complete Conversion Workflow

```sql
INSERT INTO emp(eid, ename, esal, hire_date)
VALUES(
  TO_NUMBER('1001'),
  'Rajesh',
  TO_NUMBER('50000.50'),
  TO_DATE('2026-01-15', 'YYYY-MM-DD')
);
```
