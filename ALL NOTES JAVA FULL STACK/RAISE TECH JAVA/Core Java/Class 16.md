   
Typecasting in java  
===================  
Process of converting from one datatype to another datatype is called typecasting.  
   
In java, typecasting can be performed in two ways.  
   
1) Implicit typecasting   
   
2) Explicit typecasting   
   
   
   
1) Implicit typecasting   
-----------------------  
If we want to store small value into a bigger variable then we need to use implicit typecasting.  
   
A compiler is responsible to perform implicit typecasting.  
   
There is no possibility to loss the information.  
   
It is also known as Widening or Upcasting.  
   
We can perform implicit typecasting as follow.  
   
ex:  
byte        -->        short  
-->  
int -->        long --> float --> double                                        -->  
char  
   
ex:  
---  

```java
class Test 
{
    public static void main(String[] args) 
    {
        byte b = 10;
        int i = b;
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
        char ch = 'a';
        int i = ch;
        System.out.println(i); // 97
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
        int i = 10;
        float f = i;
        System.out.println(f);//  10.0
    }
}
```

   
   
2) Explicit typecasting   
----------------------  
If we want to store bigger value into small variable then we need to use explicit typecasting.  
   
A programmer is responsible to perform explicit typecasting.  
   
There is a possibility to loss the information.  
   
It is also known as Narrowing or Downcasting.  
   
We can perform explicit typecasting as follow.  
   
ex:  
byte        <--        short  
<--  
int <--        long <-- float <-- double                                        <--  
char  
   
ex:  
---  

```java
class Test 
{
    public static void main(String[] args) 
    {
        double d = 10.56d;
        int i = (int)d;
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
        int i = 65;
        char ch = (char)i;
        System.out.println(ch); // A
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
        int i = 130;
        byte b = (byte)i;
        System.out.println(b); // -126
    }
}
```

   
   
Q) Write a java program to accept employee salary and find out 10% of TDS?  
   
   

```java
import java.util.Scanner;
class Test 
{
    public static void main(String[] args) 
    {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter the employee salary :");
        int salary = sc.nextInt();
         
        double tds = (double)salary*10/100; 
         
        System.out.println("10 percent of TDS is ="+tds);
    }
}
```

   
   
Q) Write a java program to accept six marks of a student then find out total and average?  
   
   

```java
class Test 
{
    public static void main(String[] args) 
    {
        int m1=89,m2=45,m3=39,m4=77,m5=81,m6=74;
         
        int total = m1+m2+m3+m4+m5+m6;
         
        double average = (double)total/6;
         
        System.out.println("Total :"+total);
        System.out.println("Average :"+average);
    }
}
```

   
   
Types of blocks   
===============  
A block is a set of statements which is enclosed in a curly braces i.e {}.  
   
We have three types of blocks in java.  
   
1) Instance block   
   
2) Static block   
   
3) Local block   
   
   
1) Instance block  
-----------------  
Instance block is used to initialize instance variables.  
   
Instance block must and should declare immediately after the class.  
   
Instance block will execute when instance of a class is created.  
   
We can declare instance block as follow.  
   
syntax:  
-------          

```java
//instance block 
{
```

-  
- // set of statements  
-  
}  
   
ex:  
---  

```java
class Test 
{
    //instance block
    {
        System.out.println("instance-block");
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
    //instance block
    {
        System.out.println("instance-block");
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
instance-block   
   
   
ex:  
---  

```java
class Test 
{
    //instance block
    {
        System.out.println("instance-block");
    }
     
    public static void main(String[] args) 
    {
        Test t1 = new Test();
        System.out.println("main-method");        
        Test t2 = new Test();
    }
}
```

o/p:  
instance-block  
main-method  
instance-block   
   
   
ex:  
---  

```java
class Test 
{
    //instance variable
    int i;
     
    //instance block 
    {
        i = 100;
    }
     
    public static void main(String[] args) 
    {
        Test t = new Test();
        System.out.println(t.i);//100
    }
}
```

   
   
2) Static block   
---------------  
Static block is used to initialize static variables.  
   
Static block must and should declare immediately after the class using static keyword.  
   
Static block will execute at the time of class loading.  
   
We can declare static block as follow.  
   
syntax:  
-------  

```java
//static block 
```

static  
{  
-  
- // set of statements  
-  
}  
   
ex:  
---  

```java
class Test 
{
    //static block 
    static
    {
        System.out.println("static-block");
    }
     
    public static void main(String[] args) 
    {
        System.out.println("main-method");
    }
}
```

o/p:  
static-block   
main-method  
   
ex:  
---  

```java
class Test 
{
    //instance block
    {
        System.out.println("instance-block");
    }
    //static block 
    static
    {
        System.out.println("static-block");
    }
     
    public static void main(String[] args) 
    {
        System.out.println("main-method");
        Test t = new Test();
    }
}
```

o/p:  
static-block   
main-method  
instance-block   
   
ex:  
---  

```java
class Test 
{
    //static variable 
    static boolean b;
     
    //static block 
    static 
    {
        b = true;
    }
     
    public static void main(String[] args) 
    {
        System.out.println(b); //true
    }
}
```

   
Q) Can we execute java program without main method?  
   
Till 1.6 version it is possible to execute java program without main method using static block. But from 1.7 version onwards it is not possible to execute java program without main method.  
   
ex:  
---  

```java
class Test 
{
    static
    {
        System.out.println("Hello World");
        System.exit(0);
    }
}
```

   
3) Local block   
--------------  
Local block is used to initialize local variables.  
   
Local block must and should declare inside methods and constructors.  
   
Local block will execute just like a normal statement.  
   
We can declare local block as follow.  
   
syntax:  
-----  

```java
//local block 
{
```

-  
- //set of statements   
-  
}  
   
ex:  
---  

```java
class Test 
{
     
    public static void main(String[] args)
    {
        System.out.println("stmt1");
         
        //local block 
        {
            System.out.println("stmt2");
        }
         
        System.out.println("stmt3");
    }
}
```

o/p:  
stmt1  
stmt2  
stmt3  
   
ex:  
---  

```java
class Test 
{
    public static void main(String[] args)
    {
        //local variable 
        int i;
         
        //local block 
        {
            i = 200;
        }
         
        System.out.println(i); // 200
    }
}
```

   
   
Assignment   
==========  
Q) Write a java program to convert CGPA to percentage?  
   
Q) Write a java program to convert time to seconds?  
   
input:  
h = 10           
m = 23    
s = 30  
   
output:  
37410  
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
