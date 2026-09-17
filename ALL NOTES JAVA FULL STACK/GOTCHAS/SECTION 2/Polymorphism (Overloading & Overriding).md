# Polymorphism

Definition: The word Polymorphism is derived from Greek words, where poly means "many" and morphism means "forms". Therefore, the ability to represent in different forms is called polymorphism.

- Main Objective: To provide flexibility.

## In Java, polymorphism is divided into two types:

## 1. Compile Time Polymorphism

A polymorphism which exhibits at compile time is called compile-time polymorphism.

- It is also known as static polymorphism or early binding.
- Method resolution is taken care of by the compiler based on the reference type.
- Examples: Method Overloading, Method Hiding.

## 2. Runtime Polymorphism

A polymorphism which exhibits at runtime is called runtime polymorphism.

- It is also known as dynamic polymorphism or late binding.
- Method resolution is taken care of by the JVM based on the runtime object.
- Example: Method Overriding.

## Method Overloading

Definition: Having the same method name with different parameters/signatures in a single class is called method overloading.

- Methods present in the class are called overloaded methods.
- Method resolution is taken care of by the compiler based on the reference type.
- Advantage: Method overloading reduces the complexity of programming.

### Code Example:

```java
class ECOI {  
    // Overloaded methods  
    public void search(int epicNo) {  
        System.out.println("Details Found via epicNo");  
    }  
    public void search(String details) {  
        System.out.println("Details Found via details");  
    }  
    public void search(long phoneNo) {  
        System.out.println("Details Found via phoneNo");  
    }  
}

class Voter {  
    public static void main(String[] args) {  
        ECOI ecoi = new ECOI();  
        ecoi.search(1234);  
        ecoi.search("Niyaz");  
        ecoi.search(99999L);  
    }  
}
```

## FAQ: Can we overload the main method in Java?

Yes, we can overload the main method in Java, but the JVM will always execute the specific main method with the String[] parameter only.

Java

```java
class Test {  
    public static void main(String[] args) {  
        System.out.println("String-array arg");  
    }  
    public static void main(int[] iargs) {  
        System.out.println("int-array arg");  
    }  
}
```

## Method Overriding

Definition: Having the same method name with the same parameters in two different classes (Parent and Child) is called method overriding.

- Methods present in the Parent class are called overridden methods.
- Methods present in the Child class are called overriding methods.
- Method resolution is taken care of by the JVM based on the runtime object.

### Code Example:

```java
class Parent {  
    // Overridden methods  
    public void property() {  
        System.out.println("Land+House+Gold");  
    }  
    public void marry() {  
        System.out.println("Trisha");  
    }  
}

class Child extends Parent {  
    // Overriding methods  
    @Override  
    public void marry() {  
        System.out.println("Rashmika");  
    }  
}

class Test {  
    public static void main(String[] args) {  
        Parent p = new Parent();  
        p.property(); // Land+House+Gold  
        p.marry();    // Trisha  
         
        Child c = new Child();  
        c.property(); // Land+House+Gold  
        c.marry();    // Rashmika  
         
        // Dynamic Polymorphism: Parent reference holding Child object  
        Parent p1 = new Child();  
        p1.property(); // Land+House+Gold  
        p1.marry();    // Rashmika (JVM looks at the runtime object, which is Child)  
    }  
}
```

Note: If we declare any method as final, overriding of that method is not possible (it will cause a compile-time error if attempted).

## Method Hiding

Definition: Method hiding is exactly the same as method overriding, but it applies specifically to static methods.

## Method Overriding vs. Method Hiding

|   |   |   |
|---|---|---|
|Feature|Method Overriding|Method Hiding|
|Method Type|Methods must be non-static.|Methods must be static.|
|Method Resolution|Taken care of by the JVM based on the runtime object.|Taken care of by the compiler based on the reference type.|
|Alternative Names|Runtime polymorphism, dynamic polymorphism, or late binding.|Compile-time polymorphism, static polymorphism, or early binding.|

### Code Example:

```java
class Parent {  
    public static void property() {  
        System.out.println("House-Not For Sale");  
    }  
}

class Child extends Parent {  
    public static void property() {  
        System.out.println("House-For Sale");  
    }  
}

class Test {  
    public static void main(String[] args) {  
        // Since methods are static, the compiler resolves based on the reference type (Parent)  
        Parent p = new Child();  
        p.property(); // House-Not For Sale  
    }  
}
```
