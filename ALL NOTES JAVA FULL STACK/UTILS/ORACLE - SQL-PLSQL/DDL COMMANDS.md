## DDL COMMANDS

### CREATE TABLE

```sql
CREATE TABLE tablename(colname dataType(size), …(), ….(),);
```

Ex:

```sql
CREATE TABLE student(rollno number(4), name varchar2(12), address varchar2(12));
```

**DESCRIBE / DESC** | syntax |

```sql
DESC tablename;
```

Will get the structure of table.

### DROP TABLE - removes the table object.

```sql
DROP TABLE tablename;
```

### TRUNCATE TABLE - remove all rows while keeping table structure.

```sql
TRUNCATE TABLE tablename;
```

### RENAME TABLE

```sql
RENAME oldname TO newname;
```

### ALTER TABLE - To moidfy an existing table structure

- ADD - adds column
- MODIFY - Used to change column definition(SIZE).
- DROP - drop column.
- RENAME COLUMN - rename.

### ADD

```sql
ALTER TABLE student ADD(mobile number(10)); -- single
```

```sql
ALTER TABLE student ADD(mobile number(10), parentmobile number(10)); -- multi
```

### MODIFY

```sql
ALTER TABLE student MODIFY(roll number(5)); -- single
```

```sql
ALTER TABLE student MODIFY(roll number(5), name varchar2(20)); -- multi
```

```sql
ALTER TABLE employees MODIFY phone_number VARCHAR2(30); - dataType only its tis empty
```

### DROP

```sql
ALTER TABLE student DROP(mobile); -- drops column
```

```sql
ALTER TABLE student DROP(mobile, parentmobile); -- drops column
```

### RENAME

```sql
ALTER TABLE student RENAME COLUMN roll TO rollno;
```
