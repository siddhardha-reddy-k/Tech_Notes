# Operators in Java

Operator precedence decides which operator is evaluated first when multiple operators are used in the same expression.

## Order (highest to lowest priority)

| Priority    | Operators                 | Example              |
| ----------- | ------------------------- | -------------------- |
| 1 (highest) | `()` parentheses          | `(2 + 3) * 4`        |
| 2           | `++ --` (unary), `!`, `~` | `-a`, `!flag`, `a++` |
| 3           | `* / %`                   | `a * b`, `a % b`     |
| 4           | `+ -` (binary)            | `a + b`, `a - b`     |
| 5           | `< <= > >=`               | comparisons          |
| 6           | `== !=`                   | equality             |
| 7           | `&&`                      | logical AND          |
| 8           | \|\|                      | logical OR           |
| 9 (lowest)  | `= += -= *= /= %=`        | assignment           |

An operator is a symbol used to perform operations on operands.

Example:

```java
c = a + b;
```

`+` and `=` are operators, while `a`, `b`, and `c` are operands.

---

# Types of Operators in Java

## 1. Arithmetic Operators

Used to perform mathematical operations.

```text
+   Addition
-   Subtraction
*   Multiplication
/   Division
%   Remainder
```

Precedence:

```text
* / %   → higher
+ -     → lower
```

### Integer vs Floating-Point Division

```java
System.out.println(5 / 2);    // 2
System.out.println(5 / 2.0);  // 2.5
```

Rule:

```text
int / int → integer division

If a floating-point operand is involved
→ floating-point division
```

### Division by Zero

Integral constant division by zero:

```java
10 / 0;   // CTE
10 % 0;   // CTE
```

With a variable:

```java
int x = 0;
System.out.println(10 / x);
```

Result:

```text
RTE — ArithmeticException
```

Floating-point division by zero:

```java
System.out.println(10.0 / 0); // Infinity
System.out.println(0.0 / 0);  // NaN
```

---

## 2. Assignment Operators

Used to assign or update values.

```text
=
+=
-=
*=
/=
%=
```

Variables can be reassigned unless they are declared as `final`.

```java
int i = 10;
i = 20;       // valid

final int x = 10;
// x = 20;    // CTE
```

Chained assignment is valid:

```java
int i, j;

i = j = 10;
```

Invalid:

```java
int i = 1, 2; // CTE
```

---

## 3. Ternary (Conditional) Operator

A compact form of simple `if-else`.

Syntax:

```java
condition ? valueIfTrue : valueIfFalse;
```

Example:

```java
int a = 10;
int b = 20;

int max = a > b ? a : b;
```

The condition is evaluated first.

- If `true` → first expression is returned.
- If `false` → second expression is returned.

---

## 4. Bitwise Operators

Operate directly on individual bits of integral values.

```text
&   AND
|   OR
^   XOR
~   NOT
```

Rules:

```text
& → 1 only when both bits are 1
| → 1 when at least one bit is 1
^ → 1 when bits are different
~ → flips all bits
```

For an integer `n`:

```text
~n = -(n + 1)
```

### `&` and `|` with booleans

`&` and `|` can also operate on boolean values.

Unlike `&&` and `||`, they evaluate **both operands**.

```java
boolean result = false & someCondition();
```

`someCondition()` is still evaluated.

---

## 5. Logical Operators

Used with boolean expressions.

```text
&&   Logical AND
||   Logical OR
!    Logical NOT
```

Rules:

```text
&& → true only when both conditions are true
|| → true when at least one condition is true
!  → reverses boolean value
```

### Short-Circuit Evaluation

`&&` and `||` use short-circuit evaluation.

```java
false && expression
```

`expression` is not evaluated.

```java
true || expression
```

`expression` is not evaluated.

Example:

```java
int x = 0;

boolean result = x != 0 && 10 / x > 2;
```

The second condition is skipped, so no `ArithmeticException` occurs.

Quick comparison:

```text
&&  ||  → short-circuit
&   |   → evaluate both boolean operands
```

---

## 6. Relational and Equality Operators

Used to compare values and return a boolean result.

```text
>
>=
<
<=
==
!=
```

Example:

```java
int age = 20;

System.out.println(age >= 18); // true
```

### `==` with Primitives vs Objects

For primitive values:

```java
int a = 10;
int b = 10;

System.out.println(a == b); // true
```

`==` compares the values.

For object references:

```java
String a = new String("java");
String b = new String("java");

System.out.println(a == b);      // false
System.out.println(a.equals(b)); // true
```

Rule:

```text
Primitive == → compares values

Object == → compares references

equals() → may compare logical/content equality,
depending on the class implementation
```

### Chained Comparisons

Java does not support mathematical-style chained comparisons.

```java
0 < x < 20
```

Result:

```text
CTE
```

Correct:

```java
0 < x && x < 20
```

---

## 7. Shift Operators

Used to shift bits left or right.

```text
<<   Left Shift
>>   Signed Right Shift
>>>  Unsigned Right Shift
```

### Left Shift `<<`

Shifts bits to the left.

For many positive integer values, this behaves similarly to multiplying by powers of 2.

```java
10 << 2
```

Approximately:

```text
10 × 2² = 40
```

### Signed Right Shift `>>`

Shifts bits to the right while preserving the sign bit.

For many positive integer values, this behaves similarly to dividing by powers of 2.

```java
8 >> 2
```

Result:

```text
2
```

### Unsigned Right Shift `>>>`

Shifts bits to the right and fills the new left-side bits with `0`.

```java
int x = -8;

System.out.println(x >> 1);   // -4
System.out.println(x >>> 1);  // 2147483644
```

Rule:

```text
>>   → signed right shift
>>>  → unsigned right shift
```

### Important

Do not treat shifting as universally identical to multiplication or division.

Example:

```java
System.out.println(-7 / 2);   // -3
System.out.println(-7 >> 1);  // -4
```

---

## 8. Unary Increment / Decrement Operators

```text
++   Increment
--   Decrement
```

### Post-Increment / Post-Decrement

```java
i++;
i--;
```

Rule:

```text
First Take, Then Change
```

The current value is used first, then the variable is updated.

Example:

```java
int i = 5;

int x = i++;

System.out.println(x); // 5
System.out.println(i); // 6
```

### Pre-Increment / Pre-Decrement

```java
++i;
--i;
```

Rule:

```text
First Change, Then Take
```

The variable is updated first, then the new value is used.

Example:

```java
int i = 5;

int x = ++i;

System.out.println(x); // 6
System.out.println(i); // 6
```

### Invalid Uses

```java
100++;   // CTE
(++i)++; // CTE
```

---

## `i = i++`

```java
int i = 5;

i = i++;

System.out.println(i);
```

Output:

```text
5
```

Mental model:

```java
int temp = i; // temp = 5
i = i + 1;    // i = 6
i = temp;     // i = 5
```

The post-increment returns the original value, and the assignment writes that original value back into `i`.

---

## Multiple Increment Example

```java
int i = 5;

int result = i++ + ++i;
```

Evaluation:

```text
i++  → contributes 5, i becomes 6

++i  → i becomes 7, contributes 7
```

Result:

```text
result = 12
i = 7
```

---

# Quick Interview Recall

```text
* / % have higher precedence than + -

int / int → integer division

floating-point operand involved
→ floating-point division

&& || → short-circuit

& | with booleans
→ both operands evaluated

Primitive ==
→ compares values

Object ==
→ compares references

equals()
→ logical/content equality depending on implementation

<<  → left shift
>>  → signed right shift
>>> → unsigned right shift

Post increment
→ use first, then change

Pre increment
→ change first, then use

i = i++
→ original value gets assigned back
```
