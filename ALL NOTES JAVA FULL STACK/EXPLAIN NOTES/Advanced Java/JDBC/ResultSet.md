## 6. ResultSet

`ResultSet` represents rows returned by a `SELECT` query.

Example:

```java
ResultSet rs = ps.executeQuery();
```

Suppose Oracle returns:

```text
EID   ENAME   ESAL
101   Sid     40000
102   Ravi    35000
```

`ResultSet` allows Java to read those rows one by one.

### Cursor Concept

Initially, the cursor is positioned **before the first row**.

```text
cursor
  ↓
before first row

101   Sid     40000
102   Ravi    35000
```

Calling:

```java
rs.next();
```

moves the cursor to the next row.

```text
→ 101   Sid     40000
  102   Ravi    35000
```

Calling it again moves to the next row.

When no more rows exist:

```java
rs.next()
```

returns:

```text
false
```

### Reading Multiple Rows

```java
while (rs.next()) {
    System.out.println(
            rs.getString("ename")
    );
}
```

### Reading One Expected Row

```java
if (rs.next()) {
    System.out.println(
            rs.getString("ename")
    );
}
```

### Reading Columns by Name

```java
rs.getInt("eid");
rs.getString("ename");
rs.getInt("esal");
```

This is usually clearer.

### Reading Columns by Position

For:

```sql
SELECT eid, ename, esal
FROM emp;
```

you can use:

```java
rs.getInt(1);
rs.getString(2);
rs.getInt(3);
```

Positions start from:

```text
1
```

not `0`.

### Common Getter Methods

```java
getInt()
getString()
getDouble()
getBoolean()
getDate()
```

### Important Rule

You must move the cursor before reading a row.

Wrong:

```java
ResultSet rs = ps.executeQuery();

System.out.println(
        rs.getString("ename")
);
```

Correct:

```java
ResultSet rs = ps.executeQuery();

if (rs.next()) {
    System.out.println(
            rs.getString("ename")
    );
}
```

### Complete JDBC Flow So Far

```java
Connection con =
        DriverManager.getConnection(
                url,
                username,
                password
        );

String sql =
        "SELECT * FROM emp WHERE eid = ?";

PreparedStatement ps =
        con.prepareStatement(sql);

ps.setInt(1, 101);

ResultSet rs =
        ps.executeQuery();

while (rs.next()) {
    System.out.println(
            rs.getInt("eid") + " " +
            rs.getString("ename") + " " +
            rs.getInt("esal")
    );
}

rs.close();
ps.close();
con.close();
```

Mental model:

```text
Connection
    ↓
PreparedStatement
    ↓
Bind parameters
    ↓
Execute SQL
    ↓
ResultSet
    ↓
rs.next()
    ↓
Read columns
    ↓
Close resources
```

---