   
Marker interface   
================  
Interface which does not have any methods and constants is called marker interface.  
   
In general, empty interface is called marker interface.  
   
We have following list of marker interfaces in java.  
ex:  
Serializable           
Cloneable   
Remote   
and etc.  
   
By using marker interface we will get some ability to do.  
   
   
   
   
Abstract class   
==============  
It is a collection of zero or more abstract methods and concrete methods.  
   
A abstract keyword is applicable for methods and classes but not for variables.  
   
It is not possible to create object for abstract class.  
   
To write the implementation of abstract methods we will us sub classes.  
   
By default every abstract method is a public and abstract.  
   
Abstract class contains only instance variables.  
   
syntax:  
-------  
abstract class <class_name>  
{  
-  
- //abstract methods   
- //concrete methods   
- // instance variables  
-  
}  
   
If we know partial implementation then we need to use abstract class.  
   
   
ex:  
---  

```java
abstract class Vehicle
{
    //abstract method 
    public abstract void sound();
}
class Car extends Vehicle
{
    @Override
    public void sound()
    {
        System.out.println("Booor Booor");
    }
}
class Test 
{
    public static void main(String[] args)
    {
        Car c = new Car();
        c.sound();
    }
}
```

   
ex:  
---  

```java
abstract class Plan 
{
    //instance variable 
    protected double rate;
     
    //abstract method 
    public abstract void getRate();
     
    //concrete method 
    public void calculateBillAmt(int units)
    {
        System.out.println("Total Units :"+units);
        System.out.println("Total Bill : "+ (units*rate));
    }
}
class DomesticPlan extends Plan 
{
    @Override 
    public void getRate()
    {
        rate = 2.5d;
    }
}
class CommericalPlan extends Plan 
{
    @Override
    public void getRate()
    {
        rate = 5.0d;
    }
}
class Test 
{
    public static void main(String[] args)
    {
        DomesticPlan dp = new DomesticPlan();
        dp.getRate();
        dp.calculateBillAmt(250);
         
        CommericalPlan cp = new CommericalPlan();
        cp.getRate();
        cp.calculateBillAmt(250);
    }
}
```

   
   
Q) What is the difference between interface and abstract class?  
   
| interface | abstract class |
| --- | --- |
| To declare interface we will use<br>interface keyword. | To declare abstract class we will use<br>abstract keyword. |
| It is a blue print of a class and<br>it is a collection of abstract methods,<br>default methods, static methods and<br>private methods. | It is a collection of abstract methods<br>and concrete methods. |
| It contains contants. | It contains instance variables. |
| We can achieve multiple inheritance. | We can't achieve multiple inheritance. |
| To write the implementation of<br>abstract methods we will use<br>implementation class. | To write the implementation of<br>abstract methods we will use<br>sub class. |
| It does not allow blocks. | It allows blocks. |
| It does not allow constructors. | It allows constructors. |
| If we know only specification then<br>we need to use interface. | If we know partial implementation<br>then we need to use abstract class. |
   
   
Abstraction Example   
==================  
Using abstract classes and interfaces we can achieve abstraction.  
   
ex:  
---  

```java
abstract class Shape
{
    public abstract void draw();
}
class Circle extends Shape 
{
    @Override
    public void draw()
    {
        System.out.println("circle");
    }
}
class Test 
{
    public static void main(String[] args)
    {
        Circle c = new Circle();
        c.draw();
    }
}
```

   
ex:  
---  

```java
interface Payment 
{
    public abstract void paymentMethod();
}
class PaymentImpl implements Payment 
{
    @Override
    public void paymentMethod()
    {
        System.out.println("UPI Payment");
    }
}
class Test 
{
    public static void main(String[] args)
    {
        Payment p = new PaymentImpl();
        p.paymentMethod();
    }
}
```

   
Packages  
========  
It is a collection of classes, interfaces, enums and annotations.  
   
Here enum is a special class and annotation is a special interface.  
   
In general , a package is a collection of classes and interfaces.  
   
Package is also known as folder or a directory.  
   
In java, packages are divided into two types.  
   
1) Predefined packages   
   
2) Userdefined packages   
   
1) Predefined packages  
----------------------  
Built-in packages are called predefined packages.  
ex:  
java.lang   (Default package)  
java.io  
java.util  
java.time  
java.text   
java.util.stream   
java.sql   
javax.servlet   
and etc.  
   
   
2) Userdefined packages  
------------------------  
Packages which are created by the user based on the application requirements are called user defined packages or custom packages.  
   
We can declare user defined package as follow.  
   
syntax:  
-------  
package  <package_name>;  
   
It is recommanded to declare package name in reverse order of url.  
ex:  

```java
    package  com.ihub.www;
    package  in.raisetech.www;
    package  com.google.www;
 
ex:
---
package  com.ihub.www;
import java.util.Calendar;
class Test 
{
    public static void main(String[] args)
    {
        Calendar c = Calendar.getInstance();
        int h = c.get(Calendar.HOUR_OF_DAY);
         
        if(h<12)
            System.out.println("Good Morning");
        else if(h<16)
            System.out.println("Good Afternoon");
        else if(h<20)
            System.out.println("Good Evening");
        else
            System.out.println("Good Night");
    }
}
```

We can compile above program as follow.  
ex:  
current directory   
     |  
javac   -d   .   Test.java  
|  
destination folder   
   
We can run above program as follow.  
ex:  
java   com.ihub.www.Test   
|     |  
package-name  class-name   
   
   
Enum   
=====  
Enum concept introduced in Java 1.5.  
   
Enum is a group of named constants.  
   
Using enum we can create our own datatype called enumerated datatype.  
   
When compare to old language enum, java enum is more powerful.  
   
To declare a enum we will use enum keyword.  
   
syntax:  
-----  

```java
enum type_name
{
    value1,value2,....,valueN
}
```

ex:  
---  

```java
enum  Months 
{
    JAN,FEB,MAR
}
```

   
Internal implementation of enum   
-------------------------------  
Every enum, internally consider as class cocept and it extends with java.lang.Enum class.  
   
Every enum constant is a reference variable of enum type.  
   
ex:  
enum Months                 public final class Months extends java.lang.Enum   
{                        {  
JAN,FEB,MAR =>                public static final Months JAN = new Months();          
}                                public static final Months FEB = new Months();  
public static final Months MAR = new Months();  
}  
   
Declaration and Usage of enum   
-----------------------------  

```java
enum Months 
{
    JAN,FEB,MAR
}
class Test 
{
    public static void main(String[] args)
    {
        Months m = Months.JAN;
        System.out.println(m);
    }
}
```

   
ex:  
---  

```java
enum Drinks 
{
    COLA,CAMPA,PEPSI
}
class Test 
{
    public static void main(String[] args)
    {
        Drinks d = Drinks.CAMPA;
        switch(d)
        {
            case COLA : System.out.println("Coka Cola"); break;
        case CAMPA : System.out.println("Campa Energy Drink"); break;
            case PEPSI : System.out.println("PEPSI Brand"); break;
        }
    }
}
```

   
java.lang.Enum  
---------------  
Power to enum will be inherited from java.lang.Enum class.  
It contains following two methods.  
   
1) values()  
---------  
It returns group of constants from enum.  
   
2) ordinal()   
------------  
It returns ordinal number.  
   
ex:  
--  

```java
enum Week
{
    MON,TUE,WED,THU,FRI,SAT,SUN
}
class Test 
{
    public static void main(String[] args)
    {
        Week[] w = Week.values();
        for(Week w1 : w)
        {
            System.out.println(w1.ordinal()+" ---- "+w1);
        }
    }
}
```

   
When compare to old language enum, java enum is more powerful because in addition to constants we can declare constructors, variables and methods.  
   
ex:  
---  

```java
enum Cloths 
{
    SILK,KHADI,COTTON;
     
    Cloths()
    {
        System.out.println("constructor");
    }
}
class Test 
{
    public static void main(String[] args)
    {
        Cloths c = Cloths.SILK;
    }
}        
```

   
ex:  
---  

```java
enum Cloths 
{
    SILK,KHADI,COTTON;
     
    static int i = 10;
    public static void main(String[] args)
    {
        System.out.println(i);
    }
}
```

   
   
