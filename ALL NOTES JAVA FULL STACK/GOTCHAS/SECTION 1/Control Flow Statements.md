# Control Flow Statements — Gotchas

## `if` Requires `boolean`

```
int x = 10;

if (x) {
    System.out.println("Hi");
}
```

**Result:** CTE

**Rule:** Java does not treat numbers as boolean values. `if` requires a boolean expression.

---

## Assignment Inside `if`

```
boolean flag = false;

if (flag = true) {
    System.out.println("YES");
}
```

**Output:**

```
YES
```

**Rule:** Assignment is an expression. `flag = true` assigns `true` and also evaluates to `true`.

```
int x = 0;

if (x = 10) {
}
```

**Result:** CTE

`x = 10` evaluates to `int`, not `boolean`.

---

## Dangling `else`

```
if (x > 0)
    if (y > 10)
        System.out.println("A");
    else
        System.out.println("B");
```

**Rule:** `else` belongs to the nearest unmatched `if`.

---

## `switch` Fall-Through

```
int n = 2;

switch (n) {
    case 2:
        System.out.println("Two");
    case 3:
        System.out.println("Three");
    default:
        System.out.println("Default");
}
```

**Output:**

```
Two
Three
Default
```

**Rule:** After a matching case, execution continues sequentially until `break` or the end of the switch.

---

## `default` Does Not Always Execute

```
int n = 2;

switch (n) {
    default:
        System.out.print("D ");
    case 1:
        System.out.print("1 ");
    case 2:
        System.out.print("2 ");
    case 3:
        System.out.print("3 ");
}
```

**Output:**

```
2 3
```

**Rule:** `default` can appear anywhere. Execution starts at the matching case; Java does not automatically return to `default`.

---

## `case` Must Be Compile-Time Constant

```
int x = 2;

switch (2) {
    case x:
}
```

**Result:** CTE

But:

```
final int x = 2;

switch (2) {
    case x:
}
```

**Result:** Valid

**Rule:** Case labels require compile-time constant values.

---

## `final` Alone Is Not Enough

```
int a = 2;
final int x = a;

switch (2) {
    case x:
}
```

**Result:** CTE

**Rule:** `final` does not automatically make a variable a compile-time constant.

---

## Duplicate `case` Values

```
final int x = 2;

switch (2) {
    case x:
    case 2:
}
```

**Result:** CTE

**Rule:** Two case labels cannot resolve to the same constant value.

---

## `continue` Can Cause Infinite `while`

```
int i = 0;

while (i < 3) {
    if (i == 1)
        continue;

    i++;
}
```

At `i == 1`, `i++` is skipped forever.

**Result:** Infinite loop

**Rule:** `continue` skips the remaining statements in the current iteration.

---

## `continue` in a `for` Loop

```
for (int i = 0; i < 3; i++) {
    if (i == 1)
        continue;

    System.out.print(i + " ");
}
```

**Output:**

```
0 2
```

**Rule:** In a basic `for` loop, `continue` transfers control to the update expression before the next condition check.

---

## `while(true)` + Unreachable Code

```
while (true) {
}

System.out.println("Done");
```

**Result:** CTE

**Rule:** The compiler knows the constant condition is always true, so the following statement is unreachable.

---

## Ordinary Boolean Variable Is Different

```
boolean flag = true;

while (flag) {
}

System.out.println("Done");
```

**Result:** Compiles

At runtime the loop runs forever.

**Rule:** An ordinary variable is not a compile-time constant expression, even if currently initialized with `true`.

---

## `break` Exits Only the Nearest Construct

```
for (int i = 1; i <= 3; i++) {
    switch (i) {
        case 2:
            break;
        default:
            System.out.print(i + " ");
    }
}
```

**Output:**

```
1 3
```

**Rule:** This `break` exits the `switch`, not the surrounding `for`.

---

## `break` in Nested Loops

```
for (int i = 1; i <= 2; i++) {
    for (int j = 1; j <= 3; j++) {
        if (j == 2)
            break;

        System.out.print(i + "" + j + " ");
    }
}
```

**Output:**

```
11 21
```

**Rule:** Plain `break` exits only the nearest loop.

---

## `continue` in Nested Loops

```
for (int i = 1; i <= 2; i++) {
    for (int j = 1; j <= 3; j++) {
        if (j == 2)
            continue;

        System.out.print(i + "" + j + " ");
    }
}
```

**Output:**

```
11 13 21 23
```

**Rule:** Plain `continue` affects only the nearest loop.

---

## `return` vs `break`

```
continue → skips current loop iteration

break    → exits nearest loop or switch

return   → exits the entire current method
```

---

## Empty Statement After `if`

```
int x = 5;

if (x > 0);
{
    System.out.println("Positive");
}
```

**Output:**

```
Positive
```

**Rule:** `;` is a valid empty statement. The `if` controls the empty statement, while the following block executes independently.

---

# Quick Recall

```
if(int)                  → CTE
if(flag = true)          → valid; assignment evaluates to boolean

else                     → nearest unmatched if

switch without break     → fall-through
default                  → does not automatically run
case                     → compile-time constant required
duplicate case values    → CTE

while(true) + code after → unreachable → CTE
while(variable)          → may compile even if variable currently true

continue in while        → may skip manual increment
continue in for          → update expression still runs

break                    → nearest loop/switch
continue                 → nearest loop
return                   → entire method

if(condition);           → if controls empty statement
```