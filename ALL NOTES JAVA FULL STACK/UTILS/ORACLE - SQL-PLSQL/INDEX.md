## INDEX

An **Index** is a database structure used to dramatically improve data retrieval performance.

- **Analogy:** Think of it like the index at the back of a textbook. Instead of reading every page to find a topic, you look up the term in the index and jump straight to the correct page number.

### How Indexes Work Behind the Scenes

By default, database tables are stored as **Heap Tables** (rows are stored in the order they are inserted, with no specific sorting). Without an index, searching for data requires a **Full Table Scan**, meaning the database must open and read every single row from top to bottom.

When you create an index, Oracle builds a separate, highly organized background structure:

1. **The B-Tree Data Structure: Oracle stores a sorted copy of the indexed column values paired with a RowID (the exact physical disk address of that row in the main table).**
2. **Binary Search: Because the index is pre-sorted, Oracle uses a fast binary search algorithm (splitting the search space in half repeatedly) to locate the value in milliseconds, then jumps directly to the row using its RowID.**

Example:

```sql
CREATE INDEX idx1 ON emp(esal);
```

Then a query involving:

```sql
SELECT * FROM emp WHERE esal=42000;
```

may benefit from the index depending on the optimizer and data distribution.

### SIMPLE INDEX

Index on one column.

```sql
CREATE INDEX idx1 ON emp(esal);
```

### COMPOSITE / COMPLEX INDEX

Index on multiple columns.

```sql
CREATE INDEX idx2 ON emp(eid,ename);
```

Useful when queries frequently use the indexed columns in appropriate combinations.

### VIEW INDEXES

```sql
SELECT index_name
FROM user_indexes;
```

### DROP INDEX

```sql
DROP INDEX idx1;
```

### Performance Trade-Off: Why Not Index Everything?

While indexes make SELECT queries much faster, they come with a cost:

- **Slower Writes (INSERT, UPDATE, DELETE):** Every time data changes in the table, Oracle has to update and re-balance every associated index.
- **Storage Space:** Indexes consume additional disk space.
