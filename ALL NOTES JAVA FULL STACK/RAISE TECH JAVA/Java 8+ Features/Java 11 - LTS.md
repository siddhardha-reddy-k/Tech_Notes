## Release Overview

Java 11 was released in **2018** and is an **LTS release**.

Main interview-relevant additions:

- String API improvements
    
- Files API improvements
    
- Standard HTTP Client
    
- `var` in lambda parameters
    

---

# 1. String API Improvements

```
"   ".isBlank();

"Java\nSQL".lines();

" Java ".strip();

" Java".stripLeading();

"Java ".stripTrailing();

"Java".repeat(3);
```

### `strip()` vs `trim()`

- `trim()` → older whitespace handling
    
- `strip()` → Unicode-aware
    

---

# 2. Files API Improvements

Simplified reading and writing text files.

```
String data = Files.readString(path);

Files.writeString(path, "Hello");
```

---

# 3. HTTP Client

Java 11 standardized the modern HTTP Client API.

```
HttpClient client = HttpClient.newHttpClient();
```

Supports:

- HTTP/1.1
    
- HTTP/2
    
- Synchronous requests
    
- Asynchronous requests
    

---

# 4. `var` in Lambda Parameters

Java 11 allows `var` in lambda parameters.

```
(var a, var b) -> a + b
```

Useful when annotations are needed on lambda parameters.

---

# Interview Summary

**Java 11 = LTS + String improvements + Files improvements + HTTP Client +** `**var**` **in lambdas**