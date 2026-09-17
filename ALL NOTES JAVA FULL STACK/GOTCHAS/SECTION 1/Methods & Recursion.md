# Methods & Recursion — Gotchas

## Java Is Always Pass-by-Value

```
static void change(int x) {
    x = 50;
}

int a = 10;
change(a);

System.out.println(a);
```

**Output:** `10`

**Rule:** Method receives a copy of the primitive value.

---

## Objects Are NOT Passed by Reference

```
static void change(Student s) {
    s.marks = 100;
}
```

Both references point to the same object, so object state can change.

```
st ──► Object
s  ──► Object
```

**Rule:** Java copies the **reference value**. Java is still pass-by-value.

---

## Reassigning Parameter Does Not Reassign Caller Reference

```
static void change(Student s) {
    s = new Student();
}
```

**Rule:** Only local parameter `s` receives the new reference. The caller's reference is unchanged.

---

## Return Type Must Be Compatible

```
static int get() {
    return 10.5;
}
```

**Result:** CTE

`10.5` is `double`.

---

## `return;` in `void`

```
static void test() {
    return;
}
```

**Result:** Valid

**Rule:** `return;` exits the method without returning a value.

---

## Var-Args Is an Array

```
static void show(int... nums) {
    System.out.println(nums.length);
}

show();
```

**Output:** `0`

`nums` behaves as `int[]`.

---

## Var-Args Must Be Last

```
void test(int... x, String s) { }
```

**Result:** CTE

---

## Only One Var-Arg

```
void test(int... x, String... s) { }
```

**Result:** CTE

---

## Recursive Call Before vs After Statement

```
System.out.print(n + " ");
test(n - 1);
```

For `test(3)`:

```
3 2 1
```

But:

```
test(n - 1);
System.out.print(n + " ");
```

prints:

```
1 2 3
```

**Rule:** Statements after the recursive call execute during stack unwinding.

---

## Missing Terminating Base Case

```
static void test(int n) {
    test(n + 1);
}
```

**Result:** RTE — `StackOverflowError`

**Rule:** Every recursive call creates another stack frame until stack space is exhausted.

---

# Quick Recall

```
parameter → method declaration
argument  → method call

Java → always pass-by-value

primitive argument
→ primitive value copied

object argument
→ reference value copied

void + return;
→ valid

var-arg → internally array
var-arg → last parameter
one var-arg maximum

recursive call → new stack frame
base case      → stops recursion
returning calls → stack unwinding
no termination → StackOverflowError
```