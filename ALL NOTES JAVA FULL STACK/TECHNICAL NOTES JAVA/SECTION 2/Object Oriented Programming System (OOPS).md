# Object Oriented Programming System (OOPS)

OOPS stands for Object Oriented Programming System. It was introduced to deal with real-world entities using a programming language.

A language is said to be object-oriented if it supports the following features:

- Class
- Object
- Abstraction
- Encapsulation
- Inheritance
- Polymorphism

## Class

A class is a blueprint of an object (e.g., a design or template).

- It is a logical entity.
- It is a collection of objects.

### Supported Modifiers:

- default, public, final, abstract, sealed, non-sealed

## Syntax to declare a class:

```java
// Modifiers are optional  
[Modifier] class class_name [extends parent_class_name] [implements interface_name] {  
    // class body  
}
```

## Object

An object is the outcome of a blueprint.

- It is an instance of a class (where "instance" means allocating memory for our data members).
- It is a physical entity.
- It is a collection of properties and behaviors.

## Example (Dog):

- Properties: Name, Color, Breed, Weight, Height, etc.
- Behaviors: Eating, Playing, Sleeping, Barking, etc.

It is possible to create more than one object from a single class.

## Syntax to create an object:

```java
class_name reference_variable = new constructor();  
// Example:  
Test t = new Test();
```

## Code Example:x

```java
class Test {  
    public static void main(String[] args) {  
        Test t1 = new Test();  
        Test t2 = new Test();  
         
        System.out.println(t1.hashCode());  
        System.out.println(t2.hashCode());  
         
        System.out.println(t1); // Test@Hexadecimalvalue  
        System.out.println(t2.toString()); // Test@Hexadecimalvalue  
    }  
}
```

## Important Object Methods

## hashCode()

For every object, the JVM creates a unique identification number called a hash code.

- To read the hash code of an object, we use the hashCode() method.
- The hashCode() method is present in the Object class.

## toString()

Whenever we try to display any object reference directly or indirectly, the toString() method is executed.

- The toString() method is present in the Object class.

### Code Example:

```java
class Test {  
    public static void main(String[] args) {  
        Test t = new Test();  
        System.out.println(t); // Test@Hexadecimalnumber  
        System.out.println(t.toString()); // Test@Hexadecimalnumber  
         
        int[] arr = {10, 20, 30};  
        System.out.println(arr); // [I@Hexadecimalnumber  
        System.out.println(arr.toString()); // [I@Hexadecimalnumber  
    }  
}
```

## Overriding toString() Example:

```java
class Test {  
    public static void main(String[] args) {  
        Test t = new Test();  
        System.out.println(t);  
        System.out.println(t.toString());  
    }  
     
    @Override  
    public String toString() {  
        return "Hello World";  
    }  
}
```

## Difference Between Class and Object

|               |                                               |                                                 |
| ------------- | --------------------------------------------- | ----------------------------------------------- |
| Feature       | Class                                         | Object                                          |
| Keyword       | To declare a class, we use the class keyword. | To declare an object, we use the new keyword.   |
| Definition    | It is a blueprint of an object.               | It is an instance of a class.                   |
| Entity Type   | It is a logical entity.                       | It is a physical entity.                        |
| Collection    | It is a collection of objects.                | It is a collection of properties and behaviors. |
| Modification  | It cannot be modified.                        | It can be modified.                             |
| Redeclaration | It cannot be redeclared.                      | It can be redeclared.                           |
