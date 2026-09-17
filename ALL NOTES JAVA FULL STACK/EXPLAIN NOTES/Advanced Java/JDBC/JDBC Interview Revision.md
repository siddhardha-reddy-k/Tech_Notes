# 20. JDBC Interview Revision

## What is JDBC?

**JDBC = Java Database Connectivity**

JDBC is a Java API used to connect Java applications with relational databases, execute SQL, and process results.

## JDBC Architecture

```text
Java Application
      ↓
JDBC API
      ↓
JDBC Driver
      ↓
Database
```

## Basic JDBC Flow

```text
Connection
→ Statement / PreparedStatement
→ Execute SQL
→ ResultSet
→ Process data
→ Close resources
```

## Connection

`Connection` represents an active session between Java and the database.

```java
DriverManager.getConnection(...)
```

## Statement vs PreparedStatement

```text
Statement
→ SQL executed directly
→ dynamic values often concatenated
→ unsafe with user input
```

```text
PreparedStatement
→ uses ? placeholders
→ values bound separately
→ safer
→ cleaner
→ preferred
```

## Why PreparedStatement Prevents SQL Injection

```sql
SELECT * FROM emp
WHERE ename = ?
```

```java
ps.setString(1, name);
```

The value is treated as data, not SQL syntax.

## executeQuery() vs executeUpdate()

```text
executeQuery()
→ SELECT
→ returns ResultSet
```

```text
executeUpdate()
→ INSERT / UPDATE / DELETE
→ returns affected row count
```

## ResultSet

`ResultSet` stores rows returned by a `SELECT` query.

```java
while (rs.next()) {
}
```

`rs.next()` moves the cursor to the next row.

## Try-with-Resources

Automatically closes:

```text
Connection
PreparedStatement
ResultSet
```

## Transactions

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

## Batch Processing

Groups multiple similar SQL operations and executes them together.

```java
addBatch();
executeBatch();
```

## CallableStatement

Used to call stored procedures or functions from Java.

Basic awareness is enough for most fresher roles.

## DataSource

A modern way to provide database connections.

Commonly used with:

```text
Connection Pooling
Spring
Spring Boot
```

## Connection Pooling

Keeps reusable database connections instead of creating a new connection for every request.

Common pool:

```text
HikariCP
```

## DAO

DAO means:

```text
Data Access Object
```

It separates database access code from business logic.

Typical methods:

```java
save()
findById()
findAll()
update()
delete()
```

## Basic Layered Structure

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

## High-Priority Topics

Know these well:

```text
Connection
PreparedStatement
ResultSet
CRUD
Try-with-resources
Transactions
Batch processing
DataSource
Connection pooling
DAO
SQL Injection
```

## Low-Priority Topics

Basic awareness is enough:

```text
CallableStatement
ResultSet types
Metadata
Date/Time JDBC APIs
BLOB/CLOB
```

## Final Mental Model

```text
Java
→ JDBC
→ Database

Connection
→ PreparedStatement
→ SQL
→ ResultSet

SELECT
→ executeQuery()

INSERT / UPDATE / DELETE
→ executeUpdate()

Modern backend
→ DataSource
→ Connection Pool
→ DAO / Repository style
```
