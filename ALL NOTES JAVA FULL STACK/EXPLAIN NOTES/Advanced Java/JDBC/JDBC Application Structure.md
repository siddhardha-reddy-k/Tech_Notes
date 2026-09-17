# 18. JDBC Application Structure

For learning, JDBC code can stay inside `main()`.

In a real application, responsibilities should be separated.

A simple structure:

```text
Model
DAO
Database Connection
Service
Main / Controller
```

## Model

Represents application data.

```java
class Employee {

    int eid;
    String ename;
    int esal;
    int deptno;
}
```

## Database Connection

Keeps connection-related code separate.

```java
class DBConnection {

    static Connection getConnection() {
        // return connection
    }
}
```

This avoids repeating connection code everywhere.

## DAO

DAO means:

```text
Data Access Object
```

It handles database operations.

Typical methods:

```java
save(Employee employee);

findById(int id);

findAll();

update(Employee employee);

delete(int id);
```

## Service

The service layer contains business logic.

Example:

```text
EmployeeService
```

It may call `EmployeeDAO` for database operations.

## Main / Controller

Starts the application or receives requests.

It should not contain all database logic directly.

## Basic Flow

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

## Why Separate Layers?

With layers, code becomes easier to:

```text
Read
Maintain
Test
Change
```

## Core Idea

```text
Model
→ represents data

DAO
→ database operations

Service
→ business logic

Connection / DataSource
→ database connection

Main / Controller
→ starts or receives request
```
