# 13. Metadata

Metadata means:

```text
Data about data
```

JDBC mainly has two common metadata APIs.

## ResultSetMetaData

Used to get information about query result columns.

```java
ResultSetMetaData md =
        rs.getMetaData();
```

Common methods:

```java
md.getColumnCount();
md.getColumnName(1);
md.getColumnTypeName(1);
```

It can tell you:

```text
How many columns?
What are their names?
What are their types?
```

## DatabaseMetaData

Used to get information about the database and driver.

```java
DatabaseMetaData dbmd =
        con.getMetaData();
```

It can provide:

```text
Database name
Database version
Driver name
Driver version
```

## Difference

```text
ResultSetMetaData
→ information about query result columns

DatabaseMetaData
→ information about database/driver
```

Interview-level awareness is enough for now.
