# Java Packages Overview

A package is essentially a folder or directory that acts as a collection of classes, interfaces, enums, and annotations.

- Predefined Packages: Built-in Java packages provided by the system (e.g., java.lang which is imported by default, java.io, java.util).
- User-Defined Packages: Custom packages created by the programmer.
- Declaration Rule: Use the package keyword at the very top of your file. It is highly recommended to use a reverse URL naming convention.

- Example: package com.ihub.www;

- Compilation: You must instruct the compiler to create the folder structure using the -d flag.

- Example: javac -d . Test.java (The . places the generated package folder in the current directory).

- Execution: You must run the program using its fully qualified name (package name + class name).

- Example: java com.ihub.www.Test

## Enum (Enumeration) Overview

Introduced in Java 1.5, an enum is a special datatype used to group a set of named constants.

- Internal Implementation: Behind the scenes, every enum is treated as a final class that automatically extends the java.lang.Enum class. Every constant you declare inside it is converted into a public static final object reference of that enum type.
- Usage: Enums are highly type-safe and can be used seamlessly inside switch statements.
- Key Predefined Methods:

- values(): Returns an array containing all the constants present in the enum.
- ordinal(): Returns the numeric index position (starting from 0) of a specific enum constant.

- Java Enum Power: Unlike enums in older languages (like C/C++), Java enums are incredibly powerful. Alongside constants, you can define variables, regular methods, constructors, and even a main method directly inside an enum.

- Important Note: If you define a constructor inside an enum, the JVM will automatically execute that constructor once for every single constant at the time the enum is loaded.
