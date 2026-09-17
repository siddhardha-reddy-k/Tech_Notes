# 1. JDBC Introduction

## JDBC

**JDBC = Java Database Connectivity**

JDBC is a Java API used to connect Java applications with relational databases and execute SQL.

Basic architecture:

```text
Java Application
      ↓
JDBC API
      ↓
JDBC Driver
      ↓
Database
```

## Main JDBC Packages

```java
java.sql
javax.sql
```

Important APIs:

```java
DriverManager
Connection
Statement
PreparedStatement
ResultSet
SQLException
DataSource
```

## JDBC Driver

A JDBC driver allows Java/JDBC to communicate with a specific database.

Examples:

```text
Oracle      → Oracle JDBC Driver
MySQL       → MySQL JDBC Driver
PostgreSQL  → PostgreSQL JDBC Driver
```

Modern applications mainly use **Type 4 drivers**.

## Driver Loading

Old style:

```java
Class.forName("oracle.jdbc.driver.OracleDriver");
```

Modern JDBC usually supports automatic driver loading if the driver is present in the classpath.

---

# 2. JDBC Basic Flow

Main JDBC flow:

```text
Get Connection
      ↓
Create Statement
      ↓
Execute SQL
      ↓
Process Result
      ↓
Close Resources
```

For `SELECT`:

```java
ResultSet rs = ps.executeQuery();
```

For `INSERT`, `UPDATE`, `DELETE`:

```java
int rows = ps.executeUpdate();
```

Difference:

```text
executeQuery()
→ SELECT
→ returns ResultSet

executeUpdate()
→ INSERT / UPDATE / DELETE
→ returns affected row count
```

---

# 3. Connection

`Connection` represents an active session between Java and the database.

Create connection:

```java
Connection con =
        DriverManager.getConnection(
                url,
                username,
                password
        );
```

Important class:

```java
DriverManager
```

Important method:

```java
DriverManager.getConnection()
```

Example Oracle URL:

```text
jdbc:oracle:thin:@//localhost:1521/FREEPDB1
```

Close connection:

```java
con.close();
```

Database-related failures commonly throw:

```java
SQLException
```

---

# 4. Statement

`Statement` is used to execute SQL directly.

Create:

```java
Statement stmt = con.createStatement();
```

SELECT:

```java
ResultSet rs =
        stmt.executeQuery(
                "SELECT * FROM emp"
        );
```

INSERT / UPDATE / DELETE:

```java
int rows =
        stmt.executeUpdate(sql);
```

General method:

```java
stmt.execute(sql);
```

## Main Problem with Statement

Dynamic values are often added using string concatenation:

```java
String sql =
        "SELECT * FROM emp WHERE ename = '" +
        name +
        "'";
```

Problems:

```text
SQL Injection
Messy parameter handling
```

Because user input can become part of the SQL syntax.

---

# 5. PreparedStatement ⭐

`PreparedStatement` is preferred over `Statement` for dynamic SQL values.

Create:

```java
String sql =
        "SELECT * FROM emp WHERE eid = ?";

PreparedStatement ps =
        con.prepareStatement(sql);
```

Bind parameter:

```java
ps.setInt(1, 101);
```

Execute:

```java
ResultSet rs = ps.executeQuery();
```

For INSERT / UPDATE / DELETE:

```java
int rows = ps.executeUpdate();
```

## Placeholder Numbering

```java
WHERE deptno = ? AND esal > ?
```

```java
ps.setInt(1, 10);
ps.setInt(2, 30000);
```

```text
1 → first ?
2 → second ?
```

Common setters:

```java
setInt()
setString()
setDouble()
setBoolean()
```

## Statement vs PreparedStatement

```text
Statement
→ SQL passed during execution
→ dynamic values often concatenated
→ vulnerable to SQL injection

PreparedStatement
→ SQL structure prepared earlier
→ values bound separately
→ safer and cleaner
```

## Why PreparedStatement Prevents SQL Injection

SQL structure:

```sql
SELECT * FROM emp WHERE ename = ?
```

Value:

```text
Sid' OR '1'='1
```

The value is treated as data, not SQL syntax.

## `?` vs Oracle `&`

```text
?
→ JDBC parameter placeholder

&
→ Oracle client substitution variable
```

They are different mechanisms.

---

# 6. ResultSet ⭐

`ResultSet` stores rows returned by a `SELECT` query.

Create:

```java
ResultSet rs = ps.executeQuery();
```

## Cursor

The cursor initially stays **before the first row**.

Move to next row:

```java
rs.next();
```

`next()` returns:

```text
true  → row exists
false → no more rows
```

Multiple rows:

```java
while (rs.next()) {
}
```

Single expected row:

```java
if (rs.next()) {
}
```

## Reading Columns

By column name:

```java
rs.getInt("eid");
rs.getString("ename");
rs.getInt("esal");
```

By column index:

```java
rs.getInt(1);
rs.getString(2);
rs.getInt(3);
```

Column indexing starts from:

```text
1
```

not `0`.

Common getters:

```java
getInt()
getString()
getDouble()
getBoolean()
getDate()
```

---

# Must-Know Interview Questions

## What is JDBC?

JDBC is a Java API used to connect Java applications with relational databases, execute SQL, and process database results.

## What is a JDBC driver?

A JDBC driver is database-specific software that enables JDBC to communicate with a particular database.

## What is Connection?

`Connection` represents an active database session between the Java application and the database.

## What is Statement?

`Statement` is used to execute SQL directly against the database.

## What is PreparedStatement?

`PreparedStatement` is a precompiled/parameterized SQL statement that supports `?` placeholders and separates SQL structure from parameter values.

## Why is PreparedStatement preferred over Statement?

Because it:

- Prevents normal SQL injection through parameters
- Handles dynamic values cleanly
- Makes code easier to read
- Can reuse the same SQL structure with different values

## What is ResultSet?

`ResultSet` represents rows returned by a `SELECT` query.

## What does `rs.next()` do?

It moves the ResultSet cursor to the next row and returns `true` if a row exists.

## Difference between `executeQuery()` and `executeUpdate()`?

```text
executeQuery()
→ used for SELECT
→ returns ResultSet

executeUpdate()
→ used for INSERT / UPDATE / DELETE
→ returns affected row count
```

---

---
# 7. CRUD with JDBC

## CRUD

```text
C → Create  → INSERT
R → Read    → SELECT
U → Update  → UPDATE
D → Delete  → DELETE
```

Main rule:

```text
SELECT
→ executeQuery()
→ returns ResultSet

INSERT / UPDATE / DELETE
→ executeUpdate()
→ returns affected row count
```

Typical flow:

```text
Connection
→ PreparedStatement
→ set parameters
→ execute
→ process result
```

---

# 8. Resource Management ⭐

Main JDBC resources:

```text
Connection
Statement / PreparedStatement
ResultSet
```

Preferred approach:

```java
try (
    Connection con = ...;
    PreparedStatement ps = ...
) {
}
```

Why?

```text
→ resources close automatically
→ safer if exceptions occur
→ avoids manual close()
```

JDBC resources implement:

```java
AutoCloseable
```

Resources close in reverse order:

```text
ResultSet
PreparedStatement
Connection
```

---

# 9. Transactions ⭐

A transaction is a group of database operations treated as one unit.

```text
All succeed
or
All fail
```

Important methods:

```java
con.setAutoCommit(false);

con.commit();

con.rollback();
```

Flow:

```text
setAutoCommit(false)
→ execute operations
→ success → commit()
→ failure → rollback()
```

Use transactions when multiple changes must succeed together.

---

# 10. Batch Processing ⭐

Batch processing is used to execute multiple similar SQL operations together.

Important methods:

```java
addBatch();
executeBatch();
```

Example idea:

```text
addBatch()
addBatch()
addBatch()
    ↓
executeBatch()
```

Return type:

```java
int[]
```

Main benefit:

```text
fewer database round trips
→ better performance
```

Commonly used with transactions.

---

# 11. CallableStatement

Used to call stored procedures or stored functions.

```text
PreparedStatement
→ normal SQL

CallableStatement
→ stored procedures / functions
```

Supports:

```text
IN parameters
OUT parameters
```

Basic awareness is enough for most fresher roles.

---

# 12. ResultSet Types

Main types:

```text
TYPE_FORWARD_ONLY
→ moves only forward

TYPE_SCROLL_INSENSITIVE
→ can move forward/backward
→ usually does not reflect later DB changes

TYPE_SCROLL_SENSITIVE
→ scrollable
→ may reflect DB changes
```

Common movement methods:

```java
next()
previous()
first()
last()
absolute()
relative()
```

Low priority for fresher interviews.

---

# 13. Metadata

## ResultSetMetaData

Gives information about query result columns.

Examples:

```java
getColumnCount()
getColumnName()
getColumnTypeName()
```

## DatabaseMetaData

Gives information about the database and driver.

Examples:

```text
Database name
Database version
Driver name
Driver version
```

Difference:

```text
ResultSetMetaData
→ result columns

DatabaseMetaData
→ database / driver
```

---

# 14. Date and Time with JDBC

Traditional JDBC classes:

```java
java.sql.Date
java.sql.Time
java.sql.Timestamp
```

Basic mapping:

```text
DATE
TIME
TIMESTAMP
```

Modern Java commonly uses:

```java
LocalDate
LocalDateTime
```

Common methods:

```java
getDate()
getTimestamp()
setDate()
setTimestamp()
getObject()
setObject()
```

---

# 15. BLOB and CLOB

```text
BLOB
→ Binary Large Object
→ large binary data
→ images / PDFs / files
```

```text
CLOB
→ Character Large Object
→ large text data
```

Common methods:

```java
getBlob()
setBlob()

getClob()
setClob()
```

Low priority for fresher interviews.

---

# 16. DataSource ⭐

`DataSource` is a managed way to obtain database connections.

Instead of:

```java
DriverManager.getConnection(...)
```

modern applications often use:

```java
dataSource.getConnection()
```

Main idea:

```text
DriverManager
→ direct/simple connection creation

DataSource
→ managed connection source
→ commonly used with connection pooling
→ preferred in modern applications
```

Common in Spring / Spring Boot.

---

# 17. Connection Pooling ⭐

Connection pooling reuses database connections instead of creating a new connection for every request.

Without pooling:

```text
create connection
→ use
→ destroy
```

With pooling:

```text
borrow connection
→ use
→ return to pool
```

Benefits:

```text
better performance
less connection creation overhead
better resource usage
```

Common pool:

```text
HikariCP
```

Spring Boot commonly uses HikariCP.

Important point:

```java
con.close();
```

with a pool usually returns the connection to the pool.

---

# 18. JDBC Application Structure

Simple layered structure:

```text
Controller / Main
      ↓
Service
      ↓
DAO
      ↓
JDBC
      ↓
Database
```

Responsibilities:

```text
Model
→ represents data

DAO
→ database operations

Service
→ business logic

Connection / DataSource
→ database connectivity

Controller / Main
→ starts / receives request
```

Purpose:

```text
clean separation
easier maintenance
easier testing
```

---

# 19. DAO Pattern ⭐

DAO means:

```text
Data Access Object
```

Purpose:

```text
separate database access logic
from business logic
```

Typical methods:

```java
save()
findById()
findAll()
update()
delete()
```

Flow:

```text
Service
→ DAO
→ JDBC
→ Database
```

DAO keeps SQL/JDBC code in one layer.

---

# 20. JDBC Interview Revision

## Must Know Well

```text
What is JDBC?
JDBC architecture
Connection
Statement
PreparedStatement
Statement vs PreparedStatement
SQL Injection
ResultSet
executeQuery() vs executeUpdate()
CRUD
try-with-resources
Transactions
commit() / rollback()
Batch processing
DataSource
Connection pooling
DAO pattern
```

## Basic Awareness

```text
CallableStatement
ResultSet types
Metadata
Date / Time JDBC APIs
BLOB / CLOB
```

