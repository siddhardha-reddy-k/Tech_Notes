# 15. BLOB and CLOB

BLOB and CLOB are used to store large data.

## BLOB

```text
BLOB
= Binary Large Object
```

Used for large binary data such as:

```text
Images
PDFs
Binary files
```

JDBC methods may include:

```java
rs.getBlob(...);
ps.setBlob(...);
```

## CLOB

```text
CLOB
= Character Large Object
```

Used for very large text data.

JDBC methods may include:

```java
rs.getClob(...);
ps.setClob(...);
```

## Core Difference

```text
BLOB
→ large binary data

CLOB
→ large text data
```

Low priority for fresher interviews.
