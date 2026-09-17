## 4. Statement

`Statement` is used to send SQL directly from Java to the database.

Import:

```java
import java.sql.Statement;
```

Create it from a `Connection`:

```java
Statement stmt = con.createStatement();
```

### executeQuery()

Used for:

```sql
SELECT
```

Example:

```java
ResultSet rs =
        stmt.executeQuery(
                "SELECT * FROM emp"
        );
```

It returns:

```java
ResultSet
```

### executeUpdate()

Used mainly for:

```sql
INSERT
UPDATE
DELETE
```

Example:

```java
int rows = stmt.executeUpdate(
        "UPDATE emp SET esal = 50000 WHERE eid = 101"
);
```

The returned integer represents the number of affected rows.

### execute()

General-purpose method:

```java
boolean result = stmt.execute(sql);
```

When the SQL type is already known, `executeQuery()` or `executeUpdate()` is usually clearer.

### Working Example

```java
Statement stmt = con.createStatement();

ResultSet rs = stmt.executeQuery(
        "SELECT * FROM emp"
);

while (rs.next()) {
    System.out.println(
            rs.getInt("eid") + " " +
            rs.getString("ename") + " " +
            rs.getInt("esal") + " " +
            rs.getInt("deptno")
    );
}
```

### Main Problem with Statement

When dynamic values are needed, developers may build SQL using string concatenation.

Example:

```java
String name = userInput;

String sql =
        "SELECT * FROM emp WHERE ename = '" +
        name +
        "'";
```

This has two main problems:

1. SQL Injection
2. Messy parameter handling

Example malicious input:

```text
Sid' OR '1'='1
```

The final SQL could become:

```sql
SELECT *
FROM emp
WHERE ename = 'Sid' OR '1'='1';
```

Since:

```sql
'1'='1'
```

is always true, the query may return unintended rows.

This is why `PreparedStatement` is preferred for dynamic values.

---
