# Technical - All

## 0. Foundations (Data, DBMS, Oracle, Architecture)

**Q: What is Data?**

Raw facts, values, or observations that can be stored, processed and analyzed to obtain meaningful information.

**Q: Types of Data — 3 types:**

1. **Structured Data** — organized in fixed format, rows & columns. (ex: table with Id, Name, Address)
2. **Semi-Structured Data** — doesn't follow strict table structure but has organization via tags/keys/metadata. (ex: JSON, XML)
3. **Unstructured Data** — no predefined structure. (ex: files, images, videos, Gmail inbox, social media content)

**Q: DBMS vs RDBMS?**

| DBMS | RDBMS |
|---|---|
| Database Management System | Relational Database Management System |
| Stores data in files | Stores data in tables |
| Not designed for large data | Designed to handle large amounts of data |
| Connects only one user at a time | Connects multiple users at a time |
| Does not support normalization | Supports normalization |
| No security of data | High security of data |

**Q: What is RDBMS?**

A database management system that stores data in related tables and provides mechanism to process, manage, and modify the data. (ex: cust_id relates customer table to order table)

Examples: Oracle, MySQL, SQL Server, PostgreSQL.

**Q: What is Oracle?**

A relational database management system provided by Oracle Corporation. Used to store, manage, retrieve, or modify structured data.

Provides two languages:

1. SQL — Structured Query Language
2. PL/SQL — Procedural Language Extensions to SQL

**Q: Client/Server Architecture — 3 parts:**

- **Frontend** — visible to end-user to perform operations. (ex: Java, .NET, Python, Perl)
- **Communication Channel** — bridge between frontend and backend. (ex: JDBC – Java DB Connectivity, ODBC – Open DB Connectivity, PDBC – Python DB Connectivity)
- **Backend** — not visible to end-user, performs operations based on frontend instructions. (ex: Oracle, MySQL, PostgreSQL, Teradata, MariaDB)

**Q: What is SQL?**

SQL stands for Structured Query Language, pronounced "SEQUEL."

- Used to interact with the Oracle database.
- It is a command-based language.
- It is a case-insensitive language.
- Every command must start with a verb (create, insert, update, delete...).
- Every command must end with a semicolon.
- Developed by Mr. Codd in 1972 (by IBM).

**Q: What is a Table?**

An object used to store data in the form of rows and columns.

- Data present in a table is case-sensitive (e.g. `WHERE name='alan' ≠ WHERE name='Alan'`) — but the SQL command/keywords themselves are case-insensitive.

**Q: What is a Schema?**

A memory location which is used to run SQL commands.

---

## 1. Sub-languages of SQL

**5 sub-languages:**

| # | Language | Full Form | Commands | Count |
|---|---|---|---|---|
| 1 | DDL | Data Definition Language | maintains objects in database — create, alter, drop, truncate, rename | 5 |
| 2 | DML | Data Manipulation Language | manipulates data in database — insert, update, delete, merge | 4 |
| 3 | DRL/DQL | Data Retrieve/Query Language | retrieves data — select | 1 |
| 4 | TCL | Transaction Control Language | maintains transactions — commit, rollback, savepoint | 3 |
| 5 | DCL | Data Control Language | controls access to data — grant, revoke | 2 |

---

## 2. DDL Commands

1. create — tables
2. alter — columns
3. drop — tables
4. truncate — rows/records
5. rename — tables

- **CREATE TABLE** — creates tables in database.
- **DESC** — used to see the structure of a table.
- **DROP TABLE** — used to drop the table.
- **TRUNCATE TABLE** — used to delete the rows permanently from the table.
- **RENAME** — used to rename table name.

**Q: DELETE vs TRUNCATE?**

| DELETE | TRUNCATE |
|---|---|
| DML command | DDL command |
| Deletes data temporarily | Deletes data permanently |
| Can rollback the data | Can't rollback the data |
| WHERE clause can be used | WHERE clause can't be used |

**ALTER command — 4 activities:**

i) Adding new columns

```sql
ALTER TABLE ADD (col datatype(size));
```

ii) Modifying existing columns

```sql
ALTER TABLE MODIFY (col datatype(size));
```

- Can increase/decrease size only if existing values fit new size.
- Can change datatype only when column is empty.

iii) Dropping columns

```sql
ALTER TABLE DROP (col1,col2,...);
```

iv) Renaming columns

```sql
ALTER TABLE RENAME COLUMN old_name TO new_name;
```

---

## 3. DML Commands

### INSERT

Used to insert a row/record into a database table. 3 approaches:

1. All columns:

```sql
INSERT INTO student VALUES(101,'raja','hyd');
```

2. Selected columns:

```sql
INSERT INTO student(sno,sname) VALUES(104,'ramulu');
```

(unlisted columns get NULL)

3. Dynamic input using `&`:

```sql
INSERT INTO student VALUES(&sno,'&sname','&sadd');
```

**NULL** — represents undefined or unavailable data.

**INSERT ALL** — used to insert bulk records in one statement:

```sql
INSERT ALL
 INTO student (sno,sname,sadd) VALUES (106,'Alice','Texas')
 INTO student (sno,sname,sadd) VALUES (107,'Bob','Florida')
SELECT * FROM dual;
```

### UPDATE

Used to modify the rows present in a database table.

```sql
UPDATE table SET col=value WHERE condition;
```

Note: without WHERE, all rows get updated.

### DELETE

Used to delete rows from a database table.

```sql
DELETE FROM table WHERE condition;
```

Note: without WHERE, all rows get deleted.

### COMMIT

Used to make changes permanent to the database.

---

## 4. SELECT / DQL

**SELECT** — used to retrieve the rows/records from a database table. `*` = all rows and columns.

**Projection** — process of selecting specific columns from a database table.

**Arithmetic operations in SELECT:**

```sql
SELECT sno+100, sname FROM student;
```

**Column Alias** — a user-defined, temporary name given to a column. (AS or without AS)

**Interview queries:**

- List tables in database:

```sql
SELECT * FROM tab;
```

- Display logical database name:

```sql
SELECT * FROM global_name;
```

---

## 5. WHERE Clause

Used to select specific rows from a database table.

### Logical Operators — 3 types

1. **AND** — combines all conditions, returns rows only if all conditions are true. Conditions must be from the same row.
2. **OR** — combines conditions, returns rows if at least one condition is true. Conditions can be from any row match.
3. **NOT** — reverse of a condition; returns rows except the condition. `<>` is also a NOT operator.

### BETWEEN Operator

Returns records matching within a range of values. Declare lower limit first, then higher limit. Applicable mainly for numbers (also dates).

### IN Operator

Replacement for OR operator — returns records that are in the given list of values.

### Pattern Matching — 2 operators

1. `%` (Percentage) — matches zero or more characters.
2. `_` (Underscore) — matches exactly one character position.

| Requirement | Query |
|---|---|
| Starts with A | `LIKE 'A%'` |
| Ends with n | `LIKE '%n'` |
| Contains l | `LIKE '%l%'` |
| Second letter l | `LIKE '_l%'` |
| Third letter r | `LIKE '__r%'` |
| Second-last letter i | `LIKE '%i_'` |

---

## 6. Functions

**Definition:** Functions are used to manipulate the data items and give the result.

**2 types:**

1. **Group Functions / Multiple Row Functions** — applicable for multiple rows. (`sum(), avg(), max(), min(), count(), count(exp)`)
2. **Scalar Functions / Single Row Functions** — applicable for a single row.

### Group Functions

**Q: COUNT(*) vs COUNT(exp)?**

| COUNT(*) | COUNT(exp) |
|---|---|
| Returns number of records present in table | Returns number of values present in a column |
| Includes NULL records | Won't include NULL values |

### DUAL Table

A dummy table which contains one row and one column. Used to perform arithmetic operations and to see the current system date.

### Scalar Functions — 4 sub-categories

i) Character Functions  
ii) Number Functions  
iii) Date Functions  
iv) Conversion Functions

### i) Character Functions

| Function | Purpose |
|---|---|
| UPPER() | convert string to uppercase |
| LOWER() | convert string to lowercase |
| INITCAP() | display string with initial capital |
| LPAD() | pad characters towards left side |
| RPAD() | pad characters towards right side |
| LTRIM() | trim characters from left side |
| RTRIM() | trim characters towards right side |
| TRIM() | trim characters from both sides |
| REPLACE() | replace a character/substring |
| CONCAT() | concatenate two strings |
| REGEXP_SUBSTR() | extract part of string via regex pattern |

```sql
regexp_substr(name,'\S+',1,1)
```

→ first word; `,1,2` → second word.

### ii) Number Functions

| Function | Purpose |
|---|---|
| ABS() | convert number to positive |
| SQRT() | exact square root |
| POWER(A,B) | returns power value (A^B) |
| CEIL() | returns ceil value (round up) |
| FLOOR() | returns floor value (round down) |
| ROUND() | returns nearest value |
| TRUNC() | returns number without decimals (no rounding) |
| GREATEST() | returns greatest value |
| LEAST() | returns least value |

**Q: ceil(10.6) vs floor(10.6) vs round(10.5) vs trunc(10.56)?**

- ceil(10.6)=11
- floor(10.6)=10
- round(10.5)=11
- round(10.4)=10
- trunc(10.56)=10
- trunc(-187.38)=-187

### iii) Date Functions

| Function | Purpose |
|---|---|
| ADD_MONTHS() | adds months to a given date |
| MONTHS_BETWEEN() | returns number of months between two dates |
| NEXT_DAY() | returns next date of a given day within a week |
| LAST_DAY() | returns last date of a month |

Every database software supports a different date pattern — Oracle: dd-MMM-yy, MySQL: yyyy-MM-dd.

### iv) Conversion Function

Used to convert from one datatype to another.

Main function: **TO_CHAR()** — has two pseudo-forms:

1. Number TO_CHAR() — takes 9 digits, dollar/euro symbols.

```sql
TO_CHAR(esal,'$99,999')
```

2. Date TO_CHAR() — format masks: dd-MM-yyyy, HH:MI:SS, year, month, day, etc.

---

## 7. GROUP BY Clause

Used to divide the rows into groups so group functions can be applied.

- The column used in SELECT must also appear in GROUP BY.
- GROUP BY is declared after WHERE clause.

---

## 8. HAVING Clause

Used to filter the rows/groups from GROUP BY clause. Must be declared after GROUP BY clause.

---

## 9. ORDER BY Clause

Used to arrange the rows in a table. By default arranges in ascending order.

Clause order:

`FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY`

---

## 10. Integrity Constraints

**Definition:** Rules applied on tables to achieve accuracy and quality of data. 5 constraints, created at 2 levels — Column level and Table level.

### 1) NOT NULL

- Does not accept NULL values.
- Can accept duplicate values.
- Can be created only at column level.

### 2) UNIQUE

- Does not accept duplicate values.
- Can accept NULL values.
- Can be created at column level and table level.

### 3) PRIMARY KEY

- A combination of NOT NULL and UNIQUE.
- Does not accept duplicates or NULLs.
- A table can have only one primary key.
- Can be created at column level and table level.

### 4) FOREIGN KEY

Used to establish the relationship between two tables.

- Also known as parent-child or master-detail relationship.
- Parent table must have a primary key or unique key; child table must have the foreign key.
- Foreign key accepts only those values present in the primary key.
- Primary key and foreign key column names may or may not match, but datatype must match.
- Foreign key accepts duplicates and NULL values.
- To drop related tables: drop child table first, then parent table.

### 5) CHECK

**Definition:** Describes the domain of a column — i.e., what type of value a column must accept.

- Can be created at column level and table level.

**Q: Add/Drop a constraint on an existing table?**

```sql
ALTER TABLE emp ADD PRIMARY KEY(eid);
ALTER TABLE emp DROP PRIMARY KEY;
```

---

## 11. ROWID / ROWNUM

**Q: ROWID vs ROWNUM?**

| ROWID | ROWNUM |
|---|---|
| Permanent | Temporary |
| Memory location where records are stored in a table | Gives row numbers, starts at 1, increments by 1 |

**Q: First 3 records from emp?**

```sql
SELECT * FROM emp WHERE rownum<=3;
```

or (12c+)

```sql
SELECT * FROM emp ORDER BY eid FETCH FIRST 3 ROWS ONLY;
```

**Q: 4th record from emp?**

```sql
SELECT * FROM emp WHERE rownum<=4
MINUS
SELECT * FROM emp WHERE rownum<=3;
```

or

```sql
SELECT * FROM emp ORDER BY empno OFFSET 3 ROWS FETCH NEXT 1 ROW ONLY;
```

---

## 12. Sequence

**Definition:** An object used to generate numbers.

```sql
CREATE SEQUENCE seq_name START WITH value INCREMENT BY value;
```

**2 pseudocolumns:**

1. **NEXTVAL** — generates next number in the sequence.
2. **CURRVAL** — returns the last number generated by the sequence (session must have called NEXTVAL first).

- List sequences:

```sql
SELECT sequence_name FROM user_sequences;
```

- Drop sequence:

```sql
DROP SEQUENCE seq_name;
```

---

## 13. TCL Commands

1. **COMMIT** — makes the changes permanent to the database.
2. **ROLLBACK** — undoes the changes which are not permanent (not yet committed).
3. **SAVEPOINT** — maintains a logical marking in the database; instead of a complete rollback, we can rollback up to a savepoint.

---

## 14. DCL Commands

**Privileges** — permission given to a user. 2 types:

1. **System privilege** — permission given by the DBA to a user.
2. **Object privilege** — permission given by one developer to another developer.

- **GRANT** — used to grant permissions to a user.

```sql
GRANT privilege1, privilege2 TO user_name;
```

- **REVOKE** — used to revoke permissions from a user.

```sql
REVOKE privilege1, privilege2 FROM user_name;
```

Typical DCL flow: DBA creates users → grants connect, resource (login + basic object-creation rights) → owner grants select/update/delete on specific objects to other users → owner/DBA revokes as needed.

---

## 15. Synonyms

**Definition:** Alternate name given to a database table/object.

- Can be used in place of the object name for all commands.
- Main purpose: convenience, abstraction, and security.

```sql
CREATE SYNONYM sy1 FOR student;
```

- List synonyms:

```sql
SELECT synonym_name FROM user_synonyms;
```

- Drop synonym:

```sql
DROP SYNONYM sy1;
```

---

## 16. Indexes

**Definition:** Used to improve the performance of the SELECT command/statement. (Index in a book is similar to index in a table.)

- Create index only on columns widely used in the WHERE clause.
- When an index is created, two columns get built internally: ROWID and the indexed column — all rows in the indexed column are stored in ascending order.

**2 types:**

1. **Simple index** — index created for one column only.
2. **Complex index** — index created for multiple columns.

```sql
CREATE INDEX idx1 ON emp(eid); -- simple
CREATE INDEX idx2 ON emp(esal,job); -- complex
```

- List indexes:

```sql
SELECT index_name FROM user_indexes;
```

- Drop index:

```sql
DROP INDEX idx1;
```

---

## 17. Joins

| Join Type | Returns |
|---|---|
| Cartesian Product | every row × every row, no condition (accidental) |
| Equi Join (old syntax) | WHERE t1.col = t2.col |
| Inner Join (ANSI) | JOIN ... ON — only matching rows |
| Non-Equi Join | join using operator other than = (e.g. BETWEEN) |
| Self Join | table joined with itself, needs 2 aliases |
| Left Outer Join | all left rows + matches; unmatched right = NULL |
| Right Outer Join | all right rows + matches; unmatched left = NULL |
| Full Outer Join | all rows from both, unmatched = NULL on either side |
| Cross Join | intentional cartesian product |
| Natural Join | auto-joins on same-named column(s), no ON needed — risky |
| USING clause | explicit version of natural join, name the shared column |

**Mental model:**

| Join | What survives |
|---|---|
| INNER | only matches |
| LEFT OUTER | matches + left leftovers |
| RIGHT OUTER | matches + right leftovers |
| FULL OUTER | matches + both leftovers |

**Q: NATURAL JOIN risk?**

Joins on ALL same-named columns automatically — if two tables share an unexpected column (e.g. created_date), it silently joins on that too, causing wrong/missing results without error.

**Q: ON vs USING vs NATURAL?**

| Feature | ON | USING | NATURAL |
|---|---|---|---|
| Explicit column | Yes | Yes (named) | No (auto) |
| Different column names | Works | Doesn't | Doesn't |
| Output column | twice (t1.col, t2.col) | once | once |
| Risk | none | none | high |
| Production use | best | ok | avoid |

**Q: Self Join use case?**

Comparing rows within same table — e.g., employees in same department, manager-subordinate relationships.

---

## 18. Views

**Definition:** A view = stored query, not stored data. Re-runs live against base table every time.

- **Simple View** — one table, no joins/grouping. DML generally allowed, passes through to base table.
- **Complex View** — multiple tables/joins/aggregates. DML restricted/blocked if ambiguous.
- **WITH READ ONLY** — blocks all DML through the view, no exceptions.
- **WITH CHECK OPTION** — prevents inserting/updating rows through the view that would violate the view's own WHERE clause.
- **Materialized View** — physically stores query result (snapshot), unlike normal view. Doesn't auto-update; needs manual/scheduled refresh (`DBMS_MVIEW.REFRESH`). Used for expensive queries/reporting.

```sql
CREATE VIEW v1 AS SELECT * FROM emp;
CREATE MATERIALIZED VIEW v5 AS SELECT * FROM emp;
DROP VIEW v1;
DROP MATERIALIZED VIEW v5;
```

**Q: View vs Materialized View?**

| View | Materialized View |
|---|---|
| Storage: none, just query | stores actual data |
| Freshness: always live/current | stale until refreshed |
| Speed: slower (re-runs each time) | faster (reads snapshot) |
| Use case: simple abstraction | heavy queries/reporting |

---

## 19. MERGE (Upsert)

Combines UPDATE + INSERT in one statement — matched rows update, unmatched rows insert.

```sql
MERGE INTO emp e
USING emp_updates u
ON (e.eid = u.eid)
WHEN MATCHED THEN
   UPDATE SET e.esal = u.esal
WHEN NOT MATCHED THEN
   INSERT (eid, ename, esal, deptno)
   VALUES (u.eid, u.ename, u.esal, u.deptno);
```

- INTO table = target.
- USING table = source (feed/staging data).
- Common use: syncing data feeds, ETL, bulk sync operations.

---

## 20. Set Operations (bonus)

| Operation | Duplicates | Rows Returned |
|---|---|---|
| UNION | removed | combined unique rows from both |
| UNION ALL | kept | all rows, faster (no dedup) |
| INTERSECT | removed | common rows in both |
| MINUS | removed | rows in 1st query, not in 2nd |

**Rule:** same number of columns, compatible datatypes, across both queries.
