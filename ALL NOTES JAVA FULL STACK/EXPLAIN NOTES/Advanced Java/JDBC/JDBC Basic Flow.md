## 2. JDBC Basic Flow

Almost every JDBC program follows this general flow:

```text
1. Get Connection
      ↓
2. Create Statement
      ↓
3. Execute SQL
      ↓
4. Process Result
      ↓
5. Close Resources
```

Example:

```java
Connection con = ...;

PreparedStatement ps =
        con.prepareStatement("SELECT * FROM emp");

ResultSet rs = ps.executeQuery();

while (rs.next()) {
    System.out.println(rs.getString("ename"));
}
```

### Step 1 — Connection

```java
Connection con = ...;
```

`Connection` represents an active connection between Java and the database.

```text
Java Application ↔ Oracle Database
```

### Step 2 — Create a Statement

JDBC provides different statement types:

```java
Statement
PreparedStatement
CallableStatement
```

For normal backend work, `PreparedStatement` is usually preferred.

### Step 3 — Execute SQL

For a `SELECT` query:

```java
ResultSet rs = ps.executeQuery();
```

Flow:

```text
Java
 ↓
SQL
 ↓
JDBC Driver
 ↓
Oracle
```

### Step 4 — Process the Result

A `SELECT` query returns:

```java
ResultSet
```

The rows are read one by one using:

```java
rs.next();
```

### Step 5 — Close Resources

Resources should be closed after use:

```java
rs.close();
ps.close();
con.close();
```

Later, try-with-resources can manage this automatically.

### Query vs Update

For:

```sql
SELECT
```

use:

```java
executeQuery()
```

which returns:

```java
ResultSet
```

For:

```sql
INSERT
UPDATE
DELETE
```

use:

```java
executeUpdate()
```

which returns the number of affected rows.

Example:

```java
int rows = ps.executeUpdate();
```

---
