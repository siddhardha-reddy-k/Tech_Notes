# 7. CRUD with JDBC

CRUD means:

```text
C → Create  → INSERT
R → Read    → SELECT
U → Update  → UPDATE
D → Delete  → DELETE
```

JDBC CRUD mainly uses `PreparedStatement`.

## INSERT

```java
String sql =
        "INSERT INTO emp(eid, ename, esal, deptno) " +
        "VALUES (?, ?, ?, ?)";

PreparedStatement ps = con.prepareStatement(sql);

ps.setInt(1, 121);
ps.setString(2, "Sid2");
ps.setInt(3, 45000);
ps.setInt(4, 10);

int rows = ps.executeUpdate();
```

`executeUpdate()` returns the number of affected rows.

## SELECT by ID

```java
String sql =
        "SELECT * FROM emp WHERE eid = ?";

PreparedStatement ps = con.prepareStatement(sql);

ps.setInt(1, 121);

ResultSet rs = ps.executeQuery();

if (rs.next()) {
    System.out.println(
            rs.getInt("eid") + " " +
            rs.getString("ename") + " " +
            rs.getInt("esal")
    );
}
```

## SELECT All

```java
String sql = "SELECT * FROM emp";

PreparedStatement ps = con.prepareStatement(sql);

ResultSet rs = ps.executeQuery();

while (rs.next()) {
    System.out.println(
            rs.getInt("eid") + " " +
            rs.getString("ename")
    );
}
```

## UPDATE

```java
String sql =
        "UPDATE emp SET esal = ? WHERE eid = ?";

PreparedStatement ps = con.prepareStatement(sql);

ps.setInt(1, 50000);
ps.setInt(2, 121);

int rows = ps.executeUpdate();
```

## DELETE

```java
String sql =
        "DELETE FROM emp WHERE eid = ?";

PreparedStatement ps = con.prepareStatement(sql);

ps.setInt(1, 121);

int rows = ps.executeUpdate();
```

## Core Idea

```text
SELECT
→ executeQuery()
→ ResultSet

INSERT / UPDATE / DELETE
→ executeUpdate()
→ affected row count
```

The basic JDBC structure stays the same:

```text
Connection
→ PreparedStatement
→ set parameters
→ execute
→ process result if needed
```
