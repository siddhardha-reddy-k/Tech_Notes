# 10. Batch Processing

Batch processing means grouping multiple similar SQL operations and executing them together.

Useful mainly for:

```text
Bulk INSERT
Bulk UPDATE
```

## Without Batch

```text
INSERT → execute
INSERT → execute
INSERT → execute
```

## With Batch

```text
addBatch()
addBatch()
addBatch()
      ↓
executeBatch()
```

## Example

```java
String sql =
        "INSERT INTO emp(eid, ename, esal, deptno) " +
        "VALUES (?, ?, ?, ?)";

PreparedStatement ps = con.prepareStatement(sql);

ps.setInt(1, 133);
ps.setString(2, "A");
ps.setInt(3, 40000);
ps.setInt(4, 10);
ps.addBatch();

ps.setInt(1, 134);
ps.setString(2, "B");
ps.setInt(3, 45000);
ps.setInt(4, 20);
ps.addBatch();

ps.setInt(1, 135);
ps.setString(2, "C");
ps.setInt(3, 50000);
ps.setInt(4, 30);
ps.addBatch();

int[] result = ps.executeBatch();
```

## Main Methods

```java
addBatch()
executeBatch()
```

`addBatch()` stores the current parameter set.

`executeBatch()` executes all batched operations.

## Return Type

```java
int[] result = ps.executeBatch();
```

Each array value corresponds to one batched command.

## Batch + Transaction

```java
con.setAutoCommit(false);

ps.addBatch();
ps.addBatch();
ps.addBatch();

ps.executeBatch();

con.commit();
```

If something fails:

```java
con.rollback();
```

## Core Idea

```text
Batch Processing
→ groups similar operations
→ reduces repeated database round trips
→ improves performance
```
