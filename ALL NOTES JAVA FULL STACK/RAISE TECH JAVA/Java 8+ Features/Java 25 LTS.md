## Release Overview

Java 25 was released in **2025** and is an **LTS release**.

Main interview-relevant finalized features:

- Module Import Declarations
    
- Compact Source Files and Instance `main()` Methods
    
- Flexible Constructor Bodies
    

---

# 1. Module Import Declarations

Allows importing exported packages from an entire module.

```
import module java.base;
```

Reduces import boilerplate and builds on JPMS introduced in Java 9.

---

# 2. Compact Source Files & Instance `main()`

Allows simpler Java programs without explicitly declaring a class.

```
void main() {
    System.out.println("Hello");
}
```

Useful mainly for:

- Small programs
    
- Learning
    
- Examples
    
- Scripting-style code
    

Normal application development can still use the traditional class-based structure.

---

# 3. Flexible Constructor Bodies

Allows certain statements before calling `super()` or `this()`.

```
Child(int value) {

    if (value < 0) {
        throw new IllegalArgumentException();
    }

    super(value);
}
```

Useful for validating or preparing constructor arguments before invoking the parent constructor.

---

# Preview Awareness

Java 25 also continues preview work on features such as:

- Primitive types in pattern matching
    

For interviews, basic awareness is enough.

---

# Interview Summary

```
Java 25 → LTS
├── Module Import Declarations
├── Compact Source Files / Instance main()
├── Flexible Constructor Bodies
└── Primitive Pattern Matching → Preview
```

**Java 25 = latest LTS generation with simpler source syntax and continued modernization of Java.**