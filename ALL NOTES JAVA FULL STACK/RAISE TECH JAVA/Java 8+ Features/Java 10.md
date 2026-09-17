## Release Overview

Java 10 was released in **2018**.

Main interview-relevant feature:

- Local Variable Type Inference using `var`
    

---

# `var`

`var` lets the compiler infer the type of a local variable from its assigned value.

```
var name = "Java";
var age = 22;
```

Equivalent to:

```
String name = "Java";
int age = 22;
```

Java remains **statically typed**. The type is fixed at compile time.

```
var number = 10;
number = "Java"; // Compile-time error
```

## Rules

- Only for local variables
    
- Must be initialized
    
- Cannot infer from `null`
    
- Cannot be used for instance/class fields
    

```
var value = null; // Invalid
```

## Interview Point

**Java 10 =** `**var**` **for local variable type inference.**