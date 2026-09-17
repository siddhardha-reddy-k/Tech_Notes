# Operators — Gotchas

## Short-Circuit vs Non-Short-Circuit

```
int x = 0;

boolean a = x != 0 && 10 / x > 2;
```

**Output:** `false`

`10 / x` is not executed.

```
boolean b = x != 0 & 10 / x > 2;
```

**Result:** RTE — `ArithmeticException`

**Rule:**

```
&&  ||  → short-circuit
&   |   → both boolean operands are evaluated
```

---

## `||` vs `|`

```
int x = 0;

boolean a = x == 0 || 10 / x > 1;
```

**Output:** `true`

```
boolean b = x == 0 | 10 / x > 1;
```

**Result:** RTE — `ArithmeticException`

---

## Java Does Not Support Chained Comparisons

```
int x = 10;

boolean result = 0 < x < 20;
```

**Result:** CTE

Java effectively reaches:

```
(0 < x) < 20
```

which becomes:

```
boolean < int
```

Invalid.

Correct:

```
0 < x && x < 20
```

---

## Integer Division by Literal Zero

```
System.out.println(10 / 0);
```

**Result:** CTE

```
System.out.println(10 % 0);
```

**Result:** CTE

But:

```
int x = 0;

System.out.println(10 / x);
```

**Result:** RTE — `ArithmeticException`

**Rule:** Constant integral division/modulo by zero can be rejected at compile time. With an ordinary variable, the zero value is encountered during execution.

---

## Floating-Point Division by Zero

```
System.out.println(10.0 / 0);
```

**Output:**

```
Infinity
```

```
System.out.println(0.0 / 0);
```

**Output:**

```
NaN
```

**Rule:** Floating-point division by zero does not throw `ArithmeticException`.

---

## Shift Is Not Always the Same as Division

```
System.out.println(-7 / 2);
System.out.println(-7 >> 1);
```

**Output:**

```
-3
-4
```

**Rule:** Treat `>> n` as division by `2ⁿ` only as a basic mental shortcut. Negative values can behave differently.

---

# Quick Recall

```
&& / || → short-circuit

& / | with boolean operands
→ evaluate both sides

0 < x < 20
→ CTE

10 / 0
→ CTE

int x = 0;
10 / x
→ RTE ArithmeticException

10.0 / 0
→ Infinity

0.0 / 0
→ NaN
```