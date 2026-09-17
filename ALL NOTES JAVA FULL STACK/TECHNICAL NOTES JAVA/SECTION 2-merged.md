### Abstraction - Interfaces & Abstract Classes

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

|   |   |   |
|---|---|---|
|Feature|Interface|Abstract Class|
|Keyword|To declare, we use the interface keyword.|To declare, we use the abstract keyword.|
|Contents|Blueprint of a class; collection of abstract, default, static, and private methods.|Collection of zero or more abstract methods and concrete methods.|
|Variables|Contains only constants (public static final).|Contains instance variables.|
|Multiple Inheritance|We can achieve multiple inheritance.|We cannot achieve multiple inheritance.|
|Implementation|To implement abstract methods, we use an implementation class (implements).|To implement abstract methods, we use a subclass (extends).|
|Blocks|It does not allow initialization blocks.|It allows blocks.|
|Constructors|It does not allow constructors.|It allows constructors.|
|When to use|If we know only the specification.|If we know the partial implementation.|
||||

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



### Constructors & Keywords (this super)

# Constructors

Definition: A constructor is a special method used to initialize an object.

- It must have the exact same name as the class name.
- It is called automatically when an instance of a class (an object) is created.
- It does not allow a return type. (Note: If you provide a return type, the compiler will not throw an error, but Java will simply treat it as a regular method, not a constructor).

### Accepted Modifiers:

- default, public, private, protected

## Constructors are divided into two main types:

1. User-defined constructor
2. Default constructor

## 3. User-Defined Constructor

A constructor created by the user based on the application's requirements. It is classified into two types:

### i) Zero-Argument Constructor

A constructor where we do not pass any arguments.

```java
class Test {  
    // 0-argument constructor  
    public Test() {  
        System.out.println("constructor");         
    }  
     
    public static void main(String[] args) {  
        System.out.println("main-method");  
        Test t = new Test(); // Constructor is called here  
    }  
}  
// Output:  
// main-method  
// constructor
```

### ii) Parameterized Constructor

A constructor that accepts parameters, typically used to initialize instance variables with user-provided values at the time of object creation.

```java
class Employee {  
    private int empId;  
    private String empName;  
    private double empSal;  
     
    // Parameterized constructor  
    Employee(int empId, String empName, double empSal) {  
        this.empId = empId;  
        this.empName = empName;  
        this.empSal = empSal;  
    }  
     
    public void getEmployeeDetails() {  
        System.out.println("Employee Id : " + empId);  
        System.out.println("Employee Name : " + empName);  
        System.out.println("Employee Salary : " + empSal);  
    }  
}

class Test {  
    public static void main(String[] args) {  
        Employee e = new Employee(201, "Alan", 10000d);  
        e.getEmployeeDetails();  
    }  
}
```

## 2. Default Constructor

It is a compiler-generated constructor provided automatically for every Java class only if the programmer does not define at least a zero-argument constructor.

- To see the default constructor generated by the compiler, you can compile the file and use the Java Disassembler tool:

- javac Test.java
- javap -c Test

## Constructor Overloading

Having the same constructor name with different parameters (different type, number, or order) in a single class is called constructor overloading.

```java
class A {  
    A() {  
        System.out.println("0-arg const");  
    }  
    A(int i) {  
        System.out.println("int-arg const");  
    }  
    A(double d) {  
        System.out.println("double-arg const");  
    }  
}

class Test {  
    public static void main(String[] args) {  
        A a1 = new A();        // Calls 0-arg  
        A a2 = new A(10);      // Calls int-arg  
        A a3 = new A(10.56d);  // Calls double-arg  
    }  
}
```

## The this Keyword

The this keyword is a reference variable used to refer to the current class object. It can be utilized in three primary ways:

## 1. To refer to current class variables

Used to resolve ambiguity when instance variables and local variables (like constructor parameters) have the same name.

```java
class A {  
    int i = 10;  
    int j = 20;  
     
    A(int i, int j) {  
        System.out.println(i + " " + j);           // 100 200 (Local variables)  
        System.out.println(this.i + " " + this.j); // 10 20 (Instance variables)  
    }  
}
```

## 2. To refer to current class methods

Used to explicitly call another method within the same class.

```java
class A {  
    public void methodOne() {  
        System.out.println("MethodOne");  
        this.methodTwo(); // Calls the current class method  
    }  
    public void methodTwo() {  
        System.out.println("MethodTwo");  
    }  
}
```

## 3. To refer to current class constructors

Used for constructor chaining (calling one constructor from another within the same class). It must be the very first statement in the constructor.

```java
class A {  
    A() {  
        System.out.println("0-arg const");  
    }  
    A(int i) {  
        this(); // Calls A()  
        System.out.println("int-arg const");  
    }  
    A(double d) {  
        this(10); // Calls A(int i)  
        System.out.println("double-arg const");  
    }  
}  
// Calling 'new A(10.5d)' will print:  
// 0-arg const  
// int-arg const  
// double-arg const
```

## The super Keyword

The super keyword is a reference variable used to refer to the immediate superclass (parent class) object. It is also utilized in three ways:

## 1. To refer to superclass variables

Used when the parent class and child class have variables with the exact same name.

```java
class A {  
    int i = 10;  
    int j = 20;  
}

class B extends A {  
    int i = 100;  
    int j = 200;  
     
    B(int i, int j) {  
        System.out.println(this.i + " " + this.j);   // 100 200 (Current class instance variables)  
        System.out.println(i + " " + j);             // 1000 2000 (Local variables passed in)  
        System.out.println(super.i + " " + super.j); // 10 20 (Parent class instance variables)  
    }  
}
```

## 2. To refer to superclass methods

Used to invoke a parent class method that has been overridden by the child class.

```java
class A {  
    public void methodOne() {  
        System.out.println("MethodOne");  
    }  
}

class B extends A {  
    public void methodTwo() {  
        super.methodOne(); // Calls parent's method  
        System.out.println("MethodTwo");  
    }  
}
```

## 3. To refer to superclass constructors

Used to invoke the parent class's constructor. Like this(), super() must be the very first statement in the constructor. (Note: If you don't explicitly write super(), the Java compiler automatically injects a default super() call into the child's constructor).

```java
class A {  
    A() {  
        System.out.println("A-const");  
    }  
}

class B extends A {  
    B() {  
        super(); // Calls parent constructor A()  
        System.out.println("B-const");  
    }  
}
```



### Data Security - Data Hiding & Encapsulation

# Data Hiding

Data hiding is the process of hiding object data from unauthorized access.

- We can achieve data hiding using the private modifier.
- The main objective of data hiding is to provide security.

### Code Example:

```java
class Account {  
    // Hidden data  
    private double balance = 10000d;  
}

class Student {  
    public static void main(String[] args) {  
        Account acc = new Account();  
        // This will cause a compilation error because balance is private  
        System.out.println(acc.balance);  
    }  
}
```

## Abstraction

Definition: Hiding internal implementation and highlighting the set of services.

- Best Example: A GUI ATM machine. The bank hides the internal implementation (how the machine communicates with the server, counts money, etc.) and only highlights the set of services to the user (banking, withdrawal, mini statement).
- Implementation: We can implement abstraction using abstract classes and interfaces.

### Advantages:

1. Provides security by hiding the internal implementation.
2. Makes enhancement easier because internal systems can be changed without affecting the end-user.
3. Provides flexibility for the end-user to use the system.
4. Improves the maintainability of an application.

## Encapsulation

Definition: The process of encapsulating (grouping) variables and their associated methods into a single entity.

A class is considered a fully "encapsulated class" if it supports both data hiding and abstraction.

- Key Rule: Abstraction hides complexity; encapsulation protects data.
- Implementation: For every private variable, you must write public setter and getter methods to allow controlled access.

### Advantages:

1. Provides security.
2. Makes enhancement easier.
3. Provides flexibility to the end-user.
4. Improves maintainability of an application.

## Disadvantage:

- It increases the length of the code and can slow down the execution process.

### Code Example:

```java
class Student {  
    // Current class variables (Data Hiding)  
    private int studId;  
    private String studName;  
    private double studFee;

// Setter methods    public void setStudId(int studId) {  
        this.studId = studId;  
    }  
    public void setStudName(String studName) {  
        this.studName = studName;  
    }  
    public void setStudFee(double studFee) {  
        this.studFee = studFee;  
    }

// Getter methods    public int getStudId() {  
        return studId;  
    }  
    public String getStudName() {  
        return studName;  
    }  
    public double getStudFee() {  
        return studFee;  
    }  
}

class Test {  
    public static void main(String[] args) {  
        Student s = new Student();  
        s.setStudId(101);  
        s.setStudName("Alan");  
        s.setStudFee(10000d);

System.out.println("Student Id : " + s.getStudId());  
        System.out.println("Student Name : " + s.getStudName());  
        System.out.println("Student Fee : " + s.getStudFee());  
    }  
}
```

## Abstraction vs. Encapsulation

|   |   |   |
|---|---|---|
|Feature|Abstraction|Encapsulation|
|Definition|Hiding internal implementation and highlighting the set of services.|Grouping variables and associated methods into a single entity.|
|Best Example|ATM Machine.|A medical Capsule.|
|Implementation|Achieved using abstract classes and interfaces.|Achieved using access modifiers (like private).|
|Process Type|It is the process of gaining information.|It is the process of containing information.|
|Primary Use|Used to hide the data.|Used to protect the data.|
|Problem Level|Solves issues at the design level.|Solves issues at the implementation level.|

## Abstraction and Encapsulation Explained

## Encapsulation vs Abstraction — Summarized

## Encapsulation

- Protects data with private + controlled access (getters/setters)
- Prevents direct manipulation of variables
- Example: private int result; + public void add(int num) method

## Abstraction

- Hides how something works, shows only what it does
- Uses abstract classes/interfaces to define interface, hide implementation
- Example: User calls processPayment(500), doesn't see the 50 lines of API calls inside

## Key Table

|   |   |   |
|---|---|---|
||Encapsulation|Abstraction|
|Protects|✅ Data|❌|
|Hides|❌|✅ Complexity|

## Real Analogy

- Encapsulation = Car's fuel tank we can only pour fuel through the controlled access of fuel door. (protects data)
- Abstraction = we control the car using Steering wheel but we don’t get to know how engine works(hides how engine works)

## Bottom Line

- Encapsulation = mechanism (access modifiers like private)
- Abstraction = principle (hiding complexity via interfaces/abstract classes)
- They're complementary, not the same thing

## Example :

```java
public class Student {    private String name;    private int age;    private double gpa;    private List<Integer> marks;       public boolean isEligibleForScholarship() {        calculateGPA();        return gpa >= 3.5 && age >= 18;    }       private void calculateGPA() {        double sum = marks.stream().mapToInt(Integer::intValue).sum();        this.gpa = sum / marks.size();    }       public void addMark(int mark) {        if (mark >= 0 && mark <= 100) {            marks.add(mark);            calculateGPA();        }    }  
}

// Using it  
Student student = new Student("Sid", 20);  
student.addMark(95);  
student.addMark(88);

if (student.isEligibleForScholarship()) {    System.out.println("You got scholarship!");  

}
```

## This is fully encapsulated because:

- Encapsulation: Data is private, validated access through addMark()
- Abstraction: User just calls isEligibleForScholarship(), doesn't see GPA calculation inside

## POJO(Plain Old Java Object) vs. Java Bean(specialized POJO)

A comparison between a Plain Old Java Object (POJO) and a standard Java Bean class:

|   |   |   |
|---|---|---|
|Feature|POJO|Java Bean|
|Serialization|Cannot be serialized.|Can be serialized.|
|Constructors|May or may not have a constructor.|Must have at least a zero-argument (default) constructor.|
|Field Visibility|Fields can have any visibility level.|Fields can only have private visibility.|
|Inheritance|Cannot extend other classes.|Can extend other classes.|
|Interfaces|Cannot implement other interfaces.|Can implement other interfaces.|
|Annotations|Cannot use other annotations.|Can use other annotations.|



### Date and Time Handling in Java

# Topic 1: Core Date/Time Classes (LocalDate, LocalTime, LocalDateTime, ZonedDateTime)

What it is: Java 8 introduced java.time package — much better than old java.util.Date/Calendar. Four classes, each handling a different combo:

|   |   |   |   |   |
|---|---|---|---|---|
|Class|Has Date?|Has Time?|Has Timezone?|Example use|
|LocalDate|✅|❌|❌|Birthday, deadline|
|LocalTime|❌|✅|❌|Alarm clock, race timing|
|LocalDateTime|✅|✅|❌|Local meeting schedule|
|ZonedDateTime|✅|✅|✅|Flight schedule, global meetings|

Key method: .now() — every class has it, gets current value from system clock.

java

```java
LocalDate today = LocalDate.now();

LocalTime time = LocalTime.now();

LocalDateTime dateTime = LocalDateTime.now();

ZonedDateTime zonedDateTime = ZonedDateTime.now();
```

Gotcha to remember: LocalDate/LocalTime/LocalDateTime are all timezone-unaware — they represent a value with no concept of "where." Only ZonedDateTime knows about timezone. This distinction gets tested directly in "which class would you use for X" MCQs.

## Also useful — creating specific (not "now") values:

java

```java
LocalDate specificDate = LocalDate.of(2026, 1, 26);  // year, month, day

LocalTime specificTime = LocalTime.of(14, 30);        // hour, minute
```

## Practice Q1:

## Write a program that:

1. Prints the current date, current time, and current date-time (all three, using .now())
2. Creates a specific LocalDate for your birthday (any year) using .of()
3. Prints how many days are left until that birthday this year (hint: look up Period.between() — new method, haven't covered it, but try figuring it out — it's a common one)

```java
import java.time.LocalDate;

import java.time.LocalTime;

import java.time.LocalDateTime;

import java.time.Period;

public class Test {

    public static void main(String[] args) {

        // Part 1: current values

        LocalDate today = LocalDate.now();

        LocalTime currentTime = LocalTime.now();

        LocalDateTime currentDateTime = LocalDateTime.now();

        System.out.println("Today's Date: " + today);

        System.out.println("Current Time: " + currentTime);

        System.out.println("Current Date and Time: " + currentDateTime);

        // Part 2: specific birthday

        LocalDate birthday = LocalDate.of(today.getYear(), 8, 15); // e.g. Aug 15

        // Part 3: days left until birthday

        Period period = Period.between(today, birthday);

        if (birthday.isBefore(today)) {

            // birthday already passed this year, calculate for next year

            birthday = birthday.plusYears(1);

            period = Period.between(today, birthday);

        }

        System.out.println("Your birthday this year: " + birthday);

        System.out.println("Days left until birthday: " + period.getDays()

            + " (Months: " + period.getMonths() + ", Years: " + period.getYears() + ")");

    }

}
```

## Walkthrough of the new part (Period):

- Period.between(startDate, endDate) calculates the difference between two LocalDates as years + months + days (not total days — that's a common confusion).
- Gotcha: if birthday already happened this year (e.g., today is July 26 and birthday was in March), Period.between() would give you a negative or misleading result. That's why there's a check: if (birthday.isBefore(today)) → push it to next year with plusYears(1) before calculating.
- period.getDays() alone gives you just the day component — not "total days remaining." If you want a single total day count instead, you'd use a different class: ChronoUnit.DAYS.between(today, birthday) — worth knowing both exist:

- Period → breaks difference into years/months/days (human-readable)
- ChronoUnit.DAYS.between() → gives one raw number of days

Topic 2: Formatting Dates (DateTimeFormatter)

What it is: Formatting = converting a date/time object into a string following a specific pattern. Without formatting, LocalDate.now() prints as 2026-07-26 (ISO default) — fine for logs, ugly for user-facing display.

Key class: DateTimeFormatter — you define a pattern, then call .format() on your date object.

```java
LocalDate today = LocalDate.now();

DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd/MM/yyyy");

String formatted = today.format(formatter);

System.out.println(formatted); // e.g. 26/07/2026
```

## Common pattern symbols (memorize these, they're asked directly):

|   |   |   |
|---|---|---|
|Symbol|Meaning|Example|
|yyyy|4-digit year|2026|
|MM|2-digit month|07|
|MMM|short month name|Jul|
|MMMM|full month name|July|
|dd|2-digit day|26|
|EEEE|full weekday name|Sunday|
|HH|hour (24-hr)|14|
|mm|minutes|30|
|ss|seconds|45|

Gotcha: the formatter is reusable — you can call .format() on multiple different dates with the same formatter object. Also, DateTimeFormatter is applicable to LocalDate, LocalTime, LocalDateTime — same class works across all of them, as long as the pattern matches what the object actually holds (e.g., don't put HH:mm in a pattern and apply it to a LocalDate — it has no time component, will throw an exception).

## Practice Q:

## Write a program that:

1. Gets today's date
2. Formats and prints it in three different styles: dd-MM-yyyy, MMMM dd, yyyy, and EEEE, MMM dd yyyy

```java
import java.time.LocalDate;

import java.time.format.DateTimeFormatter;

public class Test {

    public static void main(String[] args) {

        LocalDate today = LocalDate.now();

        DateTimeFormatter formatter1 = DateTimeFormatter.ofPattern("dd-MM-yyyy");

        DateTimeFormatter formatter2 = DateTimeFormatter.ofPattern("MMMM dd, yyyy");

        DateTimeFormatter formatter3 = DateTimeFormatter.ofPattern("EEEE, MMM dd yyyy");

        System.out.println("Style 1: " + today.format(formatter1));

        System.out.println("Style 2: " + today.format(formatter2));

        System.out.println("Style 3: " + today.format(formatter3));

    }

}
```

Topic 3: Time Zones (ZoneId, ZonedDateTime, ZoneOffset, OffsetDateTime)

What it is: So far everything was timezone-blind. Real apps (flight booking, global meetings, IBM enterprise systems) need to know which timezone a moment belongs to.

|   |   |
|---|---|
|Class|What it represents|
|ZoneId|An identifier for a timezone region, e.g. "Asia/Kolkata", "America/New_York"|
|ZonedDateTime|Date + time + full timezone (handles daylight saving rules automatically)|
|ZoneOffset|A fixed offset from UTC, e.g. +05:30 — no region rules, just a raw number|
|OffsetDateTime|Date + time + offset only (no full timezone identity) — common in databases|

## Key methods:

java

```java
ZoneId zone = ZoneId.of("Asia/Kolkata");

ZonedDateTime zdt = ZonedDateTime.now(zone);
```

## The critical method for real use — converting between zones:

java

```java
ZonedDateTime newYorkTime = zdt.withZoneSameInstant(ZoneId.of("America/New_York"));
```

withZoneSameInstant() — this is the one to remember. It keeps the actual moment in time unchanged, just recalculates what that moment looks like in a different zone's local clock. (Contrast: there's also withZoneSameLocal() which does the opposite — keeps the clock numbers the same but shifts the actual instant. Rarely used, but good to know it exists so you don't confuse the two.)

Gotcha: ZoneId.of("IST") does NOT work — Java doesn't recognize abbreviations like IST/EST/PST because they're ambiguous (IST could mean India Standard Time or Israel Standard Time). You must use full region names like "Asia/Kolkata".

## Practice Q:

## Write a program that:

1. Gets the current ZonedDateTime in "Asia/Kolkata"
2. Converts and prints the same instant in "America/New_York" and "Europe/London"
3. Format the output nicely using a DateTimeFormatter pattern that includes date, time, and zone abbreviation (hint: zone abbreviation pattern symbol is zzz)

```java
import java.time.ZonedDateTime;

import java.time.ZoneId;

import java.time.format.DateTimeFormatter;

public class Test {

    public static void main(String[] args) {

        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd-MM-yyyy HH:mm:ss zzz");

        ZonedDateTime kolkataTime = ZonedDateTime.now(ZoneId.of("Asia/Kolkata"));

        System.out.println("Kolkata: " + kolkataTime.format(formatter));

        ZonedDateTime newYorkTime = kolkataTime.withZoneSameInstant(ZoneId.of("America/New_York"));

        System.out.println("New York: " + newYorkTime.format(formatter));

        ZonedDateTime londonTime = kolkataTime.withZoneSameInstant(ZoneId.of("Europe/London"));

        System.out.println("London: " + londonTime.format(formatter));

    }

}
```

## Walkthrough:

- kolkataTime is the anchor — the actual real-world instant.
- withZoneSameInstant() called twice, once per target zone — each call keeps the same underlying instant (same point on the universal timeline) but re-renders it in that zone's local wall-clock time.
- Notice New York is ~10.5 hrs behind Kolkata and London ~5.5 hrs behind — that's IST offset (+5:30) doing its job.
- zzz in the pattern gives the abbreviated zone name (IST, EDT, GMT) — note EDT vs EST depends on daylight saving, which ZonedDateTime handles automatically based on the date. That's actually the whole point of using ZonedDateTime over ZoneOffset — DST rules are baked in.

Topic 4: Parsing Dates from Strings

What it is: Parsing = converting a String into a structured date object (opposite of formatting, which goes date → string). This matters because user input, form fields, CSV files, API responses — they all give you dates as plain text, and you need to convert that text into a LocalDate/LocalDateTime to actually work with it (compare, calculate, store).

## Key method:

java

```java
LocalDate date = LocalDate.parse("2026-07-26"); // works directly — ISO format is default
```

But if the string isn't in ISO format (yyyy-MM-dd), you must supply a matching DateTimeFormatter:

java

```java
DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd/MM/yyyy");

LocalDate date = LocalDate.parse("26/07/2026", formatter);
```

Critical rule: the pattern in your formatter must exactly match the shape of the string, or it throws DateTimeParseException (a checked-ish runtime exception — actually it's unchecked, but you should still catch it since bad user input is common).

Gotcha to remember: DateTimeParseException is a RuntimeException (unchecked) — Java doesn't force you to catch it with try-catch, but you absolutely should whenever parsing user input, because malformed date strings are extremely common in real apps (typos, wrong format, empty fields).

## Practice Q:

## Write a program that:

1. Takes a date string from the user via Scanner in dd-MM-yyyy format (e.g. 26-07-2026)
2. Parses it into a LocalDate using a matching DateTimeFormatter
3. If parsing fails (user types garbage), catch DateTimeParseException and print a friendly error message instead of crashing
4. If successful, print the parsed date back in a different format: EEEE, MMMM dd, yyyy

```java
import java.time.LocalDate;

import java.time.format.DateTimeFormatter;

import java.time.format.DateTimeParseException;

import java.util.Scanner;

public class Test {

    public static void main(String[] args) {

        try (Scanner sc = new Scanner(System.in)) {

            System.out.println("Enter a date (dd-MM-yyyy): ");

            String input = sc.nextLine();

            DateTimeFormatter inputFormatter = DateTimeFormatter.ofPattern("dd-MM-yyyy");

            try {

                LocalDate parsedDate = LocalDate.parse(input, inputFormatter);

                DateTimeFormatter outputFormatter = DateTimeFormatter.ofPattern("EEEE, MMMM dd, yyyy");

                System.out.println("Parsed Date: " + parsedDate.format(outputFormatter));

            } catch (DateTimeParseException e) {

                System.err.println("Invalid date format! Please use dd-MM-yyyy. Error: " + e.getMessage());

            }

        }

    }

}
```

## Walkthrough:

- Two separate formatters — inputFormatter (matches what the user typed) and outputFormatter (how you want to display it). This is the standard pattern: parse with one format, display with another.
- LocalDate.parse(input, inputFormatter) — the two-argument version, needed because your string isn't in default ISO format.
- Notice the try-catch is nested inside the try-with-resources block, not combined — that's intentional. The Scanner's try-with-resources handles closing the resource; the inner try-catch handles the parsing failure specifically. If you typed them as one combined catch, you couldn't distinguish "Scanner problem" from "bad date format."
- Test it with garbage input like "hello" or wrong format like "2026-07-26" (ISO instead of dd-MM-yyyy) — should print the friendly error instead of an ugly stack trace crash.



### Design Patterns (Singleton)

# Singleton Class

- Definition: It is a design pattern which ensures that a class must have only one instance.
- Concept: A class which allows us to create only one object is called singleton class.
- Requirements: To create a singleton class we required private constructor and static method.
- Purpose: The main purpose of singleton class is we can control object creations, save some memory and maintain consistency cross the application.

```java
import java.util.*;  

class Singleton  
{  
        static Date date = null;  
        private Singleton()  
        {  

                System.out.println("constructor");  

        }  
        public static Date getInstance()  
        {  
                if(date==null)  
                {  

                        date = new Date();  

                }  

                return date;  

        }  
}  
class Test  
{  
        public static void main(String[] args)  
        {  

                Date d1 = Singleton.getInstance();  
                System.out.println(d1);  
                System.out.println(d1.hashCode());  
                  
                Date d2 = Singleton.getInstance();  
                System.out.println(d2);  
                System.out.println(d2.hashCode());  

        }  
}
```



### File and Directory Management in java

# Overview  

Topic 1: File Class

What it is: File class = represents a path (file or folder). It's just metadata handler — doesn't read/write actual content. Think of it as "pointer to a location," not the content itself.

Key methods: exists(), createNewFile(), delete(), isDirectory(), canRead(), canWrite(), length(), getName(), getPath()

Gotcha: new File("x.txt") does NOT create the file on disk — it just creates a Java object representing that path. You need createNewFile() to actually create it.

## Practice Questions:

1. Write a program that checks if a file "data.txt" exists. If not, create it. If yes, print its size in bytes and last modified time.

```java
import java.io.File;

import java.io.IOException;

import java.util.Date;

public class Test {

    public static void main(String[] args) {

        File file = new File("data.txt");

        if (!file.exists()) {

            try {

                if (file.createNewFile()) {

                    System.out.println("File is created data.txt");

                    long sizeInBytes = file.length();

                    long lastModifiedMillis = file.lastModified();

                    Date lastModified = new Date(lastModifiedMillis);

                    System.out.println("Size : " + sizeInBytes + " Bytes");

                    System.out.println("Last Modified: " + lastModified);

                } else {

                    System.out.println("Failed to create the file");

                }

            } catch (IOException e) {

                System.err.println("An error occered while creating the file " + e.getMessage());

            }

        } else {

            System.out.println("file 'data.txt' exists");

            long sizeInBytes = file.length();

            long lastModifiedMillis = file.lastModified();

            Date lastModified = new Date(lastModifiedMillis);

            System.out.println("Size : " + sizeInBytes + " Bytes");

            System.out.println("Last Modified: " + lastModified);

        }

    }

}
```

1. Write a program that takes a folder path and prints whether it's a file, a directory, or doesn't exist at all.

```java
import java.io.File;

public class Test {

    public static void main(String[] args) {

        File file = new File(".");

        if (!file.exists()) {

            System.out.println("Path does not exist");

        } else if (file.isFile()) {

            System.out.println("This is a file");

        } else if (file.isDirectory()) {

            System.out.println("This is a Directory");

        }

    }

}
```

## 1. Write a program that lists all .txt files in a given directory (hint: listFiles() with a filter).

## Approach mine -

```java
import java.io.File;

public class Test {

    public static void main(String[] args) {

        File file = new File(".");

        File[] fileArray = file.listFiles();

        if (fileArray != null) {

            for (File name : fileArray) {

                if (name.getName().endsWith(".txt")) {

                    System.out.println(name.getName());

                }

            }

        } else {

            System.err.println("Not a Direcotry or Cant read");

        }

    }

}
```

## Apraoch Claude:

```java
import java.io.File;

public class Test {

    public static void main(String[] args) {

        File folder = new File(".");

        File[] txtFiles = folder.listFiles((dir, name) -> name.endsWith(".txt"));

        if (txtFiles == null) {

            System.out.println("Not a valid directory or an I/O error occurred");

        } else if (txtFiles.length == 0) {

            System.out.println("No .txt files found");

        } else {

            for (File f : txtFiles) {

                System.out.println(f.getName());

            }

        }

    }

}
```

Topic 2: Writing to Files (FileWriter + BufferedWriter)

## Quick concept recap:

- FileWriter → writes character data to a file. Creates the file if it doesn't exist. Overwrites existing content by default.
- BufferedWriter → wraps FileWriter to batch writes efficiently (fewer actual disk hits = faster).
- write() → writes a string. newLine() → adds a line break (platform-independent, better than hardcoding \n).
- Must close() at the end — otherwise buffered data may never actually get flushed to disk.
- Append mode: new FileWriter("file.txt", true) — that second boolean param means "append instead of overwrite."

Exception to expect: IOException — same reasoning as before (permission, disk, invalid path).

## Practice Q1:

Write a program using Scanner to take 5 strings from user input (one at a time), and write each one on its own line to notes.txt. Use FileWriter + BufferedWriter. Remember to close the writer at the end.

```java
import java.io.FileWriter;

import java.io.BufferedWriter;

import java.util.Scanner;

import java.io.IOException;

public class Test {

    public static void main(String[] args) {

        try (FileWriter fw = new FileWriter("Siddu.txt");

                BufferedWriter bw = new BufferedWriter(fw);

                Scanner sc = new Scanner(System.in);) {

            System.out.println("Enter the 5 Strings. Press enter after each line");

            for (int i = 1; i <= 5; i++) {

                System.out.println("Enter Line " + i + ": ");

                String line = sc.nextLine();

                bw.write(line);

                bw.newLine();

            }

            System.out.println("SuccessFully Saved to Siddu.txt");

        } catch (IOException e) {

            System.err.println("An error occured while writing to the file." +       e.getMessage());

        }

    }

}
```

Creating all the objects in try block, will automatically close it.

## Practice Q2:

Modify this concept slightly — write a program that appends a new line to Siddu.txt every time you run it (don't overwrite previous runs' data). Add a fixed string like "Log entry" plus today's date (you can hardcode a string for now, or if you want to combine modules — use LocalDate.now() from Date/Time module, your call).

```java
import java.io.FileWriter;

import java.io.BufferedWriter;

import java.time.LocalDate;

import java.io.IOException;

public class Test {

    public static void main(String[] args) {

        try (FileWriter fw = new FileWriter("Siddu.txt", true);

                BufferedWriter bw = new BufferedWriter(fw);) {

            LocalDate today = LocalDate.now();

            String logEntry = "Log Entry - " + today;

            bw.write(logEntry);

            bw.newLine();

            System.out.println("SuccessFully Appended: " + logEntry);

        } catch (IOException e) {

            System.err.println("An error occured while writing to the file." + e.getMessage());

        }

    }

}
```

Topic 3: Reading Files (FileReader + BufferedReader)

## Quick concept:

- FileReader → reads character data from a file.
- BufferedReader → wraps it, adds readLine() — reads one full line at a time (way better than reading char-by-char).
- Loop pattern: readLine() returns null when it hits end of file — that's your loop's exit condition.
- Exception: if the file doesn't exist, FileReader's constructor throws FileNotFoundException immediately (a subclass of IOException).

## Practice Q:

Write a program that reads Siddu.txt (the one you just built) line by line and prints each line to console, prefixed with a line number (e.g. 1: Enter Line 1). Use try-with-resources like before.

```java
import java.io.FileReader;

import java.io.BufferedReader;

import java.io.IOException;

public class Test {

    public static void main(String[] args) {

        try (BufferedReader br = new BufferedReader(new FileReader("Siddu.txt"));) {

            String line;

            int lineNumber = 1;

            while ((line = br.readLine()) != null) {

                System.out.println(lineNumber + ": " + line);

                lineNumber++;

            }

        } catch (IOException e) {

            System.err.println("An error occured while writing to the file." + e.getMessage());

        }

    }

}
```

Topic 4: Byte Streams (FileInputStream + FileOutputStream)

## Quick concept:

- Everything so far (FileReader/FileWriter) handled character data — text, with encoding.
- Byte streams handle raw bytes — works for any data type: text, images, videos, zip files, anything.
- Classes: InputStream/OutputStream are abstract base classes. You use FileInputStream (read bytes) and FileOutputStream (write bytes).
- read() reads one byte at a time, returns an int (0-255). Returns -1 when end of file is reached (this is your loop exit condition — same idea as readLine() returning null, just a different sentinel value).
- write(int b) writes one byte. There's also write(byte[] b) to write a whole array at once.

Classic interview gotcha: why does read() return int and not byte? Because a byte can only hold -128 to 127, but you need a way to signal "end of file" using a value that can't be a real byte — so Java uses int and reserves -1 specifically for EOF, since -1 isn't achievable from a byte read (0-255 range).

## Practice Q1:

Write a program that copies Siddu.txt into a new file called Siddu_copy.txt using FileInputStream and FileOutputStream — reading and writing one byte at a time in a loop. Use try-with-resources.

```java
import java.io.FileInputStream;

import java.io.FileOutputStream;

import java.io.IOException;

public class Test {

    public static void main(String[] args) {

        try (FileInputStream fis = new FileInputStream("Siddu.txt");

                FileOutputStream fos = new FileOutputStream("Siddu_copy.txt")) {

            int data;

            while ((data = fis.read()) != -1) {

                fos.write(data);

            }

            System.out.println("File SuccessFully copied using byte streams");

        } catch (IOException e) {

            System.err.println("An error occured during file copying" + e.getMessage());

        }

    }

}
```

## Approach 2 faster read 1024 bytes at a time

```java
import java.io.FileInputStream;

import java.io.FileOutputStream;

import java.io.IOException;

public class Test {

    public static void main(String[] args) {

        try (FileInputStream fis = new FileInputStream("Siddu.txt");

                FileOutputStream fos = new FileOutputStream("Siddu_copy2.txt")) {

            byte[] buffer = new byte[1024];

            int bytesRead;

            while ((bytesRead = fis.read(buffer)) != -1) {

                fos.write(buffer, 0, bytesRead);

            }

            System.out.println("File copied using buffered byte streams");

        } catch (IOException e) {

            System.err.println("An error occurred during file copying: " + e.getMessage());

        }

    }

}
```

## Another appraoch usingn bufferClasses easy! Just like bufferWrite

Topic 5: Directories (mkdir/mkdirs, list, delete)

## Quick concept:

Two APIs exist — java.io.File (older, simpler) and java.nio.file (newer, better exceptions). For now, stick with File since it matches what you've been using.

- Creating:

- mkdir() → creates one directory. Fails (false) if parent directories don't exist.
- mkdirs() → creates the directory and any missing parent folders along the way.
- Both return boolean — true if created, false if it failed or already exists.

- Listing:

- list() → returns String[] of names (files + subfolders) inside a directory.
- listFiles() → returns File[] instead (you used this already in Topic 1, Q3, with the filter).
- Gotcha: both return null if the path isn't a directory or doesn't exist — never skip the null check.

- Deleting:

- delete() → works on files always, but for directories, only if the directory is empty. Returns false otherwise (silently — no exception, no error message telling you why).

Interview gotcha to remember: mkdir() vs mkdirs() is asked a lot — "single vs single+parents" is the whole answer.

## Practice Q1:

## Write a program that:

1. Creates a folder called "Reports" (check if it already exists first, print appropriate message either way)
2. Inside that logic, also try creating a nested path "Reports/2026/January" using the other method (the one that handles missing parents) — this should work even though Reports/2026 doesn't exist yet.

```java
import java.io.File;

public class Test {

    public static void main(String[] args) {

        // Part 1: create "Reports" folder

        File reportsFolder = new File("Reports");

        if (reportsFolder.exists()) {

            System.out.println("Reports folder already exists");

        } else {

            if (reportsFolder.mkdir()) {

                System.out.println("Reports folder created successfully");

            } else {

                System.out.println("Failed to create Reports folder");

            }

        }

        // Part 2: create nested path Reports/2026/January

        File nestedFolder = new File("Reports/2026/January");

        if (nestedFolder.exists()) {

            System.out.println("Nested folder already exists");

        } else {

            if (nestedFolder.mkdirs()) {

                System.out.println("Nested folder structure created successfully");

            } else {

                System.out.println("Failed to create nested folders");

            }

        }

    }

}

// no try-catch needed, since mkdir()/mkdirs() don't throw exceptions, they just return false on failure.
```

## The java.nio version

```java
import java.nio.file.Files;

import java.nio.file.Path;

import java.nio.file.Paths;

import java.io.IOException;

public class Test {

    public static void main(String[] args) {

        Path nestedPath = Paths.get("ReportsNio/2026/January");

        if (Files.exists(nestedPath)) {

            System.out.println("Nested folder already exists");

        } else {

            try {

                Files.createDirectories(nestedPath);

                System.out.println("Nested folder structure created successfully");

            } catch (IOException e) {

                System.err.println("Failed to create directories: " + e.getMessage());

            }

        }

    }

}
```

What's different: Paths.get(String) builds a Path object (same idea as new File(...), just the newer type). Files.createDirectories() is the mkdirs() equivalent — creates missing parents too. Key difference: it throws IOException instead of silently returning false. That's the whole selling point of NIO — you actually find out why something failed.

Q2: Listing Directory Contents

```java
import java.io.File;

public class Test {

    public static void main(String[] args) {

        File folder = new File("."); // current directory

        String[] contents = folder.list();

        if (contents == null) {

            System.out.println("Not a valid directory");

        } else if (contents.length == 0) {

            System.out.println("Directory is empty");

        } else {

            System.out.println("Contents of " + folder.getAbsolutePath() + ":");

            for (String name : contents) {

                System.out.println(" - " + name);

            }

        }

    }

}
```

Why this works: list() gives you plain filenames as String[] — both files and subfolders mixed together, no distinction. If you needed to know which are folders vs files, you'd loop through and call new File(folder, name).isDirectory() on each — but for now, just listing names is enough. The null check matters here just like with listFiles() earlier.

## The java.nio version

```java
import java.nio.file.*;

import java.io.IOException;

public class Test {

    public static void main(String[] args) {

        Path folder = Paths.get(".");

        try (DirectoryStream<Path> stream = Files.newDirectoryStream(folder)) {

            System.out.println("Contents of " + folder.toAbsolutePath() + ":");

            for (Path entry : stream) {

                System.out.println(" - " + entry.getFileName());

            }

        } catch (IOException e) {

            System.err.println("Error reading directory: " + e.getMessage());

        }

    }

}
```

What's different: Files.newDirectoryStream() gives you an iterable DirectoryStream<Path> — notice it's used in try-with-resources (it holds a system resource that needs closing, unlike File.list() which just returns a plain array). You loop with a normal for-each. No null check needed — if the directory is invalid, it throws IOException directly instead of giving you a silent null.

Q3: Deleting an Empty Directory

```java
import java.io.File;

public class Test {

    public static void main(String[] args) {

        File folder = new File("Reports/2026/January");

        if (!folder.exists()) {

            System.out.println("Folder does not exist");

        } else if (folder.delete()) {

            System.out.println("Folder deleted successfully");

        } else {

            System.out.println("Failed to delete — folder may not be empty");

        }

    }

}
```

## The java.nio version

```java
import java.nio.file.*;

import java.io.IOException;

public class Test {

    public static void main(String[] args) {

        Path folder = Paths.get("ReportsNio/2026/January");

        try {

            Files.delete(folder);

            System.out.println("Folder deleted successfully");

        } catch (NoSuchFileException e) {

            System.err.println("Folder does not exist");

        } catch (DirectoryNotEmptyException e) {

            System.err.println("Cannot delete — folder is not empty");

        } catch (IOException e) {

            System.err.println("Delete failed: " + e.getMessage());

        }

    }

}
```

This is the big payoff. Remember how File.delete() just returned false with no explanation? Here, Files.delete() throws specific exceptions — NoSuchFileException if it's not there, DirectoryNotEmptyException if it has contents. You catch each one separately and know exactly what went wrong. This is the exact interview answer for "why is NIO better than File for error handling."

Key gotcha here (this is the one that trips people up): delete() returns false silently if the directory has anything inside it — no exception, no error message telling you why it failed. It just returns false, same as if the folder didn't exist or you lacked permission. Since January is empty (you just created it, nothing inside), this will succeed. But try running it a second time on Reports (not January) — since Reports still contains the 2026 subfolder, delete() will return false, and you won't know why unless you already know this rule.

This is exactly why java.nio.file.Files.delete() is considered better in modern Java — it throws a specific exception (DirectoryNotEmptyException) instead of silently returning false. Just good to know for interviews, not something you need to use yet.

Other useful Files methods of java.nio worth knowing (quick list, no need to practice all):

|   |   |
|---|---|
|Method|Purpose|
|Files.copy(source, target)|Copies a file (no manual byte-loop needed!)|
|Files.move(source, target)|Moves/renames a file|
|Files.readAllLines(path)|Reads entire file into a List<String> — one line, no BufferedReader loop|
|Files.write(path, byteArrayOrLines)|Writes to a file — one line, no BufferedWriter setup|
|Files.isDirectory(path) / Files.isRegularFile(path)|Same as File's isDirectory/isFile|
|Files.size(path)|File size in bytes|

Notice Files.readAllLines() and Files.write() basically replace everything you did manually with FileReader/FileWriter in one line each — that's why NIO is called "more efficient," it's less boilerplate too, not just better exceptions.



### Inheritance - Class Relationships (Is-A & Has-A)

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



### Object Oriented Programming System (OOPS)

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



### Polymorphism (Overloading & Overriding)

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
