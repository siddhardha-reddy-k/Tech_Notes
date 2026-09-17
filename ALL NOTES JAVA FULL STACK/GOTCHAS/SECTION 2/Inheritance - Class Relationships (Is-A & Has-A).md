# Inheritance in Java

Definition: It is a mechanism in which one class inherits the properties of another class. Deriving a class in the presence of an existing class is called inheritance.

- Main Objective: To provide reusability (write once, reuse multiple times).

## In Java, there are five types of inheritance:

1. Single Level Inheritance
2. Multi-Level Inheritance
3. Multiple Inheritance
4. Hierarchical Inheritance
5. Hybrid Inheritance

## 6. Single Level Inheritance

If we derive a class in the presence of one base class, it is called single level inheritance.

### Hierarchy:

A (Parent / Base / Super class)  
|  
B (Child / Derived / Sub class)

### Code Example:

```java
class A {  
    public void methodOne() {  
        System.out.println("MethodOne");  
    }  
}

class B extends A {  
    public void methodTwo() {  
        System.out.println("MethodTwo");  
    }  
}

class Test {  
    public static void main(String[] args) {  
        A a = new A();  
        a.methodOne();  
         
        B b = new B();  
        b.methodOne(); // Inherited method  
        b.methodTwo(); // Own method  
    }  
}
```

## 2. Multi-Level Inheritance

If we derive a class in the presence of one base class, and that base class is derived from another base class, it is called multi-level inheritance.

### Hierarchy:

A  
|         
B  
|         
C

### Code Example:

```java
class A {  
    public void methodOne() {  
        System.out.println("MethodOne");  
    }  
}

class B extends A {  
    public void methodTwo() {  
        System.out.println("MethodTwo");  
    }  
}

class C extends B {  
    public void methodThree() {  
        System.out.println("MethodThree");  
    }  
}

class Test {  
    public static void main(String[] args) {  
        A a = new A();  
        a.methodOne();  
         
        B b = new B();  
        b.methodOne();  
        b.methodTwo();  
         
        C c = new C();  
        c.methodOne();   // Inherited from A  
        c.methodTwo();   // Inherited from B  
        c.methodThree(); // Own method  
    }  
}
```

## 3. Multiple Inheritance

In Java, a class cannot extend more than one class simultaneously because Java does not support multiple inheritance for classes.

Why Java does not support it: There is a chance of raising the ambiguity problem (the Diamond Problem). If two parent classes have a method with the exact same signature, the child class wouldn't know which one to inherit.

P1.m1()                        P2.m1()  
   |------------------------------|  
                  |  
                C.m1()   <-- Ambiguity: Which m1() is inherited?

## Invalid Class Example:

```java
class A {}  
class B {}  
class C extends A, B {} // C.T.E (Compile Time Error) - Invalid
```

The Workaround (Interfaces): While classes cannot achieve this, an interface can extend more than one interface. Therefore, we can achieve the multiple inheritance concept through interfaces.

```java
interface A {}  
interface B {}  
interface C extends A, B {} // Valid
```

## The Role of the Object Class

- Direct Child: If your class does not extend any other class, it is directly a child class of the Object class.
- Indirect Child: If your class extends some other class, it becomes an indirect child class of the Object class.

## Cyclic Inheritance

Java does not support cyclic inheritance.

Java

```java
class A extends B {}  
class B extends A {} // C.T.E - Invalid
```

## 4. Hierarchical Inheritance

If we derive multiple classes using a single base class, it is called hierarchical inheritance.

### Hierarchy:

       A  
       |  
  |---------|  
  B         C

### Code Example:  

```java
class A {  
    public void methodOne() {  
        System.out.println("MethodOne");  
    }  
}

class B extends A {  
    public void methodTwo() {  
        System.out.println("MethodTwo");  
    }  
}

class C extends A {  
    public void methodThree() {  
        System.out.println("MethodThree");  
    }  
}

class Test {  
    public static void main(String[] args) {  
        A a = new A();  
        a.methodOne();  
         
        B b = new B();  
        b.methodOne();  
        b.methodTwo();  
         
        C c = new C();  
        c.methodOne();  
        c.methodThree();  
    }  
}
```

## 5. Hybrid Inheritance

Hybrid inheritance is a combination of two or more types of inheritance. Because it relies on multiple inheritance structurally, Java does not support hybrid inheritance for classes.

### Hierarchy:

Plaintext

       A  
       |  
  |---------|  
  B         C

  |---------|  
       |  
       D

## Is-A Relationship (Inheritance)

The Is-A relationship is the fundamental concept behind inheritance in Object-Oriented Programming.

- Implementation: We implement an Is-A relationship using the extends keyword.
- Main Objective: To provide code reusability.
- Examples of Is-A:

- A Dog is an Animal.
- A Laptop is a Computer.
- Ravi is a Human. (Note: This relationship is unidirectional. A Dog is an Animal, but an Animal is not necessarily a Dog).

### Code Example

```java
class Animal {  
    public void eat() {  
        System.out.println("Eat Method");  
    }  
}

// Dog inherits from Animal using 'extends'  
class Dog extends Animal {  
    public void sleep() {  
        System.out.println("Sleep Method");  
    }  
}

class Test {  
    public static void main(String[] args) {  
        // Case 1: Parent reference, Parent object  
        Animal a = new Animal();  
        a.eat(); // Valid  
         
        // Case 2: Child reference, Child object  
        Dog d = new Dog();  
        d.eat();   // Valid (Inherited from Animal)  
        d.sleep(); // Valid (Own method)  
         
        // Case 3: Parent reference, Child object (Upcasting)  
        Animal a1 = new Dog();  
        a1.eat(); // Valid  
        // a1.sleep(); // Invalid: Parent reference cannot see Child-specific methods  
         
        // Case 4: Child reference, Parent object (Downcasting)  
        // Dog d1 = new Animal(); // COMPILE TIME ERROR (C.T.E)  
    }  
}
```

## Key Conclusions on Object Creation

1. Property Flow: Whatever properties and methods exist in the Parent class automatically come to the Child class. However, whatever properties exist in the Child class never go to the Parent class.
2. Reference vs. Object: A Parent reference can hold a Child object (e.g., Animal a1 = new Dog();). But a Child reference cannot hold a Parent object (e.g., Dog d1 = new Animal(); is strictly invalid).

## Has-A Relationship

The Has-A relationship is a concept used to establish a relationship between two separate classes through their objects. It is also known as Composition and Aggregation.

- Implementation: Unlike the Is-A relationship (which uses the extends keyword), there is no specific keyword to implement a Has-A relationship. Most commonly, we use the new operator to instantiate the object of one class inside another.
- Main Objective: To provide reusability.
- Drawback: It increases the dependency between two components.

## Real-world Examples of Has-A:

- Course has a Content
- Car has an Engine
- Fan has a Switch
- Course has a Trainer

## General Has-A Relationship Example

In this example, the SriLaxmi class has a RaiseTech object to access its course details.

```java
class RaiseTech {  
    public String courseName() {  
        return "FSD Java with GenAI";  
    }  
    public double courseFee() {  
        return 25000d;  
    }  
    public String trainerName() {  
        return "Niyaz sir";  
    }  
}

class SriLaxmi {  
    public void getCourseDetails() {  
        // Implementing Has-A relationship using 'new' operator  
        RaiseTech rt = new RaiseTech();  
        System.out.println("Course Name : " + rt.courseName());  
        System.out.println("Course Fee : " + rt.courseFee());  
        System.out.println("Trainer Name : " + rt.trainerName());  
    }  
}

class Student {  
    public static void main(String[

] args) {  
        SriLaxmi sl = new SriLaxmi();  
        sl.getCourseDetails();  
    }  
}
```

The Has-A relationship is further divided into two specific types based on how strongly the objects are connected: Composition and Aggregation.

## 1. Composition (Strong Association)

Definition: Without an existing container object, there is no chance of having a contained object. The relationship between the container and the contained object is called composition, which represents a strong association.

- Analogy: A Car and an Engine. If the Car (container) is destroyed, its specific internal Engine (contained object) is also destroyed.

Code Example (Composition): Notice how the Engine is created inside the Car's constructor. The Engine cannot exist without the Car being created first.

```java
class Engine {  
    public void engineStart() {  
        System.out.println("Engine started");  
    }  
}

class Car {  
    Engine e;  
     
    // Engine object is strictly created inside the Car object  
    Car() {  
        e = new Engine();  
    }  
     
    public void carStart() {  
        e.engineStart();  
        System.out.println("Car Moved");  
    }  
}

class Test {  
    public static void main(String[] args) {  
        Car c = new Car();  
        c.carStart();  
    }  
}
```

## 2. Aggregation (Loose Association)

Definition: Without an existing container object, there is a chance of having a contained object. The relationship between the container and the contained object is called aggregation, which represents a loose association.

- Analogy: A Car and a generic Engine. The Engine is built independently in a factory. It can exist on its own, and later be placed inside a Car. If the Car is destroyed, the Engine could theoretically be taken out and still exist.

Code Example (Aggregation): Notice how the Engine is created outside (in the main method) and then passed to the Car's constructor. The Engine exists independently of the Car.

Java

```java
class Engine {  
    public void engineStart() {  
        System.out.println("Engine started");  
    }  
}

class Car {  
    Engine e;  
     
    // Engine object is passed into the Car, not created by it  
    Car(Engine e) {  
        this.e = e;  
    }  
     
    public void carStart() {  
        e.engineStart();  
        System.out.println("Car Moved");  
    }  
}

class Test {  
    public static void main(String[] args) {  
        // Engine is created independently  
        Engine e = new Engine();  
         
        // Engine is injected into the Car  
        Car c = new Car(e);  
        c.carStart();  
    }  
}
```

## Sealed Classes:

- Used to restrict inheritance by specifying exactly which child classes are permitted to extend a parent class.
- Implemented using the sealed class modifier and the permits keyword.
- Any permitted child class must declare itself as final (cannot be extended), sealed (must permit its own subclasses), or non-sealed (open for regular extension).
