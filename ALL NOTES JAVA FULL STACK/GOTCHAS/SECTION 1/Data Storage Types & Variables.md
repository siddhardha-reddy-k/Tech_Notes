# Data Storage Types & Variables — Gotchas

> Interview revision only.  
> Contains non-obvious Java behavior, compile-time rules, and code traps.

---

## 1. Compile Time vs Runtime

### Compile Time

Compiler checks things such as:

- Type compatibility
    
- Scope
    
- Definite assignment
    
- Constant expressions
    
- Whether constant values fit into smaller types
    

### Runtime

JVM performs things such as:

- Actual method execution
    
- Object creation
    
- Branch execution
    
- Arithmetic
    
- Runtime overflow
    
- Runtime exceptions
    

---

## 2. Local Variables — Definite Assignment

Local variables do **not** get default values.

They do not need initialization at declaration, but they must be definitely assigned before use.

```
int x;
x = 10;

System.out.println(x); // Valid
```

```
int x;

System.out.println(x); // CTE
```

**Rule:** Local variable must be definitely assigned before use.

---

## 3. Scope vs Definite Assignment

```
int x;

System.out.println(x);
```

**Result:** CTE — not initialized.

```
if (true) {
    int x = 10;
}

System.out.println(x);
```

**Result:** CTE — `x` is out of scope.

These are different problems.

---

## 4. Primitive Widening

```
byte → short → int → long → float → double
                 ↑
char ────────────┘
```

Examples:

```
byte b = 10;
int i = b;       // Valid

int x = 10;
long l = x;      // Valid

float f = 10;
double d = f;    // Valid
```

`boolean` does not participate in numeric conversion.

---

## 5. Integer Literals are `int` by Default

```
long x = 100;
```

Valid:

```
int literal → widened to long
```

But:

```
long x = 10000000000;
```

**Result:** CTE

The literal itself is too large for `int`.

Correct:

```
long x = 10000000000L;
```

---

## 6. Floating-Point Literals

Decimal literals are `double` by default.

```
float f = 10.5; // CTE
```

Correct:

```
float f = 10.5f;
```

or explicitly:

```
float f = (float) 10.5;
```

---

## 7. Constant Narrowing

Although `10` is an `int` literal:

```
byte b = 10;
```

is valid.

The compiler knows `10` is a constant and checks that it fits inside `byte`.

```
byte a = 127; // Valid
byte b = 128; // CTE
```

**Rule:** Compile-time integer constant + value fits destination type → narrowing may be allowed.

---

## 8. Normal Variable vs Compile-Time Constant

```
int x = 10;
byte b = x;
```

**Result:** CTE

`x` is an ordinary `int` variable.

But:

```
final int x = 10;
byte b = x;
```

**Result:** Valid

`x` is a compile-time constant and `10` fits inside `byte`.

---

## 9. `final` Does NOT Always Mean Compile-Time Constant

```
int x = 20;

final int y = x;

byte b = y;
```

**Result:** CTE

`y` cannot be reassigned, but its initializer `x` is not a constant expression.

Compare:

```
final int y = 20;

byte b = y; // Valid
```

**Remember:**

```
final ≠ automatically compile-time constant
```

---

## 10. Constant Expressions

```
final int a = 100;
final int b = 27;

byte c = a + b;
```

Valid because compiler evaluates:

```
100 + 27 = 127
```

and `127` fits inside `byte`.

But:

```
final int a = 100;
final int b = 28;

byte c = a + b;
```

**Result:** CTE

`128` does not fit inside `byte`.

---

## 11. Numeric Promotion During Arithmetic

`byte`, `short`, and `char` are promoted to `int` during normal arithmetic.

```
byte a = 10;
byte b = 20;

byte c = a + b; // CTE
int d = a + b;  // Valid
```

### Promotion Rule

```
If either operand is double → double
else if either is float     → float
else if either is long      → long
else                         → int
```

Examples:

```
byte + short   → int
byte + byte    → int
char + char    → int
int + long     → long
long + float   → float
float + float  → float
float + double → double
char + double  → double
```

---

## 12. Compound Assignment vs Normal Assignment

```
byte b = 10;

b = b + 1;
```

**Result:** CTE

`b + 1` produces an `int`.

But:

```
b += 1;
```

is valid.

So are:

```
b++;
++b;
```

Compound assignment and increment/decrement include an implicit conversion back to the variable's type.

Mental model:

```
b += 1;
```

roughly behaves like:

```
b = (byte) (b + 1);
```

---

## 13. byte Overflow

`byte` range:

```
-128 ... 127
```

```
byte b = 127;
b++;

System.out.println(b);
```

**Output:**

```
-128
```

It then continues:

```
127
↓
-128
-127
-126
...
```

Overflow does **not always become** `**-128**`.

It wraps according to the value.

Example:

```
byte b = 120;

b += 10;

System.out.println(b);
```

**Output:**

```
-126
```

---

## 14. Explicit Cast Can Lose High Bits

```
byte b = 10;

b = (byte) (b + 130);

System.out.println(b);
```

Calculation:

```
10 + 130
= 140
```

Converting `140` to `byte` wraps:

```
140 - 256 = -116
```

**Output:**

```
-116
```

---

## 15. `char` Numeric Behavior

Java `char` represents a UTF-16 code unit.

```
char ch = 'A';
int x = ch;

System.out.println(x);
```

**Output:**

```
65
```

During arithmetic, `char` is promoted to `int`.

```
char ch = 'A';

System.out.println(ch + 1);
System.out.println((char) (ch + 1));
```

**Output:**

```
66
B
```

---

## 16. `char` Overflow

`char` range:

```
0 ... 65535
```

```
char ch = 65535;

ch++;

System.out.println((int) ch);
```

**Output:**

```
0
```

`char` wraps around when incremented beyond its maximum value.

---

## 17. Definite Assignment + Conditions

This compiles:

```
int x;

if (true) {
    x = 10;
}

System.out.println(x);
```

**Output:**

```
10
```

The compiler knows the constant condition `true`.

But:

```
int y;

boolean condition = true;

if (condition) {
    y = 10;
}

System.out.println(y);
```

**Result:** CTE

`condition` is an ordinary variable, so the compiler cannot guarantee that the assignment will occur.

A compile-time constant condition can be treated differently:

```
final boolean condition = true;
```

---

# Quick Recall

```
Integer literal → int by default
Decimal literal → double by default

byte / short / char arithmetic → int

Numeric promotion:
double > float > long > int

Local variables → no default values
Local variables → must be definitely assigned before use

byte b = 10              → Valid
byte b = 128             → CTE

int x = 10
byte b = x               → CTE

final int x = 10
byte b = x               → Valid

int x = 10
final int y = x
byte b = y               → CTE

byte + byte              → int

b = b + 1                → CTE for byte
b += 1                   → Valid
b++                      → Valid

byte overflow            → wraps
char overflow            → wraps
```