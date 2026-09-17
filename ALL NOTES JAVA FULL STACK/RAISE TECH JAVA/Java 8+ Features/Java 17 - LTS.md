
## Release Overview

Java 17 was released in **2021** and is an **LTS release**.

Main interview-relevant feature:

- Sealed Classes & Interfaces
    

---

# Sealed Classes & Interfaces

A sealed class controls which classes are allowed to extend it.

```
public sealed class Shape
        permits Circle, Rectangle {
}
```

Only permitted classes can extend `Shape`.

```
final class Circle extends Shape {
}

non-sealed class Rectangle extends Shape {
}
```

Permitted subclasses must be one of:

- `final` → cannot be extended further
    
- `sealed` → continues restricted inheritance
    
- `non-sealed` → opens inheritance again
    

Same concept works with interfaces.

```
public sealed interface Payment
        permits CardPayment, UpiPayment {
}
```

## Why Use Sealed Types

- Controlled inheritance
    
- Better domain modeling
    
- Safer class hierarchies
    
- Works well with pattern matching
    

---

# Interview Summary

```
Normal class  → anyone can extend
final class   → nobody can extend
sealed class  → only permitted classes can extend
```

**Java 17 = LTS + Sealed Classes & Interfaces**