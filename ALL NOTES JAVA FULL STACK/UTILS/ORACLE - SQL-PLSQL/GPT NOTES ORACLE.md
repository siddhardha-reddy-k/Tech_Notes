PL/SQL

PL/SQL = Procedural Language extension to SQL

PL/SQL adds programming capabilities to SQL.

It supports:

Variables, Conditions, Loops, Exception handling, Cursors, Procedures, Functions, Packages, Triggers

It can reduce repeated client/server communication by grouping multiple operations into a server-side block.

PL/SQL BLOCK

Basic structure:

DECLARE  
    -- Declaration section  
BEGIN  
    -- Executable section  
EXCEPTION  
    -- Exception section  
END;  
/

SERVEROUTPUT

To display DBMS_OUTPUT.PUT_LINE output in SQL*Plus/SQLcl-style environments

SET SERVEROUTPUT ON;

HELLO WORLD

BEGIN  
    DBMS_OUTPUT.PUT_LINE('Hello World');  
END;  
/

/ submits the PL/SQL block in tools such as SQL*Plus.

VARIABLES

DECLARE  
    A NUMBER;  
    B NUMBER;  
    C NUMBER;  
BEGIN  
    A:=10;  
    B:=20;  
    C:=A+B;

DBMS_OUTPUT.PUT_LINE(C);  
END;  
/

DECLARATION + INITIALIZATION

DECLARE  
    A NUMBER := 10;  
    B NUMBER := 20;  
    C NUMBER := A+B;  
BEGIN  
    DBMS_OUTPUT.PUT_LINE(  
        'Sum = ' || C  
    );  
END;  
/

String concatenation

||

Example:

DBMS_OUTPUT.PUT_LINE(  
    'Salary = ' || A  
);

PL/SQL DML

DML can be executed inside PL/SQL.

INSERT

BEGIN  
    INSERT INTO student  
    VALUES(105,'Alan','USA');

DBMS_OUTPUT.PUT_LINE('Record Inserted');  
END;  
/

UPDATE

BEGIN  
    UPDATE student  
    SET sname='Rani'  
    WHERE sno=105;

DBMS_OUTPUT.PUT_LINE('Record Updated');  
END;  
/

DELETE

BEGIN  
    DELETE FROM student  
    WHERE sno=105;

DBMS_OUTPUT.PUT_LINE('Record Deleted');  
END;  
/

SELECT INTO

In PL/SQL, a normal SELECT that returns data into variables uses INTO.

DECLARE  
    L_ename emp.ename%TYPE;  
BEGIN  
    SELECT ename  
    INTO L_ename  
    FROM emp  
    WHERE eid=201;

DBMS_OUTPUT.PUT_LINE(L_ename);  
END;  
/

MULTIPLE COLUMNS WITH SELECT INTO

DECLARE  
    L_ename emp.ename%TYPE;  
    L_esal  emp.esal%TYPE;  
BEGIN  
    SELECT ename,esal  
    INTO L_ename,L_esal  
    FROM emp  
    WHERE eid=202;

DBMS_OUTPUT.PUT_LINE(  
        L_ename || ' ' || L_esal  
    );  
END;  
/

%TYPE

%TYPE allows a variable to inherit the datatype of a table column.

DECLARE  
    L_ename emp.ename%TYPE;  
    L_esal  emp.esal%TYPE;  
BEGIN  
    ...  
END;  
/

Advantage

If the database column datatype changes, the variable declaration automatically follows it.

%ROWTYPE

%ROWTYPE creates a record capable of holding an entire row.

DECLARE  
    L_emp emp%ROWTYPE;  
BEGIN  
    SELECT *  
    INTO L_emp  
    FROM emp  
    WHERE eid=204;

DBMS_OUTPUT.PUT_LINE(  
        L_emp.eid || ' ' ||  
        L_emp.ename || ' ' ||  
        L_emp.esal  
    );  
END;  
/

Individual fields:

L_emp.eid  
L_emp.ename  
L_emp.esal

CONTROL STATEMENTS

IF THEN

Executes code only when condition is TRUE.

DECLARE  
    A NUMBER:=100;  
BEGIN  
    IF A>50 THEN  
        DBMS_OUTPUT.PUT_LINE('A is greater');  
    END IF;  
END;  
/

IF THEN ELSE

DECLARE  
    A NUMBER:=100;  
BEGIN  
    IF A>50 THEN  
        DBMS_OUTPUT.PUT_LINE('A is greater');  
    ELSE  
        DBMS_OUTPUT.PUT_LINE('A is smaller or equal');  
    END IF;  
END;  
/

IF ELSIF ELSE

Used for multiple conditions.

DECLARE  
    A NUMBER:=103;  
BEGIN  
    IF A=100 THEN  
        DBMS_OUTPUT.PUT_LINE('Option 100');

ELSIF A=103 THEN  
        DBMS_OUTPUT.PUT_LINE('Option 103');

ELSIF A=108 THEN  
        DBMS_OUTPUT.PUT_LINE('Option 108');

ELSE  
        DBMS_OUTPUT.PUT_LINE('Invalid option');  
    END IF;  
END;  
/

LOOPS

SIMPLE LOOP

A simple loop continues until an EXIT condition is reached.

DECLARE  
    A NUMBER:=1;  
BEGIN  
    LOOP  
        DBMS_OUTPUT.PUT_LINE(A);

EXIT WHEN A=10;

A:=A+1;  
    END LOOP;  
END;  
/

WHILE LOOP

Condition is checked before each iteration.

DECLARE  
    A NUMBER:=1;  
BEGIN  
    WHILE A<=10 LOOP  
        DBMS_OUTPUT.PUT_LINE(A);  
        A:=A+1;  
    END LOOP;  
END;  
/

FOR LOOP

BEGIN  
    FOR A IN 1..10 LOOP  
        DBMS_OUTPUT.PUT_LINE(A);  
    END LOOP;  
END;  
/

The loop variable is automatically managed by the FOR loop.

Reverse

For descending ranges:

BEGIN  
    FOR A IN REVERSE 10..1 LOOP  
        DBMS_OUTPUT.PUT_LINE(A);  
    END LOOP;  
END;  
/

EXCEPTIONS

EXCEPTION

An exception represents an error condition raised during PL/SQL execution.

Two broad categories in the notes:

1. Predefined exceptions  
2. User-defined exceptions

NO_DATA_FOUND

Raised when SELECT INTO returns no rows.

DECLARE  
    L_ename emp.ename%TYPE;  
BEGIN  
    SELECT ename  
    INTO L_ename  
    FROM emp  
    WHERE eid=999;

DBMS_OUTPUT.PUT_LINE(L_ename);

EXCEPTION  
    WHEN NO_DATA_FOUND THEN  
        DBMS_OUTPUT.PUT_LINE(  
            'Employee not found'  
        );  
END;  
/

TOO_MANY_ROWS

Raised when a single-row SELECT INTO returns more than one row.

DECLARE  
    L_ename emp.ename%TYPE;  
BEGIN  
    SELECT ename  
    INTO L_ename  
    FROM emp  
    WHERE deptno=10;

EXCEPTION  
    WHEN TOO_MANY_ROWS THEN  
        DBMS_OUTPUT.PUT_LINE(  
            'More than one employee found'  
        );  
END;  
/

 ZERO_DIVIDE

Raised when dividing by zero.

DECLARE  
    A NUMBER;  
BEGIN  
    A:=10/0;

EXCEPTION  
    WHEN ZERO_DIVIDE THEN  
        DBMS_OUTPUT.PUT_LINE(  
            'Cannot divide by zero'  
        );  
END;  
/

VALUE_ERROR

Can occur when a value cannot fit into a variable or when a conversion/assignment causes a value error.

DECLARE  
    A NUMBER(3);  
BEGIN  
    A:=12345;

EXCEPTION  
    WHEN VALUE_ERROR THEN  
        DBMS_OUTPUT.PUT_LINE(  
            'Value error'  
        );  
END;  
/

DUP_VAL_ON_INDEX

Raised when an insert/update violates a unique or primary-key constraint.

BEGIN  
    INSERT INTO emp  
    VALUES(201,'Brook',67000,50,'CEO',100);

EXCEPTION  
    WHEN DUP_VAL_ON_INDEX THEN  
        DBMS_OUTPUT.PUT_LINE(  
            'Duplicate value'  
        );  
END;  
/

OTHERS

Catches exceptions not handled by earlier handlers.

BEGIN  
    ...  
EXCEPTION  
    WHEN OTHERS THEN  
        DBMS_OUTPUT.PUT_LINE(  
            'Some error occurred'  
        );  
END;  
/

WHEN OTHERS should generally be the last exception handler.

USER-DEFINED EXCEPTION

Create your own exception according to application requirements.

Steps

1. Declare exception  
2. Raise exception  
3. Handle exception

Example:

DECLARE  
    MY_EX EXCEPTION;  
    A NUMBER:=100;  
BEGIN

IF A>50 THEN  
        RAISE MY_EX;  
    END IF;

DBMS_OUTPUT.PUT_LINE(A);

EXCEPTION  
    WHEN MY_EX THEN  
        DBMS_OUTPUT.PUT_LINE(  
            'Value is too large'  
        );  
END;  
/

CURSORS

 CURSOR

A cursor is a mechanism used by PL/SQL to process the result of a SQL statement.

Two major types:

1. Implicit Cursor  
2. Explicit Cursor

IMPLICIT CURSOR

Oracle automatically manages the cursor.

Common attributes:

SQL%ISOPEN  
SQL%FOUND  
SQL%NOTFOUND  
SQL%ROWCOUNT

SQL%ISOPEN

For implicit SQL cursors, this is generally FALSE after the statement has completed.

BEGIN  
    UPDATE student  
    SET sname='Alan'  
    WHERE sno=104;

IF SQL%ISOPEN THEN  
        DBMS_OUTPUT.PUT_LINE('Open');  
    ELSE  
        DBMS_OUTPUT.PUT_LINE('Closed');  
    END IF;  
END;  
/

SQL%FOUND

TRUE if the most recent SQL statement affected/returned a row as applicable.

Example:

BEGIN  
    UPDATE student  
    SET sname='Alan'  
    WHERE sno=104;

IF SQL%FOUND THEN  
        DBMS_OUTPUT.PUT_LINE(  
            'Record Updated'  
        );  
    END IF;  
END;  
/

SQL%NOTFOUND

Opposite of %FOUND.

BEGIN  
    UPDATE student  
    SET sname='Alan'  
    WHERE sno=999;

IF SQL%NOTFOUND THEN  
        DBMS_OUTPUT.PUT_LINE(  
            'Record Not Updated'  
        );  
    END IF;  
END;  
/

SQL%ROWCOUNT

Returns number of rows affected by the most recent DML statement.

BEGIN  
    UPDATE student  
    SET sname='Raja';

DBMS_OUTPUT.PUT_LINE(  
        SQL%ROWCOUNT || ' rows updated'  
    );  
END;  
/

EXPLICIT CURSOR

Programmer explicitly controls:

DECLARE  
OPEN  
FETCH  
CLOSE

Used when processing multiple rows returned by a query.

EXPLICIT CURSOR STEPS

1. Declare cursor  
2. Open cursor  
3. Fetch rows  
4. Close cursor

EXPLICIT CURSOR EXAMPLE

DECLARE

CURSOR c1 IS  
        SELECT ename  
        FROM emp;

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

CURSOR WITH MULTIPLE COLUMNS

DECLARE

CURSOR c1 IS  
        SELECT ename,esal  
        FROM emp;

L_ename emp.ename%TYPE;  
    L_esal  emp.esal%TYPE;

BEGIN

OPEN c1;

LOOP

FETCH c1  
        INTO L_ename,L_esal;

EXIT WHEN c1%NOTFOUND;

DBMS_OUTPUT.PUT_LINE(  
            L_ename || ' ' || L_esal  
        );

END LOOP;

CLOSE c1;

END;  
/

CURSOR WITH %ROWTYPE

DECLARE

CURSOR c1 IS  
        SELECT *  
        FROM emp;

L_emp emp%ROWTYPE;

BEGIN

OPEN c1;

LOOP

FETCH c1 INTO L_emp;

EXIT WHEN c1%NOTFOUND;

DBMS_OUTPUT.PUT_LINE(  
            L_emp.eid || ' ' ||  
            L_emp.ename || ' ' ||  
            L_emp.esal  
        );

END LOOP;

CLOSE c1;

END;  
/

EXPLICIT CURSOR ATTRIBUTES

c1%ISOPEN  
c1%FOUND  
c1%NOTFOUND  
c1%ROWCOUNT

PART 27 — PROCEDURES

PROCEDURE

A procedure is a named PL/SQL program unit stored in the database.

It is reusable.

Syntax

CREATE OR REPLACE PROCEDURE procedure_name  
IS  
BEGIN  
    statements;  
END;  
/

HELLO WORLD PROCEDURE

CREATE OR REPLACE PROCEDURE p1  
IS  
BEGIN  
    DBMS_OUTPUT.PUT_LINE(  
        'Hello World'  
    );  
END;  
/

Execute:

EXEC p1;

PROCEDURE PARAMETERS

Three common parameter modes:

IN  
OUT  
IN OUT

IN PARAMETER

Used to pass a value into a procedure.

CREATE OR REPLACE PROCEDURE  
sum_two_numbers(  
    A IN NUMBER,  
    B IN NUMBER  
)  
IS  
BEGIN  
    DBMS_OUTPUT.PUT_LINE(A+B);  
END;  
/

Execute:

EXEC sum_two_numbers(10,20);

OUT PARAMETER

Used to return a value through a procedure parameter.

CREATE OR REPLACE PROCEDURE  
sum_ret(  
    A IN NUMBER,  
    B IN NUMBER,  
    C OUT NUMBER  
)  
IS  
BEGIN  
    C:=A+B;  
END;  
/

Execute using bind variable

VARIABLE N NUMBER;

EXEC sum_ret(20,30,:N);

PRINT N;

IN OUT PARAMETER

Accepts an input value and returns a modified value through the same parameter.

CREATE OR REPLACE PROCEDURE  
ret_square(  
    A IN OUT NUMBER  
)  
IS  
BEGIN  
    A:=A*A;  
END;  
/

Execute:

VARIABLE N NUMBER;

Initialize:

BEGIN  
    :N:=5;  
END;  
/

Execute:

EXEC ret_square(:N);

Print:

PRINT N;

Result:

25

PROCEDURE WITH TABLE DATA

Insert procedure:

CREATE OR REPLACE PROCEDURE  
insert_record(  
    L_sno   IN student.sno%TYPE,  
    L_sname IN student.sname%TYPE,  
    L_sadd  IN student.sadd%TYPE  
)  
IS  
BEGIN

INSERT INTO student  
    VALUES(L_sno,L_sname,L_sadd);

DBMS_OUTPUT.PUT_LINE(  
        'Record Inserted'  
    );

END;  
/

Execute:

EXEC insert_record(105,'Alan','USA');

UPDATE PROCEDURE

CREATE OR REPLACE PROCEDURE  
update_record(  
    L_sno IN student.sno%TYPE  
)  
IS  
BEGIN

UPDATE student  
    SET sname='Rani'  
    WHERE sno=L_sno;

DBMS_OUTPUT.PUT_LINE(  
        'Record Updated'  
    );

END;  
/

DELETE PROCEDURE

CREATE OR REPLACE PROCEDURE  
delete_record(  
    L_sno IN student.sno%TYPE  
)  
IS  
BEGIN

DELETE FROM student  
    WHERE sno=L_sno;

DBMS_OUTPUT.PUT_LINE(  
        'Record Deleted'  
    );

END;  
/

 LIST PROCEDURES

SELECT object_name  
FROM user_objects  
WHERE object_type='PROCEDURE';

PROCEDURE SOURCE CODE

SELECT text  
FROM user_source  
WHERE name='INSERT_RECORD';

DROP PROCEDURE

DROP PROCEDURE insert_record;

PART 28 — FUNCTIONS

151. FUNCTION

A function is a named PL/SQL program unit that returns a value.

Syntax

CREATE OR REPLACE FUNCTION function_name  
RETURN datatype  
IS  
BEGIN  
    ...  
    RETURN value;  
END;  
/

152. FUNCTION — ADD TWO NUMBERS

CREATE OR REPLACE FUNCTION  
ret_sum(  
    A NUMBER,  
    B NUMBER  
)  
RETURN NUMBER  
IS  
BEGIN  
    RETURN A+B;  
END;  
/

Execute:

SELECT ret_sum(10,20)  
FROM dual;

Result:

30

153. FUNCTION — TAX

CREATE OR REPLACE FUNCTION  
ret_tax(  
    salary NUMBER  
)  
RETURN NUMBER  
IS  
BEGIN  
    RETURN salary*10/100;  
END;  
/

Execute:

SELECT ret_tax(10000)  
FROM dual;

Use with table:

SELECT eid,  
       ename,  
       esal,  
       ret_tax(esal) AS tax  
FROM emp;

154. LIST FUNCTIONS

SELECT object_name  
FROM user_objects  
WHERE object_type='FUNCTION';

155. FUNCTION SOURCE

SELECT text  
FROM user_source  
WHERE name='RET_SUM';

156. DROP FUNCTION

DROP FUNCTION ret_sum;

157. PROCEDURE vs FUNCTION

|   |   |
|---|---|
|Procedure|Function|
|May return values through OUT/IN OUT parameters|Must return a value|
|Can perform DML|Can perform DML in PL/SQL, subject to SQL invocation restrictions|
|Called as a procedure|Can be called as an expression when valid|
|EXEC procedure_name(...)|SELECT function_name(...) FROM dual is common|
|Does not require a RETURN clause|Requires a RETURN datatype and a returned value|

The original notes simplify this by saying DML is allowed in procedures but not functions. The more accurate rule is that a PL/SQL function can contain DML, but there are restrictions when the function is invoked from SQL.

PART 29 — PACKAGES

158. PACKAGE

A package is a collection of related PL/SQL program units.

It can contain:

Procedures  
Functions  
Variables  
Constants  
Cursors  
Types  
Exceptions

A package normally has two parts:

1. Package Specification  
2. Package Body

3. PACKAGE SPECIFICATION

Contains declarations that are publicly accessible.

CREATE OR REPLACE PACKAGE pkg1  
IS

PROCEDURE sum_num(  
        A IN NUMBER,  
        B IN NUMBER  
    );

END pkg1;  
/

160. PACKAGE BODY

Contains implementation.

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

161. EXECUTE PACKAGE PROCEDURE

EXEC pkg1.sum_num(10,20);

162. PACKAGE WITH FUNCTION

Specification:

CREATE OR REPLACE PACKAGE pkg2  
IS

FUNCTION ret_sum(  
        A NUMBER,  
        B NUMBER  
    )  
    RETURN NUMBER;

END pkg2;  
/

Body:

CREATE OR REPLACE PACKAGE BODY pkg2  
IS

FUNCTION ret_sum(  
        A NUMBER,  
        B NUMBER  
    )  
    RETURN NUMBER  
    IS  
    BEGIN  
        RETURN A+B;  
    END;

END pkg2;  
/

Call:

SELECT pkg2.ret_sum(20,30)  
FROM dual;

163. LIST PACKAGES

SELECT object_name  
FROM user_objects  
WHERE object_type='PACKAGE';

164. PACKAGE SOURCE

SELECT text  
FROM user_source  
WHERE name='PKG1';

165. DROP PACKAGE

DROP PACKAGE pkg1;

Package body:

DROP PACKAGE BODY pkg1;

PART 30 — BULK INSERT

166. INSERT ALL

Used to insert multiple records.

INSERT ALL

INTO student(sno,sname,sadd)  
    VALUES(101,'Raja','HYD')

INTO student(sno,sname,sadd)  
    VALUES(102,'Ravi','DELHI')

INTO student(sno,sname,sadd)  
    VALUES(103,'Ramana','VIZAG')

INTO student(sno,sname,sadd)  
    VALUES(104,'Ramulu','PUNE')

SELECT *  
FROM dual;

PART 31 — TRIGGERS

167. TRIGGER

A trigger is a stored PL/SQL program unit that executes automatically when a specified database event occurs.

Common DML events:

INSERT  
UPDATE  
DELETE

Common timings:

BEFORE  
AFTER

The repository also mentions INSTEAD OF, which is commonly used with views.

168. BASIC TRIGGER

CREATE OR REPLACE TRIGGER trg1  
BEFORE INSERT  
ON student  
BEGIN

DBMS_OUTPUT.PUT_LINE(  
        'Thanks for inserting'  
    );

END;  
/

Now:

INSERT INTO student  
VALUES(105,'Alan','USA');

The trigger automatically executes.

169. MULTIPLE EVENTS

A trigger can handle multiple DML events.

CREATE OR REPLACE TRIGGER trg2  
AFTER INSERT OR UPDATE OR DELETE  
ON student  
BEGIN

IF INSERTING THEN

DBMS_OUTPUT.PUT_LINE(  
            'Insert operation'  
        );

ELSIF UPDATING THEN

DBMS_OUTPUT.PUT_LINE(  
            'Update operation'  
        );

ELSE

DBMS_OUTPUT.PUT_LINE(  
            'Delete operation'  
        );

END IF;

END;  
/

170. STATEMENT-LEVEL TRIGGER

Default trigger behavior is statement-level when FOR EACH ROW is not specified.

It executes once per SQL statement.

Example:

CREATE OR REPLACE TRIGGER trg3  
BEFORE UPDATE  
ON student  
BEGIN

DBMS_OUTPUT.PUT_LINE(  
        'Update performed'  
    );

END;  
/

If:

UPDATE student  
SET sname='Raja';

updates 5 rows, the statement-level trigger executes once.

171. ROW-LEVEL TRIGGER

Uses:

FOR EACH ROW

Example:

CREATE OR REPLACE TRIGGER trg4  
BEFORE DELETE  
ON student  
FOR EACH ROW  
BEGIN

DBMS_OUTPUT.PUT_LINE(  
        'Row deleted'  
    );

END;  
/

If 5 rows are deleted, the trigger fires once for each affected row.

172. TRIGGER PREDICATES

Inside a multi-event trigger:

INSERTING  
UPDATING  
DELETING

Example:

IF INSERTING THEN  
    ...  
ELSIF UPDATING THEN  
    ...  
ELSIF DELETING THEN  
    ...  
END IF;

173. LIST TRIGGERS

SELECT object_name  
FROM user_objects  
WHERE object_type='TRIGGER';

174. TRIGGER SOURCE

SELECT text  
FROM user_source  
WHERE name='TRG3';

175. DROP TRIGGER

DROP TRIGGER trg1;

PART 33 — DATABASE OBJECT QUERIES

179. LIST TABLES

SELECT *  
FROM tab;

180. DATABASE NAME

SELECT *  
FROM global_name;

181. LIST PROCEDURES

SELECT object_name  
FROM user_objects  
WHERE object_type='PROCEDURE';

182. LIST FUNCTIONS

SELECT object_name  
FROM user_objects  
WHERE object_type='FUNCTION';

183. LIST PACKAGES

SELECT object_name  
FROM user_objects  
WHERE object_type='PACKAGE';

184. LIST TRIGGERS

SELECT object_name  
FROM user_objects  
WHERE object_type='TRIGGER';

185. LIST VIEWS

SELECT view_name  
FROM user_views;

186. LIST SYNONYMS

SELECT synonym_name  
FROM user_synonyms;

187. LIST INDEXES

SELECT index_name  
FROM user_indexes;

188. LIST SEQUENCES

SELECT sequence_name  
FROM user_sequences;

PART 34 — INTERVIEW QUERIES

189. DISPLAY ALL EMPLOYEES

SELECT *  
FROM emp;

190. DISPLAY SELECTED COLUMNS

SELECT eid,  
       ename,  
       esal  
FROM emp;

191. ANNUAL SALARY

SELECT eid,  
       ename,  
       esal,  
       esal*12 AS annual_sal  
FROM emp;

192. DEPARTMENT 10 EMPLOYEES

SELECT *  
FROM emp  
WHERE deptno=10;

193. MANAGERS

SELECT *  
FROM emp  
WHERE job='Manager';

194. SALARY GREATER THAN 35000

SELECT *  
FROM emp  
WHERE esal>35000;

195. NULL COMMISSION

SELECT *  
FROM emp  
WHERE comm IS NULL;

196. SALARY BETWEEN 35000 AND 60000

SELECT *  
FROM emp  
WHERE esal BETWEEN 35000 AND 60000;

197. EMPLOYEES IN DEPARTMENTS 10,20,30

Using OR

SELECT *  
FROM emp  
WHERE deptno=10  
OR deptno=20  
OR deptno=30;

Using IN

SELECT *  
FROM emp  
WHERE deptno IN(10,20,30);

Using BETWEEN

SELECT *  
FROM emp  
WHERE deptno BETWEEN 10 AND 30;

BETWEEN is appropriate here only because the department numbers happen to form a continuous numeric range. IN is safer when you mean specifically 10, 20 and 30.

198. EMPLOYEES NOT IN DEPARTMENT 10

SELECT *  
FROM emp  
WHERE deptno<>10;

or:

SELECT *  
FROM emp  
WHERE NOT deptno=10;

199. NAMES STARTING WITH A

SELECT *  
FROM emp  
WHERE ename LIKE 'A%';

200. NAMES ENDING WITH N

SELECT *  
FROM emp  
WHERE ename LIKE '%n';

201. SECOND CHARACTER = L

SELECT *  
FROM emp  
WHERE ename LIKE '_l%';

202. INCREMENT SALARY

UPDATE emp  
SET esal=esal+1000  
WHERE eid=204;

203. CHANGE JOB

UPDATE emp  
SET job='Salesman'  
WHERE eid=202;

204. DELETE EMPLOYEE

DELETE FROM emp  
WHERE eid=203;

205. DELETE EMPLOYEES WITH NULL COMMISSION

DELETE FROM emp  
WHERE comm IS NULL;

206. SECOND HIGHEST SALARY

SELECT MAX(esal)  
FROM emp  
WHERE esal <  
(  
    SELECT MAX(esal)  
    FROM emp  
);

207. HIGHEST SALARY

SELECT MAX(esal)  
FROM emp;

208. LOWEST SALARY

SELECT MIN(esal)  
FROM emp;

209. TOTAL SALARY

SELECT SUM(esal)  
FROM emp;

210. AVERAGE SALARY

SELECT AVG(esal)  
FROM emp;

211. EMPLOYEE COUNT

SELECT COUNT(*)  
FROM emp;

212. DEPARTMENT-WISE SALARY

SELECT deptno,  
       SUM(esal)  
FROM emp  
GROUP BY deptno;

213. DEPARTMENT-WISE AVERAGE

SELECT deptno,  
       AVG(esal)  
FROM emp  
GROUP BY deptno;

214. DEPARTMENT-WISE MAXIMUM

SELECT deptno,  
       MAX(esal)  
FROM emp  
GROUP BY deptno;

215. GROUPS WITH TOTAL SALARY > 40000

SELECT deptno,  
       SUM(esal)  
FROM emp  
GROUP BY deptno  
HAVING SUM(esal)>40000;

216. EMPLOYEE + DEPARTMENT NAME

SELECT e.eid,  
       e.ename,  
       d.dname  
FROM emp e  
JOIN dept d  
ON e.deptno=d.deptno;

217. FIRST THREE RECORDS

SELECT *  
FROM emp  
FETCH FIRST 3 ROWS ONLY;

Older/common Oracle approach:

SELECT *  
FROM emp  
WHERE ROWNUM<=3;

218. LAST THREE RECORDS

SELECT *  
FROM emp  
ORDER BY eid DESC  
FETCH FIRST 3 ROWS ONLY;

PART 35 — QUICK DIFFERENCES FOR INTERVIEWS

219. DELETE vs TRUNCATE vs DROP

|   |   |   |   |
|---|---|---|---|
|Feature|DELETE|TRUNCATE|DROP|
|Category|DML|DDL|DDL|
|Removes rows|Yes|Yes|Yes|
|Removes table|No|No|Yes|
|WHERE allowed|Yes|No|No|
|Table structure remains|Yes|Yes|No|
|Rollback before commit|Yes|No, because DDL commits|No|
|Can delete selected rows|Yes|No|No|

220. PRIMARY KEY vs UNIQUE

|   |   |
|---|---|
|Primary Key|UNIQUE|
|Identifies row|Enforces uniqueness|
|Cannot be NULL|NULLs are allowed in Oracle|
|One primary-key constraint per table|Multiple unique constraints possible|
|UNIQUE + NOT NULL semantics|UNIQUE only|

221. PRIMARY KEY vs FOREIGN KEY

|   |   |
|---|---|
|Primary Key|Foreign Key|
|Identifies row in its table|References key in another table|
|Unique|Duplicates allowed|
|Cannot be NULL|NULL allowed unless separately restricted|
|Parent key|Child key|

222. WHERE vs HAVING

|   |   |
|---|---|
|WHERE|HAVING|
|Filters rows|Filters groups|
|Before GROUP BY|After GROUP BY|
|Usually row-level conditions|Commonly aggregate conditions|

Example:

SELECT deptno,SUM(esal)  
FROM emp  
WHERE esal>10000  
GROUP BY deptno  
HAVING SUM(esal)>40000;

223. ROWID vs ROWNUM

|   |   |
|---|---|
|ROWID|ROWNUM|
|Identifies physical row location|Pseudocolumn for row numbering|
|Related to physical storage|Related to result-row processing|
|Can be used to identify a row|Useful for limiting rows|
|Not sequential|Starts at 1 for the result processing|

224. PROCEDURE vs FUNCTION

|   |   |
|---|---|
|Procedure|Function|
|Reusable PL/SQL program|Reusable PL/SQL program|
|May return through OUT parameters|Must return a value|
|Called as a procedure|Can be used as an expression when valid|
|Commonly invoked with EXEC|Often invoked using SELECT/PLSQL|
|Can perform DML|DML rules depend on how the function is invoked|

225. IMPLICIT vs EXPLICIT CURSOR

|   |   |
|---|---|
|Implicit|Explicit|
|Managed by Oracle|Managed by programmer|
|Automatically opened|Programmer opens|
|Automatically fetched|Programmer fetches|
|Automatically closed|Programmer closes|
|SQL%FOUND etc.|cursor_name%FOUND etc.|

226. SIMPLE VIEW vs MATERIALIZED VIEW

|   |   |
|---|---|
|View|Materialized View|
|Stores query definition|Stores query result|
|Data comes from base table at query time|Result can be physically stored|
|Usually reflects current base data|May need refresh|
|Lightweight virtual representation|Useful for performance/reporting scenarios|

227. SIMPLE INDEX vs COMPOSITE INDEX

|   |   |
|---|---|
|Simple Index|Composite Index|
|One column|Multiple columns|
|INDEX(col1)|INDEX(col1,col2)|
|Useful for one-column access patterns|Useful for multi-column access patterns|

228. AND vs OR

AND

All conditions must be true.

WHERE deptno=10  
AND job='Clerk'

OR

At least one condition must be true.

WHERE deptno=10  
OR deptno=20

229. IN vs OR

These can often express the same equality-list condition.

WHERE deptno IN(10,20,30)

Equivalent:

WHERE deptno=10  
OR deptno=20  
OR deptno=30

IN is generally cleaner.

230. % vs _

|   |   |
|---|---|
|%|_|
|Zero or more characters|Exactly one character|
|A%|A_|
|Any number of characters after A|Exactly one character after A|

Examples:

LIKE 'A%'

Starts with A.

LIKE '_A%'

Second character is A.