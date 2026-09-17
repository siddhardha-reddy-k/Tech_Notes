## Release Overview

Java 21 was released in **2023** and is an **LTS release**.

Main interview-relevant features:

- Virtual Threads
    
- Pattern Matching for `switch`
    
- Record Patterns
    
- Sequenced Collections
    

---

# 1. Virtual Threads

Lightweight threads managed by the JVM.

```
Thread.startVirtualThread(() -> {
    System.out.println("Task");
});
```

Best suited for highly concurrent, especially I/O-heavy applications.

Important:

- Cheaper than traditional platform threads
    
- Allows very large numbers of concurrent tasks
    
- Does not make CPU-bound work automatically faster
    

---

# 2. Pattern Matching for `switch`

Allows `switch` to match types directly.

```
String result = switch (obj) {
    case Integer i -> "Integer: " + i;
    case String s  -> "String: " + s;
    default        -> "Unknown";
};
```

Reduces repeated `instanceof` checks and casting.

---

# 3. Record Patterns

Allows direct extraction of record components.

```
record Point(int x, int y) {}

if (obj instanceof Point(int x, int y)) {
    System.out.println(x);
    System.out.println(y);
}
```

Mental model:

```
Record         → stores structured data
Record Pattern → extracts structured data
```

---

# 4. Sequenced Collections

Introduced common APIs for collections with a defined encounter order.

Main interfaces:

```
SequencedCollection
SequencedSet
SequencedMap
```

Common operations include:

```
getFirst()
getLast()
addFirst()
addLast()
removeFirst()
removeLast()
reversed()
```

Provides a consistent way to work with first, last, and reversed order.

---

# Interview Summary

```
Java 21 → LTS
├── Virtual Threads
├── Pattern Matching for switch
├── Record Patterns
└── Sequenced Collections
```

**Most important:** Virtual Threads