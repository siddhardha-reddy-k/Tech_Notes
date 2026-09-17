## Release Overview

Java 9 was released in **2017**.

It was an important release because it introduced major structural changes to the Java platform, especially the **Java Platform Module System (JPMS)**.

Java 9 also introduced several useful improvements to Collections, Streams, Optional, Interfaces, and developer tooling.

### Main Java 9 Features

- Java Platform Module System (JPMS)
    
- Collection Factory Methods
    
- Stream API improvements
    
- Optional improvements
    
- Private methods in interfaces
    
- JShell
    

---

# 1. Java Platform Module System (JPMS)

The **Java Platform Module System** introduced a new level of organization above packages.

Before Java 9:

```
Class
↓
Package
↓
JAR
```

From Java 9:

```
Class
↓
Package
↓
Module
```

A module is a group of related packages.

Modules allow applications to explicitly define:

- What other modules they depend on
    
- Which packages they expose to other modules
    

A module is defined using:

```
module-info.java
```

Example:

```
module com.app {
    requires java.sql;
    exports com.app.service;
}
```

### `requires`

Declares dependency on another module.

```
requires java.sql;
```

The module needs functionality from the `java.sql` module.

### `exports`

Makes a package accessible to other modules.

```
exports com.app.service;
```

Without exporting it, the package remains hidden from other modules.

### Why JPMS Was Introduced

- Better modularity
    
- Explicit dependencies
    
- Stronger encapsulation
    
- Better organization of large applications
    
- Ability to divide the Java platform itself into modules
    

### Interview Point

JPMS was introduced in **Java 9**.

It provides modularity above the package level using `module-info.java`.

---

# 2. Collection Factory Methods

Java 9 introduced convenient factory methods for creating small collections.

## `List.of()`

```
List<String> names = List.of("Java", "SQL", "Spring");
```

## `Set.of()`

```
Set<String> languages = Set.of("Java", "Python", "C++");
```

## `Map.of()`

```
Map<Integer, String> languages = Map.of(
        1, "Java",
        2, "SQL"
);
```

These methods create **unmodifiable collections**.

Example:

```
List<String> names = List.of("Java", "SQL");

names.add("Spring");
```

Throws:

```
UnsupportedOperationException
```

They also do not allow `null` elements.

### Interview Point

Java 9 introduced:

```
List.of()
Set.of()
Map.of()
```

for convenient creation of unmodifiable collections.

---

# 3. Stream API Improvements

Java 9 added several useful methods to the Stream API.

## `takeWhile()`

Processes elements while a condition remains true.

```
List<Integer> numbers = List.of(1, 2, 3, 10, 4, 5);

numbers.stream()
       .takeWhile(n -> n < 5)
       .forEach(System.out::println);
```

Output:

```
1
2
3
```

Processing stops when the first element fails the condition.

---

## `dropWhile()`

Skips elements while a condition remains true.

```
numbers.stream()
       .dropWhile(n -> n < 5)
       .forEach(System.out::println);
```

Output:

```
10
4
5
```

Once the condition becomes false, the remaining elements are processed.

---

## `Stream.ofNullable()`

Creates a stream containing one element if the value is non-null.

```
Stream.ofNullable(value);
```

If:

```
value != null
```

it creates a stream containing the value.

If:

```
value == null
```

it creates an empty stream.

---

# 4. Optional Improvements

Java 9 added additional operations to `Optional`.

## `ifPresentOrElse()`

Allows separate actions for:

- Value present
    
- Value absent
    

```
optional.ifPresentOrElse(
        System.out::println,
        () -> System.out.println("No value")
);
```

If the value exists:

```
Value action executes
```

If the Optional is empty:

```
Else action executes
```

Java 8 already had:

```
ifPresent()
```

Java 9 added:

```
ifPresentOrElse()
```

---

# 5. Private Methods in Interfaces

Java 8 introduced:

- Default methods
    
- Static methods
    

Java 9 added:

- Private methods
    
- Private static methods
    

Example:

```
interface Demo {

    default void method1() {
        helper();
    }

    default void method2() {
        helper();
    }

    private void helper() {
        System.out.println("Common logic");
    }
}
```

Private methods allow common implementation logic to be reused by other methods inside the interface.

They cannot be accessed by implementing classes.

### Purpose

Avoid duplicating common code between:

```
default
```

and

```
static
```

interface methods.

---

# 6. JShell

Java 9 introduced **JShell**.

JShell is Java's interactive **REPL**.

REPL:

```
Read
Evaluate
Print
Loop
```

It allows Java code to be executed without creating:

```
class
main()
```

Example:

```
jshell> int x = 10

jshell> x * 2
$2 ==> 20
```

Useful for:

- Quickly testing Java syntax
    
- Experimenting with APIs
    
- Learning Java
    
- Testing small pieces of code
    

---

# Java 9 — Interview Summary

Java 9 is mainly remembered for:

```
Java 9
│
├── JPMS / Module System ⭐
│   └── module-info.java
│
├── Collection Factory Methods
│   ├── List.of()
│   ├── Set.of()
│   └── Map.of()
│
├── Stream Improvements
│   ├── takeWhile()
│   ├── dropWhile()
│   └── Stream.ofNullable()
│
├── Optional Improvements
│   └── ifPresentOrElse()
│
├── Private Methods in Interfaces
│
└── JShell
```

## Most Important Feature

**Java Platform Module System (JPMS)**

Java 9 introduced modules above packages to provide:

- Explicit dependencies
    
- Strong encapsulation
    
- Better modularity
    

Defined using:

```
module-info.java
```

## Quick Recall

**Java 9 = Modules + Collection Factory Methods + Stream/Optional improvements + Private Interface Methods + JShell**