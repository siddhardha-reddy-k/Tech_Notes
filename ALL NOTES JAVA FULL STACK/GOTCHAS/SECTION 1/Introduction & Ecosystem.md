# Introduction & Ecosystem

## Java Is Not Purely Object-Oriented

```
Java has primitive types:
byte, short, int, long, float, double, char, boolean
```

**Rule:** Java supports OOP strongly, but primitives are not objects.

---

## Java Is Both Compiled and Runtime-Executed

```
.java
 ↓ javac
.class bytecode
 ↓ JVM
Interpreter / JIT
 ↓
Native Code
```

**Rule:** Java source is compiled to bytecode; the JVM executes it using interpretation and JIT compilation.

---

## Platform Independence Does NOT Mean JVM Independence

```
Bytecode → Platform-independent
JVM      → Platform-specific implementation
```

**Rule:** The same bytecode can run on different platforms because each platform has its own JVM implementation.

---

## Bytecode Is Not Machine Code

```
.java source
   ↓
.class bytecode
   ↓
native machine code
```

**Rule:** Bytecode is JVM instruction format, not CPU-native machine code.

---

## `javac` vs `java`

```
javac Test.java
→ compiles source code

java Test
→ launches JVM and runs class
```

**Rule:** `javac` is the compiler; `java` is the launcher/runtime command.

---

## Strong Typing Does NOT Mean No Implicit Conversion

```
int x = 10;
long y = x;
```

**Result:** Valid

**Rule:** Java allows compatible implicit conversions such as widening. Strong typing means incompatible types are strictly controlled.

---

## JDK / JRE / JVM Are Not the Same

```
JDK → development tools + runtime components
JRE → runtime environment concept
JVM → executes bytecode
```

**Rule:** JVM is only one part of the Java runtime architecture.

---

## Modern JDK Does Not Use the Old Separate JRE Layout

```
Old mental model:
JDK contains JRE contains JVM
```

Useful conceptually, but not a literal modern installation structure.

**Rule:** Modern Java distributions, especially JDK 11+, do not follow the old separate JRE packaging model.

---

## Class Loading ≠ Class Initialization

```
Loading
→ Linking
→ Initialization
```

**Rule:** Loading a class definition and initializing its static state are different lifecycle stages.

---

## Linking Has Multiple Steps

```
Linking
├─ Verification
├─ Preparation
└─ Resolution
```

**Rule:** Linking is not a single operation.

---

## Preparation vs Initialization

```
Preparation
→ allocates class-level storage
→ assigns initial/default values

Initialization
→ executes static initialization
→ assigns explicit static values
```

**Rule:** Static fields can first receive default values before explicit initialization runs.

---

## ClassLoader Naming Changed

```
Modern:
Bootstrap → Platform → Application
```

**Rule:** The old "Extension ClassLoader" terminology was replaced by "Platform ClassLoader" in modern Java.

---

## Parent Delegation Direction

```
Application asks Platform
Platform asks Bootstrap
```

**Rule:** A child class loader normally delegates upward first before attempting to load the class itself.

---

## Heap vs Stack

```
Heap
→ objects / arrays
→ shared

JVM Stack
→ stack frames / local method execution data
→ per-thread
```

**Rule:** Object data and method-call execution data are handled in different runtime areas.

---

## Every Method Call Creates a Stack Frame

```
method call
→ new stack frame

method return
→ frame removed
```

**Rule:** Deep recursion can exhaust stack memory even if heap memory is available.

---

## Method Area ≠ Metaspace Exactly

```
Method Area → JVM specification concept
Metaspace   → HotSpot implementation mechanism
```

**Rule:** Do not use the terms as exact synonyms.

---

## Metaspace Replaced PermGen in HotSpot

```
Java 8+
PermGen → removed
Metaspace → used for class metadata
```

**Rule:** This is an implementation detail of HotSpot JVM.

---

## Shared vs Thread-Private Runtime Areas

```
Shared:
Heap
Method Area / class-level data

Thread-private:
JVM Stack
PC Register
Native Method Stack
```

**Rule:** Each thread has its own execution stack and PC register.

---

## JIT Does Not Compile Everything Immediately

```
Bytecode
→ interpretation / profiling
→ hot code detected
→ JIT compilation
```

**Rule:** JIT focuses on frequently executed code based on runtime profiling.

---

## "Hot Code" Means Frequently Executed Code

```
frequently executed method / code path
→ candidate for JIT optimization
```

**Rule:** JIT decisions are runtime-driven.

---

## GC Eligibility ≠ Immediate Collection

```
Object unreachable
→ eligible for GC
≠ immediately collected
```

**Rule:** Java does not guarantee the exact time an eligible object is reclaimed.

---

## `obj = null` Does Not Delete the Object

```
obj = null;
```

**Rule:** This only removes one reference. The object becomes eligible for GC only if no reachable references remain.

---

## `System.gc()` Is Not a Guarantee

```
System.gc();
```

**Rule:** It is only a request/suggestion for garbage collection; it does not guarantee immediate collection.

---

## GC Mainly Manages Heap Objects

```
Heap object becomes unreachable
→ eligible for GC
```

**Rule:** Do not describe GC as manually clearing stack frames or all JVM memory areas.

---

## JVM Memory Areas ≠ Java Memory Model

```
JVM Memory Areas
→ Heap, Stack, PC, Method Area, Native Stack

JMM
→ visibility, ordering, atomicity, happens-before
```

**Rule:** These are completely different concepts.

---

## Java SE vs Jakarta EE

```
Java SE
→ core Java platform

J2EE → Java EE → Jakarta EE
→ enterprise specifications
```

**Rule:** Jakarta EE is the modern continuation of Java EE.

---

## Java Ecosystem ≠ Java Language

```
Java Language
≠ Spring
≠ Hibernate
≠ Maven
≠ Gradle
```

**Rule:** These are technologies/tools around Java, not language features.

---

## WORA Has a Condition

```
Write Once, Run Anywhere
```

**Rule:** Bytecode can run anywhere a compatible JVM/runtime and required dependencies are available.

---

# Quick Recall

```
Java → not purely OOP because primitives exist

.java → source
.class → bytecode
bytecode ≠ machine code

javac → compiler
java  → launcher

bytecode → platform-independent
JVM      → platform-specific implementation

Java → compiled to bytecode + interpreted/JIT at runtime

strong typing ≠ no implicit conversions

Loading ≠ Linking ≠ Initialization

Linking:
Verification → Preparation → Resolution

Bootstrap → Platform → Application

Heap → shared objects
Stack → per-thread method frames

Method Area ≠ exactly Metaspace

JIT → hot code
hot code → frequently executed code

unreachable → eligible for GC
eligible ≠ immediately collected

obj = null → removes reference, not object

System.gc() → request, not guarantee

JVM Memory Areas ≠ JMM

Java SE → core platform
Jakarta EE → enterprise specifications

Spring / Hibernate / Maven → ecosystem, not Java language
```