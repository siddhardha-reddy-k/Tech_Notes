### Arrays in Java

# Java Arrays Overview

An array is a collection of homogeneous data elements, allowing you to store multiple values in a single variable rather than using separate variables for each value.

## Pros & Cons

- Advantages: Represents multiple elements under one variable name and is highly recommended for performance.
- Disadvantages: Fixed in size (cannot grow or shrink once created) and requires you to know the exact size you need in advance.

Types of Arrays Single Dimensional, Double Dimensional, and Multi-Dimensional.

## Array Lifecycle & Rules

- Declaration: You must not specify the size during declaration. (e.g., int[] arr; or int arr[];).
- Creation: Because arrays are treated as objects in Java, they are created using the new keyword. (e.g., arr = new int[3];).

- Rule 1: You must specify the size during creation.
- Rule 2: An array size of 0 is completely legal.
- Rule 3: Providing a negative size will cause a runtime NegativeArraySizeException.
- Rule 4: The array size must be a byte, short, int, or char. (Decimals cause a Compile Time Error).
- Rule 5: The maximum allowed size is the maximum value of an int (2147483647).

- Initialization: Arrays automatically get default values upon creation. You can override these using the index (e.g., arr[0] = 10;). Accessing an index outside the array size throws an ArrayIndexOutOfBoundsException.
- One-Line Shortcut: You can declare, create, and initialize simultaneously: int[] arr = {10, 20, 30};.

## length vs length()

- length: A predefined final variable used specifically for arrays to return their size (e.g., arr.length).

- length(): A predefined method used specifically for String objects to return the number of characters (e.g., s.length()).

## Jagged Array

- Definition: Also known as an "array of arrays." It is a multi-dimensional array where each row can have a different number of columns (a different column size).
- Structure: Instead of a perfect rectangular grid, the rows are uneven. For example, row 0 might have 4 elements, row 1 might have 2 elements, and row 2 might have 3 elements.
- Iteration: When looping through a jagged array, you must check the specific length of each row dynamically (e.g., using arr[i].length for the inner column loop) to avoid out-of-bounds errors.

## Anonymous Array

- Definition: A nameless array declared without assigning it to a variable.
- Purpose: Used strictly for instant or one-time use. It is highly useful when you need to pass an array directly as an argument to a method without needing to store it for future use.
- Declaration: Created and initialized on the fly using the new keyword and providing the values immediately.

- Single Dimensional Example: new int[]{10, 20, 30};
- Double Dimensional Example: new int[][]{{1, 2}, {3, 4, 5}};



### Collection Framework & Generics

# Generics

- Arrays are typesafe. It means we can give guarantee that what type of elements are present in arrays.
- Collections are not typesafe. It means we can't provide guarantee that what type of elements are present in Collections.
- To overcome above limitations Sun Micro System introduced Generics concept in 1.5 version.
- The main objective of Generics is:

1. To make make Collections as typesafe.
2. To avoid typecasting problem.

java.util package: Arrays vs Collections

|   |   |
|---|---|
|Arrays|Collections|
|It is a collection of homogeneous data elements.|It is a collection of homogeneous and hetrogeneous data elements.|
|It is fixed in size.|It is growable in nature.|
|Performance point of view arrays are recommanded to use.|Memory point of view Collections are recommanded to use.|
|Arrays are not implemented based on data structure concept. So we can't expect any ready made method.|Collections are implemented based on data structure concept. So we can expect readymade methods.|
|It can hold primitive types and object types.|It can hold only object types.|
|It is typesafe.|It is not typesafe.|

## Collection Framework

- Collection framework defines several classes and interfaces to represent group of objects in a single entity.

## Collection Interface

- Collection is an interface which is present in java.util package.
- Collection is a root interface for entire Collection Framework.
- If we want to represent group of individual objects in a single entity then we need to use Collection interface.

## List Interface

- It is a child interface of Collection interface.
- If we want to represent group of individual objects in a single entity where duplicate objects are allowed and order is preserved then we need to use List interface.

## List.of() vs Arrays.asList()

|   |   |
|---|---|
|List.of()|Arrays.asList()|
|It is introduced in Java 9.|It is introduced in 1.2 version.|
|It gives immutable object.|It gives mutable object.|
|We can't add, remove and replace the elements.|We can't add, remove but we can replace the elements.|
|It does not allow null value.|It supports null value.|

## List Implementations

## ArrayList

- The underlying data structure is resizable array or growable array.
- Duplicate objects are allowed.
- Insertion order is preserved.
- Hetrogeneous objects are allowed.
- Null insertion is possible.
- It implements List, Serializable, Cloneable and RandomAccess inteface.

## LinkedList

- The underlying data structure is doubly LinkedList.
- Duplicates are allowed.
- Insertion order is preserved.
- Hetrogeneous objects are allowed.
- Null insertion is possible.
- It implements List, Serializable, Cloneable and Deque interface.

## ArrayList vs LinkedList

|   |   |
|---|---|
|ArrayList|LinkedList|
|The underlying data structure is resizable array or growable array.|The underlying data structure is doubly LinkedList.|
|It is best for storing and retrieving the data.|It is best for manipulating the data.|
|Memory address for ArrayList elements is contigeous.|Memory address for LinkedList elements is not contigeous.|
|When ArrayList is initialized a default capacity 10 is assigned to it.|There is no case of default capacity.|

## Vector

- The underlying data structure is resizable array or growable array.
- Duplicate objects are allowed.
- insertion order is preserved.
- Hetrogeneous objects are allowed.
- Null insertion is possible.
- Vector is synchronized. Hence it is thread safe.

## ArrayList vs Vector

|   |   |
|---|---|
|ArrayList|Vector|
|It is a non-legacy class.|It is a legacy class.|
|It is introduced in 1.2 version.|It is introduced in 1.0 version.|
|At a time multiple threads are allowed to operate ArrayList object. Hence it is not thread safe.|At a time only one thread is allowed to operate Vector object. Hence it is thred safe.|
|There is not waiting threads effectively performance is high.|There is a waiting threads effectively performance is low.|

## Stack

- It is a child class of Vector class.
- If we depend upon Last In First Out(LIFO) order then we need to use Stack.

## Set Interface

- It is a child interface of Collection interface.
- If we want to represent group of individual objects in a single entity where duplicate objects are not allowed and order is not preserved then we need to use Set interface.

## Set.of()

- It is introduced in Java 9.
- It gives immutable object.
- It does not allow duplicates.
- It does not accept null values.

## Set Implementations

## HashSet

- The underlying data structure is Hashtable.
- Duplicate objects are not allowed.
- Insertion order is not preserved.
- Hetrogeneous objects are allowed.
- Null insertion is possible.

## HashSet vs LinkedHashSet

|   |   |
|---|---|
|HashSet|LinkedHashSet|
|The underlying data structure is Hashtable.|The underlying data structure is Hashtable and LinkedList.|
|Insertion order is not preserved.|Insertion order is preserved.|
|It is introduced in 1.2 version.|It is introduced in 1.4 version.|

## TreeSet

- The underlying data structure Balanced Tree.
- Duplicate objects are not allowed.
- Insertion order is not preserved because it takes sorting order of an hashcode.
- Hetrogenous objects are not allowed otherwise we will ClassCastException.
- Null insertion is not possible otherwiser we will get NullPointerException.

## Comparable vs Comparator

|   |   |
|---|---|
|Comparable|Comparator|
|Comparable is an interface which is present in java.lang package.|Comparator is an interface which is present in java.util package.|
|Comparable interface contains only one method i.e compareTo() method.|Comparator interface contains following two methods i.e compare() and equals() method.|
|If we depend upon default natural sorting order then we need to use Comparable interface.|If we depend upon customized sorting order then we need to use Comparator interface.|

## Map Interface

- It is not a child interface of Collection interface.
- If we want to represent group of individual objects in key and value pair then we need to use Map interface.
- key and value both must be objects.
- Key can't be duplicate but value can be duplicate.
- Each key and value pair is called one-entry.

## Map.of()

- It is introduced in java 9.
- It gives immutable objects.
- key and value can't be null.

## Map Implementations

## HashMap

- The underlying data structure is Hashtable.
- Key can't be duplicate but value can be duplicate.
- Insertion order is not preserved because it takes hashcode of the key.
- Key and value both can be hetrogeneous.
- Key and value both can be null.

## HashMap vs LinkedHashMap

|   |   |
|---|---|
|HashMap|LinkedHashMap|
|The underlying data structure is Hashtable.|The underlying data structure is Hashtable and LinkedList.|
|Insertion is not preserved.|Insertion order is preserved.|
|It is introduced in 1.2 version.|It is introduced in 1.4 version.|

## TreeMap

- The underlying data structure is Red Black Tree.
- Key can't be duplicate but value can be duplicate.
- If we depend upon default natural sorting order then keys must be homogeneous and comparable.
- If we depend upon customized sorting order then keys must be hetrogeneous and non-comparable.
- Key can't be null but value can be null.

## Hashtable

- The underlying data structure is Hashtable.
- Key can't be duplicate but value can be duplicate.
- Insertion order is descending order of the key.
- Key and value both can be hetrogeneous.
- Key and value both can't be null.

Cursors are used to read objects one by one from Collections. There are three types of cursors in Java:

## 1) Enumeration

- Definition: It is used to read objects one by one from legacy Collection objects.
- Methods (2):

- public boolean hasMoreElements()
- public Object nextElement()

- Limitations:

- It is not a universal cursor (only works with legacy collections like Vector).
- Using Enumeration, we can perform read operations but not remove operations.

## 2) Iterator

- Definition: It is used to read objects one by one from any Collection object. Hence, it is a universal cursor.
- Methods (3):

- public boolean hasNext()
- public Object next()
- public void remove()

- Limitations:

- Enumeration and Iterator are used to read objects in the forward direction but not in the backward direction (they are not bi-directional cursors).
- Using Iterator, we can perform read and remove operations, but not adding and replacement of new objects.

## 3) ListIterator

- Definition: 5ListIterator is a child interface of Iterator. It is used to read objects one by one exclusively from List Collection objects.
- Capabilities: It overcomes Iterator's limitations by allowing bi-directional movement. Using ListIterator we can perform read, remove, adding, and replacement of new objects.
- Methods (9):

- Forward: hasNext(), next(), nextIndex()
- Backward: hasPrevious(), previous(), previousIndex()
- Operations: remove(), add(E), set€

## Technical Round Quick Comparison

|   |   |   |   |
|---|---|---|---|
|Feature|Enumeration|Iterator|ListIterator|
|Applicable to|Legacy Collections only|Any Collection (Universal)|List Collections only|
|Direction|Forward only|Forward only|Bi-directional (Forward & Backward)|
|Operations Allowed|Read|Read, Remove|Read, Remove, Add, Replace (Set)|
|Creation|v.elements()|c.iterator()|l.listIterator()|



### Exception Handling

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



### File IO & Serialization

# File Handling (java.io.File)

The File class represents file and directory pathnames. Instantiating a File object does not immediately create a physical file on the disk; it merely checks if the file exists or creates a reference to it.

- exists(): Checks if the file or directory already exists.
- createNewFile(): Creates a new physical file if it does not already exist.
- mkdir(): Creates a new directory.

## Character Streams

## FileWriter & FileReader

These classes communicate directly with physical files to handle character-oriented data.

|   |   |   |   |
|---|---|---|---|
|Class|Purpose|Key Methods|Limitations|
|FileWriter|Writes character data into a file.|write(int), write(char[]), write(String), flush(), close().|Requires manual insertion of line separators (\n).|
|FileReader|Reads character data from a file.|read() (returns unicode value, -1 if end), read(char[]), close().|Reads character by character, which is not convenient.|

## BufferedWriter & BufferedReader

To overcome the limitations of FileWriter and FileReader, these classes provide enhanced reading and writing capabilities. They cannot communicate with files directly and require the support of a Writer or Reader object.

|   |   |   |
|---|---|---|
|Class|Purpose|Key Enhancements|
|BufferedWriter|Enhanced character writing.|Introduces the newLine() method to insert a new line into a file.|
|BufferedReader|Enhanced character reading.|Introduces the readLine() method to read data line-by-line rather than character-by-character.|

## PrintWriter

PrintWriter is an enhanced writer used to write character-oriented data into a file.

- It can communicate directly with a file or take the support of a Writer object.
- The main advantage over FileWriter and BufferedWriter is that it allows inserting any type of data, especially primitive data.
- Provides convenient methods like print() and println() for int, char, String, double, and boolean data types.

## Byte Streams

Byte streams are used to handle data in the form of byte streams.

- FileOutputStream: Used to insert the data in the form of byte of streams.
- FileInputStream: Used to read the data in the form of byte of streams.

## Various Ways to Provide Input in Java

## There are following ways to provide inputs in Java:

- Command Line Argument: Input is captured directly via the String[] args array in the main method.
- BufferedReader Class: Uses new BufferedReader(new InputStreamReader(System.in)) to read input line-by-line.
- Console Class: Uses System.console().readLine() to read input directly from the console.
- Scanner Class: Uses new Scanner(System.in) and provides specific methods like nextInt(), next(), and nextDouble() to parse input types.

## Serialization & Deserialization

## Serialization

- Definition: A process of storing object data into a file, or converting object state to file state.
- Implementation: Requires ObjectOutputStream and FileOutputStream.
- Requirement: We can perform serialization only for serialized objects. To create a serialized object, the class must implement the Serializable marker interface.

## Deserialization

- Definition: A process of taking the data from a file and representing an object, or converting file state to object state.
- Implementation: Requires ObjectInputStream and FileInputStream.
- Requirement: Similar to serialization, it requires the class to implement the Serializable marker interface. It utilizes the readObject() method to reconstruct the object.



### Inner Classes

# Inner Classes in Java

Core Concept: An inner class is simply a class declared inside another class.

- Origin: Introduced in Java 1.1 to fix GUI event-handling bugs, but became highly popular for general programming.
- Rule: Regular inner classes cannot contain static members.
- Compilation: When compiled, Java generates separate .class files (e.g., compiling Outer with an Inner class generates Outer.class and Outer$Inner.class).

## 1. Normal / Regular Inner Class

- What it is: A standard class written directly inside another class.
- How it works: It is deeply tied to the outer class. To create an object of the inner class, you must first create an object of the outer class.
- Object Creation: Outer.Inner i = new Outer().new Inner();

## 2. Static Inner Class

- What it is: An inner class declared with the static keyword.
- How it works: Because it is static, it is independent of the outer class's instances. You do not need an existing outer class object to create it.
- Object Creation: Inner i = new Inner();

## 3. Method Local Inner Class

- What it is: A class declared entirely inside a method block.
- How it works: Its scope is strictly limited to that specific method.
- Purpose: Used when you have complex, repetitive logic that applies only to that specific method and nowhere else in the program.

## 4. Anonymous Inner Class (Detailed)

What it is: A class without a name. It combines class declaration and object instantiation into a single step.

Why use it? Normally, if you have an interface or an abstract class, you cannot create an object from it directly. You have to create a brand-new, separate class that implements or extends it, write the logic, and then create an object of that new class. An Anonymous Inner Class lets you skip all that. It allows you to provide the implementation "on the fly" exactly where you need it, which is perfect for code you only plan to use once.

How it works: You use the new keyword alongside the interface or abstract class name, followed immediately by curly braces {} containing the overriding methods.

## Example (Implementing an Interface on the fly):

```java
interface ATM {  
    public void deposit();  
}

class Test {  
    public static void main(String[] args) {  
         
        // This is the Anonymous Inner Class  
        // We are instantly implementing the ATM interface without creating a separate class file  
        ATM atm = new ATM() {  
            public void deposit() {  
                System.out.println("Deposit Method Executed");  
            }  
        };  
         
        atm.deposit();  
    }  
}
```



### Java 8 Features & Streams

- Functional Interface: An interface with exactly one abstract method (Single Abstract Method / SAM interface). It can contain any number of default, static, and private methods, and is optionally marked with @FunctionalInterface.

- Lambda Expression (()->{}): A concise way to represent functional interfaces without needing a name, return type, or modifier. Used to achieve functional programming.
- Stream API (java.util.stream): Allows functional style programming to perform bulk operations on Collections. Key functions include:

- map(): Modifies elements.
- filter(): Conditionally selects elements.
- sorted(), count(), max(), min(), distinct().
- Stream.concat(): Merges multiple streams.

- forEach() Loop: Introduced in Java 8 to concisely iterate over objects within Collections like Lists, Sets, and Maps.
- Method Reference (::): A special, highly concise type of lambda expression used to call existing methods directly.
- Optional Class (java.util.Optional): Used to perform graceful null checks to avoid NullPointerException. Created using Optional.empty(), Optional.of(), or Optional.ofNullable().

## Functional Interface

A Functional Interface is an interface with exactly one abstract method.

## Example:

```java
@FunctionalInterface  
interface Calculator {  
    int calculate(int a, int b);  
}
```

A Lambda Expression provides the implementation of its abstract method.

```java
Calculator add = (a, b) -> a + b;
```

@FunctionalInterface is optional, but helps ensure the interface has only one abstract method.

## Lambda Expressions

A Lambda Expression is a short way to provide the implementation of a Functional Interface.

### Syntax:

## (parameters) -> expression

## Example:

## (a, b) -> a + b

Used to write concise implementations without creating an anonymous class.

- When you write Calculator f = (a, b) -> a + b;, Java does create an object behind the scenes (an instance of some auto-generated class implementing Calculator), and f points to that object.
- So yes — colloquially people do say "the lambda" to mean that object, but technically: lambda expression → compiled into → an object whose class implements the functional interface, with the abstract method's body = your lambda's logic.

You now have the real foundation solid: functional interface = a contract with exactly one blank to fill in, lambda = the shortest way to fill that blank in.

## Built-in Functional Interfaces

## Available in:

## java.util.function

|   |   |   |   |
|---|---|---|---|
|Interface|Input → Output|Method|What it does|
|Predicate<T>|T → boolean|test()|Tests a condition|
|Function<T,R>|T → R|apply()|Takes input and returns a result|
|Consumer<T>|T → void|accept()|Takes input and performs an action|
|Supplier<T>|() → T|get()|Supplies/returns a value|
|BiPredicate<T,U>|(T,U) → boolean|test()|Tests a condition using two inputs|
|BiFunction<T,U,R>|(T,U) → R|apply()|Takes two inputs and returns a result|
|BiConsumer<T,U>|(T,U) → void|accept()|Takes two inputs and performs an action|
|UnaryOperator<T>|T → T|apply()|Takes and returns the same type|
|BinaryOperator<T>|(T,T) → T|apply()|Takes two same-type inputs and returns the same type|

## Key Specializations

## UnaryOperator<T>  = Function<T, T>

## BinaryOperator<T> = BiFunction<T, T, T>

## Common Chaining Methods

## Predicate → and(), or(), negate()  

## Function  → andThen(), compose(), identity()  

## Consumer  → andThen()

## Method References

A Method Reference is a shorthand for a lambda that directly calls an existing method.

Uses the :: operator.

## Types

|   |   |   |
|---|---|---|
|Type|Syntax|Example|
|Static Method|Class::staticMethod|Integer::parseInt|
|Particular Object|object::method|printer::print|
|Arbitrary Object|Class::method|String::toUpperCase|

## Example:

```java
Function<String, String> upper = String::toUpperCase;
```

## Equivalent lambda:

## text -> text.toUpperCase()

## Constructor References

A Constructor Reference is a shorthand for a lambda that creates an object.

### Syntax:

## ClassName::new

## Example:

```java
Function<String, Employee> create = Employee::new;
```

## Equivalent lambda:

## name -> new Employee(name)

The Functional Interface determines which constructor is called based on its parameters.

## Stream API

Used to process data from collections in a functional style.

## Collection → Stream → Operations → Result

|   |   |
|---|---|
|Type / Operation|What it does|
|stream()|Creates a stream from a collection|
|filter()|Keeps elements matching a condition|
|map()|Transforms each element|
|flatMap()|Flattens nested elements into one stream|
|distinct()|Removes duplicates|
|sorted()|Sorts elements|
|limit(n)|Takes first n elements|
|skip(n)|Skips first n elements|
|peek()|Performs an action while processing elements|

## Terminal Operations

|   |   |
|---|---|
|Operation|What it does|
|forEach()|Performs an action on each element|
|collect()|Collects results into a collection|
|reduce()|Combines elements into one result|
|count()|Counts elements|
|min()|Finds minimum element|
|max()|Finds maximum element|
|findFirst()|Returns first element|
|findAny()|Returns any element|
|anyMatch()|Checks if any element matches|
|allMatch()|Checks if all elements match|
|noneMatch()|Checks if no elements match|

## Stream Pipeline

## Source → Intermediate Operations → Terminal Operation

## Example:

```java
numbers.stream()  
       .filter(n -> n > 5)  
       .map(n -> n * 2)  
       .forEach(System.out::println);
```

## Important:

Intermediate → Returns Stream → Can chain  
Terminal     → Produces Result → Ends Stream

## Collectors

Collectors provides utility methods to collect and process Stream results.

## Used with:

## .collect(...)

|   |   |
|---|---|
|Collector|What it does|
|toList()|Collects elements into a List|
|toSet()|Collects elements into a Set (removes duplicates)|
|joining()|Joins String elements into one String|
|counting()|Counts elements|
|summingInt()|Calculates sum|
|averagingInt()|Calculates average|
|minBy()|Finds minimum element|
|maxBy()|Finds maximum element|
|summarizingInt()|Gets count, sum, min, max, average|
|groupingBy()|Groups elements based on a key|
|partitioningBy()|Divides elements into true and false groups|
|mapping()|Transforms elements inside a collector|
|toMap()|Collects elements into a Map|
|collectingAndThen()|Performs an operation after collecting|
|reducing()|Reduces elements into one result|
|teeing()|Processes stream using two collectors simultaneously|

## Important Mental Models

## groupingBy(element → key)  

## Same key → Same group

groupingBy(  
    WHERE to group,  
    WHAT to do with each group  
)

toMap(  
    Key mapper,  
    Value mapper  
)

## Important Gotchas

## toSet() → Removes duplicates  

## joining() → Works with String/CharSequence elements  

toMap() → Duplicate keys throw an exception  
          unless a merge function is provided  

## counting() → Returns Long

## Most Important

toList()  
toSet()  
joining()  
groupingBy()  
partitioningBy()  
mapping()  
counting()  
summarizingInt()  
toMap()

## Optional<T>

- Container representing a value that may be present or absent.
- Makes possible null explicit and reduces unsafe null handling.

## Creation

## Optional.of(value)

- Value must be non-null.
- Null → NullPointerException.

## Optional.ofNullable(value)

- Use when value may be null.
- Null → Optional.empty().

## Optional.empty()

- Represents no value.

## Getting Value

## get()

- Returns value.
- Empty → NoSuchElementException.
- Avoid blind usage.

## orElse(value)

- Returns value or default.
- Default is eagerly evaluated.

## orElseGet(() -> value)

- Returns value or lazy default.
- Supplier executes only if Optional is empty.

## orElseThrow()

- Returns value or throws exception.
- Can provide custom exception.

## Transforming

## map()

- Transforms contained value.
- Mapper returns a normal value.

## flatMap()

- Use when mapper returns an Optional.
- Prevents Optional<Optional<T>>.

## filter()

- Keeps value only if condition is true.
- Otherwise becomes empty.

## Best Interview Difference

## orElse() vs orElseGet()

- orElse() → eager fallback evaluation.
- orElseGet() → lazy fallback evaluation.

## map() vs flatMap()

- map() → function returns normal value.
- flatMap() → function returns Optional.

## Avoid

- Blindly using get()
- Optional.of() for possibly null values
- Returning null from Optional-returning methods
- Using Optional as fields or method parameters
- Optional<List<T>> — use empty collections instead

## One-line Mental Model

of → guaranteed value  
ofNullable → possibly null  
empty → no value  
map → transform  
flatMap → Optional-returning transform  
filter → conditional retention  
orElse → default  
orElseGet → lazy default  
orElseThrow → absence is an error

## Best definition for an interview:

Optional<T> is a container that explicitly represents the presence or absence of a value, helping make null handling safer and APIs more expressive.



### Multi-Threading & Concurrency

Based on your instructions, here is the organized, focused, and code-minimized summary of your notes for technical round preparation.

# Section 3 (Core Utilities) -> Multi-Threading & Concurrency

- Thread vs. Process:

- A thread is a lightweight sub-process (e.g., screen share, chat box). Multiple threads run concurrently and can communicate with each other.
- A process is a collection of threads (e.g., Zoom Meeting). Multiple processes run concurrently but are independent and cannot communicate with each other.

- Multitasking: Executing several tasks simultaneously.

- Thread-based: Tasks are part of the same program; best suited for the programmatic level.
- Process-based: Tasks are independent processes; best suited for the OS level.

- Multi-Threading Basics: Executing several threads simultaneously to implement multimedia graphics, video games, and animations. In Java, the API handles 90% of the multithreading work.
- Ways to Create a Thread:

- Extending the Thread class.
- Implementing the Runnable interface.

- Thread Execution & Schedulers:

- Thread Scheduler: Decides execution order when multiple threads wait. The mechanism depends on the JVM vendor, meaning execution order or exact output cannot be expected.
- t.start() vs t.run(): Calling start() creates a new thread that executes run() automatically. Calling run() directly does not create a thread and executes like a normal method.

- Thread Lifecycle State: Born/New -> Ready/Runnable (after start()) -> Running (when allocated CPU) -> Dead (when run() completes).
- Thread Names & Priorities:

- Threads have explicitly provided or JVM-generated names (e.g., setName(), getName()).
- Priority ranges from 1 (MIN_PRIORITY) to 10 (MAX_PRIORITY), with 5 as NORM_PRIORITY. Exceeding 10 throws an IllegalArgumentException.
- Highest priority threads execute first; execution order for same-priority threads is unpredictable.

- Daemon Thread: A low-priority background thread (like Garbage Collector) providing services to user threads. It dies automatically when all user threads die.
- Preventing Execution:

- yield(): Pauses the current thread to give a chance to other waiting threads of the same priority.
- join(): Makes a thread wait until the completion of another specific thread; throws InterruptedException.
- sleep(): Pauses a thread for a specific duration; throws InterruptedException.

- Synchronization:

- Addresses data inconsistency and thread interference by allowing only one thread to execute at a time using a lock mechanism.
- Applicable to methods and blocks.
- Provides thread safety but increases thread waiting time, affecting performance.
- Static Synchronization: The lock is placed on the class rather than the object.

- Inter-Thread Communication:

- Achieved via wait(), notify(), and notifyAll() methods present in the Object class.
- Requires a synchronized area. wait() immediately releases the lock, while notify()/notifyAll() do not.

- Deadlocks: Occurs when two threads are mutually waiting for an object lock acquired by the other, and neither is able to release their lock.



### Packages & Enums

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



### Regex

# Step 1: The 4 String Methods (just the shape, no regex yet)

```java
str.matches(pattern)              // true/false — does WHOLE string fit the pattern?  
str.replaceAll(pattern, newText)  // replace ALL matches  
str.replaceFirst(pattern, newText)// replace only FIRST match  
str.split(pattern)                // break string into array  
```

### Step 2: Literal characters (simplest possible regex)

A regex with just plain letters matches those exact letters. No symbols yet.

```java
"cat".matches("cat");     // true  -> exact match  
"cat".matches("dog");     // false  
"cat".matches("ca");      // false -> matches() needs the WHOLE string, not part
```

Nothing fancy here. Understood? Now we add power one symbol at a time.

### Step 3: . — matches ANY one character

```java
"cat".matches("c.t");   // true  -> . matched 'a'  
"cot".matches("c.t");   // true  -> . matched 'o'  
"cbt".matches("c.t");   // true  -> . matched 'b'  
"ct".matches("c.t");    // false -> . must match exactly ONE character, but none exists here  
"caat".matches("c.t");  // false -> too many characters, . only covers ONE spot
```

So . = "any single character, exactly one slot." Nothing about "many" yet — that's next.

### Step 4: Quantifiers — HOW MANY times does the previous thing repeat?

This is the part you got confused on. A quantifier always applies to the single character/group right before it. Let's build it up one symbol at a time.

## ? — the thing before it appears 0 or 1 times (optional)

```java
"color".matches("colou?r");   // true  -> u appeared 0 times... wait let's check  
"colour".matches("colou?r");  // true  -> u appeared 1 time
```

Here u? means "u is optional." Both color and colour match.

* — the thing before it appears 0 or MORE times

```java
"ct".matches("ca*t");     // true  -> 'a' appeared 0 times  
"cat".matches("ca*t");    // true  -> 'a' appeared 1 time  
"caaat".matches("ca*t");  // true  -> 'a' appeared 3 times  
"cbt".matches("ca*t");    // false -> 'b' is not 'a', doesn't matter how many
```

a* means "zero or more a's." It does NOT mean "any character repeated" — only the specific thing right before the * repeats.

+ — the thing before it appears 1 or MORE times (this is the one I used too early last time)

```java
"ct".matches("ca+t");     // false -> need AT LEAST 1 'a', got 0  
"cat".matches("ca+t");    // true  -> 1 'a'  
"caaat".matches("ca+t");  // true  -> 3 a's, still fine
```

So a+ = "one or more a's." Difference from *: + requires at least 1, * allows 0.

## {n}, {n,}, {n,m} — exact/range counts

```java
"caat".matches("ca{2}t");     // true  -> exactly 2 a's  
"cat".matches("ca{2}t");      // false -> only 1 a, needed exactly 2  
"caaaat".matches("ca{2,4}t"); // true  -> 4 a's, within range 2 to 4  
"caaaaat".matches("ca{2,4}t");// false -> 5 a's, too many
```

Now going back to my earlier example: "[a-z]+" meant "one or more of anything in a-z." That + is exactly what you just learned — apply it to a character class, which is next.

### Step 5: Character classes [...] — pick from a set, still just ONE slot

```java
"c".matches("[abc]");     // true  -> c is in the set {a,b,c}  
"d".matches("[abc]");     // false -> d is not in the set  
"5".matches("[0-9]");     // true  -> range shorthand, 0 through 9  
"g".matches("[a-z]");     // true  -> range a through z
```

[...] by itself is still ONE character slot — same rule as ., just restricted to a set instead of "anything."

Now combine with quantifier, same rule as before — quantifier applies to whatever is immediately to its left:

```java
"hello".matches("[a-z]+");   // true -> "one or more chars from a-z" — NOW this makes sense  
"Hello".matches("[a-z]+");   // false -> H is uppercase, not in [a-z]  
"12345".matches("[0-9]+");   // true  
```

### Step 6: Predefined Character Classes — just shortcuts for common [...]

These save you from typing [0-9], [a-zA-Z0-9_] etc. every time. Still ONE slot, same quantifier rules apply.

\d   ==  [0-9]              // digit  
\D   ==  [^0-9]              // NOT a digit (^ inside [] means "opposite")  
\w   ==  [a-zA-Z0-9_]        // word char (letters, digits, underscore)  
\W   ==  [^a-zA-Z0-9_]        // NOT a word char  
\s   ==  [ \t\n\r]            // whitespace (space, tab, newline...)  
\S   ==  [^ \t\n\r]            // NOT whitespace

⚠️ In Java code you must double the backslash: "[\\d](file://d)" not "\d" (single \ in a Java string is an escape character for the string itself, so Java needs \\ to actually produce one \ for the regex engine).

## Examples — same drill as before:

```java
"5".matches("\\d");        // true  
"a".matches("\\d");        // false  
"12345".matches("\\d+");   // true -> one or more digits  
"12a45".matches("\\d+");   // false -> 'a' breaks it, whole string must match

"hello_123".matches("\\w+"); // true -> letters+digits+underscore all allowed  
"hello 123".matches("\\w+"); // false -> space is NOT a word char

"   ".matches("\\s+");     // true -> one or more whitespace  
"a b".matches("\\s+");     // false -> 'a' and 'b' aren't whitespace, whole string fails
```

That's really it — \d, \w, \s are just named shortcuts for [...] sets you already understand.

### Step 7: Anchors — ^ and $ (position, not a character)

Big mental shift: anchors don't match a character. They match a position in the string.

^   // means "start of string"  
$   // means "end of string"

Since matches() already forces whole-string matching, ^/$ don't add much with matches(). They matter a LOT with replaceAll() / split() where you're searching inside a bigger string, not matching the whole thing.

```java
"hello world".replaceAll("^h", "H");    
// "Hello world" -> only replaces h if it's at the START

"cat cat cat".replaceAll("cat$", "DOG");  
// "cat cat DOG" -> only replaces cat if it's at the END
```

## \b — word boundary (edge between word-char and non-word-char)

```java
"cat category".replaceAll("\\bcat\\b", "DOG");  
// "DOG category" -> only the standalone word "cat" replaced,  
// NOT the "cat" inside "category" because there's no boundary there
```

## Without \b:

```java
"cat category".replaceAll("cat", "DOG");  
// "DOG DOGegory" -> oops, matched inside "category" too
```

This \b example is a genuinely common interview/practical gotcha — "replace whole word only" always needs \b.

### Step 8: Groups ()

A group lets you treat multiple characters as ONE unit — so you can apply a quantifier to a whole chunk, not just one character.

```java
"hahaha".matches("(ha)+");   // true -> (ha) is one unit, repeated 3 times  
"haha".matches("ha+");        // false -> WITHOUT parens, + only applies to 'a', so this means h + (1 or more a's) -> doesn't match "haha"
```

This is the difference: ha+ vs (ha)+ — same rule as always, quantifier binds to whatever is immediately before it. Without (), that's just the last single character. With (), it's the whole group.

## Groups also let you capture and reuse a piece of the match:

```java
"aabb".replaceAll("(a)", "[$1]");  
// "[a][a]bb" -> $1 refers back to whatever group 1 captured
```

## Remember this one from earlier? Now it should make sense:

```java
"aaabbbccc".replaceAll("(.)\\1+", "$1");  
// (.)   -> capture any ONE character into group 1  
// [\\1+](file://1+)  -> one or more repeats of whatever group 1 captured  
// $1    -> in the replacement, put back just that one character  
// result: "abc"
```

### Step 9: Greedy vs Lazy

By default *, +, {n,m} are greedy — they grab as much as possible.

```java
"<a><b>".replaceAll("<.+>", "X");  
// "X" -> .+ greedily grabbed EVERYTHING from first < to the LAST >
```

Add a ? after the quantifier to make it lazy — grab as little as possible:

```java
"<a><b>".replaceAll("<.+?>", "X");  
// "XX" -> now it stops at the FIRST >, matches <a> and <b> separately
```

⚠️ Note: this ? is different from the earlier "0 or 1" ?. Here, ? right after another quantifier (+?, *?) means "be lazy instead of greedy." Context tells you which meaning applies.



### String Processing

# String in Java

A String is a collection of characters enclosed in double quotes.

1. Immutability Strings in Java are immutable. This means once a String object is created, it cannot be modified. If you attempt to change its value, the JVM will not modify the original object; instead, it will create a completely new object to hold the changed value.

## 2. Comparison: == vs .equals()

- == Operator: Used for reference/address comparison. It checks if two variables point to the exact same object in memory. (Example: new String("raise") == new String("raise") returns false because they are two different objects in memory).
- .equals() Method: Used for content comparison. It checks if the actual text inside the objects is exactly the same (it is case-sensitive). (Example: s1.equals(s2) returns true if both contain "raise").

3. Memory Allocation (Heap vs. SCP) When you create a String using the new keyword (e.g., new String("raise")), Java creates two objects:

- One in the Heap area (which your variable reference points to).
- One in the String Constant Pool (SCP) area.

## Rules of the String Constant Pool (SCP):

- No Duplicates: Object creation in the SCP is optional. The JVM first checks if an object with the same content already exists in the SCP. If it does, it reuses it. If not, it creates a new one.
- Garbage Collection: Even if SCP objects lose all their references, the Garbage Collector cannot touch them.
- Lifecycle: SCP objects are only destroyed when the JVM terminates or shuts down completely.

## String Methods

- length(): Gets the character count. Example: "hi".length() outputs 2

- toUpperCase(): Converts to capital letters. Example: "hi".toUpperCase() outputs "HI"
- toLowerCase(): Converts to small letters. Example: "HI".toLowerCase() outputs "hi"
- concat(): Joins two strings together. Example: "a".concat("b") outputs "ab"

- matches(): Checks if the string matches a regex pattern. Example: "12".matches("\\d+") outputs true
- split(): Breaks the string into an array based on a delimiter. Example: "a b".split(" ") outputs ["a", "b"]
- join(): Merges strings or an array with a separator. Example: String.join("-", "a", "b") outputs "a-b"

- equals(): Checks for exact content match (case-sensitive). Example: "a".equals("A") outputs false
- equalsIgnoreCase(): Checks for content match ignoring case. Example: "a".equalsIgnoreCase("A") outputs true

- charAt(): Gets the character at a specific index position. Example: "abc".charAt(1) outputs 'b'
- replaceAll(): Replaces text using a regex pattern. Example: "a1b".replaceAll("\\d", "") outputs "ab"

- trim(): Removes starting and ending spaces. Example: " a ".trim() outputs "a"

- substring(): Extracts a part of the string starting from an index. Example: "abc".substring(1) outputs "bc"
- indexOf(): Finds the first index position of a character or word. Example: "abc".indexOf('b') outputs 1
- toCharArray(): Converts the string into a character array. Example: "ab".toCharArray() outputs ['a', 'b']
- contains(): Checks if a sequence of characters exists inside the string. Example: "abc".contains("b") outputs true

## StringBuffer

Overview: Unlike String (which creates a new object for every change), StringBuffer allows changes to be made within the same object. It is a mutable sequence of characters, heavily recommended when string content changes frequently.

### Key Features:

- Thread Safety: All methods are synchronized. Only one thread can operate on it at a time, making it thread-safe but slower due to thread waiting times.
- Version: Introduced in Java 1.0.
- Capacity Logic:

- Default capacity is 16.
- When max capacity is reached, the new capacity is calculated as: (current_capacity + 1) * 2.

- If initialized with a String, capacity is: string.length() + 16.

### Constructors:

- StringBuffer(): Creates an empty object with a default capacity of 16.
- StringBuffer(int capacity): Creates an empty object with a specified initial capacity.
- StringBuffer(String s): Creates an object pre-filled with the specified string.

### Extracted Methods:

- capacity(): Returns the current allocated memory (capacity) of the buffer.
- append(String/int): Adds the specified data to the end of the current sequence.
- reverse(): Reverses the entire sequence of characters.
- insert(int index, String word): Inserts a word at the specified index position.
- charAt(int index): Returns the character at the specified index.
- length(): Returns the total number of characters currently in the buffer.
- toString(): Converts the StringBuffer object back into a standard, immutable String.
- delete(int index, int Index); sb.delete(1, 3); Hlo for Hello
- replace(int index, int Indexd, String "String"); sb.replace(1, 3, "Java"); HJavalo

## StringBuilder

Overview: StringBuilder is exactly the same as StringBuffer in functionality and methods, but it is designed for single-threaded environments.

### Key Differences from StringBuffer:

- Thread Safety: Methods are not synchronized. Multiple threads can operate on it simultaneously, meaning it is not thread-safe.
- Performance: Because there is no waiting time for threads, its performance is much higher than StringBuffer.
- Version: Introduced later, in Java 1.5.

Methods: It uses the exact same methods as StringBuffer (e.g., reverse(), append(), toString()).

## StringTokenizer

Overview: Present in the java.util package, StringTokenizer is used to break a string into smaller pieces (tokens) based on a specific delimiter (like a space or a comma). Note: This is considered a legacy utility class. For modern Java applications, using the String.split() method is recommended instead.

### Constructor:

- StringTokenizer(String str, String delimiter): Creates a tokenizer for the given string, using the specified delimiter to split it.

### Extracted Methods:

- countTokens(): Returns the total number of tokens (pieces) available.
- hasMoreTokens(): Returns a boolean (true/false) checking if there are any more tokens left to process.
- nextToken(): Returns the next available token as a String.
- hasMoreElements(): Functions identically to hasMoreTokens(), but returns a boolean.
- nextElement(): Functions identically to nextToken(), but returns an Object instead of a String (requires casting, e.g., (String) st.nextElement()).

## Summary of Usage (The Golden Rule)

- String: Use when content is fixed (Immutable).
- StringBuffer: Use when content changes frequently AND thread safety is required (Mutable, Synchronized, Slower).
- StringBuilder: Use when content changes frequently AND thread safety is NOT required (Mutable, Not Synchronized, Faster).



### Types of Objects & Cloning

# Types of Objects in Java

- Immutable Objects: Cannot be changed after creation. If you attempt to modify it, Java automatically creates a completely new object to hold the changes. (Examples: String, Wrapper classes).
- Mutable Objects: Can be changed after creation. Any modifications are applied directly to the original object without creating a new one. (Examples: StringBuffer, StringBuilder).

## Object Cloning

Cloning is the process of creating an exact duplicate of an object. To enable cloning, a class must implement the Cloneable interface (a marker interface that contains no methods or constants) and utilize the clone() method from the Object class.

## Shallow Cloning vs. Deep Cloning

- Shallow Cloning: Creates an exact duplicate of the object reference. Both variables point to the exact same object in memory (meaning they will share the exact same hashCode). (Example: Test t2 = t1;).
- Deep Cloning: Creates an exact duplicate of the actual object. It allocates new memory for the duplicate, resulting in two completely independent objects (meaning they will have different hashCodes). This is achieved using the clone() method.



### Wrapper Classes

# Wrapper Classes in Java

Core Concept: A Wrapper Class wraps a simple primitive data type (like int or double) into a full Java Object (like Integer or Double).

## 1. Why Do We Need Them?

- To use Collections: Advanced Java structures like ArrayList or HashMap cannot store primitive types. They only accept Objects.
- To access Utility Methods: Primitives only hold values. Wrapper classes come with built-in tools for data conversion (e.g., converting a text "100" into an actual number 100).

## 2. The Primitive to Wrapper Mapping

Everything is capitalized. Note the two exceptions where the name is spelled out fully (Integer, Character).

|   |   |
|---|---|
|Primitive Type|Wrapper Class|
|byte|Byte|
|short|Short|
|int|Integer|
|long|Long|
|float|Float|
|double|Double|
|boolean|Boolean|
|char|Character|

## 3. Key Utility Methods (Data Conversion)

### A. valueOf()

- Purpose: Converts a primitive OR a String into a Wrapper Object.
- Exception: Character only accepts primitive char, not Strings.
- Example:  

```java
    Integer obj1 = Integer.valueOf(10);  
    Integer obj2 = Integer.valueOf("20");
```

### B. parseXxx()

- Purpose: Converts a String directly into a primitive type. Highly used for processing user inputs.
- Example:  

```java
    int a = Integer.parseInt("200");  
    double d = Double.parseDouble("99.99");
```

### C. xxxValue()

- Purpose: Extracts the primitive type out of a Wrapper Object.
- Example:  

```java
    Integer obj = Integer.valueOf(50);  
    int a = obj.intValue();
```

### D. toString()

- Purpose: Converts a primitive or Wrapper Object into text (String).
- Example:  

```java
    String text = Integer.toString(500); // Turns number 500 into word "500"
```

## 4. Special Binary Conversions

## The Integer class has built-in tools to handle binary math:

- Binary String to Decimal Number: Integer.parseInt("1010", 2); (Outputs 10)
- Decimal Number to Binary String: Integer.toBinaryString(15); (Outputs "1111")

## 5. Autoboxing & Autounboxing

Java handles the conversion between primitives and objects automatically behind the scenes to save you time.

- Autoboxing: Automatic conversion from primitive -> Object.

- What you write: Integer i = 10;

- What Java does: Integer i = Integer.valueOf(10);

- Autounboxing: Automatic conversion from Object -> primitive.

- What you write: int a = i; (assuming i is an Integer object)

- What Java does: int a = i.intValue();
