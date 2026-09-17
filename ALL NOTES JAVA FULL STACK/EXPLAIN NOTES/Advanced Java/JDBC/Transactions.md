# 9. Transactions

A transaction is a group of database operations treated as one unit.

```text
All succeed
or
All fail
```

## Example

Money transfer:

```text
1. Deduct money from Account A
2. Add money to Account B
```

Both should succeed together.

## Auto-Commit

By default, JDBC normally uses:

```java
autoCommit = true
```

To control the transaction manually:

```java
con.setAutoCommit(false);
```

## Commit

If everything succeeds:

```java
con.commit();
```

This makes the changes permanent.

## Rollback

If something fails:

```java
con.rollback();
```

This cancels the uncommitted changes.

## Basic Pattern

```java
try (
    Connection con =
            DriverManager.getConnection(
                    url,
                    username,
                    password
            )
) {

    con.setAutoCommit(false);

    try {

        // SQL operation 1
        // SQL operation 2

        con.commit();

    } catch (SQLException e) {

        con.rollback();
        throw e;
    }

} catch (SQLException e) {
    e.printStackTrace();
}
```

## Why `throw e`?

The inner `catch` handles transaction recovery:

```java
con.rollback();
```

Then:

```java
throw e;
```

passes the exception to the outer `catch`.

```text
SQL fails
→ rollback()
→ throw e
→ outer catch handles error
```

## Important Methods

```java
con.setAutoCommit(false);
con.commit();
con.rollback();
```

## Core Idea

```text
Transaction
= multiple SQL operations treated as one unit
```
