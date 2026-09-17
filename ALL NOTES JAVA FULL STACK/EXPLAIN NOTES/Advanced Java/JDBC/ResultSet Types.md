# 12. ResultSet Types

A normal `ResultSet` usually moves forward row by row.

```java
while (rs.next()) {
}
```

## TYPE_FORWARD_ONLY

Moves only forward:

```text
row 1 → row 2 → row 3
```

This is the common/default type.

## Scrollable ResultSet

A scrollable ResultSet can move in different directions.

Methods include:

```java
next()
previous()
first()
last()
absolute()
relative()
```

## Main Types

```text
TYPE_FORWARD_ONLY
→ moves only forward

TYPE_SCROLL_INSENSITIVE
→ forward/backward
→ usually does not reflect later DB changes

TYPE_SCROLL_SENSITIVE
→ scrollable
→ may reflect database changes
```

## Priority

Low priority for fresher interviews.

Remember:

```text
Normal ResultSet
→ forward only

Scrollable ResultSet
→ can move backward and forward
```
