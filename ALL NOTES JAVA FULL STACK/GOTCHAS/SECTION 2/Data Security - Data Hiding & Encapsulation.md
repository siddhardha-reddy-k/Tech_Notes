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
