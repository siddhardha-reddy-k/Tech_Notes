# Java 8 Functional Programming — Cheat Sheet

> Goal: This is not a detailed explanation document.  
> Use it to quickly reactivate concepts after forgetting them.  
> First try recalling from the questions without looking at the answers/examples.

---

# 1. The Big Picture

```
Functional Interface
        ↓
Lambda / Method Reference
        ↓
Behavior can be passed around
        ↓
Used in Streams / Optional / APIs
```

---

# 2. Functional Interfaces

|Interface|Input|Output|Main Method|
|---|---|---|---|
|`Predicate<T>`|T|boolean|`test()`|
|`Function<T, R>`|T|R|`apply()`|
|`Consumer<T>`|T|nothing|`accept()`|
|`Supplier<T>`|nothing|T|`get()`|

### Mental Model

```
Predicate → asks a question
Function  → transforms something
Consumer  → does something
Supplier  → provides something
```

### Examples

```
Predicate<Integer> isEven = n -> n % 2 == 0;

Function<String, String> upper = String::toUpperCase;

Consumer<String> print = System.out::println;

Supplier<Integer> number = () -> 100;
```

---

# 3. Functional Interface Chaining

## Predicate

```
p1.and(p2)
p1.or(p2)
p1.negate()
```

Mental model:

```
and     → both conditions
or      → either condition
negate  → reverse condition
```

---

## Function

```
function1.andThen(function2)
```

```
Input → function1 → function2
```

```
function1.compose(function2)
```

```
Input → function2 → function1
```

---

## Consumer

```
consumer1.andThen(consumer2)
```

```
Input → consumer1 → consumer2
```

---

# 4. Lambda → Method Reference

Use a method reference when the lambda only forwards arguments to an existing method.

```
x -> x.toUpperCase()
```

↓

```
String::toUpperCase
```

Examples:

```
x -> x.length()
```

↓

```
String::length
```

```
x -> System.out.println(x)
```

↓

```
System.out::println
```

```
(a, b) -> Integer.compare(a, b)
```

↓

```
Integer::compare
```

---

# 5. Stream Pipeline

```
Source
  ↓
Intermediate Operations
  ↓
Terminal Operation
```

Example:

```
numbers.stream()
       .filter(...)
       .map(...)
       .sorted()
       .collect(...);
```

---

# 6. Intermediate Operations

## `filter()`

Keep matching elements.

```
.filter(n -> n % 2 == 0)
```

```
[1, 2, 3, 4]
↓
[2, 4]
```

---

## `map()`

Transform each element.

```
.map(n -> n * 10)
```

```
[1, 2, 3]
↓
[10, 20, 30]
```

---

## `flatMap()`

Each element becomes another Stream, then all inner streams are flattened into one Stream.

```
Stream<T>
   ↓
Each element → Stream<R>
   ↓
Flatten
   ↓
Stream<R>
```

Example:

```
.flatMap(List::stream)
```

Sentence example:

```
.flatMap(sentence ->
    Arrays.stream(sentence.split(" "))
)
```

Mental trigger:

> Nested structure / one item produces multiple items → think `flatMap()`.

---

## `distinct()`

Remove duplicates.

```
.distinct()
```

---

## `sorted()`

Sort elements.

```
.sorted()
```

Custom sorting:

```
.sorted(Comparator.comparingInt(String::length))
```

Descending:

```
.sorted(
    Comparator.comparingInt(String::length)
              .reversed()
)
```

---

## `skip()`

Ignore first `n` elements.

```
.skip(2)
```

---

## `limit()`

Take only first `n` elements.

```
.limit(3)
```

---

# 7. Terminal Operations

## `forEach()`

Perform an action for each element.

```
.forEach(System.out::println)
```

---

## `collect()`

Collect the Stream into another structure.

```
.collect(Collectors.toList())
```

---

## `reduce()`

Combine many elements into one.

Sum:

```
.reduce(0, (a, b) -> a + b)
```

Multiply:

```
.reduce(1, (a, b) -> a * b)
```

---

## `count()`

Count elements.

```
.count()
```

---

## Match Operations

```
.anyMatch(...)
```

→ At least one?

```
.allMatch(...)
```

→ Every item?

```
.noneMatch(...)
```

→ No items?

---

## `findFirst()`

Get the first matching result.

```
.findFirst()
```

Returns `Optional<T>`.

---

## `min()` / `max()`

```
.min(Integer::compare)

.max(Integer::compare)
```

Important:

```
Comparator → defines ordering

min() → selects smallest according to ordering
max() → selects largest according to ordering
```

---

# 8. Collectors

## `toList()`

```
.collect(Collectors.toList())
```

```
Stream → List
```

---

## `joining()`

Join Strings.

```
.collect(Collectors.joining(", "))
```

Example:

```
Sam, Raj, Anna
```

---

## `groupingBy()`

Group elements based on a calculated key.

```
.collect(
    Collectors.groupingBy(String::length)
)
```

Result:

```
Map<Key, List<Item>>
```

Example:

```
Sam  → 3
Raj  → 3
Anna → 4

↓

3 → [Sam, Raj]
4 → [Anna]
```

Mental trigger:

> Multiple possible groups based on some key → `groupingBy()`.

---

## `partitioningBy()`

Split elements into two groups.

```
.collect(
    Collectors.partitioningBy(
        n -> n % 2 == 0
    )
)
```

Result:

```
Map<Boolean, List<Item>>
```

```
true  → matching items
false → non-matching items
```

Mental trigger:

> Only true / false groups → `partitioningBy()`.

---

# 9. Quick Decision Guide

```
Need to remove items?
→ filter()

Need to transform items?
→ map()

Nested lists / split strings into multiple values?
→ flatMap()

Remove duplicates?
→ distinct()

Arrange elements?
→ sorted()

Ignore first elements?
→ skip()

Take limited elements?
→ limit()

Perform action?
→ forEach()

Save result?
→ collect()

Many values → one value?
→ reduce()

Find smallest/largest?
→ min() / max()

Check conditions?
→ anyMatch() / allMatch() / noneMatch()

Group by categories?
→ groupingBy()

Split into true/false?
→ partitioningBy()
```

---

# 10. Recall Questions

## Functional Interfaces

### Question 1

You receive a `String` and need to check whether its length is greater than 5.

Which Functional Interface would you use?

---

### Question 2

You receive a `String` and need to convert it to uppercase.

Which Functional Interface would you use?

---

### Question 3

You receive an object and only need to print/process it without returning anything.

Which Functional Interface would you use?

---

### Question 4

You need to generate/provide a value without receiving any input.

Which Functional Interface would you use?

---

# Stream Recall Problems

## Question 5

Given:

```
List<Integer> numbers =
    List.of(1, 2, 3, 4, 5, 6);
```

Get only even numbers and multiply them by 10.

What operations would you use?

---

## Question 6

Given:

```
List<List<Integer>> numbers;
```

Convert all nested lists into one flat list.

Which operation should immediately come to your mind?

---

## Question 7

Given:

```
List<String> sentences =
    List.of(
        "Java is fun",
        "Streams are powerful"
    );
```

Convert all sentences into individual words.

What combination involving `flatMap()` would you use?

---

## Question 8

Given a list of names:

- Remove duplicates
    
- Convert to uppercase
    
- Sort alphabetically
    
- Collect into a List
    

Try writing the pipeline without looking at notes.

---

## Question 9

Given numbers:

```
[1, 2, 3, 4, 5, 6, 7, 8]
```

Skip the first 2 and take the next 3.

Which operations?

---

## Question 10

Given a list of numbers:

Find the smallest and largest values.

What methods and Comparator would you use?

---

# Collectors Recall Problems

## Question 11

Given:

```
List<String> names =
    List.of("Sam", "Raj", "Anna");
```

Convert it into:

```
Sam | Raj | Anna
```

Which Collector?

---

## Question 12

Given employees or names, group them based on a calculated property such as:

```
name length
department
age
```

Which Collector?

What is the default result structure?

---

## Question 13

Split numbers into:

```
Even
Odd
```

Which Collector?

What are the keys of the resulting Map?

---

# Combined Recall Problems

## Question 14

Given multiple sentences:

1. Extract all words
    
2. Convert to lowercase
    
3. Remove duplicates
    
4. Sort alphabetically
    
5. Join into one String
    

Try writing the entire pipeline.

---

## Question 15

Given numbers:

1. Keep numbers greater than 10
    
2. Remove duplicates
    
3. Sort
    
4. Skip the first result
    
5. Take the next 3
    
6. Multiply by 2
    
7. Collect into a List
    

Write the pipeline from memory.

---

# Final Mental Model

```
Functional Interface
        ↓
Lambda / Method Reference
        ↓
Pass behavior
        ↓
Stream Pipeline

Source
 ↓
Intermediate Operations
 ↓
Intermediate Operations
 ↓
Terminal Operation
```

> Don't try to memorize every method.
> 
> When solving a problem, first identify:
> 
> **What needs to happen to the data?**
> 
> Then choose the Stream operation that matches that transformation.