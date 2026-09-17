# Abstraction (Recap)

Definition: Hiding internal implementation and highlighting the set of services is called abstraction.

- Best Example: GUI ATM machine (hides internal implementation, highlights services like banking, withdrawal, etc.).
- Implementation: Achieved using abstract classes and interfaces.

### Advantages:

1. Gives security by hiding internal implementation.
2. Enhancement becomes easier without affecting the end-user.
3. Provides flexibility to the end-user.
4. Improves maintainability of an application.

## Interface

Definition: It is a blueprint of a class and a collection of abstract methods, default methods, static methods, and private methods.

- Abstract Methods: Incomplete methods that end with a semicolon and don't have a body (e.g., void methodOne();).
- By default, every abstract method in an interface is public and abstract. // public static final int speed = 120; +
- Constants: Interfaces contain only constants, which are implicitly public static final.
- Instantiation: It is not possible to create an object (instantiate) an interface.
- Implementation: To write the implementation for abstract methods, we use an implementation class. We can create an object of the implementation class because it contains methods with bodies.
- Use Case: If we depend strictly upon the Service Requirement Specification, we need to use an interface.

### Syntax:

```java
interface interface_name {  
    // abstract methods  
    // default methods  
    // static methods  
    // private methods  
    // constants  
}
```

## Basic Interface Implementation

```java
interface Animal {  
    public abstract void eat();  
}

class Dog implements Animal {  
    @Override  
    public void eat() {  
        System.out.println("Pedigree");  
    }  
}

class Test {  
    public static void main(String[] args) {  
        Animal a = new Dog();  
        a.eat();  
    }  
}
```

(Note: You can also use an Anonymous Inner Class to implement an interface on the fly without a separate class file, as shown in previous notes).

## Overriding Multiple Methods

If an interface contains multiple methods, the implementation class must override all of them; otherwise, you will get a compile-time error.

```java
interface A {  
    void view();  
    public void show();  
    abstract void see();  
    public abstract void display();  
}

class B implements A {  
    @Override  
    public void view() { System.out.println("View Method"); }  
    @Override  
    public void show() { System.out.println("Show Method"); }  
    @Override  
    public void see() { System.out.println("See Method"); }  
    @Override  
    public void display() { System.out.println("Display Method"); }  
}
```

## Multiple Inheritance via Interfaces

A class cannot extends more than one class. However, an interface can extends more than one interface, and a class can implements more than one interface. This is how Java achieves multiple inheritance.

## 1. Interface extending multiple interfaces:

```java
interface A { void methodOne(); }  
interface B { void methodTwo(); }  
interface C extends A, B { void methodThree(); }

class D implements C {  
    @Override  
    public void methodOne() { System.out.println("MethodOne"); }  
    @Override  
    public void methodTwo() { System.out.println("MethodTwo"); }  
    @Override  
    public void methodThree() { System.out.println("MethodThree"); }  
}
```

## 2. Class implementing multiple interfaces:

```java
interface Father {  
    float HT = 6.2f;  
    void height();  
}  
interface Mother {  
    float HT = 5.8f;  
    void height();  
}

class Child implements Father, Mother {  
    public void height() {  
        float height = (Father.HT + Mother.HT) / 2;  
        System.out.println("Child Height : " + height);  
    }  
}

class Test {  
    public static void main(String[] args) {  
        Child c = new Child();  
        c.height();  
    }  
}
```

## Marker Interface

Definition: An interface which does not have any methods or constants is called a marker interface. In general, an empty interface is called a marker interface.

- Purpose: By using a marker interface, an object gets some specific ability or behavior from the JVM.
- Examples: Serializable, Cloneable, Remote.

## Abstract Class

Definition: It is a collection of zero or more abstract methods and concrete (implemented) methods.

- The abstract keyword is applicable for classes and methods, but not for variables.
- Instantiation: It is not possible to create an object for an abstract class.
- Implementation: To write the implementation of abstract methods, we use subclasses (extends).
- Unlike interfaces, abstract classes contain instance variables rather than just constants.
- Use Case: If we know partial implementation, then we need to use an abstract class.

### Syntax:

```java
abstract class <class_name> {  
    // abstract methods  
    // concrete methods  
    // instance variables  
}
```

-

## Abstract Class Example (Billing System)

```java
abstract class Plan {  
    // Instance variable  
    protected double rate;  
     
    // Abstract method (no body)  
    public abstract void getRate();  
     
    // Concrete method (has body)  
    public void calculateBillAmt(int units) {  
        System.out.println("Total Units :" + units);  
        System.out.println("Total Bill : " + (units * rate));  
    }  
}

class DomesticPlan extends Plan {  
    @Override  
    public void getRate() {  
        rate = 2.5d;  
    }  
}

class CommericalPlan extends Plan {  
    @Override  
    public void getRate() {  
        rate = 5.0d;  
    }  
}

class Test {  
    public static void main(String[] args) {  
        DomesticPlan dp = new DomesticPlan();  
        dp.getRate();  
        dp.calculateBillAmt(250);  
         
        CommericalPlan cp = new CommericalPlan();  
        cp.getRate();  
        cp.calculateBillAmt(250);  
    }  
}
```

## Interface vs. Abstract Class

|                      |                                                                                     |                                                                   |
| -------------------- | ----------------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| Feature              | Interface                                                                           | Abstract Class                                                    |
| Keyword              | To declare, we use the interface keyword.                                           | To declare, we use the abstract keyword.                          |
| Contents             | Blueprint of a class; collection of abstract, default, static, and private methods. | Collection of zero or more abstract methods and concrete methods. |
| Variables            | Contains only constants (public static final).                                      | Contains instance variables.                                      |
| Multiple Inheritance | We can achieve multiple inheritance.                                                | We cannot achieve multiple inheritance.                           |
| Implementation       | To implement abstract methods, we use an implementation class (implements).         | To implement abstract methods, we use a subclass (extends).       |
| Blocks               | It does not allow initialization blocks.                                            | It allows blocks.                                                 |
| Constructors         | It does not allow constructors.                                                     | It allows constructors.                                           |
| When to use          | If we know only the specification.                                                  | If we know the partial implementation.                            |
|                      |                                                                                     |                                                                   |

## Abstraction Implementation Examples

Using abstract classes and interfaces, we can achieve abstraction.

### Example 1: Using Abstract Class

```java
abstract class Shape {  
    public abstract void draw();  
}  
class Circle extends Shape {  
    @Override  
    public void draw() {  
        System.out.println("circle");  
    }  
}
```

### Example 2: Using Interface

```java
interface Payment {  
    public abstract void paymentMethod();  
}  
class PaymentImpl implements Payment {  
    @Override  
    public void paymentMethod() {  
        System.out.println("UPI Payment");  
    }  
}
```

## Default & Static Methods in Interfaces (Java 8 Update):

- Default Methods: Interfaces can now contain non-abstract methods tagged with the default keyword, which can be overridden by implementing classes.
- Static Methods: Interfaces can also contain non-abstract methods tagged with the static keyword, which cannot be overridden.
