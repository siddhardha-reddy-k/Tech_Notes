   
Wrapper classes  
===============  
The main objective of wrapper class are   
   
1) To wrap primitive to wrapper object and vice versa.  
   
2) To define several utility methods  
   
   
| Primitive Type | Wrapper class |
| --- | --- |
| byte<br>short<br>int<br>long<br>float<br>double<br>boolean<br>char | Byte<br>Short<br>Integer<br>Long<br>Float<br>Double<br>Boolean<br>Character |
   
constructor   
-----------  
For every wrapper class we have two constructors. One will take corresponding primitive as an argument and another will take corresponding String as an argument.  
ex:  
| Wrapper class | constructor |
| --- | --- |
| Byte<br>Short<br>Integer<br>Long<br>Float<br>Double<br>Boolean<br>Character | byte or String<br>short or String<br>int or String<br>long or String<br>float or String<br>double or String<br>boolean or String<br>char |
   
ex:  
--  

```java
class Test 
{
    public static void main(String[] args) 
    {
        Integer i1 = Integer.valueOf(10);
        System.out.println(i1);
         
        Integer i2 = Integer.valueOf("20");
        System.out.println(i2);
    }
}
```

   
ex:  
---  

```java
class Test 
{
    public static void main(String[] args) 
    {
        Boolean b1 = Boolean.valueOf(true);
        System.out.println(b1);
         
        Boolean b2 = Boolean.valueOf("false");
        System.out.println(b2);
    }
}
```

   
ex:  
---  

```java
class Test 
{
    public static void main(String[] args) 
    {
        Character c = Character.valueOf('a');
        System.out.println(c); 
    }
}
```

   
Utility Methods  
===============  
   
1) valueOf()   
------------  
It is used to convert primitive type or String type to wrapper object.  
   
ex:  
--  

```java
class Test 
{
    public static void main(String[] args) 
    {
        int a = 10;
         
        Integer i = Integer.valueOf(a);
         
        System.out.println(i); // 10
    }
}
```

   
ex:  
---  

```java
class Test 
{
    public static void main(String[] args) 
    {
        String str = "100";
         
        Integer i = Integer.valueOf(str);
         
        System.out.println(i); // 100
    }
}
```

   
   
2) xxxValue()   
-------------  
It is used to convert wrapper object to primitive type.  
   
ex:  
---  

```java
class Test 
{
    public static void main(String[] args) 
    {
        Integer i = Integer.valueOf(10);
         
        byte b = i.byteValue();
        System.out.println(b); 
         
        short s = i.shortValue();
        System.out.println(s); 
         
        int a = i.intValue();
        System.out.println(a); 
    }
}
```

   
   
3) parseXxx()  
-------------  
It is used to convert String type to primitive type.  
   
ex:  
---  

```java
class Test 
{
    public static void main(String[] args) 
    {
        String str = "200";
         
        int a = Integer.parseInt(str);
        System.out.println(a); 
         
        float f = Float.parseFloat(str);
        System.out.println(f); 
         
        double d = Double.parseDouble(str);
        System.out.println(d); 
    }
}
```

   
4) toString()   
--------------  
It is used to convert primitive type or wrapper object to string type.  
   
ex:  
---  

```java
class Test 
{
    public static void main(String[] args) 
    {
        Integer i = Integer.valueOf(10);
         
        String s = i.toString();
         
        System.out.println(s);
    }
}
```

   
ex:  
---  

```java
class Test 
{
    public static void main(String[] args) 
    {
        int a = 200;
        String s = Integer.toString(a);
        System.out.println(s);
    }
}
```

   
   
Q) Write a java program to perform sum of two binary numbers?  
   
Input:  
1010  
0101  
Output:  
1111  
   
   

```java
import java.util.Scanner;
class Test 
{
    public static void main(String[] args) 
    {
        Scanner sc = new Scanner(System.in);
         
        System.out.println("Enter the first binary number :");
        String binary1 = sc.next(); // 1010
         
        System.out.println("Enter the second binary number :");
        String binary2 = sc.next();  // 0101
         
        //convert binary to decimal number 
        int a = Integer.parseInt(binary1,2);  //10
        int b = Integer.parseInt(binary2,2);  //5
         
        int c = a + b;
         
        //convert decimal to binary number 
        String result = Integer.toBinaryString(c);
        System.out.println(result);
    }
}
```

   
   
   
Q) What is Autoboxing and Autounboxing ?   
   
Autoboxing   
==========  
Automatic conversion from primitive type to wrapper object performed by the compiler at the time of compilation is called autoboxing.  
   
Autoboxing internally uses valueOf() method.  
   
ex:  
---  

```java
class Test 
{
    public static void main(String[] args) 
    {
        //primitive type 
        int a = 10;
         
        //wrapper object 
        Integer i = a;
         
        System.out.println(i); //10
    }
}
```

   
   
Autounboxing  
------------  
Automatic convertion from wrapper object to primitive type performed by the compiler at the time of compilation is called autounboxing.  
   
Autounboxing internally uses xxxValue() method.  
   
ex:  
--  

```java
class Test 
{
    public static void main(String[] args) 
    {
        //wrapper object
        Integer i = Integer.valueOf(20);
             
        //primitive type 
        int a = i;
         
        System.out.println(a); // 20
    }
}
```

   
   
   
Inner classes   
============  
Sometimes we will declare a class inside another class such concept is called inner class.  
ex:  

```java
class Outer
{
    class Inner
    {        
     
    }
}
```

   
Inner classes introduced in 1.1 version as a part of event handling to remove GUI bugs.  
   
Due to powerful features and benefits of inner classes. Programmers started to use inner classes in regular programming.  
   
Inner class must declare within the scope of enclosing class.  
   
Inner class does not accept static members.  
   
We have four types of inner classes in java.  
   
1) Normal/Regular inner class  
   
2) Static inner class   
   
3) Method local inner class   
   
4) Anonymous inner class   
   
1) Normal/Regular inner class  
-----------------------------  
Sometime we will declare a class inside another class is called normal or regular inner class.  
   
ex:  
---  

```java
class Outer 
{
    class Inner 
    {
        public void methodOne()
        {
            System.out.println("Method One");
        }
    }
     
    public static void main(String[] args)
    {
        Outer.Inner i = new Outer().new Inner();
        i.methodOne();
         
        //or
         
        new Outer().new Inner().methodOne();
    }
}
```

Note:  
----  
Once if we compile above program we will get two .class files i.e   
Outer.class and  Outer$Inner.class.  
   
   
2) Static inner class   
---------------------  
Sometimes we will declare a class inside another class using static keyword is called static inner class.  
   
In regular/normal inner class, without existing container object there is no chance of having contained object.  
   
ex:  
---  

```java
class Outer 
{
    static class Inner 
    {
        public void methodOne()
        {
            System.out.println("MethodOne");
        }
    }
     
    public static void main(String[] args)
    {
        Inner i = new Inner();
        i.methodOne();
    }
}
```

   
   
3) Method local inner class  
----------------------------  
Sometimes we will declare class inside a method is called method local inner class.  
   
The main objective of method local inner class to execute method specific repeated  logic.  
   
ex:  
---  

```java
class Outer 
{
    public void m1()
    {
        class Inner 
        {
            public void sum(int a,int b)
            {
                System.out.println(a+b);
            }
        }
        Inner i = new Inner();
        i.sum(1,2);
        i.sum(10,20);
        i.sum(100,200);
    }
    public static void main(String[] args)
    {
        Outer o = new Outer();
        o.m1();
    }
}
```

   
   
4) Anonymous inner class  
------------------------  
Sometimes we will declare a class without name such type of nameless class is called anonymous inner class.  
   
ex:  
---  

```java
interface ATM
{
    public abstract void deposit();
}
class Test
{
    public static void main(String[] args)
    {
        //anonymous inner class
        ATM atm = new ATM()
        {
            public void deposit()
            {
                System.out.println("Deposit Method");
            }
        };
        atm.deposit();
    }
}
```

   
ex:  
---  

```java
abstract class Payment
{
    public abstract void paymentMethod();
}
class Test
{
    public static void main(String[] args)
    {
        //anonymous inner class
        Payment p = new Payment()
        {
            public void paymentMethod()
            {
                System.out.println("Card Payment");
            }
        };
        p.paymentMethod();
    }
}
```

   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
