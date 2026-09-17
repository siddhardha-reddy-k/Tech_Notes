## 1. JDBC Introduction

### What is JDBC?

**JDBC (Java Database Connectivity)** is a Java API used to connect Java applications with relational databases.

It allows a Java program to:

- Connect to a database
- Execute SQL statements
- Read data returned by the database
- Insert, update, and delete data
- Manage transactions

Basic idea:

```text
Java Application
      ↓
    JDBC
      ↓
   Database
```

Example:

```sql
SELECT * FROM emp;
```

JDBC provides the Java classes and interfaces needed to send this SQL to the database and receive the result.

### Why JDBC is Used

Java and the database are separate systems.

JDBC provides a standard way for Java applications to communicate with databases such as Oracle, MySQL, and PostgreSQL.

```text
Java Application
       ↓
    JDBC API
       ↓
   JDBC Driver
       ↓
    Database
```

### JDBC API

Important JDBC classes and interfaces include:

```java
Connection
DriverManager
Statement
PreparedStatement
ResultSet
SQLException
```

Most core JDBC APIs are available in:

```java
java.sql
```

Another important package is:

```java
javax.sql
```

It contains APIs such as:

```java
DataSource
```

### JDBC Driver

A JDBC driver is database-specific software that lets JDBC communicate with a particular database.

Examples:

```text
Oracle      → Oracle JDBC Driver
MySQL       → MySQL JDBC Driver
PostgreSQL  → PostgreSQL JDBC Driver
```

For Oracle, a driver such as:

```text
ojdbc11.jar
```

can be added to the project classpath.

### Driver Types

Historically, JDBC drivers were divided into:

```text
Type 1
Type 2
Type 3
Type 4
```

For modern development, **Type 4** is the important one.

A Type 4 driver is a pure Java driver that communicates directly with the database using its database protocol.

### Modern Driver Loading

Older JDBC code may contain:

```java
Class.forName("oracle.jdbc.driver.OracleDriver");
```

Modern JDBC usually does not require explicit driver loading.

If the driver JAR is available in the classpath, JDBC can automatically discover it.

### Important Mental Model

JDBC is not simply converting Java code into SQL strings.

The JDBC API and driver also handle:

- Database connections
- Parameter binding
- Java/SQL type conversion
- Authentication
- Sending SQL
- Receiving results
- Database errors
- Transaction communication

### Current Oracle Setup

Oracle version:

```text
23.26.2.0.0
```

JDBC URL:

```text
jdbc:oracle:thin:@//localhost:1521/FREEPDB1
```

The Oracle JDBC driver has been added and the connection was tested successfully.

---
