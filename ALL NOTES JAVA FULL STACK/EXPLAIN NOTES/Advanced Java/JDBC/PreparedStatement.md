
## 5. PreparedStatement

`PreparedStatement` is the preferred JDBC statement type for most application code.

It allows SQL structure and parameter values to be handled separately.

Import:

```java
import java.sql.PreparedStatement;
```

### Basic Example

```java
String sql =
        "SELECT * FROM emp WHERE eid = ?";

PreparedStatement ps =
        con.prepareStatement(sql);

ps.setInt(1, 101);

ResultSet rs = ps.executeQuery();
```

### Placeholder `?`

The `?` represents a parameter placeholder.

Example:

```java
String sql =
        "SELECT * FROM emp " +
        "WHERE deptno = ? AND esal > ?";
```

Then:

```java
ps.setInt(1, 10);
ps.setInt(2, 30000);
```

Numbering is based on placeholder position:

```text
1 → first ?
2 → second ?
3 → third ?
```

### Common Setter Methods

```java
ps.setInt(1, 101);
ps.setString(2, "Sid");
ps.setDouble(3, 45000.50);
```

The setter should match the type of value being passed.

### SELECT Example

```java
String sql =
        "SELECT * FROM emp WHERE eid = ?";

PreparedStatement ps =
        con.prepareStatement(sql);

ps.setInt(1, 101);

ResultSet rs = ps.executeQuery();

while (rs.next()) {
    System.out.println(
            rs.getInt("eid") + " " +
            rs.getString("ename") + " " +
            rs.getInt("esal")
    );
}
```

### Important Difference from Statement

With `Statement`:

```java
Statement stmt = con.createStatement();

ResultSet rs =
        stmt.executeQuery(
                "SELECT * FROM emp WHERE eid = 101"
        );
```

The SQL is passed at execution time.

With `PreparedStatement`:

```java
String sql =
        "SELECT * FROM emp WHERE eid = ?";

PreparedStatement ps =
        con.prepareStatement(sql);

ps.setInt(1, 101);

ResultSet rs = ps.executeQuery();
```

The SQL structure is supplied earlier, parameters are bound separately, and execution happens afterward.

### Why PreparedStatement Prevents Normal SQL Injection

Suppose:

```java
ps.setString(
        1,
        "Sid' OR '1'='1"
);
```

The database treats the entire input as a **string value**, not as SQL syntax.

Conceptually:

```text
SQL:
SELECT * FROM emp WHERE ename = ?

Value:
Sid' OR '1'='1
```

The SQL structure and data stay separate.

### PreparedStatement vs Oracle `&`

In Oracle tools, you may see substitution variables:

```sql
SELECT *
FROM emp
WHERE ename = '&name';
```

`&name` is an Oracle client substitution feature.

JDBC `?` parameters are different.

```text
&name
→ client-side text substitution

?
→ JDBC parameter binding
```

### Why PreparedStatement is Preferred

Main reasons:

```text
Safer   → prevents normal SQL injection through parameters
Cleaner → avoids messy string concatenation
Reusable → same SQL structure can use different values
```

---
