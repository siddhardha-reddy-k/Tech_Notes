## TCL

### COMMIT

```sql
COMMIT;
```

Makes the current transaction's changes permanent.

### ROLLBACK

```sql
ROLLBACK;
```

Undoes uncommitted transaction changes.

Example:

```sql
INSERT INTO student
VALUES(101,'Raja','HYD');
ROLLBACK;
```

The insertion is undone if it has not been committed and no implicit commit intervened.

### SAVEPOINT

Creates a marker inside a transaction.

```sql
SAVEPOINT sp1;
```

Later:

```sql
ROLLBACK TO sp1;
```

Only changes after sp1 are undone.

Example:

```sql
INSERT INTO student VALUES(101,'Raja','HYD');
SAVEPOINT sp1;
INSERT INTO student VALUES(102,'Ravi','DELHI');
SAVEPOINT sp2;
INSERT INTO student VALUES(103,'Ram','VIZAG');
ROLLBACK TO sp2;
```

## DCL

### PRIVILEGES

A privilege is permission to perform an operation.

Two broad categories:

System Privileges  
Object Privileges

### GRANT

Gives privileges to a user.

**Object Privilege**

```sql
GRANT SELECT
ON employee
TO user1;
```

Multiple:

```sql
GRANT SELECT,DELETE
ON employee
TO user1;
```

```sql
DBA> create user RAM identified by RAM123; -- RAM user with password RAM123
DBA> create user JHANSI identified by JHANSI;
DBA> grant connect,resource to ram,jhansi;
```

### REVOKE

Removes privileges.

```sql
REVOKE SELECT
ON employee
FROM user1;
```

Multiple:

```sql
REVOKE SELECT,DELETE
ON employee
FROM user1;
```
