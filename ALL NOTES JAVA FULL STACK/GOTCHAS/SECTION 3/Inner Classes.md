# Inner Classes in Java

Core Concept: An inner class is simply a class declared inside another class.

- Origin: Introduced in Java 1.1 to fix GUI event-handling bugs, but became highly popular for general programming.
- Rule: Regular inner classes cannot contain static members.
- Compilation: When compiled, Java generates separate .class files (e.g., compiling Outer with an Inner class generates Outer.class and Outer$Inner.class).

## 1. Normal / Regular Inner Class

- What it is: A standard class written directly inside another class.
- How it works: It is deeply tied to the outer class. To create an object of the inner class, you must first create an object of the outer class.
- Object Creation: Outer.Inner i = new Outer().new Inner();

## 2. Static Inner Class

- What it is: An inner class declared with the static keyword.
- How it works: Because it is static, it is independent of the outer class's instances. You do not need an existing outer class object to create it.
- Object Creation: Inner i = new Inner();

## 3. Method Local Inner Class

- What it is: A class declared entirely inside a method block.
- How it works: Its scope is strictly limited to that specific method.
- Purpose: Used when you have complex, repetitive logic that applies only to that specific method and nowhere else in the program.

## 4. Anonymous Inner Class (Detailed)

What it is: A class without a name. It combines class declaration and object instantiation into a single step.

Why use it? Normally, if you have an interface or an abstract class, you cannot create an object from it directly. You have to create a brand-new, separate class that implements or extends it, write the logic, and then create an object of that new class. An Anonymous Inner Class lets you skip all that. It allows you to provide the implementation "on the fly" exactly where you need it, which is perfect for code you only plan to use once.

How it works: You use the new keyword alongside the interface or abstract class name, followed immediately by curly braces {} containing the overriding methods.

## Example (Implementing an Interface on the fly):

```java
interface ATM {  
    public void deposit();  
}

class Test {  
    public static void main(String[] args) {  
         
        // This is the Anonymous Inner Class  
        // We are instantly implementing the ATM interface without creating a separate class file  
        ATM atm = new ATM() {  
            public void deposit() {  
                System.out.println("Deposit Method Executed");  
            }  
        };  
         
        atm.deposit();  
    }  
}
```
