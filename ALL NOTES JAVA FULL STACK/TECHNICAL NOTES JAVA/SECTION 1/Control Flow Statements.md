# Control Flow Statements

Control statements control the execution flow of a program by making decisions, repeating code, or transferring control.

## 1. Decision Making Statements

- `if`: Executes a block only when the condition is `true`.
    
- `if-else`: Executes one block if the condition is true, otherwise executes the `else` block.
    
- `if-else-if ladder`: Checks conditions sequentially; once one condition is true, the remaining blocks are skipped.
    
- `nested if`: An `if` statement inside another `if`.
    
- Java conditions must evaluate to `boolean`.
    

```
int x = 10;
if (x) { }      // CTE
```

## switch

Executes code based on matching a value with case labels.

Common supported types:

- `byte`, `short`, `char`, `int`
    
- Corresponding wrapper types
    
- `String`
    
- `enum`
    

Traditional `switch` does not support `long`, `float`, `double`, or `boolean`.

```
switch (n) {
    case 1:
        System.out.println("One");
        break;
    default:
        System.out.println("Other");
}
```

### case Labels

Case labels must be compile-time constant values.

```
int x = 2;
case x:          // CTE
```

```
final int x = 2;
case x:          // Valid if x is a compile-time constant
```

### Fall-Through

If `break` is omitted, execution continues into following cases.

```
case 1:
    System.out.println("A");
case 2:
    System.out.println("B");
```

`break` is not mandatory; it is used when fall-through is not required.

## Switch Expression

Modern `switch` can return a value.

```
int result = switch (n) {
    case 1 -> 10;
    case 2 -> 20;
    default -> 0;
};
```

- `switch statement` → performs statements.
    
- `switch expression` → produces a value.
    
- `yield` is used to return a value from a block inside a switch expression.
    

```
int result = switch (n) {
    case 1 -> {
        int x = 10;
        yield x * 2;
    }
    default -> 0;
};
```

Switch expressions became standard in Java 14.

## 2. Iteration Statements

### for Loop

Best when the number of iterations is known.

```
for (int i = 0; i < 5; i++) {
    System.out.println(i);
}
```

Execution flow:

```
Initialization → Condition → Body → Update → Condition → ...
```

- Initialization executes once.
    
- Condition is checked before every iteration.
    
- Update executes after the loop body.
    
- Variable declared inside the `for` initialization is scoped to the `for` statement.
    

### while Loop

Best when the number of iterations is unknown.

```
while (condition) {
    // code
}
```

Condition is checked before execution, so the loop may execute zero times.

### do-while Loop

Executes the body first and checks the condition afterward.

```
do {
    // code
} while (condition);
```

Executes at least once.

### Enhanced for Loop

Used to iterate directly through elements of arrays or Collections.

```
for (int n : numbers) {
    System.out.println(n);
}
```

Useful when direct element access is needed and explicit index control is not required.

## 3. Jump Statements

### break

Terminates the nearest loop or `switch`.

```
break → exit nearest loop / switch
```

### continue

Skips the remaining statements of the current loop iteration and proceeds to the next iteration.

```
continue → skip current iteration
```

In a `for` loop, control moves to the update expression before the next condition check.

### return

Immediately terminates the current method and optionally returns a value.

```
return → exit current method
```

Quick comparison:

```
break    → exits nearest loop / switch
continue → skips current loop iteration
return   → exits current method
```