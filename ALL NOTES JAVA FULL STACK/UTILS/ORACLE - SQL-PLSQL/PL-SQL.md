1. PL/SQL Basics

Topics: What is PL/SQL · Block Structure · SERVEROUTPUT · Hello World · Variables

1.1 What is PL/SQL

PL/SQL = Procedural Language extension to SQL. It adds programming capabilities to plain SQL — variables, conditions, loops, exception handling, cursors, procedures, functions, packages, triggers.

- Reduces repeated client/server round trips by grouping multiple operations into one server-side block.

1.2 Block Structure

DECLARE  
    -- Declaration section  
BEGIN  
    -- Executable section  
EXCEPTION  
    -- Exception section  
END;  
/

|   |   |   |
|---|---|---|
|Section|Required?|Purpose|
|DECLARE|Optional|Variables, cursors, exceptions|
|BEGIN|Mandatory|Executable statements|
|EXCEPTION|Optional|Error handling|

1.3 SERVEROUTPUT

To see DBMS_OUTPUT.PUT_LINE output:

SET SERVEROUTPUT ON;

1.4 Hello World

BEGIN  
    DBMS_OUTPUT.PUT_LINE('Hello World');  
END;  
/

/ submits the block for execution.

1.5 Variables

DECLARE  
    A NUMBER;  
    B NUMBER;  
    C NUMBER;  
BEGIN  
    A := 10;  
    B := 20;  
    C := A + B;  
    DBMS_OUTPUT.PUT_LINE(C);  
END;  
/

Declaration + initialization in one line:

DECLARE  
    A NUMBER := 10;  
    B NUMBER := 20;  
    C NUMBER := A + B;  
BEGIN  
    DBMS_OUTPUT.PUT_LINE('Sum = ' || C);  
END;  
/

- || is the string concatenation operator.

2. DML & Data Retrieval in PL/SQL

Topics: DML inside PL/SQL · SELECT INTO · %TYPE · %ROWTYPE

2.1 DML Inside PL/SQL

INSERT:

BEGIN  
    INSERT INTO student VALUES(105,'Alan','USA');  
    DBMS_OUTPUT.PUT_LINE('Record Inserted');  
END;  
/

UPDATE:

BEGIN  
    UPDATE student SET sname='Rani' WHERE sno=105;  
    DBMS_OUTPUT.PUT_LINE('Record Updated');  
END;  
/

DELETE:

BEGIN  
    DELETE FROM student WHERE sno=105;  
    DBMS_OUTPUT.PUT_LINE('Record Deleted');  
END;  
/

2.2 SELECT INTO

Pulls a query result into PL/SQL variable(s) — requires INTO.

DECLARE  
    L_ename emp.ename%TYPE;  
BEGIN  
    SELECT ename INTO L_ename FROM emp WHERE eid=201;  
    DBMS_OUTPUT.PUT_LINE(L_ename);  
END;  
/

Multiple columns:

DECLARE  
    L_ename emp.ename%TYPE;  
    L_esal  emp.esal%TYPE;  
BEGIN  
    SELECT ename, esal INTO L_ename, L_esal FROM emp WHERE eid=202;  
    DBMS_OUTPUT.PUT_LINE(L_ename || ' ' || L_esal);  
END;  
/

2.3 %TYPE

Lets a variable inherit a table column's datatype.

DECLARE  
    L_ename emp.ename%TYPE;  
    L_esal  emp.esal%TYPE;

Advantage: if the column's datatype changes in the DB, the variable follows automatically — no code change needed.

2.4 %ROWTYPE

Creates a record that can hold an entire row.

DECLARE  
    L_emp emp%ROWTYPE;  
BEGIN  
    SELECT * INTO L_emp FROM emp WHERE eid=204;  
    DBMS_OUTPUT.PUT_LINE(L_emp.eid || ' ' || L_emp.ename || ' ' || L_emp.esal);  
END;  
/

Access individual fields with dot notation: L_emp.eid, L_emp.ename, L_emp.esal.

3. Control Statements

Topics: IF / IF-ELSE / IF-ELSIF-ELSE · Simple Loop · While Loop · For Loop

3.1 IF THEN

DECLARE  
    A NUMBER := 100;  
BEGIN  
    IF A>50 THEN  
        DBMS_OUTPUT.PUT_LINE('A is greater');  
    END IF;  
END;  
/

3.2 IF THEN ELSE

IF A>50 THEN  
    DBMS_OUTPUT.PUT_LINE('A is greater');  
ELSE  
    DBMS_OUTPUT.PUT_LINE('A is smaller or equal');  
END IF;

3.3 IF ELSIF ELSE

For multiple conditions:

IF A=100 THEN  
    DBMS_OUTPUT.PUT_LINE('Option 100');  
ELSIF A=103 THEN  
    DBMS_OUTPUT.PUT_LINE('Option 103');  
ELSIF A=108 THEN  
    DBMS_OUTPUT.PUT_LINE('Option 108');  
ELSE  
    DBMS_OUTPUT.PUT_LINE('Invalid option');  
END IF;

3.4 Simple Loop

Runs until an explicit EXIT condition is hit.

DECLARE  
    A NUMBER := 1;  
BEGIN  
    LOOP  
        DBMS_OUTPUT.PUT_LINE(A);  
        EXIT WHEN A=10;  
        A := A+1;  
    END LOOP;  
END;  
/

3.5 While Loop

Condition checked before each iteration.

DECLARE  
    A NUMBER := 1;  
BEGIN  
    WHILE A<=10 LOOP  
        DBMS_OUTPUT.PUT_LINE(A);  
        A := A+1;  
    END LOOP;  
END;  
/

3.6 For Loop

Loop variable auto-managed — no manual increment.

BEGIN  
    FOR A IN 1..10 LOOP  
        DBMS_OUTPUT.PUT_LINE(A);  
    END LOOP;  
END;  
/

Reverse (descending):

FOR A IN REVERSE 10..1 LOOP  
    DBMS_OUTPUT.PUT_LINE(A);  
END LOOP;

4. Exception Handling

Topics: Exception categories · NO_DATA_FOUND · TOO_MANY_ROWS · ZERO_DIVIDE · VALUE_ERROR · DUP_VAL_ON_INDEX · OTHERS · User-defined exceptions

4.1 What is an Exception

An error condition raised during PL/SQL execution. Two categories:

1. Predefined exceptions (Oracle built-in)
2. User-defined exceptions (you declare and raise)

4.2 NO_DATA_FOUND

Raised when SELECT INTO returns zero rows.

DECLARE  
    L_ename emp.ename%TYPE;  
BEGIN  
    SELECT ename INTO L_ename FROM emp WHERE eid=999;  
    DBMS_OUTPUT.PUT_LINE(L_ename);  
EXCEPTION  
    WHEN NO_DATA_FOUND THEN  
        DBMS_OUTPUT.PUT_LINE('Employee not found');  
END;  
/

4.3 TOO_MANY_ROWS

Raised when a single-row SELECT INTO returns more than one row.

DECLARE  
    L_ename emp.ename%TYPE;  
BEGIN  
    SELECT ename INTO L_ename FROM emp WHERE deptno=10;  
EXCEPTION  
    WHEN TOO_MANY_ROWS THEN  
        DBMS_OUTPUT.PUT_LINE('More than one employee found');  
END;  
/

4.4 ZERO_DIVIDE

Raised on division by zero.

DECLARE  
    A NUMBER;  
BEGIN  
    A := 10/0;  
EXCEPTION  
    WHEN ZERO_DIVIDE THEN  
        DBMS_OUTPUT.PUT_LINE('Cannot divide by zero');  
END;  
/

4.5 VALUE_ERROR

Raised when a value can't fit into a variable, or a conversion/assignment fails.

DECLARE  
    A NUMBER(3);  
BEGIN  
    A := 12345;  
EXCEPTION  
    WHEN VALUE_ERROR THEN  
        DBMS_OUTPUT.PUT_LINE('Value error');  
END;  
/

4.6 DUP_VAL_ON_INDEX

Raised when an INSERT/UPDATE violates a unique or primary key constraint.

BEGIN  
    INSERT INTO emp VALUES(201,'Brook',67000,50,'CEO',100);  
EXCEPTION  
    WHEN DUP_VAL_ON_INDEX THEN  
        DBMS_OUTPUT.PUT_LINE('Duplicate value');  
END;  
/

4.7 OTHERS

Catch-all for exceptions not caught by earlier handlers. Should always be the last handler.

EXCEPTION  
    WHEN OTHERS THEN  
        DBMS_OUTPUT.PUT_LINE('Some error occurred');  
END;  
/

4.8 User-Defined Exception

Steps: Declare → Raise → Handle

DECLARE  
    MY_EX EXCEPTION;  
    A NUMBER := 100;  
BEGIN  
    IF A>50 THEN  
        RAISE MY_EX;  
    END IF;  
    DBMS_OUTPUT.PUT_LINE(A);  
EXCEPTION  
    WHEN MY_EX THEN  
        DBMS_OUTPUT.PUT_LINE('Value is too large');  
END;  
/

5. Cursors

Topics: Cursor concept · Implicit cursor & SQL% attributes · Explicit cursor (declare/open/fetch/close) · Implicit vs Explicit comparison

5.1 What is a Cursor

A mechanism PL/SQL uses to process the result set of a SQL statement. Two types: Implicit and Explicit.

5.2 Implicit Cursor

Managed automatically by Oracle. Attributes: SQL%ISOPEN, SQL%FOUND, SQL%NOTFOUND, SQL%ROWCOUNT.

SQL%ISOPEN — generally FALSE right after the statement completes (implicit cursors close automatically):

BEGIN  
    UPDATE student SET sname='Alan' WHERE sno=104;  
    IF SQL%ISOPEN THEN  
        DBMS_OUTPUT.PUT_LINE('Open');  
    ELSE  
        DBMS_OUTPUT.PUT_LINE('Closed');  
    END IF;  
END;  
/

SQL%FOUND — TRUE if the last statement affected/returned a row:

BEGIN  
    UPDATE student SET sname='Alan' WHERE sno=104;  
    IF SQL%FOUND THEN  
        DBMS_OUTPUT.PUT_LINE('Record Updated');  
    END IF;  
END;  
/

SQL%NOTFOUND — opposite of %FOUND:

BEGIN  
    UPDATE student SET sname='Alan' WHERE sno=999;  
    IF SQL%NOTFOUND THEN  
        DBMS_OUTPUT.PUT_LINE('Record Not Updated');  
    END IF;  
END;  
/

SQL%ROWCOUNT — number of rows affected by the last DML:

BEGIN  
    UPDATE student SET sname='Raja';  
    DBMS_OUTPUT.PUT_LINE(SQL%ROWCOUNT || ' rows updated');  
END;  
/

5.3 Explicit Cursor

Programmer explicitly controls it. Steps: Declare → Open → Fetch → Close.

Single column:

DECLARE  
    CURSOR c1 IS SELECT ename FROM emp;  
    L_ename emp.ename%TYPE;  
BEGIN  
    OPEN c1;  
    LOOP  
        FETCH c1 INTO L_ename;  
        EXIT WHEN c1%NOTFOUND;  
        DBMS_OUTPUT.PUT_LINE(L_ename);  
    END LOOP;  
    CLOSE c1;  
END;  
/

Multiple columns:

DECLARE  
    CURSOR c1 IS SELECT ename, esal FROM emp;  
    L_ename emp.ename%TYPE;  
    L_esal  emp.esal%TYPE;  
BEGIN  
    OPEN c1;  
    LOOP  
        FETCH c1 INTO L_ename, L_esal;  
        EXIT WHEN c1%NOTFOUND;  
        DBMS_OUTPUT.PUT_LINE(L_ename || ' ' || L_esal);  
    END LOOP;  
    CLOSE c1;  
END;  
/

With %ROWTYPE:

DECLARE  
    CURSOR c1 IS SELECT * FROM emp;  
    L_emp emp%ROWTYPE;  
BEGIN  
    OPEN c1;  
    LOOP  
        FETCH c1 INTO L_emp;  
        EXIT WHEN c1%NOTFOUND;  
        DBMS_OUTPUT.PUT_LINE(L_emp.eid || ' ' || L_emp.ename || ' ' || L_emp.esal);  
    END LOOP;  
    CLOSE c1;  
END;  
/

Explicit cursor attributes: c1%ISOPEN, c1%FOUND, c1%NOTFOUND, c1%ROWCOUNT.

5.4 Implicit vs Explicit Cursor

|   |   |
|---|---|
|Implicit|Explicit|
|Managed by Oracle|Managed by programmer|
|Automatically opened|Programmer opens|
|Automatically fetched|Programmer fetches|
|Automatically closed|Programmer closes|
|Uses SQL%FOUND etc.|Uses cursor_name%FOUND etc.|

  
 

6. Procedures

Topics: Definition & syntax · Parameter modes (IN/OUT/IN OUT) · Procedures on table data · List / view source / drop

6.1 Definition & Syntax

A named, reusable PL/SQL program unit stored in the database.

CREATE OR REPLACE PROCEDURE procedure_name  
IS  
BEGIN  
    statements;  
END;  
/

6.2 Hello World Procedure

CREATE OR REPLACE PROCEDURE p1  
IS  
BEGIN  
    DBMS_OUTPUT.PUT_LINE('Hello World');  
END;  
/

Execute: EXEC p1;

6.3 Parameter Modes

Three modes: IN, OUT, IN OUT.

IN — pass a value into the procedure (default mode):

CREATE OR REPLACE PROCEDURE sum_two_numbers(  
    A IN NUMBER,  
    B IN NUMBER  
)  
IS  
BEGIN  
    DBMS_OUTPUT.PUT_LINE(A+B);  
END;  
/  
-- Execute:  
EXEC sum_two_numbers(10,20);

OUT — return a value through a parameter:

CREATE OR REPLACE PROCEDURE sum_ret(  
    A IN NUMBER,  
    B IN NUMBER,  
    C OUT NUMBER  
)  
IS  
BEGIN  
    C := A+B;  
END;  
/  
-- Execute with bind variable:  
VARIABLE N NUMBER;  
EXEC sum_ret(20,30,:N);  
PRINT N;

IN OUT — accepts an input value, returns a modified value through the same parameter:

CREATE OR REPLACE PROCEDURE ret_square(  
    A IN OUT NUMBER  
)  
IS  
BEGIN  
    A := A*A;  
END;  
/  
-- Setup + execute:  
VARIABLE N NUMBER;  
BEGIN  
    :N := 5;  
END;  
/  
EXEC ret_square(:N);  
PRINT N;  
-- Result: 25

6.4 Procedures on Table Data

Insert:

CREATE OR REPLACE PROCEDURE insert_record(  
    L_sno   IN student.sno%TYPE,  
    L_sname IN student.sname%TYPE,  
    L_sadd  IN student.sadd%TYPE  
)  
IS  
BEGIN  
    INSERT INTO student VALUES(L_sno,L_sname,L_sadd);  
    DBMS_OUTPUT.PUT_LINE('Record Inserted');  
END;  
/  
-- Execute:  
EXEC insert_record(105,'Alan','USA');

Update:

CREATE OR REPLACE PROCEDURE update_record(  
    L_sno IN student.sno%TYPE  
)  
IS  
BEGIN  
    UPDATE student SET sname='Rani' WHERE sno=L_sno;  
    DBMS_OUTPUT.PUT_LINE('Record Updated');  
END;  
/

Delete:

CREATE OR REPLACE PROCEDURE delete_record(  
    L_sno IN student.sno%TYPE  
)  
IS  
BEGIN  
    DELETE FROM student WHERE sno=L_sno;  
    DBMS_OUTPUT.PUT_LINE('Record Deleted');  
END;  
/

6.5 List / View Source / Drop

-- List all procedures  
SELECT object_name FROM user_objects WHERE object_type='PROCEDURE';

-- View source code  
SELECT text FROM user_source WHERE name='INSERT_RECORD';

-- Drop  
DROP PROCEDURE insert_record;

7. Functions

Topics: Definition & syntax · Examples · List / view source / drop · Procedure vs Function

7.1 Definition & Syntax

A named PL/SQL unit that must return a value.

CREATE OR REPLACE FUNCTION function_name  
RETURN datatype  
IS  
BEGIN  
    ...  
    RETURN value;  
END;  
/

7.2 Examples

Add two numbers:

CREATE OR REPLACE FUNCTION ret_sum(  
    A NUMBER,  
    B NUMBER  
)  
RETURN NUMBER  
IS  
BEGIN  
    RETURN A+B;  
END;  
/  
-- Execute:  
SELECT ret_sum(10,20) FROM dual;   -- Result: 30

Tax calculation:

CREATE OR REPLACE FUNCTION ret_tax(  
    salary NUMBER  
)  
RETURN NUMBER  
IS  
BEGIN  
    RETURN salary*10/100;  
END;  
/  
-- Execute:  
SELECT ret_tax(10000) FROM dual;

-- Use with a table:  
SELECT eid, ename, esal, ret_tax(esal) AS tax  
FROM emp;

7.3 List / View Source / Drop

SELECT object_name FROM user_objects WHERE object_type='FUNCTION';  
SELECT text FROM user_source WHERE name='RET_SUM';  
DROP FUNCTION ret_sum;

7.4 Procedure vs Function

|   |   |
|---|---|
|Procedure|Function|
|May return values through OUT/IN OUT parameters|Must return a value|
|Called as a standalone statement (EXEC proc(...))|Can be called as an expression (SELECT func(...) FROM dual)|
|Does not require a RETURN clause|Requires RETURN datatype and a returned value|
|Commonly used to perform DML|Can contain DML, but SQL-context calls face restrictions|

Note: the common simplification "DML allowed in procedures but not functions" isn't fully accurate — a function can contain DML, but there are restrictions when it's invoked from within a SQL statement.

8. Packages

Topics: Concept · Specification vs Body · Execution · Package with function · List / view source / drop

8.1 What is a Package

A collection of related PL/SQL program units — procedures, functions, variables, constants, cursors, types, exceptions — bundled together. Has two parts: Specification and Body.

8.2 Package Specification

Public declarations only (the interface):

CREATE OR REPLACE PACKAGE pkg1  
IS  
    PROCEDURE sum_num(  
        A IN NUMBER,  
        B IN NUMBER  
    );  
END pkg1;  
/

8.3 Package Body

The implementation:

CREATE OR REPLACE PACKAGE BODY pkg1  
IS  
    PROCEDURE sum_num(  
        A IN NUMBER,  
        B IN NUMBER  
    )  
    IS  
    BEGIN  
        DBMS_OUTPUT.PUT_LINE(A+B);  
    END;  
END pkg1;  
/

8.4 Execute a Package Procedure

EXEC pkg1.sum_num(10,20);

8.5 Package with Function

Specification:

CREATE OR REPLACE PACKAGE pkg2  
IS  
    FUNCTION ret_sum(  
        A NUMBER,  
        B NUMBER  
    ) RETURN NUMBER;  
END pkg2;  
/

Body:

CREATE OR REPLACE PACKAGE BODY pkg2  
IS  
    FUNCTION ret_sum(  
        A NUMBER,  
        B NUMBER  
    ) RETURN NUMBER  
    IS  
    BEGIN  
        RETURN A+B;  
    END;  
END pkg2;  
/

Call: SELECT pkg2.ret_sum(20,30) FROM dual;

8.6 List / View Source / Drop

SELECT object_name FROM user_objects WHERE object_type='PACKAGE';  
SELECT text FROM user_source WHERE name='PKG1';  
DROP PACKAGE pkg1;  
DROP PACKAGE BODY pkg1;

9. Triggers

Topics: Concept & timings · Basic trigger · Multi-event trigger & predicates · Statement-level vs Row-level · List / view source / drop

9.1 What is a Trigger

A stored PL/SQL unit that executes automatically when a specified database event occurs.

- Events: INSERT, UPDATE, DELETE
- Timings: BEFORE, AFTER (and INSTEAD OF — commonly used with views)

9.2 Basic Trigger

CREATE OR REPLACE TRIGGER trg1  
BEFORE INSERT ON student  
BEGIN  
    DBMS_OUTPUT.PUT_LINE('Thanks for inserting');  
END;  
/  
-- Fires automatically on:  
INSERT INTO student VALUES(105,'Alan','USA');

9.3 Multi-Event Trigger & Predicates

A trigger can respond to multiple DML events; use INSERTING / UPDATING / DELETING to tell them apart.

CREATE OR REPLACE TRIGGER trg2  
AFTER INSERT OR UPDATE OR DELETE ON student  
BEGIN  
    IF INSERTING THEN  
        DBMS_OUTPUT.PUT_LINE('Insert operation');  
    ELSIF UPDATING THEN  
        DBMS_OUTPUT.PUT_LINE('Update operation');  
    ELSE  
        DBMS_OUTPUT.PUT_LINE('Delete operation');  
    END IF;  
END;  
/

9.4 Statement-Level vs Row-Level

Statement-level (default — no FOR EACH ROW): fires once per SQL statement, regardless of rows affected.

CREATE OR REPLACE TRIGGER trg3  
BEFORE UPDATE ON student  
BEGIN  
    DBMS_OUTPUT.PUT_LINE('Update performed');  
END;  
/  
-- Even if this updates 5 rows, trg3 fires ONCE:  
UPDATE student SET sname='Raja';

Row-level (FOR EACH ROW): fires once per affected row.

CREATE OR REPLACE TRIGGER trg4  
BEFORE DELETE ON student  
FOR EACH ROW  
BEGIN  
    DBMS_OUTPUT.PUT_LINE('Row deleted');  
END;  
/  
-- Deleting 5 rows fires trg4 5 times.

9.5 List / View Source / Drop

SELECT object_name FROM user_objects WHERE object_type='TRIGGER';  
SELECT text FROM user_source WHERE name='TRG3';  
DROP TRIGGER trg1;

10. Bulk Operations

Topics: INSERT ALL

10.1 INSERT ALL

Insert multiple records into one (or more) tables in a single statement:

INSERT ALL  
    INTO student(sno,sname,sadd) VALUES(101,'Raja','HYD')  
    INTO student(sno,sname,sadd) VALUES(102,'Ravi','DELHI')  
    INTO student(sno,sname,sadd) VALUES(103,'Ramana','VIZAG')  
    INTO student(sno,sname,sadd) VALUES(104,'Ramulu','PUNE')  
SELECT * FROM dual;

11. SQL*Plus Environment Commands

Topics: Clear screen · Connect · Disconnect

CL SCR                     -- Clear screen  
CONN username/password     -- Connect, e.g. CONN system/admin  
DISC                        -- Disconnect (or: DISCONNECT)

12. Database Object Metadata Queries

Topics: Tables · Database name · Views · Synonyms · Indexes · Sequences (Metadata queries for procedures/functions/packages/triggers live in their own sections above — 6.5, 7.3, 8.6, 9.5 — to avoid duplication.)

-- List all tables  
SELECT * FROM tab;

-- Current database name  
SELECT * FROM global_name;

-- List views  
SELECT view_name FROM user_views;

-- List synonyms  
SELECT synonym_name FROM user_synonyms;

-- List indexes  
SELECT index_name FROM user_indexes;

-- List sequences  
SELECT sequence_name FROM user_sequences;

13. SELECT & Filtering (Core SQL)

Topics: Basic SELECT · WHERE filters · LIKE patterns · Wildcards · AND vs OR · IN vs OR

13.1 Basic SELECT

SELECT * FROM emp;

SELECT eid, ename, esal FROM emp;

-- Computed column  
SELECT eid, ename, esal, esal*12 AS annual_sal FROM emp;

13.2 WHERE Filters

-- Specific department  
SELECT * FROM emp WHERE deptno=10;

-- Specific job  
SELECT * FROM emp WHERE job='Manager';

-- Salary threshold  
SELECT * FROM emp WHERE esal>35000;

-- NULL check  
SELECT * FROM emp WHERE comm IS NULL;

-- Range  
SELECT * FROM emp WHERE esal BETWEEN 35000 AND 60000;

-- Multiple departments — three equivalent approaches  
SELECT * FROM emp WHERE deptno=10 OR deptno=20 OR deptno=30;  
SELECT * FROM emp WHERE deptno IN(10,20,30);  
SELECT * FROM emp WHERE deptno BETWEEN 10 AND 30;  

BETWEEN only works here because 10/20/30 happen to form a continuous range. IN is the safer, more explicit choice when you mean specifically those values.

-- NOT IN department 10  
SELECT * FROM emp WHERE deptno<>10;  
-- or:  
SELECT * FROM emp WHERE NOT deptno=10;

13.3 LIKE Patterns

-- Starts with A  
SELECT * FROM emp WHERE ename LIKE 'A%';

-- Ends with n  
SELECT * FROM emp WHERE ename LIKE '%n';

-- Second character is L  
SELECT * FROM emp WHERE ename LIKE '_l%';

13.4 % vs _ Wildcards

|   |   |
|---|---|
|%|_|
|Zero or more characters|Exactly one character|
|A% → starts with A, any length after|A_ → A followed by exactly one character|

Examples: LIKE 'A%' (starts with A) · LIKE '_A%' (second character is A).

13.5 AND vs OR

-- AND: all conditions must be true  
WHERE deptno=10 AND job='Clerk'

-- OR: at least one condition must be true  
WHERE deptno=10 OR deptno=20

13.6 IN vs OR

These can express the same equality-list condition:

WHERE deptno IN(10,20,30)  
-- is equivalent to:  
WHERE deptno=10 OR deptno=20 OR deptno=30

IN is generally cleaner and more readable.

14. UPDATE & DELETE (Core SQL)

Topics: Increment/change values · Delete by condition · DELETE vs TRUNCATE vs DROP

14.1 UPDATE Examples

-- Increment salary  
UPDATE emp SET esal=esal+1000 WHERE eid=204;

-- Change job  
UPDATE emp SET job='Salesman' WHERE eid=202;

14.2 DELETE Examples

-- Delete specific employee  
DELETE FROM emp WHERE eid=203;

-- Delete employees with NULL commission  
DELETE FROM emp WHERE comm IS NULL;

14.3 DELETE vs TRUNCATE vs DROP

|   |   |   |   |
|---|---|---|---|
|Feature|DELETE|TRUNCATE|DROP|
|Category|DML|DDL|DDL|
|Removes rows|Yes|Yes|Yes|
|Removes table|No|No|Yes|
|WHERE allowed|Yes|No|No|
|Table structure remains|Yes|Yes|No|
|Rollback before commit|Yes|No (DDL auto-commits)|No|
|Can delete selected rows|Yes|No|No|

15. Aggregate Functions & Grouping

Topics: MAX/MIN/SUM/AVG/COUNT · 2nd highest salary · GROUP BY · HAVING · WHERE vs HAVING

15.1 Basic Aggregates

SELECT MAX(esal) FROM emp;   -- Highest salary  
SELECT MIN(esal) FROM emp;   -- Lowest salary  
SELECT SUM(esal) FROM emp;   -- Total salary  
SELECT AVG(esal) FROM emp;   -- Average salary  
SELECT COUNT(*) FROM emp;    -- Employee count

15.2 Second Highest Salary

SELECT MAX(esal) FROM emp  
WHERE esal < (SELECT MAX(esal) FROM emp);

15.3 GROUP BY

-- Department-wise total  
SELECT deptno, SUM(esal) FROM emp GROUP BY deptno;

-- Department-wise average  
SELECT deptno, AVG(esal) FROM emp GROUP BY deptno;

-- Department-wise maximum  
SELECT deptno, MAX(esal) FROM emp GROUP BY deptno;

15.4 HAVING

Filters groups (after aggregation), unlike WHERE which filters rows before grouping.

SELECT deptno, SUM(esal)  
FROM emp  
GROUP BY deptno  
HAVING SUM(esal)>40000;

15.5 WHERE vs HAVING

|   |   |
|---|---|
|WHERE|HAVING|
|Filters rows|Filters groups|
|Applied before GROUP BY|Applied after GROUP BY|
|Row-level conditions|Typically aggregate conditions|

Combined example:

SELECT deptno, SUM(esal)  
FROM emp  
WHERE esal>10000  
GROUP BY deptno  
HAVING SUM(esal)>40000;

16. Joins

Topics: Basic JOIN

16.1 Employee + Department Name

SELECT e.eid, e.ename, d.dname  
FROM emp e  
JOIN dept d ON e.deptno=d.deptno;

17. Row Limiting

Topics: First N / Last N rows · ROWID vs ROWNUM

17.1 First 3 Records

SELECT * FROM emp FETCH FIRST 3 ROWS ONLY;

-- Older/common Oracle approach:  
SELECT * FROM emp WHERE ROWNUM<=3;

17.2 Last 3 Records

SELECT * FROM emp  
ORDER BY eid DESC  
FETCH FIRST 3 ROWS ONLY;

17.3 ROWID vs ROWNUM

|   |   |
|---|---|
|ROWID|ROWNUM|
|Identifies physical row location|Pseudocolumn numbering result rows|
|Tied to physical storage|Tied to result-set processing order|
|Used to uniquely identify a row|Useful for limiting number of rows returned|
|Not sequential|Starts at 1 for each query's result set|

18. Keys & Constraints

Topics: PRIMARY KEY vs UNIQUE · PRIMARY KEY vs FOREIGN KEY

18.1 PRIMARY KEY vs UNIQUE

|   |   |
|---|---|
|Primary Key|UNIQUE|
|Identifies the row|Enforces uniqueness on a column|
|Cannot be NULL|NULLs are allowed (in Oracle)|
|Only one PK constraint per table|Multiple UNIQUE constraints allowed|
|Effectively UNIQUE + NOT NULL|UNIQUE only|

18.2 PRIMARY KEY vs FOREIGN KEY

|   |   |
|---|---|
|Primary Key|Foreign Key|
|Identifies a row in its own table|References a key in another table|
|Must be unique|Duplicates allowed|
|Cannot be NULL|NULL allowed unless separately restricted|
|The "parent" key|The "child" key|

19. Views

Topics: Simple View vs Materialized View

|   |   |
|---|---|
|View|Materialized View|
|Stores the query definition only|Stores the actual query result|
|Data pulled from base table at query time|Result can be physically stored on disk|
|Always reflects current base data|May need periodic refresh|
|Lightweight, virtual|Better for performance/reporting on large/expensive queries|

20. Indexes

Topics: Simple Index vs Composite Index

|                                        |                                       |
| -------------------------------------- | ------------------------------------- |
| Simple Index                           | Composite Index                       |
| Built on one column                    | Built on multiple columns             |
| INDEX(col1)                            | INDEX(col1, col2)                     |
| Good for single-column access patterns | Good for multi-column access patterns |