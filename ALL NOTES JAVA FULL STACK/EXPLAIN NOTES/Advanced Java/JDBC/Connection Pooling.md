# 17. Connection Pooling

Opening a new database connection is relatively expensive.

Without pooling:

```text
Request
→ create connection
→ authenticate
→ use
→ destroy connection
```

Doing this repeatedly wastes time and resources.

## What is Connection Pooling?

A connection pool keeps reusable database connections ready.

```text
Connection Pool

[ Connection 1 ]
[ Connection 2 ]
[ Connection 3 ]
[ Connection 4 ]
```

When the application needs one:

```text
Application
   ↓
borrow connection
   ↓
use it
   ↓
return connection to pool
```

## Important Point

When using a pool:

```java
con.close();
```

usually means:

```text
Return connection to pool
```

not necessarily destroy the physical connection.

## Why It Helps

```text
Without pooling
→ repeated connection creation

With pooling
→ reuse existing connections
→ better performance
→ better resource usage
```

## HikariCP

A common Java connection pool is:

```text
HikariCP
```

Spring Boot commonly uses HikariCP.

```text
Spring Boot
   ↓
DataSource
   ↓
HikariCP
   ↓
Connection Pool
   ↓
Database
```

## Core Idea

```text
Connection Pooling
→ keeps reusable database connections
→ avoids opening a new connection for every request
→ improves performance
```
