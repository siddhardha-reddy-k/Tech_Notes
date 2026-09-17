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
