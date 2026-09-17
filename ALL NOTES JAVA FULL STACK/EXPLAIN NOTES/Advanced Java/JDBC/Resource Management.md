# 8. Resource Management

JDBC resources should be closed after use.

Main resources:

```text
Connection
Statement / PreparedStatement
ResultSet
```

## Manual Closing

```java
rs.close();
ps.close();
con.close();
```

This works, but if an exception occurs before these lines, resources may remain open.

## Try-with-Resources

Preferred approach:

```java
try (
    Connection con =
            DriverManager.getConnection(
                    url,
                    username,
                    password
            );

    PreparedStatement ps =
            con.prepareStatement(
                    "SELECT * FROM emp"
            );

    ResultSet rs =
            ps.executeQuery();
) {

    while (rs.next()) {
        System.out.println(
                rs.getString("ename")
        );
    }

} catch (SQLException e) {
    e.printStackTrace();
}
```

Anything created inside:

```java
try ( ... )
```

is automatically closed.

## Why It Works

JDBC resources implement:

```java
AutoCloseable
```

So Java automatically calls `close()`.

## Close Order

Resources are closed in reverse order:

```text
Created:
Connection
PreparedStatement
ResultSet

Closed:
ResultSet
PreparedStatement
Connection
```

## Nested Try

```java
try (
    Connection con =
            DriverManager.getConnection(
                    url,
                    username,
                    password
            );

    PreparedStatement ps =
            con.prepareStatement(sql)
) {

    ps.setInt(1, 121);

    try (ResultSet rs = ps.executeQuery()) {

        while (rs.next()) {
            System.out.println(
                    rs.getString("ename")
            );
        }
    }

} catch (SQLException e) {
    e.printStackTrace();
}
```

If the inner `try` throws an `SQLException`:

```text
ResultSet closes
→ exception moves outward
→ PreparedStatement closes
→ Connection closes
→ outer catch handles exception
```

## Core Idea

```text
Manual close
→ easy to forget

Try-with-resources
→ automatic and safer
```
