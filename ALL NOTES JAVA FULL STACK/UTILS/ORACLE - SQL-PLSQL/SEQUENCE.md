### SEQUENCE

A sequence generates numeric values.

### Syntax

```sql
CREATE SEQUENCE sequence_name
START WITH value
INCREMENT BY value;
```

Example:

```sql
CREATE SEQUENCE sq1
START WITH 101
INCREMENT BY 1;
```

Another:

```sql
CREATE SEQUENCE sq2
START WITH 10
INCREMENT BY 10;
```

### NEXTVAL

Generates the next sequence value.

```sql
INSERT INTO student
VALUES(sq1.NEXTVAL,'Raja','HYD');
```

Next insertion:

```sql
INSERT INTO student
VALUES(sq1.NEXTVAL,'Ravi','DELHI');
```

Values may become:

101  
102  
103  
...

### CURRVAL

Returns the most recently generated sequence value in the current session.

```sql
SELECT sq1.CURRVAL FROM dual;
```

Usually NEXTVAL must have been referenced in the session before CURRVAL can be used.

### Modify Sequences

To change how it behaves later (e.g., change the increment):

```sql
ALTER SEQUENCE emp_seq INCREMENT BY 5;
```

### VIEW SEQUENCES

```sql
SELECT sequence_name FROM user_sequences;
```

### DROP SEQUENCE

```sql
DROP SEQUENCE sq1;
```

### The Everyday Core

- START WITH: Sets the initial number. Usex1 1 for new tables, or a higher number when migrating old data.
- INCREMENT BY: Sets the counting step. Almost always set to 1 (1, 2, 3...).
- Performance & Safety (The Critical Choices)
- CACHE: Keeps numbers in RAM for maximum speed. Use this for high-volume transactions.
- NOCACHE: Forces writes to disk to prevent gaps if the system crashes. Use this for strict financial/invoice tracking.
- NOCYCLE: Stops the sequence when it hits the limit. Always use this for Primary Keys to prevent duplicate errors.
- The Rarely Used Options
- CYCLE: Automatically loops back to the beginning when the limit is reached. (Rarely used; triggers primary key duplicate errors).
- ORDER: Forces strict chronological numbering across multi-server clusters. (Rarely used; slows down performance).
- NOORDER: Allows servers to hand out numbers out of chronological order. (Default).
- MAXVALUE / MINVALUE: Sets manual ceilings or floors. (Rarely used; the default NOMAXVALUE goes up to 10²⁸, which is plenty).
