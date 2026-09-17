# 14. Date and Time with JDBC

JDBC can read and write SQL date/time values.

Traditional JDBC classes:

```java
java.sql.Date
java.sql.Time
java.sql.Timestamp
```

## Basic Mapping

```text
DATE
→ date

TIME
→ time

TIMESTAMP
→ date + time
```

## Reading Values

```java
Date date =
        rs.getDate("join_date");

Timestamp ts =
        rs.getTimestamp("created_at");
```

## Writing Values

```java
ps.setDate(1, date);
ps.setTimestamp(2, ts);
```

## Modern Java

Modern Java commonly uses:

```java
LocalDate
LocalDateTime
```

JDBC drivers can often work with them using:

```java
rs.getObject(
        "join_date",
        LocalDate.class
);
```

or:

```java
ps.setObject(
        1,
        localDate
);
```

## Core Idea

```text
Traditional JDBC
→ Date
→ Time
→ Timestamp

Modern Java
→ LocalDate
→ LocalDateTime
```

Basic awareness is enough for now.
