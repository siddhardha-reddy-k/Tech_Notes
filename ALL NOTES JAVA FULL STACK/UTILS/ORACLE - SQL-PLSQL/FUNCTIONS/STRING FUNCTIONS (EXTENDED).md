Additional string manipulation functions for advanced text operations.

## LENGTH

Returns the number of characters in a string.

Syntax: LENGTH(string)

Example:

```sql
SELECT ename, LENGTH(ename) AS name_length FROM emp;
```

Result:

Alan → 4  
Christopher → 11

With WHERE:

```sql
SELECT * FROM emp WHERE LENGTH(ename) > 5;
```

## SUBSTR

Extracts a substring from a string.

Syntax: SUBSTR(string, start_position, [length])

Note: Position starts at 1 (not 0).

Example:

```sql
SELECT SUBSTR('Oracle Training', 1, 6) FROM dual;
```

Result: Oracle

Start position only:

```sql
SELECT SUBSTR('Oracle Training', 8) FROM dual;
```

Result: Training (from position 8 to end)

Negative position (from end):

```sql
SELECT SUBSTR('Oracle Training', -8) FROM dual;
```

Result: Training (8 characters from the end)

## INSTR

Returns the position of a substring within a string.

Syntax: INSTR(string, substring, [start_position], [occurrence])

Example:

```sql
SELECT INSTR('Hello World', 'o') FROM dual;
```

Result: 5 (first 'o' at position 5)

Start position:

```sql
SELECT INSTR('Hello World', 'o', 1) FROM dual;
```

Result: 5

Occurrence (find nth occurrence):

```sql
SELECT INSTR('Hello World', 'o', 1, 2) FROM dual;
```

Result: 8 (second 'o')

If not found:

```sql
SELECT INSTR('Hello World', 'x') FROM dual;
```

Result: 0

## CONCAT

Concatenates two strings.

Syntax: CONCAT(string1, string2)

Example:

```sql
SELECT CONCAT('Hello', ' World') FROM dual;
```

Result: Hello World

With columns:

```sql
SELECT CONCAT(ename, ' works in department ') FROM emp;
```

Alternative: || operator (more flexible)

```sql
SELECT ename || ' works in department ' FROM emp;
```

Multiple concatenations:

```sql
SELECT ename || ' - ' || job || ' - Salary: ' || esal FROM emp;
```

## REGEXP_LIKE

Searches for a pattern match using regular expressions.

Syntax: REGEXP_LIKE(string, pattern, [flags])

Example - Starts with 'A':

```sql
SELECT * FROM emp WHERE REGEXP_LIKE(ename, '^A');
```

Result: Alan, Andrew, Alice

Ends with 'n':

```sql
SELECT * FROM emp WHERE REGEXP_LIKE(ename, 'n$');
```

Result: Alan, Arun, Aiman

Contains digit:

```sql
SELECT * FROM emp WHERE REGEXP_LIKE(ename, '[0-9]');
```

Result: Emp123, John5

Case insensitive (flag 'i'):

```sql
SELECT * FROM emp WHERE REGEXP_LIKE(ename, '^A', 'i');
```

Result: Alan, andrew, Alice (ignores case)

## REGEXP_REPLACE

Replaces occurrences of a pattern with a replacement string.

Syntax: REGEXP_REPLACE(string, pattern, replacement, [flags])

Example - Replace all vowels:

```sql
SELECT REGEXP_REPLACE('Oracle Training', '[aeiou]', '*') FROM dual;
```

Result: *r*cl* Tr**n*ng

Replace all digits:

```sql
SELECT REGEXP_REPLACE('Emp123', '[0-9]', 'X') FROM dual;
```

Result: EmpXXX

Case insensitive replacement:

```sql
SELECT REGEXP_REPLACE('Hello HELLO hello', 'hello', 'Hi', 'i') FROM dual;
```

Result: Hi Hi Hi

## REGEXP_SUBSTR

Extracts substring using regular expressions.

(Already covered in your notes, but extending here)

Extract email domain:

```sql
SELECT REGEXP_SUBSTR('user@example.com', '[^@]+$') FROM dual;
```

Result: example.com

Extract numbers:

```sql
SELECT REGEXP_SUBSTR('ABC123DEF456', '[0-9]+', 1, 1) FROM dual;
```

Result: 123

## String Functions Comparison Table

| Function | Purpose | Example | Result |
|---|---|---|---|
| LENGTH | Get string length | LENGTH('Oracle') | 6 |
| SUBSTR | Extract part | SUBSTR('Oracle', 1, 3) | Ora |
| INSTR | Find position | INSTR('Oracle', 'a') | 3 |
| CONCAT | Join strings | CONCAT('Hello', ' World') | Hello World |
| REGEXP_LIKE | Pattern match | REGEXP_LIKE(name, '^A') | TRUE/FALSE |
| REGEXP_REPLACE| Replace pattern | REGEXP_REPLACE('A1B2', '[0-9]', 'X') | AXBX |

## Common Regular Expression Patterns

| Pattern | Meaning |
|---|---|
| ^ | Start of string |
| $ | End of string |
| [abc] | Any of a, b, or c |
| [0-9] | Any digit |
| [a-z] | Any lowercase letter |
| [A-Z] | Any uppercase letter |
| . | Any single character |
| * | Zero or more occurrences |
| + | One or more occurrences |
| {n} | Exactly n occurrences |
| | | OR operator |

Example: Validate Phone Number Format

```sql
SELECT * FROM emp WHERE REGEXP_LIKE(phone, '^[0-9]{10}$');
```

Matches exactly 10 digits.
