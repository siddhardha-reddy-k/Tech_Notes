## SYNONYM

### SYNONYM

A synonym provides an alternate name for a database object.

### Create

```sql
CREATE SYNONYM sy1 FOR student;
```

Now:

```sql
SELECT * FROM sy1;
```

Instead of:

```sql
SELECT * FROM student;
```

### Purpose

Convenience  
Abstraction  
Shorter object names  
Cross-schema object access

### VIEW SYNONYMS

```sql
SELECT synonym_name
FROM user_synonyms;
```

### DROP SYNONYM

```sql
DROP SYNONYM sy1;
```
