# 11. CallableStatement

`CallableStatement` is used to call stored procedures or stored functions from Java.

```text
Java
↓
CallableStatement
↓
Stored Procedure / Function
↓
Database
```

## Simple Difference

```text
PreparedStatement
→ normal SQL

CallableStatement
→ stored procedures / functions
```

## Parameters

```text
IN parameter
→ value sent from Java to database

OUT parameter
→ value returned from database to Java
```

## Example Idea

```java
CallableStatement cs =
        con.prepareCall(
                "{call get_emp_name(?, ?)}"
        );

cs.setInt(1, 101);

cs.registerOutParameter(
        2,
        Types.VARCHAR
);

cs.execute();

String name =
        cs.getString(2);
```

## Priority

For a fresher Java/Spring path, basic awareness is enough unless the project specifically uses stored procedures or PL/SQL.

Remember:

```text
CallableStatement
→ calls stored procedures/functions
→ supports IN and OUT parameters
```
