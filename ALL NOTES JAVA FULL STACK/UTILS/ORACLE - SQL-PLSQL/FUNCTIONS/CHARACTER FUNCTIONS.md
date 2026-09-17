## CHARACTER FUNCTIONS

### UPPER

Converts text to uppercase.

```sql
SELECT UPPER('oracle training') FROM dual;
```

### LOWER

Converts text to lowercase.

```sql
SELECT LOWER('ORACLE TRAINING') FROM dual;
```

### INITCAP

Capitalizes the first letter of words.

```sql
SELECT INITCAP('oracle training') FROM dual;
```

Result:

Oracle Training

### LPAD

Pads characters on the left.

```sql
SELECT LPAD('oracle',10,'z') FROM dual; --zzzzoracle
```

### RPAD

Pads characters on the right.

```sql
SELECT RPAD('oracle',10,'z') FROM dual; -oraclezzzz
```

### LTRIM

Removes specified characters from the left.

```sql
SELECT LTRIM('zzoraclezz','z') FROM dual;
```

### RTRIM

Removes specified characters from the right.

```sql
SELECT RTRIM('zzoraclezz','z') FROM dual;
```

### TRIM

Removes characters from both ends.

```sql
SELECT TRIM('z' FROM 'zzoraclezz') FROM dual;
```

### REPLACE

Replaces occurrences of a substring.

```sql
SELECT REPLACE('AlAn','A','a') FROM dual;
```

### REGEXP_SUBSTR

Useful for extracting portions of text using regular expressions.

Example:

```sql
SELECT REGEXP_SUBSTR(name,'\S+',1,1) FROM emp1;
```

First word:

Alan Morries → Alan  
Erick Anderson → Erick  

Syntax decoded  - 

REGEXP_SUBSTR(name, '\S+', 1, 1):

1. **name — The column being searched.**
2. **'\S+' — The      pattern to match (looks for a continuous block of non-space characters,      i.e., a single word).**
3. **1      (Position) — Where to start searching (starts at the first      character).**
4. **1      (Occurrence) — Which match to extract (grabs the first word found).**

Second word:

```sql
SELECT REGEXP_SUBSTR(name,'\S+',1,2) FROM emp1;
```

Result:

Morries  
Anderson
