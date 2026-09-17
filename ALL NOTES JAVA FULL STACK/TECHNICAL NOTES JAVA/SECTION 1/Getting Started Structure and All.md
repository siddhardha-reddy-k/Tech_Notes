# Getting Started — Structure & Basics

## Source File Structure

A normal Java source file may contain multiple top-level classes/interfaces.

```
package declaration   → optional
import declarations   → optional
class/interface/etc.  → one or more
```

- With normal `javac`, a `public` top-level class/interface must be in a same-named `.java` file.
    
- A source file can contain multiple non-public top-level classes.
    
- A public class does **not** have to contain `main`.
    
- Multiple classes can each contain a `main`; the class supplied to `java ClassName` is the one launched.
    

```
class A {
    public static void main(String[] args) { }
}
class B {
    public static void main(String[] args) { }
}
```

```
java A → runs A.main()
java B → runs B.main()
```

## Packages

A package provides a namespace used to organize related classes/interfaces.

```
package com.example.app;
```

- No package declaration → unnamed/default package.
    
- `java.lang` is automatically imported; it is **not** the default package.
    
- Types in the same package normally do not need an import.
    

## Imports

Imports allow a type or static member to be referred to using its simple name instead of its fully qualified name.

```
import java.time.LocalDate;     // single-type import
import java.util.*;             // on-demand import
import static java.lang.Math.*; // static import
```

- `java.util.*` imports accessible types from `java.util`, not its subpackages.
    
- Static import works with accessible `static` members.
    
- Import declarations help name resolution; they are not the same as runtime class loading.
    

## `main` Method

Standard interview/application entry-point form:

```
public static void main(String[] args) {
}
```

- `public` → accessible to launcher/runtime.
    
- `static` → callable without creating an object.
    
- `void` → returns no value.
    
- `main` → method name.
    
- `String[] args` → receives command-line arguments.  
    Valid equivalent parameter form:
    

```
public static void main(String... args)
```

`args` can be renamed to any valid identifier.

A class does not need `main` to compile. `main` is required when that class is launched as an application entry point.

### Modern Java

Java 25+ also supports more flexible candidate `main` methods, including instance/no-argument forms and compact source files.

```
void main() {
    System.out.println("Hello");
}
```

For fresher interviews and normal structured Java applications, use the standard form unless specifically asked about modern Java 25+ features.

## Command-Line Arguments

```
java Test Sid 22
```

```
public static void main(String[] args) {
    System.out.println(args[0]); // Sid
    System.out.println(args[1]); // 22
}
```

- Arguments are received as `String`.
    
- Indexing starts from `0`.
    
- `args.length` gives argument count.
    
- Numeric input must be parsed when a numeric type is needed.
    

## `System.out.println()`

```
System.out.println("Hello");
```

- `System` → predefined `final` class.
    
- `out` → `public static final` field of type `PrintStream`.
    
- `println()` → method of the `PrintStream` object referenced by `out`.
    

Common output methods:

```
System.out.print("A");        // no newline
System.out.println("A");      // newline
System.out.printf("%.2f", d); // formatted output
```

## Escape Sequences

```
\n  → newline
\t  → horizontal tab
\\  → backslash
\"  → double quote
\'  → single quote
\r  → carriage return
\b  → backspace
\f  → form feed
```

Rendering of control characters such as `\r`, `\b`, and `\f` can depend on the output environment.

## Naming Conventions

These are conventions, not compiler rules.

```
Class / Interface / Enum / Record → PascalCase
Method / Variable                 → camelCase
Constant                          → UPPER_SNAKE_CASE
Package                           → lowercase
```

Examples:

```
StudentService
getStudent()
studentName
MAX_SIZE
com.example.app
```

## Identifiers

An identifier is a name given to a program element such as a class, method, variable, or package.  
Rules:

- Case-sensitive.
    
- Cannot start with a digit.
    
- May use letters, digits, `_`, `$` and valid Unicode identifier characters.
    
- Cannot use reserved keywords where prohibited.
    
- Cannot contain spaces or arbitrary special characters.
    
- `_` by itself is not a valid identifier in modern Java.
    
- `true`, `false`, and `null` cannot be used as identifiers.  
    `$` is legal but normally avoided in manually written names.
    

## Keywords / Reserved Words

Keywords have predefined language meaning.

```
class, public, static, if, return, new, final, ...
```

Do not memorize a fixed keyword count; modern Java also has contextual/restricted keywords whose treatment depends on context.  
`const` and `goto` are reserved but unused.

## Comments

```
// Single-line comment

/* Multi-line
   comment */

/** Javadoc documentation comment */
```

Comments are ignored during normal program execution; Javadoc comments can be processed by documentation tools.