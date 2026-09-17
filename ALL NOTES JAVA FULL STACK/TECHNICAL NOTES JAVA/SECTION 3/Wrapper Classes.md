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
