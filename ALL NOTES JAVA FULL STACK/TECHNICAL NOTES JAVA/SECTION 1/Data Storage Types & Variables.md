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
