# 16. DataSource

`DataSource` is another way to obtain database connections.

Basic JDBC:

```java
Connection con =
        DriverManager.getConnection(
                url,
                username,
                password
        );
```

With `DataSource`:

```java
Connection con =
        dataSource.getConnection();
```

## Simple Difference

```text
DriverManager
→ directly uses URL, username, password
→ simple and good for learning

DataSource
→ connection configuration is managed separately
→ commonly used in modern applications
```

## Why DataSource Matters

`DataSource` works well with:

```text
Connection pooling
Application servers
Spring / Spring Boot
```

Instead of manually creating connections everywhere, the application gets them from a configured `DataSource`.

## Mental Model

```text
Application
   ↓
DataSource
   ↓
Connection
   ↓
Database
```

## In Spring

Spring commonly configures and manages a `DataSource` for the application.

## Core Idea

```text
DriverManager
→ direct/simple JDBC connection

DataSource
→ preferred in modern applications
→ commonly used with connection pooling
```
