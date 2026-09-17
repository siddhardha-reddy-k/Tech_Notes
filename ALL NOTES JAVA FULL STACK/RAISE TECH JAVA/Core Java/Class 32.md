   
1) Single Level Inheritance   
===========================  
If we derived a class in the presence of one base class is called single level inheritance.  
ex:  
A (Parent / Base / Super class)  
|  
|  
|  
B (Child / Derived / Sub class)  
   
ex:  
---  

```java
class A 
{
    public void methodOne()
    {
        System.out.println("MethodOne");
    }
}
class B extends A 
{
    public void methodTwo()
    {
        System.out.println("MethodTwo");
    }
}
class Test 
{
    public static void main(String[] args)
    {
        A a = new A();
        a.methodOne();
         
        B b = new B();
        b.methodOne();
        b.methodTwo();
    }
}
```

   
2) Multi-level inheritance  
=========================  
If we derived a class in the presence of one base class and that class is derived from another base class is called multi-level inheritance.  
   
ex:  
A  
|  
|          
B  
|  
|          
C   
   
ex:  
---  

```java
class A 
{
    public void methodOne()
    {
        System.out.println("MethodOne");
    }
}
class B extends A 
{
    public void methodTwo()
    {
        System.out.println("MethodTwo");
    }
}
class C extends B 
{
    public void methodThree()
    {
        System.out.println("MethodThree");
    }
}
class Test 
{
    public static void main(String[] args)
    {
        A a = new A();
        a.methodOne();
         
        B b = new B();
        b.methodOne();
        b.methodTwo();
         
        C c = new C();
        c.methodOne();
        c.methodTwo();
        c.methodThree();
    }
}
```

   
3) Multiple inheritance   
=======================  
In java, we can't extends more than one class simultenously because java does not support multiple inheritance.  
ex:  

```java
class A 
{
}
class B 
{
}
```

class C extends A,B  --> invalid   
{  
}  
   
But interface can extends more then one interface so we can achieve multiple inheritance concept through interfaces.  
ex:  

```java
interface A 
{
}
interface B 
{        
}
interface C extends A,B
{
}
```

   
If our class does not extends any other class then it is a directly child class of Object class.  
ex:                        Diag:  
class A                 Object  
{                        |  
|  
}                        A   
   
If our class extends some other class then it is a indirectly child class of Object class.          
ex:                        Diag:  
class A                 Object  
{                        |  
}                        |  

```java
class B extends A         A
{                        |
            |
}                        B 
```

   
Java does not support cyclic inheritance.  
ex:  

```java
class A extends B 
{
}
class B extends A 
{
}
```

   
Q) Why java does not support multiple inheritance?  
   
There is a chance of raising ambiguity problem. Hence java does not support multiple inheritance.  
   
ex:  
P1.m1()                                P2.m1()  
|-------------------------------------|  
|  
C.m1()  
   
4) Hierarchical inheritance  
===========================  
If we derived multiple classes using one base class is called hierarchical inheritance.  
   
ex:  
A  
|  
|---------------|  
B                C  
   
ex:  
---  

```java
class A 
{
    public void methodOne()
    {
        System.out.println("MethodOne");
    }
}
class B extends A 
{
    public void methodTwo()
    {
        System.out.println("MethodTwo");
    }
}
class C extends A
{
    public void methodThree()
    {
        System.out.println("MethodThree");
    }
}
class Test 
{
    public static void main(String[] args)
    {
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

   
5) Hybrid Inheritance  
=====================  
Hybrid inheritance is a combination of two or more than two inheritance.  
Java does not support hybrid inheritance.  
ex:  
A  
|  
|---------------|  
B                C  
|---------------|  
|  
D  
   
   
   
Constructors   
============  
It is a special method which is used to initialized an object.  
   
Having same name as class name is called constructor.  
   
A constructor is called when instance of a class is created.  
   
It does not allow returntype. If we take returntype then we won't get and compile time error or runtime error.  
   
A constructor will accept following modifiers.  
ex:  
default   
public   
private   
protected   
   
In java , constructors are divided into two types.  
   
1) Userdefined constructor  
   
2) Default constructor  
   
1) Userdefined constructor  
--------------------------  
A constructor which is created by the user based on the application requirement is called userdefined constructor.  
   
It is classified into two types.  
   
i) Zero Argument constructor   
   
ii) Parameterized constructor   
   
i) Zero Argument constructor  
---------------------------  
Suppose if we are not passing any argument to userdefined constructor is called zero argument constructor.  
   
ex:  
---  

```java
class Test 
{
    Test()
    {
        System.out.println("constructor");        
    }
    public static void main(String[] args)
    {
        System.out.println("main-method");
    }
}
```

o/p:  
main-method  
   
ex:  
---  

```java
class Test 
{
    public Test()
    {
        System.out.println("constructor");        
    }
    public static void main(String[] args)
    {
        System.out.println("main-method");
        Test t = new Test();
    }
}
```

   
o/p:  
main-method   
constructor   
   
ex:  
---  

```java
class Test 
{
    private Test()
    {
        System.out.println("constructor");        
    }
    public static void main(String[] args)
    {
        Test t = new Test();
        System.out.println("main-method");
    }
}
```

o/p:  
constructor  
main-method  
   
ex:  
--  

```java
class Test 
{
    protected Test()
    {
        System.out.println("constructor");        
    }
    public static void main(String[] args)
    {
        Test t1 = new Test();
        System.out.println("main-method");
        Test t2 = new Test();
    }
}
```

   
ii) Parameterized constructor  
----------------------------  

```java
class Employee 
{
    private int empId;
    private String empName;
    private double empSal;
     
    Employee(int empId,String empName,double empSal)
    {
        this.empId = empId;
        this.empName = empName;
        this.empSal = empSal;
    }
    public void getEmployeeDetails()
    {
        System.out.println("Employee Id : "+empId);
        System.out.println("Employee Name : "+empName);
        System.out.println("Employee Salary : "+empSal);
    }
}
class Test 
{
    public static void main(String[] args)
    {
        Employee e = new Employee(201,"Alan",10000d);
        e.getEmployeeDetails();
    }
}
```

   
   
2) Default constructor  
-----------------------  
It is a compiler generated constructor for every java program where we are not defining atleast zero argument constructor.  
   
To see default constructor we need to use below command.  
ex:  
javac   Test.java  
   
javap   -c   Test   
   
Diagram: class32.1  
![[attachments/image18.png]]  
   
Q) What is constructor overloading?  
   
Having same constructor name with different parameters in a single class is called constructor overloading.  
   
ex:  
---  

```java
class A 
{
    A()
    {
        System.out.println("0-arg const");
    }
    A(int i)
    {
        System.out.println("int-arg const");
    }
    A(double d)
    {
        System.out.println("double-arg const");
    }
}
class Test 
{
    public static void main(String[] args)
    {
        A a1 = new A();
        A a2 = new A(10);
        A a3 = new A(10.56d);
    }
}
```

   
Has-A relationship   
==================  
Has-A relationship is also known as composition and aggregation.  
   
There is no specific word to implements Has-A relationship but mostly we wil use new operator.  
   
The main objective of Has-A relationship is to provide reusability.  
   
Has-A relationship increases dependency between two components.  
   
ex:  
Course has Content  
Car has Engine   
Fan has Switch   
Course has Trainer   
   
ex:  
---  

```java
class RaiseTech 
{
    public String courseName()
    {
        return "FSD Java with GenAI";
    }
    public double courseFee()
    {
        return 25000d;
    }
    public String trainerName()
    {
        return "Niyaz sir";
    }
}
class SriLaxmi
{
    public void getCourseDetails()
    {
        RaiseTech rt = new RaiseTech();
        System.out.println("Course Name : "+rt.courseName());
        System.out.println("Course Fee : "+rt.courseFee());
        System.out.println("Trainer Name : "+rt.trainerName());
    }
}
class Student 
{
    public static void main(String[] args)
    {
        SriLaxmi sl = new SriLaxmi();
        sl.getCourseDetails();
    }
}
```

   
composition  
===========  
Without existing container object there is no chance of having contained object then the relationship between container and contained object is called composition which is strongly association.  
   
Diagram: class32.2  
![[attachments/image19.png]]  
ex:  
---  

```java
class Engine 
{
    public void engineStart()
    {
        System.out.println("Engine started");
    }
}
class Car 
{
    Engine e;
    Car()
    {
        e = new Engine();
    }
    public void carStart()
    {
        e.engineStart();
        System.out.println("Car Moved");
    }
}
class Test
{
    public static void main(String[] args)
    {
        Car c = new Car();
        c.carStart();
    }
}
```

   
   
aggregation  
===========  
Without existing container object there is a chance of having contained object then the relationship between container and contained object is called aggregation which is loosely association.  
   
Diagram: class32.3  
![[attachments/image20.png]]  
   

```java
class Engine 
{
    public void engineStart()
    {
        System.out.println("Engine started");
    }
}
class Car 
{
    Engine e;
    Car(Engine e)
    {
        this.e = e;
    }
    public void carStart()
    {
        e.engineStart();
        System.out.println("Car Moved");
    }
}
class Test
{
    public static void main(String[] args)
    {
        Engine e = new Engine();
        Car c = new Car(e);
        c.carStart();
    }
}
```

   
   
