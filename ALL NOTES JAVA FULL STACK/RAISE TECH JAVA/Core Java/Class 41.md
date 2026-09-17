   
A try with multiple catch blocks   
=================================  
A try block can have multiple catch blocks.  
   
If a try block contains multiple catch blocks then order of catch blocks is very important it should be from child to parent but not from parent to child.  
   
ex:  
---  

```java
class Test  
{
    public static void main(String[] args) 
    {
        try
        {
            System.out.println(10/0);
        }
        catch (ArithmeticException ae)
        {
            System.out.println("From AE");
        }
        catch (RuntimeException re)
        {
            System.out.println("From RE");
        }
        catch (Exception e)
        {
            System.out.println("From E");
        }
    }
}
```

   
Various ways to display exception details  
========================================  
Throwable class define following three methods to display exception details.  
   
1) printStackTrace()  
-------------------  
It is used to display name of the exception, description of the exception and line number of the exception.  
   
2) toString()  
------------  
It is used to display name of the exception and description of the exception.  
   
3) getMessage()   
---------------  
It is used to display description of the exception.  
   
ex:  
--  

```java
class Test  
{
    public static void main(String[] args) 
    {
        try
        {
            System.out.println(10/0);
        }
        catch(ArithmeticException ae)
        {
            ae.printStackTrace();
             
            System.out.println("==================");
             
            System.out.println(ae.toString());
             
            System.out.println("==================");
             
            System.out.println(ae.getMessage());
        }
    }
}
```

   
Q) Can we handle multiple exceptions in a single catch block ?  
   
Yes, it is possible to handle multiple exceptions in a single catch block.  
   
ex:  
--  

```java
class Test  
{
    public static void main(String[] args) 
    {
        try
        {
            //System.out.println(10/0);
             
            int[] arr = null;
            System.out.println(arr[0]);
        }
        catch(ArithmeticException | NullPointerException e)
        {
            e.printStackTrace();
        }
    }
}
```

   
finally block   
=============  
It is never recommanded to maintain cleanup code in try block because if any exception raised in try block then it won't executed.  
   
It is never recommanded to maintain cleanup code in catch block because if there is no exception in try block then catch block won't be executed.  
   
We need a place where we can maintain cleanup code and it should execute irrespective of exception raised or not such block is called finally block.  
   
syntax:  
------  
try   
{  
- //Risky code   
}  

```java
catch(Exception e)
{
```

- //Error handling code          
}  
finally  
{  
- // cleanup code   
}  
   
ex:  
---  

```java
class Test  
{
    public static void main(String[] args) 
    {
        try
        {
            System.out.println("try-block");
        }
        catch (Exception e)
        {
            e.printStackTrace();
        }
        finally
        {
            System.out.println("finally-block");
        }
    }
}
```

   
ex:  
--  

```java
class Test  
{
    public static void main(String[] args) 
    {
        try
        {
            System.out.println(10/0);
        }
        catch (ArithmeticException ae)
        {
            ae.printStackTrace();
        }
        finally
        {
            System.out.println("finally-block");
        }
    }
}
```

   
   
o/p:  
   
java.lang.ArithmeticException: / by zero  
        at Test.main(Test.java:7)  
finally-block  
   
ex:  
----  

```java
class Test  
{
    public static void main(String[] args) 
    {
        try
        {
            System.out.println("stmt1");
            System.out.println(10/0);
            System.out.println("stmt2");
        }
        catch (ArithmeticException ae)
        {
            ae.printStackTrace();
        }
        finally
        {
            System.out.println("finally-block");
        }
    }
}
```

o/p:  
stmt1  
java.lang.ArithmeticException: / by zero  
        at Test.main(Test.java:8)  
finally-block  
   
ex:  
---  

```java
class Test  
{
    public static void main(String[] args) 
    {
        int i = 1;
        try
        {
            i++;
        }
        catch (Exception e)
        {
            i++;
        }
        finally
        {
            i++;
        }
        System.out.println(i);//3
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
        try
        {
            System.out.println("try-block");
            return 0;
        }
        catch (Exception e)
        {
            System.out.println("catch-block");
            return 1;
        }
        finally
        {
            System.out.println("finally-block");
            return 2;
        }
    }
}
```

   
o/p:  
C.T.E   
   
ex:  
--  

```java
class Test  
{
    public static void main(String[] args) 
    {
        System.out.println(display());
    }
    public static int display()
    {
        try
        {
            System.out.println("try-block");
            return 0;
        }
        catch (Exception e)
        {
            System.out.println("catch-block");
            return 1;
        }
        finally
        {
            System.out.println("finally-block");
            return 2;
        }
    }
}
```

o/p:  
try-block   
finally-block   
2  
   
A try with finally combination is valid in java.  
   
ex:  
---  

```java
class Test  
{
    public static void main(String[] args) 
    {
        try
        {
            System.out.println("try-block");
        }
        finally
        {
            System.out.println("finally-block");
        }
    }
}
```

o/p:  
try-block   
finally-block   
   
   
   
   
Q) What is the difference between final, finally and finalize?  
   
final  
-----  
A final is a modifier which is applicable for variables, methods and classes.  
   
If we declare any variable as final then reinitialization of that variable is not possible.  
   
If we declare any method as final then overriding of that method is not possible.  
   
If we declare any class as final then creating child class is not possible.  
   
   
finally  
-------  
It is a block which contains cleanup code and it should execute irrespective of exception raised or not.  
   
finalize   
--------  
It is a method called by garbage collector just before destroying an object for cleanup activity.  
   
   
Garbage Collector   
=================  
Garbage collector is also known as Daemon thread.  
   
Deamon thread is a leight weight thread which runs in a background to provide services.  
   
Garbage collector is a programming feature for memory allocation and deallocation.  
   
There are two ways to call garbage collector in java.  
   
1) System.gc()   
   
2) Runtime.getRuntime().gc()   
   
1) System.gc()   
--------------  

```java
class Test  
{
    public static void main(String[] args) 
    {
        Test t = new Test();
         
        t = null;
         
        System.gc();
    }
    public void finalize()
    {
        System.out.println("finalize method");
    }
}
```

   
2) Runtime.getRuntime().gc()  
-----------------------------  

```java
class Test  
{
    public static void main(String[] args) 
    {
        Test t = new Test();
         
        t = null;
         
        Runtime.getRuntime().gc();
    }
    public void finalize()
    {
        System.out.println("finalize method");
    }
}
```

   
throw statement   
===============  
Sometimes we will create exception objects explicitly and handover to JVM manually by   
using throw statement.  
   
ex:  

```java
throw new ArithmeticException("Divisible by zero");
```

   
ex:  
---  

```java
class Test  
{
    public static void main(String[] args) 
    {
        System.out.println(10/0);
    }
}
```

Here exception object is created and handover to JVM by main method.  
   
ex:  
---  

```java
class Test  
{
    public static void main(String[] args) 
    {
        throw new ArithmeticException("Don't divide by zero");
    }
}
```

Here exception object is created explicitly and handover to JVM manually by using   
throw statement.  
   
throws statement   
===============  
If any checked exception raised in our program we must and should handle that exception by using try and catch block or by using throws statement.  
   
ex:  
---  

```java
class Test  
{
    public static void main(String[] args) 
    {
        try
        {
            Thread.sleep(3000);
            System.out.println("Welcome to Java");
        }
        catch(InterruptedException ie)
        {
            ie.printStackTrace();
        }
         
    }
}
```

   
ex:  
---  

```java
class Test  
{
    public static void main(String[] args)throws InterruptedException 
    {
        Thread.sleep(5000);
        System.out.println("Welcome to Java");
    }
}
```

   
   
try-with-resources   
==================  
A try-with-resources introduced in Java 7.  
   
A try-with-resources is a try block which contains one or more resources.  
   
A try-with-resources ensures that each resource must closed at the end of the statement.   
   
This eliminates the need for manual cleanup in a finally block.  
   
syntax:  
-------  
try()  
{  
- //risky code  
}  

```java
catch(Exception e)
{
```

- //error handling code  
}  
   
   
ex:  
---  

```java
package com.ihub.www;
 
 
 
import java.util.Scanner;
public class Demo 
{
    public static void main(String[] args) 
    {
        Scanner sc = null;
        try
        {
            sc = new Scanner(System.in);
            System.out.println("Enter the name :");
            String name = sc.nextLine();                        
            System.out.println("Welcome :"+name);
        }
        catch(Exception e)
        {
            e.printStackTrace();
        }
        finally
        {
            sc.close();
        }
    }
}
```

   
ex:  
----  

```java
package com.ihub.www;
 
 
 
import java.util.Scanner;
public class Demo 
{
    public static void main(String[] args) 
    {
         
        try(Scanner sc = new Scanner(System.in);)
        {
            System.out.println("Enter the name :");
            String name = sc.nextLine();                        
            System.out.println("Welcome :"+name);
        }
        catch(Exception e)
        {
            e.printStackTrace();
        }
 
    }
}
```

   
2) Userdefined Exceptions   
========================  
Exceptions which are created by the user based on the application requirements are called userdefined exceptions.  
ex:  
NoInterestInCourseException   
NoPracticeNoJobException  
FundNotFoundException   
ACNotWorkingException   
   
ex:  
---  

```java
import java.util.Scanner;
class TooYoungException extends RuntimeException 
{
    public TooYoungException(String msg)
    {
        super(msg);
    }
}
class TooOldException extends RuntimeException 
{
    public TooOldException(String msg)
    {
        super(msg);
    }
}
class Test 
{
    public static void main(String[] args)
    {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter the age : ");
        int age = sc.nextInt();
         
        if(age<18)
            throw new TooYoungException("U r not eligible to vote");
        else
            throw new TooOldException("U r eligible to vote");
    }
}
```

   
   
   
   
