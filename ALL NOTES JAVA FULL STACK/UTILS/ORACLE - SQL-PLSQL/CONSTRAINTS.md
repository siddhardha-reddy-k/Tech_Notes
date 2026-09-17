## CONSTRAINTS

Constraints are rules applied to table data to maintain integrity and consistency.

Five important constraints:

1. NOT NULL  
2. UNIQUE  
3. PRIMARY KEY  
4. FOREIGN KEY  
5. CHECK

CONSTRAINT IS completely optional

### NOT NULL

- Prevents a column from storing NULL.
- Allows duplicates, just not NULL.
- Only declared at **column level** (no table-level form).

```sql
CREATE TABLE student (
    roll NUMBER(3) NOT NULL,
    name VARCHAR2(10)
);
```

### UNIQUE

- Prevents duplicate **non-NULL** values; NULLs are still allowed.

```sql
-- Column level

CREATE TABLE student (
    roll NUMBER(3) UNIQUE,
    name VARCHAR2(10)
);
```

```sql
-- Table level

CREATE TABLE student (
    roll NUMBER(3),
    name VARCHAR2(10),
    UNIQUE(roll)
);
```

```sql
-- Composite UNIQUE (combination must be unique)

CREATE TABLE student (
    roll NUMBER(3),
    course_id NUMBER(3),
    UNIQUE(roll, course_id)
);
```

### PRIMARY KEY

- Uniquely identifies each row = **UNIQUE + NOT NULL** combined.
- A table can have only **one** primary key (but it can span multiple columns).

```sql
-- Column level

CREATE TABLE student (
    sno NUMBER(3) PRIMARY KEY,
    sname VARCHAR2(10)
);
```

```sql
-- Table level

CREATE TABLE student (
    sno NUMBER(3),
    sname VARCHAR2(10),
    PRIMARY KEY(sno)
);
```

```sql
-- Composite PRIMARY KEY

CREATE TABLE enrollment (
    student_id NUMBER,
    course_id NUMBER,
    PRIMARY KEY(student_id, course_id)
);
```

### FOREIGN KEY

- Establishes a relationship between **parent table** (holds referenced PK/unique key) and **child table** (holds the FK).
- Properties: can contain NULL (skips FK check, inserts directly), can contain duplicates, maintains referential integrity, references a primary/unique key.

```sql
-- Parent

CREATE TABLE college (
    sno NUMBER(3) PRIMARY KEY,
    sname VARCHAR2(10)
);
```

```sql
-- Child — column level

CREATE TABLE library (
    roll_no NUMBER(3) REFERENCES college(sno),
    book_name VARCHAR2(20)
);
```

```sql
-- Child — table level (named constraint, optional name)

CREATE TABLE library (
    roll_no NUMBER(3),
    book_name VARCHAR2(20),
    CONSTRAINT fk_roll FOREIGN KEY (roll_no)
        REFERENCES college(sno)
);
```

Insert into library fails if roll_no value doesn't exist in college.sno

### CHECK

- Restricts column values based on a condition.

```sql
-- Range check

CREATE TABLE student (
    sno NUMBER(3),
    smarks NUMBER(3) CHECK(smarks BETWEEN 0 AND 100)
);
```

```sql
-- Uppercase check

CHECK(sname = UPPER(sname))
```

```sql
-- Lowercase check

CHECK(sname = LOWER(sname))
```

### DEFAULT

Sets a default value when none is provided.

```sql
CREATE TABLE student (
    sno NUMBER(3) PRIMARY KEY,
    sname VARCHAR2(10),
    join_date DATE DEFAULT SYSDATE,
    status VARCHAR2(10) DEFAULT 'Active'
);
```

### ON DELETE CASCADE

Automatically deletes child rows when parent row is deleted.

Syntax:

```sql
CREATE TABLE library(
    roll_no NUMBER(3) REFERENCES college(sno) ON DELETE CASCADE,
    book_name VARCHAR2(20)
);
```

Example:

If student sno=101 is deleted from college table,

all library records with roll_no=101 are automatically deleted.

### ON DELETE SET NULL

Sets child column to NULL when parent is deleted.

```sql
CREATE TABLE library(
    roll_no NUMBER(3) REFERENCES college(sno) ON DELETE SET NULL,
    book_name VARCHAR2(20)
);
```

### ON DELETE RESTRICT

Prevents parent deletion if child rows exist.

Default behavior in most databases.

```sql
CREATE TABLE company_dept (
    dept_id NUMBER PRIMARY KEY,
    dept_name VARCHAR2(50) NOT NULL UNIQUE
);
```

```sql
CREATE TABLE company_employee (
    emp_id NUMBER PRIMARY KEY,
    emp_name VARCHAR2(50) NOT NULL,
    email VARCHAR2(100) UNIQUE,
    salary NUMBER(10,2) CHECK (salary > 0),
    dept_id NUMBER,
    CONSTRAINT fk_dept FOREIGN KEY (dept_id)
        REFERENCES company_dept(dept_id)
);
```

### NAMED CONSTRAINTS

Giving a constraint your own name instead of Oracle's auto-generated one (SYS_C00xxxx).

**Why bother:** easier to DROP/DISABLE/ENABLE later, and error messages actually make sense.

Example — all constraints named, one table:

```sql
CREATE TABLE emp (
    emp_id  NUMBER,
    email   VARCHAR2(100),
    salary  NUMBER,
    dept_id NUMBER,
    CONSTRAINT pk_emp     PRIMARY KEY (emp_id),
    CONSTRAINT uq_email   UNIQUE (email),
    CONSTRAINT chk_salary CHECK (salary > 0),
    CONSTRAINT fk_dept    FOREIGN KEY (dept_id) REFERENCES dept(dept_id)
);
```

**Naming convention:**

- pk_ → primary key
- fk_ → foreign key
- uq_ → unique
- chk_ → check

Adding to an Existing Table:

```sql
ALTER TABLE emp ADD CONSTRAINT pk_emp PRIMARY KEY (emp_id);

ALTER TABLE emp ADD CONSTRAINT fk_emp_dept FOREIGN KEY (dept_id) REFERENCES dept(dept_id);

ALTER TABLE emp ADD CONSTRAINT chk_salary CHECK (salary > 0);

ALTER TABLE emp ADD CONSTRAINT uq_email UNIQUE (email);
```

Managing them later:

```sql
ALTER TABLE emp DROP CONSTRAINT fk_dept;

ALTER TABLE emp DISABLE CONSTRAINT chk_salary;
```

Note: NOT NULL almost never gets named — it's just left as column-level NOT NULL.
