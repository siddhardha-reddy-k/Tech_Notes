# What is a Stream?

A Stream is a sequence of elements supporting aggregate operations. It is not a data structure and generally does not store data. It provides a declarative pipeline for processing data from a source.

Source → Intermediate Operations → Terminal Operation

**Stream vs Collection**

**Collection:** stores and manages data.

**Stream:** processes data.

Key differences:

- Collection can be traversed multiple times; Stream is generally consumed once.
- Collection supports external iteration; Stream uses internal iteration.
- Stream operations are often lazy.
- Stream does not modify the source by default.

**Stream Pipeline**

Three components:

```java
source
    .intermediateOperation()
    .intermediateOperation()
    .terminalOperation();
```

Example:

```java
list.stream()
    .filter(x -> x > 10)
    .map(x -> x * 2)
    .collect(Collectors.toList());
```

**Intermediate vs Terminal Operations**

**Intermediate operations:**

- Return another stream
- Usually lazy
- Build the pipeline

Examples:

filter(), map(), flatMap(), distinct(), sorted(), limit(), skip(), peek()

**Terminal operations:**

- Trigger pipeline execution
- Produce result/side effect
- Consume the stream

Examples:

collect(), forEach(), reduce(), count(), min(), max(), findFirst(), findAny(), anyMatch(), allMatch(), noneMatch()

**Lazy Evaluation**

Intermediate operations do not execute immediately.

Execution generally starts when a terminal operation is invoked.

Benefits:

- Avoid unnecessary processing
- Enables short-circuiting
- Allows efficient pipeline processing

**Internal vs External Iteration**

**External iteration:**

```java
for (String s : list) {
}
```

Developer controls traversal.

Internal iteration:

```java
list.stream().forEach(System.out::println);
```

Stream framework controls traversal.

**Important Operations**

**filter()**

Accepts Predicate<T>.

Keeps matching elements.

```java
.filter(x -> x > 10)
```

**map()**

Accepts Function<T, R>.

Transforms each element.

```java
.map(Employee::getName)
```

Concept:

One input → One output

**flatMap()**

Transforms each element into a stream and flattens the resulting streams.

```java
.flatMap(List::stream)
```

Concept:

Nested streams → Single flat stream

**Interview answer:**

map() performs one-to-one transformation, whereas flatMap() transforms elements into streams and flattens them into a single stream.

**distinct()**

Removes duplicates.

For objects, logical uniqueness depends on correct equals() and hashCode() implementation.

**sorted()**

Stateful intermediate operation.

```java
.sorted()

.sorted(Comparator.comparing(Employee::getSalary))

.sorted(Comparator.comparing(Employee::getSalary).reversed())
```

**limit() and skip()**

```java
.limit(n) // first n elements

.skip(n)  // skip first n elements
```

limit() is short-circuiting.

**peek()**

Mainly for debugging and observing pipeline flow.

Avoid business logic and important side effects inside peek().

**reduce() vs collect()**

**reduce()**

Combines stream elements into one result.

```java
.reduce(0, Integer::sum)
```

Use for immutable reduction:

Many elements → One value

**collect()**

Accumulates elements into a mutable result container.

```java
.collect(Collectors.toList())
```

Use:

Many elements → Collection/Container

**findFirst() vs findAny()**

**findFirst()**

Returns first element respecting encounter order.

```java
.findFirst()
```

**findAny()**

Returns any matching element.

```java
.findAny()
```

Potentially more efficient with parallel streams because ordering constraints can be relaxed.

Both return:

Optional<T>

**forEach() vs forEachOrdered()**

With parallel streams:

```java
parallelStream().forEach(...)
```

Order may not be preserved.

```java
parallelStream().forEachOrdered(...)
```

Preserves encounter order but may reduce parallel performance.

**Matching Operations**

anyMatch()

At least one element matches.

allMatch()

Every element matches.

noneMatch()

No element matches.

All can short-circuit.

**Why Streams Cannot Be Reused**

After a terminal operation, the stream is consumed.

```java
Stream<String> stream = list.stream();

stream.count();
stream.count(); // IllegalStateException
```

Create a new stream for another traversal.

**Stateless vs Stateful Operations**

**Stateless**

Process elements independently.

Examples:

filter()  
map()  
peek()

**Stateful**

Require information about other elements or previously processed elements.

Examples:

distinct()  
sorted()

Stateful operations can require additional memory and may affect performance.

**Short-Circuiting Operations**

Can terminate processing early.

Important examples:

limit()  
findFirst()  
findAny()  
anyMatch()  
allMatch()  
noneMatch()

Useful for large or infinite streams.

**Stream.of() vs Arrays.stream()**

```java
Stream.of("A", "B", "C");
```

Creates a stream from values.

```java
Arrays.stream(array);
```

Creates a stream from an array.

For primitive arrays, prefer Arrays.stream():

```java
int[] numbers = {1, 2, 3};

IntStream stream = Arrays.stream(numbers);
```

**Primitive Streams**

Java provides:

IntStream  
LongStream  
DoubleStream

Advantages:

- Avoid unnecessary boxing/unboxing
- Specialized numeric operations

Example:

```java
employees.stream()
    .mapToInt(Employee::getSalary)
    .average();
```

Useful methods:

sum()  
average()  
min()  
max()  
summaryStatistics()

**Best Interview Mental Model**

When you see a Stream pipeline, analyze it as:

1. What is the source?

2. Which operations are intermediate?

3. Which are stateless/stateful?

4. Which operations are short-circuiting?

5. Where does lazy execution end?

6. What is the terminal operation?

7. What is the final result type?

For example:

```java
employees.stream()
    .filter(e -> e.getSalary() > 50000)
    .map(Employee::getName)
    .sorted()
    .limit(5)
    .collect(Collectors.toList());
```

Answer:

Source: employees

Intermediate:  
filter → stateless  
map → stateless  
sorted → stateful  
limit → short-circuiting  

Terminal: collect

Execution: Lazy until collect() triggers processing

Result: List<String>
