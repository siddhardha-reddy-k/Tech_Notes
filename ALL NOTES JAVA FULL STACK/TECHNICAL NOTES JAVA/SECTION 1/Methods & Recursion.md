# Methods & Recursion

## Methods

A method is a block of code that performs a specific task and can be called whenever required.

## Parameters vs Arguments

```
static void add(int a, int b) { }
add(10, 20);
```

- `a`, `b` → parameters
    
- `10`, `20` → arguments
    

Parameters are declared in the method; arguments are values supplied during the method call.

## 4 Ways to Declare Methods

### 1. void + No Arguments

```
static void show() { }
```

No input and no returned value.

### 2. void + With Arguments

```
static void show(int x) { }
```

Accepts input but does not return a value.

### 3. Return Type + No Arguments

```
static int getValue() {
    return 10;
}
```

Returns a value but accepts no arguments.

### 4. Return Type + With Arguments

```
static int add(int a, int b) {
    return a + b;
}
```

Accepts input and returns a value.

## return

The returned value must be compatible with the declared return type.

```
static int get() {
    return 10;
}
```

```
static int get() {
    return 10.5;     // CTE
}
```

`void` methods do not return a value, but `return;` can terminate the method early.

```
static void test() {
    return;
}
```

## Java Is Pass-by-Value

Java always passes a copy of the value to a method.

### Primitive

```
static void change(int x) {
    x = 50;
}

int a = 10;
change(a);
```

`a` remains `10`.

### Object Reference

```
static void change(Student s) {
    s.marks = 100;
}
```

For objects, Java copies the **reference value**. Both references can therefore point to and modify the same object.

Java is not pass-by-reference.

## Var-Args

Var-args allow a method to accept zero or more arguments.

```
static void show(int... nums) { }
```

Internally, the var-arg parameter behaves like an array.

```
show();
show(10);
show(10, 20, 30);
```

Rules:

```
Only one var-arg parameter is allowed.
Var-arg must be the last parameter.
```

Valid:

```
void test(int x, String... s) { }
```

Invalid:

```
void test(String... s, int x) { }     // CTE
void test(int... x, String... s) { }  // CTE
```

# Recursion

Recursion is a technique where a method calls itself to solve a problem using smaller versions of the same problem.

```
static void test(int n) {
    if (n == 0)
        return;

    System.out.println(n);
    test(n - 1);
}
```

## Base Case

The base case stops further recursive calls.

```
if (n == 0)
    return;
```

Without a proper terminating condition, recursive calls can continue until the stack is exhausted.

## Call Stack

Every method call creates a new stack frame.

```
test(3)
→ test(2)
→ test(1)
→ test(0)
```

After the base case, calls return in reverse order. This is called **stack unwinding**.

```
test(n - 1);
System.out.println(n);
```

For `test(3)`:

```
1
2
3
```

## Missing Base Case

```
static void test(int n) {
    test(n + 1);
}
```

**Result:** RTE — `StackOverflowError`

Recursion and loops are different techniques; Java does not prohibit using them together.