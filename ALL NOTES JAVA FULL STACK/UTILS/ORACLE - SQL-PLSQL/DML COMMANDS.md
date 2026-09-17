### INSERT

syntax |

```sql
INSERT INTO tablename VALUES(val1, val2, val3 …..);
```

Ex -

```sql
INSERT INTO student VALUES(1001, 'Siddhardha', 'Hyderabad');
```

4ways to do so

### Method 1 — Insert All Columns

```sql
INSERT INTO student
VALUES(101,'Raja','Hyderabad');
```

### Method 2 — Insert Selected Columns

```sql
INSERT INTO student(rollno ,name )
VALUES(102,'Ravi'); -- null for address
```

### Method 3 — Explicit NULL

```sql
INSERT INTO student
VALUES(103,'Ram',NULL);
```

### Method 4 — Dynamic Input

```sql
INSERT INTO student
VALUES(&roll,'&name','&address');
```

## UPDATE

```sql
UPDATE tablename SET colName=data where colName=data;
```

CHANGE where THISMATCHES;

### Single cell update

```sql
UPDATE student SET roll=1002 WHERE name='Siddhardha';
```

### Multi Cell Update

```sql
UPDATE student SET roll=1002, address='India' WHERE name='Siddhardha';
```

Arithmetic Update

```sql
UPDATE student SET roll=1002+1000 WHERE name='Siddhardha';
```

If there is no  "WHERE condition" is set, every row is affected.

## DELETE - delete row

```sql
DELETE FROM tablename where roll=1001;
```

Condition to match any cell of the row.

Without where all rows will be deleted.

## TCL COMMANDS

```sql
COMMIT; -- to save the changes to the database from sql terminal.
```
