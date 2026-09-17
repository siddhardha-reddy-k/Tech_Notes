# Exception vs. Error

|   |   |   |   |
|---|---|---|---|
|Concept|Definition|Common Causes|Examples|
|Exception|Exception is a problem for which we can provide solution programmatically.|Exceptions will occur due to syntax errors.|ArithmeticException, FileNotFoundException, NullPointerException|
|Error|Error is a problem for which we can't provide solution programmatically.|Errors will occur due to lack of system resources.|OutOfMemoryError, StackOverFlowError, LinkageError|

## Types of Program Terminations

As a part of java application development it is a responsibility of a programmer to provide smooth termination for every java program.

- Smooth termination / Graceful termination: During the program execution suppose if we are not getting any interruption in the middle of the program such type of termination is called smooth termination.
- Abnormal termination: During the program execution suppose if we are getting some interruptions in the middle of the program such type of termination is called abnormal termination.

## Exception Fundamentals

- Definition: It is unwanted, unexpected event which disturbs normal flow of a program.
- Runtime Nature: Exceptions always raised at runtime so they are also known as runtime events.
- Objective: The main objective of exception handling is to provide graceful termination. If any exception raised in our program we must and should handle that exception otherwise our program will terminate abnormally.

## Exception Classification

## In java, exceptions are divided into two types:

## 1. Predefined Exceptions (Built-In)

- Checked Exceptions: Exceptions which are checked by the compiler at the time of compilation are called checked exceptions. (ex: InterruptedException, FileNotFoundException, IOException)
- Unchecked Exceptions: Exceptions which are checked by the JVM at the time of runtime are called unchecked exceptions. (ex: ArithmeticException, ClassCastException, IllegalArgumentException)

## 2. Userdefined Exceptions

- Exceptions which are created by the user based on the application requirements are called userdefined exceptions.
- (ex: NoInterestInCourseException, NoPracticeNoJobException, FundNotFoundException).

## Exception Handling Blocks

## try Block

- It is a block which contains risky code.
- It is associate with catch block and finally block.
- It is used to throw the exceptions in catch block. If exception raised in try block then it won't be executed.

## catch Block

- It is a block which contains error handling code.
- It is always associate with try block. It is used to catch the exceptions which is thrown by try block.
- A catch block will take exception name as parameter and that name must match exception class name.
- Multiple Catch Blocks: A try block can have multiple catch blocks. The order of catch blocks is very important it should be from child to parent but not from parent to child.
- Single Catch for Multiple Exceptions: It is possible to handle multiple exceptions in a single catch block using the | operator (e.g., catch(ArithmeticException | NullPointerException e)).

## finally Block

- We need a place where we can maintain cleanup code and it should execute irrespective of exception raised or not such block is called finally block.
- A try with finally combination is valid in java.

## try-with-resources

- A try-with-resources introduced in Java 7.
- It is a try block which contains one or more resources.
- It ensures that each resource must closed at the end of the statement.
- This eliminates the need for manual cleanup in a finally block.

Keyword Differences: final, finally, and finalize

|   |   |
|---|---|
|Keyword|Description|
|final|A final is a modifier which is applicable for variables, methods and classes. It prevents reinitialization (variables), overriding (methods), and creating child classes (classes).|
|finally|It is a block which contains cleanup code and it should execute irrespective of exception raised or not.|
|finalize|It is a method called by garbage collector just before destroying an object for cleanup activity.|

## Displaying Exception Details

## The Throwable class defines following three methods to display exception details:

1. printStackTrace(): It is used to display name of the exception, description of the exception and line number of the exception.
2. toString(): It is used to display name of the exception and description of the exception.
3. getMessage(): It is used to display description of the exception.

## throw vs throws Statement

- throw statement: Sometimes we will create exception objects explicitly and handover to JVM manually by using throw statement.
- throws statement: If any checked exception raised in our program we must and should handle that exception by using try and catch block or by using throws statement.

## Garbage Collector

- Garbage collector is also known as Daemon thread.
- Deamon thread is a leight weight thread which runs in a background to provide services.
- Garbage collector is a programming feature for memory allocation and deallocation.
- There are two ways to call garbage collector in java:

1. System.gc() 
2. Runtime.getRuntime().gc()
