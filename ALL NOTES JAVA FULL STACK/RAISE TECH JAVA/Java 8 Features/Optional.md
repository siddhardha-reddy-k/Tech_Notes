# Why Optional?

Optional<T> represents the possible presence or absence of a value.

Main benefit:

```java
Employee findById(int id);
```

doesn't communicate whether null is possible.

```java
Optional<Employee> findById(int id);
```

explicitly communicates possible absence.

It helps reduce unsafe null handling and makes APIs more expressive.

**Creating Optional**

**of()**

```java
Optional.of(value);
```

Use only when value is guaranteed non-null.

If value == null:

NullPointerException

**ofNullable()**

```java
Optional.ofNullable(value);
```

Use when value may be null.

non-null → Optional[value]  
null     → Optional.empty()

**empty()**

```java
Optional.empty();
```

Represents absence of value.

Never return null from a method declared to return Optional.

**get()**

```java
optional.get();
```

Returns contained value.

If empty:

NoSuchElementException

Avoid blind usage.

Interview point:

Blindly using get() defeats the purpose of Optional because it replaces a potential NPE with another runtime exception.

**orElse()**

```java
optional.orElse(defaultValue);
```

Returns contained value or fallback.

Fallback is evaluated eagerly.

Good for simple values:

```java
optional.orElse("Unknown");
```

**orElseGet() ⭐⭐⭐⭐⭐**

```java
optional.orElseGet(() -> createDefault());
```

Accepts a Supplier.

Fallback is evaluated lazily, only when Optional is empty.

Use for expensive fallback creation.

**orElse() vs orElseGet()**

| orElse() | orElseGet() |
| --- | --- |
| Takes actual value | Takes Supplier |
| Eager evaluation | Lazy evaluation |
| Fallback always evaluated | Fallback evaluated only if empty |
| Good for constants | Good for expensive operations |

Example:

```java
optional.orElse(createObject());
```

createObject() executes even if value exists.

```java
optional.orElseGet(() -> createObject());
```

createObject() executes only if Optional is empty.

**Best interview answer:**

orElse() eagerly evaluates its fallback argument, while orElseGet() lazily invokes a Supplier only when the Optional is empty.

**orElseThrow()**

```java
optional.orElseThrow();
```

Throws NoSuchElementException if empty.

Custom exception:

```java
optional.orElseThrow(
    () -> new ResourceNotFoundException()
);
```

Very common in service-layer backend code.

**map()**

Transforms contained value.

```java
Optional<String> name =
    employee.map(Employee::getName);
```

Optional<Employee>  
       ↓  
Optional<String>

If empty, remains empty.

Use when mapper returns a normal value.

**flatMap()**

Use when mapper already returns an Optional.

Bad:

```java
Optional<Optional<Address>> result =
    employee.map(Employee::getAddressOptional);
```

Correct:

```java
Optional<Address> result =
    employee.flatMap(Employee::getAddressOptional);
```

**map() vs flatMap()**

map:  
Optional<T> → function returns R → Optional<R>

flatMap:  
Optional<T> → function returns Optional<R> → Optional<R>

**filter()**

Keeps the value only when predicate matches.

```java
optional.filter(e -> e.getSalary() > 50000);
```

If condition fails:

Optional.empty()

**Optional vs Stream**

| Optional | Stream |
| --- | --- |
| Zero or one value | Zero to many values |
| Represents possible absence | Processes sequences |
| map, flatMap, filter | map, flatMap, filter |
| Empty propagates through chain | Elements flow through pipeline |

**Where Optional Should NOT Be Used ⭐⭐⭐⭐⭐**

**Avoid as fields**

```java
private Optional<String> name;
```

Usually unnecessary and can complicate serialization/frameworks.

Prefer nullable field internally and expose Optional from getter if appropriate.

**Avoid as method parameters**

Avoid:

```java
void method(Optional<String> value)
```

Usually makes APIs awkward.

Prefer normal parameters, overloading, builders, or other domain modeling.

**Avoid wrapping collections**

Avoid:

```java
Optional<List<Employee>>
```

Prefer:

```java
List<Employee>
```

Return:

```java
Collections.emptyList()
```

An empty collection already represents no elements.

**Don't make Optional itself null**

Bad:

```java
Optional<String> value = null;
```

Correct:

```java
Optional<String> value = Optional.empty();
```

**Common Interview Mistakes**

```java
Optional.of(possiblyNullValue); // Wrong if null possible
```

Use:

```java
Optional.ofNullable(possiblyNullValue);
```

```java
return null; // from Optional-returning method
```

Use:

```java
return Optional.empty();
```

```java
optional.get();
```

without guaranteeing presence.

Prefer:

```java
orElse()
orElseGet()
orElseThrow()
```

```java
optional.orElse(expensiveOperation());
```

Prefer:

```java
optional.orElseGet(() -> expensiveOperation());
```

**Best Interview Mental Model**

```text
Optional<T>
      │
      ├── Guaranteed non-null value → of()
      │
      ├── Possibly null value → ofNullable()
      │
      ├── No value → empty()
      │
      ├── Transform → map()
      │
      ├── Optional-returning transform → flatMap()
      │
      ├── Conditional retention → filter()
      │
      ├── Default → orElse()
      │
      ├── Lazy default → orElseGet()
      │
      └── Absence is error → orElseThrow()
```
