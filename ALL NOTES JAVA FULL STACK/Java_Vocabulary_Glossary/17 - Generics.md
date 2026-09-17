# 17. Generics

## Generics

A Java feature that allows classes, interfaces, and methods to work with types supplied later.

Example:

```java
Box<String>
Box<Integer>
```

The same `Box` structure can work with different types.

---

## Generic Type

A class or interface that accepts one or more type parameters.

Example:

```java
class Box<T>
```

`Box<T>` is a generic type.

---

## Type Parameter

A placeholder representing a type.

Example:

```java
class Box<T>
```

`T` is a type parameter.

Common names:

- `T` → Type
- `E` → Element
- `K` → Key
- `V` → Value
- `R` → Result

---

## Type Argument

The actual type supplied to a generic type.

Example:

```java
Box<String>
```

`String` is the type argument.

---

## Generic Class

A class that declares one or more type parameters.

Example:

```java
class Box<T>
```

---

## Generic Interface

An interface that declares one or more type parameters.

Example:

```java
interface Container<T>
```

---

## Generic Method

A method that declares its own type parameter.

Example structure:

```java
<T> void print(T item)
```

The method can work with different types.

---

## Parameterized Type

A generic type with an actual type argument supplied.

Example:

```java
Box<String>
```

`Box<String>` is a parameterized type.

---

## Raw Type

Using a generic type without supplying its type argument.

Example:

```java
Box box;
```

instead of:

```java
Box<String> box;
```

Raw types lose much of the type safety provided by generics.

---

## Wildcard

Represents an unknown generic type.

```java
?
```

Example:

```java
List<?>
```

Meaning:

A list of some unknown type.

---

## Unbounded Wildcard

A wildcard without a restriction.

```java
?
```

Example:

```java
List<?>
```

---

## Upper-Bounded Wildcard

Restricts the unknown type to a particular type or its subclasses.

```java
? extends Type
```

Example:

```java
List<? extends Number>
```

---

## Lower-Bounded Wildcard

Restricts the unknown type to a particular type or one of its supertypes.

```java
? super Type
```

Example:

```java
List<? super Integer>
```

---

## Bounded Type Parameter

A type parameter restricted to a particular hierarchy.

Example:

```java
<T extends Number>
```

---

## Multiple Bounds

A type parameter can have multiple restrictions.

Conceptually:

```java
<T extends ClassName & InterfaceName>
```

---

## Type Inference

Java determining generic type information automatically from the context.

Example:

```java
new ArrayList<>()
```

Java can often infer the missing type.

---

## Diamond Operator

The:

```java
<>
```

syntax used when Java can infer generic type arguments.

---

## Type Safety

Preventing incompatible types from being used where they do not belong.

Generics provide stronger compile-time type safety.

---

## Type Erasure

Java's mechanism where most generic type information is removed after type checking.

Generics mainly provide compile-time type safety rather than creating completely separate runtime classes for every generic combination.

---

## PECS

A common rule for wildcards:

**Producer Extends, Consumer Super**

Use:

```java
? extends T
```

when mainly reading/producing `T`.

Use:

```java
? super T
```

when mainly accepting/consuming `T`.

---
