### Control Flow Statements

# Control Flow Statements

Control statements control the execution flow of a program by making decisions, repeating code, or transferring control.

## 1. Decision Making Statements

- `if`: Executes a block only when the condition is `true`.
    
- `if-else`: Executes one block if the condition is true, otherwise executes the `else` block.
    
- `if-else-if ladder`: Checks conditions sequentially; once one condition is true, the remaining blocks are skipped.
    
- `nested if`: An `if` statement inside another `if`.
    
- Java conditions must evaluate to `boolean`.
    

```
int x = 10;
if (x) { }      // CTE
```

## switch

Executes code based on matching a value with case labels.

Common supported types:

- `byte`, `short`, `char`, `int`
    
- Corresponding wrapper types
    
- `String`
    
- `enum`
    

Traditional `switch` does not support `long`, `float`, `double`, or `boolean`.

```
switch (n) {
    case 1:
        System.out.println("One");
        break;
    default:
        System.out.println("Other");
}
```

### case Labels

Case labels must be compile-time constant values.

```
int x = 2;
case x:          // CTE
```

```
final int x = 2;
case x:          // Valid if x is a compile-time constant
```

### Fall-Through

If `break` is omitted, execution continues into following cases.

```
case 1:
    System.out.println("A");
case 2:
    System.out.println("B");
```

`break` is not mandatory; it is used when fall-through is not required.

## Switch Expression

Modern `switch` can return a value.

```
int result = switch (n) {
    case 1 -> 10;
    case 2 -> 20;
    default -> 0;
};
```

- `switch statement` → performs statements.
    
- `switch expression` → produces a value.
    
- `yield` is used to return a value from a block inside a switch expression.
    

```
int result = switch (n) {
    case 1 -> {
        int x = 10;
        yield x * 2;
    }
    default -> 0;
};
```

Switch expressions became standard in Java 14.

## 2. Iteration Statements

### for Loop

Best when the number of iterations is known.

```
for (int i = 0; i < 5; i++) {
    System.out.println(i);
}
```

Execution flow:

```
Initialization → Condition → Body → Update → Condition → ...
```

- Initialization executes once.
    
- Condition is checked before every iteration.
    
- Update executes after the loop body.
    
- Variable declared inside the `for` initialization is scoped to the `for` statement.
    

### while Loop

Best when the number of iterations is unknown.

```
while (condition) {
    // code
}
```

Condition is checked before execution, so the loop may execute zero times.

### do-while Loop

Executes the body first and checks the condition afterward.

```
do {
    // code
} while (condition);
```

Executes at least once.

### Enhanced for Loop

Used to iterate directly through elements of arrays or Collections.

```
for (int n : numbers) {
    System.out.println(n);
}
```

Useful when direct element access is needed and explicit index control is not required.

## 3. Jump Statements

### break

Terminates the nearest loop or `switch`.

```
break → exit nearest loop / switch
```

### continue

Skips the remaining statements of the current loop iteration and proceeds to the next iteration.

```
continue → skip current iteration
```

In a `for` loop, control moves to the update expression before the next condition check.

### return

Immediately terminates the current method and optionally returns a value.

```
return → exit current method
```

Quick comparison:

```
break    → exits nearest loop / switch
continue → skips current loop iteration
return   → exits current method
```


### Data Storage Types & Variables

# Java Datatypes Overview

A datatype defines the kind of value a variable can hold and determines how much memory the system needs to allocate for it.

- byte: Size is 1 byte. Range is -128 to 127. It is the smallest datatype in Java.
- short: Size is 2 bytes. Range is -32,768 to 32,767. It is rarely used.
- int: Size is 4 bytes. Range is -2^31 to 2^31-1. It is the most commonly used datatype for whole numbers.
- long: Size is 8 bytes. Range is -2^63 to 2^63-1. Used when an int is not large enough.
- float: Size is 4 bytes. Range is -3.4e38 to 3.4e38. Provides 4 to 6 decimal points of accuracy. It must be suffixed with f or F (e.g., 10.56f).
- double: Size is 8 bytes. Range is -1.7e308 to 1.7e308. Provides 14 to 16 decimal points of accuracy. It is suffixed with d or D (e.g., 10.56d).
- boolean: Size and Range are Not Applicable. Used strictly for boolean logic and can only be true or false. It cannot accept strings or uppercase values like TRUE.
- char: Size is 2 bytes. Range is 0 to 65,535. It holds a single character enclosed in single quotes (e.g., 'a').

## Important Type Casting & Unicode Rules

- Strict Typing: Assigning an incompatible value to a datatype (e.g., assigning text "Hi" to an int, or a decimal 10.56 to a byte) will trigger a Compile Time Error (C.T.E).
- Characters and Numbers: Java characters map directly to universal Unicode values (e.g., 'A' = 65, 'a' = 97).
- Char to Number: If you assign a char to an int, long, or float, Java will output its numeric Unicode value (e.g., int i = 'a'; outputs 97).
- Number to Char: If you assign a valid Unicode number to a char, Java will output the corresponding character (e.g., char ch = 65; outputs A).

## Types of Variables in Java

A variable is a name given to a memory location to store data. They are broadly categorized into Primitive variables (store basic values) and Reference variables (store object references).

## Based on their position and execution, variables are divided into three types:

## 1. Instance Variables (Non-Static) +

- Scope: Tied to the object. Created when the object is created and destroyed when the object is destroyed.
- Memory: Stored in the Heap area.
- Behavior: The value varies from object to object. Every object gets its own separate copy of the variable.
- Defaults: If not explicitly initialized, the JVM assigns default values (e.g., 0, false, null).
- Access: Can be accessed directly from instance areas, but requires an object reference to be accessed from static areas.

## 2. Static Variables (Global)

- Scope: Tied to the class (.class file). Created at class loading and destroyed at class unloading.
- Memory: Stored in the Method area.
- Behavior: The value does NOT vary from object to object. Only one single copy is created and shared across all objects.
- Defaults: The JVM assigns default values if not explicitly initialized.
- Access: Can be accessed directly from both instance and static areas. Best accessed using the Class name (e.g., Test.i).

## 3. Local Variables (Temporary)

- Scope: Tied to the execution block (methods, constructors, or blocks). Created when the block starts and destroyed when it ends.
- Memory: Stored in the Java Stack memory.
- Behavior: Strictly used for temporary requirements within a specific block of code.
- Defaults: No default values are assigned by the JVM. You will get a Compile Time Error if you try to use an uninitialized local variable.
- Modifiers: The only allowed modifier for a local variable is final.

## Types of Blocks in Java

A block is a set of statements enclosed in curly braces {}. There are three types:

## 1. Instance Block

- Purpose: Used to initialize instance variables.
- Execution: Runs automatically whenever an object (instance) of the class is created, right before the constructor.

## 2. Static Block

- Purpose: Used to initialize static variables.
- Execution: Runs automatically at the time of class loading, which means it executes even before the main method.

## 3. Local Block

- Purpose: Used to initialize local variables or isolate scope.
- Execution: Declared inside methods or constructors and executes exactly like normal sequential statements.

## Typecasting in Java

Typecasting is the process of converting a value from one datatype to another. In Java, this is done in two ways:

## 1. Implicit Typecasting (Widening / Upcasting)

- Purpose: Storing a smaller value into a larger variable type.
- Execution: Performed automatically by the compiler.
- Data Loss: No possibility of losing information.
- Flow: byte -> short -> int -> long -> float -> double (and char -> int).
- Example: byte b = 10; int i = b; (Outputs 10).

## 2. Explicit Typecasting (Narrowing / Downcasting)

- Purpose: Storing a larger value into a smaller variable type.
- Execution: Must be done manually by the programmer by explicitly stating the cast (e.g., (int)).
- Data Loss: High possibility of losing information (such as losing decimals when converting double to int).
- Flow: double -> float -> long -> int -> short -> byte.
- Example: double d = 10.56d; int i = (int)d; (Outputs 10, losing the .56).



### Getting Started Structure and All

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


### Introduction & Ecosystem

# Introduction & Java Ecosystem

## What is Java?

Java is a class-based, object-oriented, statically typed, strongly typed, platform-independent programming language originally developed at Sun Microsystems and released in 1995.

- Class-based → programs are mainly structured using classes.
    
- Object-oriented → supports encapsulation, inheritance, polymorphism and abstraction.
    
- Statically typed → types are checked mainly at compile time.
    
- Strongly typed → Java strictly enforces type compatibility.
    
- Platform-independent → Java source compiles to bytecode, which runs through a compatible JVM.
    
- Multithreaded → built-in support for concurrent execution.
    
- Automatic memory management → Garbage Collector manages unreachable heap objects.
    
- Case-sensitive → `value` and `Value` are different identifiers.  
    Java is not considered purely object-oriented because it also has primitive types such as `int`, `char`, `boolean`, etc.
    

## Static Typing vs Strong Typing

```
Static typing → WHEN types are checked.
Strong typing → HOW strictly type compatibility is enforced.
```

Java allows valid implicit conversions such as widening:

```
int x = 10;
long y = x;
```

It does not freely convert unrelated/incompatible types.

## Why Java?

Main reasons:

- Platform independence
    
- Strong type checking
    
- Automatic memory management
    
- Built-in multithreading/concurrency
    
- Large standard library
    
- Mature ecosystem and community
    
- Widely used for backend and enterprise applications
    

## Platform Independence

```
Java Source (.java)
        ↓ javac
Bytecode (.class)
        ↓ JVM
Native Machine Code
        ↓
OS / Hardware
```

Java bytecode is platform-independent; the JVM implementation is platform-dependent.

```
Same bytecode + Different OS-specific JVMs = Platform Independence
```

This is commonly called **WORA — Write Once, Run Anywhere**.

## Is Java Compiled or Interpreted?

Java uses both compilation and runtime execution techniques.

```
.java → javac → .class bytecode → JVM → Interpreter / JIT → Native Code
```

- `javac` → compile-time compiler; converts source code into bytecode.
    
- Interpreter → executes bytecode at runtime.
    
- JIT → compiles frequently executed code into optimized native machine code.  
    So Java is commonly described as **compiled to bytecode and executed by the JVM using interpretation + JIT compilation**.
    

## Bytecode

Bytecode is the platform-independent intermediate instruction format stored in `.class` files.

```
Source Code ≠ Bytecode ≠ Native Machine Code
```

## `javac` vs `java`

```
javac Test.java → compiles source → Test.class
java Test       → launches JVM and executes the class
```

`javac` is a compiler; `java` is the Java launcher.

# JDK vs JRE vs JVM

## JVM — Java Virtual Machine

The JVM is an abstract machine/runtime environment that executes Java bytecode.  
Main responsibilities:

- Class loading
    
- Bytecode verification
    
- Runtime memory management
    
- Bytecode execution
    
- JIT compilation
    
- Garbage collection
    
- Native-code interaction
    

## JRE — Java Runtime Environment

Conceptually:

```
JRE = JVM + Java runtime libraries/components
```

It provides what is required to run Java applications.  
Modern note: Oracle stopped providing a separate JRE download/image starting with JDK 11.

## JDK — Java Development Kit

```
JDK = Runtime Components + Development Tools
```

Used to develop and run Java applications.  
Important tools:

```
javac   → compiler
java    → launcher
jar     → JAR tool
javadoc → documentation generator
```

### Quick Comparison

```
JDK → Develop + Run
JRE → Run environment
JVM → Executes bytecode
```

Do not rely literally on the old `JDK contains JRE contains JVM` folder structure for modern Java; it is mainly a conceptual explanation today.

# Complete Java Execution Flow

```
.java Source
    ↓
javac
    ↓
.class Bytecode
    ↓
ClassLoader
    ↓
Loading → Linking → Initialization
    ↓
JVM Runtime Memory
    ↓
Execution Engine
    ↓
Interpreter / JIT
    ↓
Native Machine Code
    ↓
OS / Hardware
```

# Class Loading

The ClassLoader subsystem loads class definitions into the JVM.

## Class Lifecycle

```
Loading
  ↓
Linking
  ├─ Verification
  ├─ Preparation
  └─ Resolution
  ↓
Initialization
```

- Loading → finds and loads class information.
    
- Verification → checks bytecode structure and safety.
    
- Preparation → allocates class-level storage and assigns initial/default values as required.
    
- Resolution → resolves symbolic references to actual classes/members.
    
- Initialization → executes class initialization, including static initialization.
    

## ClassLoader Hierarchy

```
Bootstrap
    ↓
Platform
    ↓
Application
```

- Bootstrap → loads fundamental Java classes/modules.
    
- Platform → loads Java platform classes/modules.
    
- Application → loads application/classpath classes.
    

## Parent Delegation

A class loader normally asks its parent to load a class first.

```
Application → Platform → Bootstrap
```

Purpose: avoids unnecessary duplicate loading of core classes and maintains consistent class loading.

# JVM Runtime Memory Areas

## 1. Heap

- Shared between threads.
    
- Stores objects and arrays.
    
- Managed by Garbage Collector.
    

```
User user = new User();
```

The object is generally stored in the heap.

## 2. JVM Stack

- Each thread has its own stack.
    
- Every method call creates a stack frame.  
    A stack frame mainly contains:
    
- Local variables
    
- Operand stack
    
- Method execution/frame data
    

```
Method Call → New Stack Frame
Method Return → Frame Removed
```

## 3. PC Register

Each thread has its own Program Counter register that tracks the current JVM instruction being executed.

## 4. Method Area

Shared JVM runtime area containing per-class structures such as:

- Runtime constant pool
    
- Field/method information
    
- Method/constructor code
    

### Metaspace

HotSpot JVM uses **Metaspace** for class metadata since Java 8.

```
Method Area → JVM specification concept
Metaspace   → HotSpot implementation detail for class metadata
```

They should not be treated as exactly identical terms.

## 5. Native Method Stack

Used for execution of native methods.

## Shared vs Thread-Private

```
Shared:
Heap
Method Area / class-level runtime data

Thread-Private:
JVM Stack
PC Register
Native Method Stack
```

# Execution Engine

```
Execution Engine
├─ Interpreter
└─ JIT Compiler
```

## Interpreter

Executes bytecode instructions at runtime and allows execution to begin without compiling everything to native code first.

## JIT — Just-In-Time Compiler

The JVM profiles execution and identifies frequently executed **hot code**.

```
Bytecode
   ↓
Interpreter
   ↓
Runtime Profiling
   ↓
Hot Code
   ↓
JIT
   ↓
Optimized Native Code
```

JIT improves performance because hot code does not need to remain purely interpreted. HotSpot uses runtime profiling to decide what code is worth compiling.

# Garbage Collection

Garbage Collection automatically reclaims memory used by heap objects that are no longer reachable.

```
Object Created
    ↓
Object Becomes Unreachable
    ↓
Eligible for GC
    ↓
Memory May Be Reclaimed
```

Important:

```
Unreachable ≠ immediately destroyed
Eligible for GC ≠ immediately collected
```

```
obj = null;
```

Removing a reference may make an object eligible for GC if no reachable references remain; it does not immediately destroy the object.  
`System.gc()` requests/suggests garbage collection but does not guarantee that a specific object will be collected or that collection will occur immediately.

# JNI — Java Native Interface

JNI allows Java code to interact with native code such as C/C++.

```
Java → JNI → Native Code → OS
```

# JVM Memory vs Java Memory Model

Do not confuse them.

```
JVM Runtime Memory Areas
→ Heap, Stack, PC Register, Method Area, Native Method Stack

Java Memory Model (JMM)
→ Rules for how threads interact through shared memory
```

JMM deals with concepts such as:

- Visibility
    
- Ordering
    
- Atomicity
    
- `volatile`
    
- `synchronized`
    
- happens-before
    

# Java Platforms

## Java SE — Standard Edition

Core Java platform: language, JVM and standard APIs used as the foundation for Java development.

## Jakarta EE

Enterprise specifications built on top of Java SE for enterprise/server-side applications.

```
J2EE → Java EE → Jakarta EE
```

## Java ME

Java platform aimed mainly at constrained/embedded devices; far less important for modern mainstream backend development.

# Java Ecosystem

Common technologies around Java:

```
Core Platform → Java SE / JDK / JVM
Backend       → Spring / Spring Boot
Persistence   → JDBC / JPA / Hibernate
Build         → Maven / Gradle
Testing       → JUnit
Enterprise    → Jakarta EE
Deployment    → JAR / containers / cloud
```

These are ecosystem technologies; they are not all part of the Java language itself.

# Quick Interview Answers

## What is Java?

Java is a class-based, object-oriented, statically and strongly typed programming language. Java source code is compiled into platform-independent bytecode, which runs through a JVM. It provides automatic memory management, multithreading support and a large ecosystem.

## Why is Java Platform-Independent?

Java source is compiled into platform-independent bytecode instead of OS-specific machine code. Each operating system provides its own JVM implementation, allowing the same compatible bytecode to run on different platforms.

## Is Java Platform-Independent but JVM Platform-Dependent?

Yes.

```
Java Bytecode → Platform-Independent
JVM           → Platform-Dependent Implementation
```

## Is Java Compiled or Interpreted?

Java source is compiled by `javac` into bytecode. At runtime the JVM executes that bytecode using interpretation and JIT compilation.

## JDK vs JRE vs JVM

```
JDK → development tools + runtime
JRE → runtime environment concept
JVM → executes bytecode
```

## JVM Architecture

```
Class Loading
     ↓
Runtime Memory
     ↓
Execution Engine
     ↓
Interpreter / JIT
     ↓
Native Execution
```

Garbage Collection manages unreachable heap objects, while JNI provides native-code interaction.

## Java Code Lifecycle

```
.java → javac → .class → ClassLoader → Linking/Initialization
→ JVM Memory → Interpreter/JIT → Native Code → Execution
```


### Methods & Recursion

# Methods & Recursion

## Methods

A method is a block of code that performs a specific task and can be called whenever required.

## Parameters vs Arguments

```
static void add(int a, int b) { }
add(10, 20);
```

- `a`, `b` → parameters
    
- `10`, `20` → arguments
    

Parameters are declared in the method; arguments are values supplied during the method call.

## 4 Ways to Declare Methods

### 1. void + No Arguments

```
static void show() { }
```

No input and no returned value.

### 2. void + With Arguments

```
static void show(int x) { }
```

Accepts input but does not return a value.

### 3. Return Type + No Arguments

```
static int getValue() {
    return 10;
}
```

Returns a value but accepts no arguments.

### 4. Return Type + With Arguments

```
static int add(int a, int b) {
    return a + b;
}
```

Accepts input and returns a value.

## return

The returned value must be compatible with the declared return type.

```
static int get() {
    return 10;
}
```

```
static int get() {
    return 10.5;     // CTE
}
```

`void` methods do not return a value, but `return;` can terminate the method early.

```
static void test() {
    return;
}
```

## Java Is Pass-by-Value

Java always passes a copy of the value to a method.

### Primitive

```
static void change(int x) {
    x = 50;
}

int a = 10;
change(a);
```

`a` remains `10`.

### Object Reference

```
static void change(Student s) {
    s.marks = 100;
}
```

For objects, Java copies the **reference value**. Both references can therefore point to and modify the same object.

Java is not pass-by-reference.

## Var-Args

Var-args allow a method to accept zero or more arguments.

```
static void show(int... nums) { }
```

Internally, the var-arg parameter behaves like an array.

```
show();
show(10);
show(10, 20, 30);
```

Rules:

```
Only one var-arg parameter is allowed.
Var-arg must be the last parameter.
```

Valid:

```
void test(int x, String... s) { }
```

Invalid:

```
void test(String... s, int x) { }     // CTE
void test(int... x, String... s) { }  // CTE
```

# Recursion

Recursion is a technique where a method calls itself to solve a problem using smaller versions of the same problem.

```
static void test(int n) {
    if (n == 0)
        return;

    System.out.println(n);
    test(n - 1);
}
```

## Base Case

The base case stops further recursive calls.

```
if (n == 0)
    return;
```

Without a proper terminating condition, recursive calls can continue until the stack is exhausted.

## Call Stack

Every method call creates a new stack frame.

```
test(3)
→ test(2)
→ test(1)
→ test(0)
```

After the base case, calls return in reverse order. This is called **stack unwinding**.

```
test(n - 1);
System.out.println(n);
```

For `test(3)`:

```
1
2
3
```

## Missing Base Case

```
static void test(int n) {
    test(n + 1);
}
```

**Result:** RTE — `StackOverflowError`

Recursion and loops are different techniques; Java does not prohibit using them together.


### Operators

# Operators in Java

Operator precedence decides which operator is evaluated first when multiple operators are used in the same expression.

## Order (highest to lowest priority)

| Priority    | Operators                 | Example              |
| ----------- | ------------------------- | -------------------- |
| 1 (highest) | `()` parentheses          | `(2 + 3) * 4`        |
| 2           | `++ --` (unary), `!`, `~` | `-a`, `!flag`, `a++` |
| 3           | `* / %`                   | `a * b`, `a % b`     |
| 4           | `+ -` (binary)            | `a + b`, `a - b`     |
| 5           | `< <= > >=`               | comparisons          |
| 6           | `== !=`                   | equality             |
| 7           | `&&`                      | logical AND          |
| 8           | \|\|                      | logical OR           |
| 9 (lowest)  | `= += -= *= /= %=`        | assignment           |

An operator is a symbol used to perform operations on operands.

Example:

```java
c = a + b;
```

`+` and `=` are operators, while `a`, `b`, and `c` are operands.

---

# Types of Operators in Java

## 1. Arithmetic Operators

Used to perform mathematical operations.

```text
+   Addition
-   Subtraction
*   Multiplication
/   Division
%   Remainder
```

Precedence:

```text
* / %   → higher
+ -     → lower
```

### Integer vs Floating-Point Division

```java
System.out.println(5 / 2);    // 2
System.out.println(5 / 2.0);  // 2.5
```

Rule:

```text
int / int → integer division

If a floating-point operand is involved
→ floating-point division
```

### Division by Zero

Integral constant division by zero:

```java
10 / 0;   // CTE
10 % 0;   // CTE
```

With a variable:

```java
int x = 0;
System.out.println(10 / x);
```

Result:

```text
RTE — ArithmeticException
```

Floating-point division by zero:

```java
System.out.println(10.0 / 0); // Infinity
System.out.println(0.0 / 0);  // NaN
```

---

## 2. Assignment Operators

Used to assign or update values.

```text
=
+=
-=
*=
/=
%=
```

Variables can be reassigned unless they are declared as `final`.

```java
int i = 10;
i = 20;       // valid

final int x = 10;
// x = 20;    // CTE
```

Chained assignment is valid:

```java
int i, j;

i = j = 10;
```

Invalid:

```java
int i = 1, 2; // CTE
```

---

## 3. Ternary (Conditional) Operator

A compact form of simple `if-else`.

Syntax:

```java
condition ? valueIfTrue : valueIfFalse;
```

Example:

```java
int a = 10;
int b = 20;

int max = a > b ? a : b;
```

The condition is evaluated first.

- If `true` → first expression is returned.
- If `false` → second expression is returned.

---

## 4. Bitwise Operators

Operate directly on individual bits of integral values.

```text
&   AND
|   OR
^   XOR
~   NOT
```

Rules:

```text
& → 1 only when both bits are 1
| → 1 when at least one bit is 1
^ → 1 when bits are different
~ → flips all bits
```

For an integer `n`:

```text
~n = -(n + 1)
```

### `&` and `|` with booleans

`&` and `|` can also operate on boolean values.

Unlike `&&` and `||`, they evaluate **both operands**.

```java
boolean result = false & someCondition();
```

`someCondition()` is still evaluated.

---

## 5. Logical Operators

Used with boolean expressions.

```text
&&   Logical AND
||   Logical OR
!    Logical NOT
```

Rules:

```text
&& → true only when both conditions are true
|| → true when at least one condition is true
!  → reverses boolean value
```

### Short-Circuit Evaluation

`&&` and `||` use short-circuit evaluation.

```java
false && expression
```

`expression` is not evaluated.

```java
true || expression
```

`expression` is not evaluated.

Example:

```java
int x = 0;

boolean result = x != 0 && 10 / x > 2;
```

The second condition is skipped, so no `ArithmeticException` occurs.

Quick comparison:

```text
&&  ||  → short-circuit
&   |   → evaluate both boolean operands
```

---

## 6. Relational and Equality Operators

Used to compare values and return a boolean result.

```text
>
>=
<
<=
==
!=
```

Example:

```java
int age = 20;

System.out.println(age >= 18); // true
```

### `==` with Primitives vs Objects

For primitive values:

```java
int a = 10;
int b = 10;

System.out.println(a == b); // true
```

`==` compares the values.

For object references:

```java
String a = new String("java");
String b = new String("java");

System.out.println(a == b);      // false
System.out.println(a.equals(b)); // true
```

Rule:

```text
Primitive == → compares values

Object == → compares references

equals() → may compare logical/content equality,
depending on the class implementation
```

### Chained Comparisons

Java does not support mathematical-style chained comparisons.

```java
0 < x < 20
```

Result:

```text
CTE
```

Correct:

```java
0 < x && x < 20
```

---

## 7. Shift Operators

Used to shift bits left or right.

```text
<<   Left Shift
>>   Signed Right Shift
>>>  Unsigned Right Shift
```

### Left Shift `<<`

Shifts bits to the left.

For many positive integer values, this behaves similarly to multiplying by powers of 2.

```java
10 << 2
```

Approximately:

```text
10 × 2² = 40
```

### Signed Right Shift `>>`

Shifts bits to the right while preserving the sign bit.

For many positive integer values, this behaves similarly to dividing by powers of 2.

```java
8 >> 2
```

Result:

```text
2
```

### Unsigned Right Shift `>>>`

Shifts bits to the right and fills the new left-side bits with `0`.

```java
int x = -8;

System.out.println(x >> 1);   // -4
System.out.println(x >>> 1);  // 2147483644
```

Rule:

```text
>>   → signed right shift
>>>  → unsigned right shift
```

### Important

Do not treat shifting as universally identical to multiplication or division.

Example:

```java
System.out.println(-7 / 2);   // -3
System.out.println(-7 >> 1);  // -4
```

---

## 8. Unary Increment / Decrement Operators

```text
++   Increment
--   Decrement
```

### Post-Increment / Post-Decrement

```java
i++;
i--;
```

Rule:

```text
First Take, Then Change
```

The current value is used first, then the variable is updated.

Example:

```java
int i = 5;

int x = i++;

System.out.println(x); // 5
System.out.println(i); // 6
```

### Pre-Increment / Pre-Decrement

```java
++i;
--i;
```

Rule:

```text
First Change, Then Take
```

The variable is updated first, then the new value is used.

Example:

```java
int i = 5;

int x = ++i;

System.out.println(x); // 6
System.out.println(i); // 6
```

### Invalid Uses

```java
100++;   // CTE
(++i)++; // CTE
```

---

## `i = i++`

```java
int i = 5;

i = i++;

System.out.println(i);
```

Output:

```text
5
```

Mental model:

```java
int temp = i; // temp = 5
i = i + 1;    // i = 6
i = temp;     // i = 5
```

The post-increment returns the original value, and the assignment writes that original value back into `i`.

---

## Multiple Increment Example

```java
int i = 5;

int result = i++ + ++i;
```

Evaluation:

```text
i++  → contributes 5, i becomes 6

++i  → i becomes 7, contributes 7
```

Result:

```text
result = 12
i = 7
```

---

# Quick Interview Recall

```text
* / % have higher precedence than + -

int / int → integer division

floating-point operand involved
→ floating-point division

&& || → short-circuit

& | with booleans
→ both operands evaluated

Primitive ==
→ compares values

Object ==
→ compares references

equals()
→ logical/content equality depending on implementation

<<  → left shift
>>  → signed right shift
>>> → unsigned right shift

Post increment
→ use first, then change

Pre increment
→ change first, then use

i = i++
→ original value gets assigned back
```
