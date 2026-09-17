# Core Concept

A Collector defines how stream elements are accumulated into a final result.

Stream → collect(Collector) → Result

Examples: toList(), toSet(), toMap(), joining(), groupingBy(), partitioningBy()

collect() is terminal; Collectors provides collection strategies.

**toList()**

```java
List<String> names = stream.collect(Collectors.toList());
```

Collects elements into a List.

Do not rely on a specific implementation being returned.

**toSet()**

```java
Set<String> result = stream.collect(Collectors.toSet());
```

Removes duplicates based on equals() and hashCode().

**toMap()**

Basic:

```java
Collectors.toMap(
    keyMapper,
    valueMapper
)
```

Example:

```java
Map<Integer, String> map = employees.stream()
    .collect(Collectors.toMap(
        Employee::getId,
        Employee::getName
    ));
```

Duplicate keys throw an exception unless a merge function is provided.

```java
Collectors.toMap(
    keyMapper,
    valueMapper,
    mergeFunction
)
```

Keep first:

```java
(a, b) -> a
```

Keep latest:

```java
(a, b) -> b
```

Highest salary:

```java
BinaryOperator.maxBy(
    Comparator.comparing(Employee::getSalary)
)
```

Function.identity() means: x -> x

Useful:

```java
toMap(Employee::getId, Function.identity())
```

**joining()**

Joins CharSequence elements into one String.

```java
joining()

joining(", ")

joining(", ", "[", "]")
```

Example:

```java
String names = employees.stream()
    .map(Employee::getName)
    .collect(Collectors.joining(", "));
```

**counting()**

```java
Collectors.counting()
```

Equivalent in simple cases to:

```java
stream.count()
```

Most useful as a downstream collector:

```java
groupingBy(
    Employee::getDepartment,
    counting()
)
```

**groupingBy()**

Basic:

```java
groupingBy(classifier)
```

Example:

```java
Map<String, List<Employee>> result =
    employees.stream()
        .collect(groupingBy(Employee::getDepartment));
```

With downstream collector:

```java
groupingBy(
    classifier,
    downstreamCollector
)
```

**Examples:**

Count:

```java
groupingBy(
    Employee::getDepartment,
    counting()
)
```

Average:

```java
groupingBy(
    Employee::getDepartment,
    averagingDouble(Employee::getSalary)
)
```

Maximum:

```java
groupingBy(
    Employee::getDepartment,
    maxBy(Comparator.comparing(Employee::getSalary))
)
```

**Downstream Collector — Key Concept**

A downstream collector defines what happens **inside each group**.

Pattern:

```java
groupingBy(
    classifier,
    downstreamCollector
)
```

This is one of the most important concepts in Collectors.

**mapping()**

Usually used as a downstream collector.

```java
mapping(
    mapper,
    downstreamCollector
)
```

Example:

```java
groupingBy(
    Employee::getDepartment,
    mapping(
        Employee::getName,
        toList()
    )
)
```

Meaning:

Group employees by department, then convert employees to names inside each group.

**partitioningBy()**

Partitions based on a boolean predicate.

```java
partitioningBy(predicate)
```

Result:

Map<Boolean, List<T>>

Example:

```java
partitioningBy(
    e -> e.getSalary() > 70000
)
```

Creates:

true → matching employees  
false → non-matching employees

With downstream collector:

```java
partitioningBy(
    predicate,
    counting()
)
```

**groupingBy() vs partitioningBy()**

| groupingBy | partitioningBy |
| --- | --- |
| Uses classifier | Uses Predicate |
| Multiple groups | Boolean partitions |
| Keys can be many values | Keys are true/false |

**summarizingInt()**

Returns:

IntSummaryStatistics

Provides:

getCount()  
getSum()  
getMin()  
getMax()  
getAverage()

Example:

```java
employees.stream()
    .collect(
        Collectors.summarizingInt(Employee::getAge)
    );
```

Also:

summarizingLong()  
summarizingDouble()

**collectingAndThen()**

Performs an additional transformation after another collector finishes.

Pattern:

```java
collectingAndThen(
    downstreamCollector,
    finisher
)
```

Example:

```java
collectingAndThen(
    toList(),
    Collections::unmodifiableList
)
```

Very common with maxBy():

```java
groupingBy(
    Employee::getDepartment,
    collectingAndThen(
        maxBy(Comparator.comparing(Employee::getSalary)),
        Optional::get
    )
)
```

**Collector Internal Components**

Conceptually, a Collector has:

Supplier  
Accumulator  
Combiner  
Finisher

**Supplier**

Creates result container.

**Accumulator**

Adds elements.

**Combiner**

Combines partial results, important for parallel streams.

**Finisher**

Transforms accumulated result into final result.

This explains advanced collectors and collectingAndThen().

**Most Important Interview Pattern**

Memorize the reasoning, not just syntax:

```text
groupingBy(
    What determines the group?,
    What should happen inside each group?
)
```

Examples:

Department → List<Employee>  
Department → Count  
Department → Average Salary  
Department → Max Salary Employee  
Department → List<Employee Names>

Code patterns:

```java
// Group
groupingBy(Employee::getDepartment)

// Count
groupingBy(Employee::getDepartment, counting())

// Names
groupingBy(
    Employee::getDepartment,
    mapping(Employee::getName, toList())
)

// Highest paid
groupingBy(
    Employee::getDepartment,
    maxBy(comparing(Employee::getSalary))
)

// Highest paid without Optional
groupingBy(
    Employee::getDepartment,
    collectingAndThen(
        maxBy(comparing(Employee::getSalary)),
        Optional::get
    )
)
```

**Final Interview Insight**

Most Collector interview questions are variations of this flow:

1. Do I need a List/Set/Map?
   ↓
2. Do I need grouping?
   ↓
3. What determines the key?
   ↓
4. What should happen inside each group?
   ↓
5. Do I need a downstream collector?
   ↓
6. Do I need a final transformation?
