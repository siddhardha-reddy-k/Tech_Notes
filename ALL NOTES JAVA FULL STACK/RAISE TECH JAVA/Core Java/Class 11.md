   
Var-Arg Method  
==============  
Untill 1.4 version, it is not possible to declare a method with variable number of arguments.But from 1.5 version onwards it is possible to declare a method with variable number of arguments.  
   
We can declare var-arg method as follow.  
ex:  
   
var-arg parameter  
  |  
       ---------  

```java
void methodOne(int...  i)
```

   |  
ellipse   
   
Here var-arg parameter is a replacement of single dimensional array.  
ex:  
...    ----->  []  
   
We can invoke var-arg method with any number of integer values including zero.  
   
ex:1  
----  

```java
class Test 
{
    public static void main(String[] args)
    {
        methodOne();
    }
    public static void methodOne()
    {
        System.out.println("0-arg method");
    }        
}
```

   
ex:2  
-----  

```java
class Test 
{
    public static void main(String[] args)
    {
        methodOne(10);
    }
    public static void methodOne(int i)
    {
        System.out.println("one-arg method");
    }
     
}
```

   
ex:3  
----  

```java
class Test 
{
    public static void main(String[] args)
    {
        methodOne(10,20);
    }
    public static void methodOne(int i,int j)
    {
        System.out.println("two-arg method");
    }
     
}
```

   
ex:4  
-----  

```java
class Test 
{
    public static void main(String[] args)
    {
        methodOne();
        methodOne(10);
        methodOne(10,20);
        methodOne(10,20,30);
    }
    public static void methodOne(int...  i)
    {
        System.out.println("var-arg method");
    }
     
}
```

   
Note:  
-----  
In realtime we will use var-arg method when number of inputs are not fixed to a method.  
   
ex:  
---  

```java
class Zomato
{
    public static void main(String[] args)
    {
        //bookOrder("Biryani");        
        bookOrder("Biryani","Chicken65");        
    }
    public static void bookOrder(String...  items)
    {
        //System.out.println(items[0]);
        System.out.println(items[0]+" "+items[1]);
    }
}
```

   
case1:  
------  
We can mix var-arg parameter with general parameters.  
ex:  

```java
void methodOne(int x,int... y)
```

   
   
case2:  
-----  
If we mix var-arg parameter with general parameter then var-arg parameter   
must be last parameter.  
ex:          
void methodOne(int... x,int y)   //invalid   

```java
void methodOne(int x,int... y)
```

   
case3:  
-----  
A var-arg method can have only one var-arg parameter.  
ex:  

```java
void methodOne(int... x)   
```

void methodOne(int... x,int... y)  //invalid   
   
   
   
   
Java Source File Structure   
==========================  
   
case1:  
------  
A java program can have multiple classes.  
   
case2:  
------  
If a java program contains multiple classes then we need to check which class   
contains main method and that class treated as main class.  
ex:  
   
Student.java  
--------------  

```java
class Recording 
{
    String source = "LMS";        
}
class Student
{
    public static void main(String[] args)
    {
        Recording r = new Recording();
        System.out.println(r.source);
    }
}
```

   
If we compile above program we will get two .class files i.e   
Recording.class and Student.class.  
   
case3:  
-----  
If a java program contains multiple classes with main method then atleast one   
class we need to declared as public and that public class treated as main class.  
ex:  
A.java  
------  

```java
public class A
{
    public static void main(String[] args)
    {
        System.out.println("A-class");
    }
}
class B
{
    public static void main(String[] args)
    {
        System.out.println("B-class");
    }
}        
```

If we compile above program we will get two .class files i.e A.class and B.class.  
ex:  
javac  A.java  
   
java   A (A class will execute)  
java   B (B class will execute)  
DSA Platform Questions   
======================                  
Q)   
   
Birthday Gift Contribution  
   
Rahul and Rohan wanted to buy a birthday gift for their friend. Rahul contributed 200 rupees and Rohan contributed 300 rupees. Write a Java program to find the total amount collected for the gift.  
   

```java
public class GiftContribution 
{
            public static void main(String[] args) 
    {
        int a = 200;
        int b = 300;
        System.out.println(a+b);         
    }
}
```

   
   
Q)  
   
Library Book Purchase  
   
A school library purchased 15 science books and 20 mathematics books. Write a Java program to find the total number of books purchased.  
   
   

```java
class BookPurchase
{
             public static void main(String[] args)
    {
        BookPurchase bp = new BookPurchase();
        bp.purchase(); 
    }
    public void purchase()
    {
        int a = 15;
        int b = 20;
        System.out.println(a+b);
    }        
}
```

   
   
Q)  
Water Consumption  
   
A family used 250 liters of water in the morning and 180 liters in the evening. Write a Java program to calculate the total water consumed.  
   
   

```java
class WaterConsumption
{
             public static void main(String[] args)
    {
        purchase(); 
    }
    public static void purchase()
    {
        int m = 250;
        int e = 180;
        System.out.println(m+e);
    }
}
```

   
Assignments  
===========  
1)  
   
Water Left in Tank  
   
A water tank initially contained 1000 liters of water. During the day, 350 liters were used. Write a Java program to find the amount of water left in the tank.  
   
   
2)   
Employee Salary  
   
An employee earns 1200 rupees per day. He worked for 25 days in a month. Write a Java program to calculate his monthly salary.  
   
   
3)  
   
Chocolate Distribution  
   
A teacher has 60 chocolates and wants to distribute them equally among 12 students. Write a Java program to find how many chocolates each student will receive.  
   
4)  
   
Remaining Chocolates  
   
A shopkeeper has 53 chocolates and packs them into boxes that can hold 10 chocolates each. Write a Java program to find how many chocolates are left unpacked.  
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
