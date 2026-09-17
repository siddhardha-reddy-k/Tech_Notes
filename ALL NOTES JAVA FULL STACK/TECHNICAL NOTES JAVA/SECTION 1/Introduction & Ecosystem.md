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