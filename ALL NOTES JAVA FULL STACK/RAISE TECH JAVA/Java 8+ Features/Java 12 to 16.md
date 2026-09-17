## Release Overview

For interview preparation, the important finalized features from Java 12–16 are:

- Switch Expressions
    
- Text Blocks
    
- Records
    
- Pattern Matching for `instanceof`
    

---

# 1. Switch Expressions — Java 14

Modern `switch` can return a value directly.

```
String result = switch (day) {
    case 1 -> "Mon";
    case 2 -> "Tue";
    default -> "Unknown";
};
```

Benefits:

- Less boilerplate
    
- No accidental fall-through
    
- Can be used as an expression
    

For multi-line cases:

```
String result = switch (day) {
    default -> {
        yield "Unknown";
    }
};
```

---

# 2. Text Blocks — Java 15

Simplifies multi-line strings.

```
String json = """
        {
          "name": "Sid"
        }
        """;
```

Useful for:

- JSON
    
- SQL
    
- HTML
    
- Multi-line text
    

---

# 3. Records — Java 16

Records are compact data-carrier classes.

```
record Employee(int id, String name) {}
```

Java automatically provides:

- Constructor
    
- Accessor methods
    
- `equals()`
    
- `hashCode()`
    
- `toString()`
    

Accessors:

```
employee.id();
employee.name();
```

Records are implicitly `final`.

---

# 4. Pattern Matching for `instanceof` — Java 16

Combines type checking and casting.

```
if (obj instanceof String text) {
    System.out.println(text.length());
}
```

Replaces:

```
if (obj instanceof String) {
    String text = (String) obj;
}
```

---

# Interview Summary

```
Java 14 → Switch Expressions
Java 15 → Text Blocks
Java 16 → Records
Java 16 → Pattern Matching for instanceof
```