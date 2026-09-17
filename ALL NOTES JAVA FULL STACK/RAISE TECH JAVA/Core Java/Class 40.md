   
Q) Write a java program to multiply two arrays?  
   
input:  
3 6 7  
2 1   
output:  
7707 (367*21)  
   

```java
class Test 
{
    public static void main(String[] args) 
    {
        int[] arr1 = {3,6,7};
        int[] arr2 = {2,1}; 
        int a = Integer.parseInt(arrayToString(arr1));
        int b = Integer.parseInt(arrayToString(arr2));
        System.out.println(a*b);
    }
    public static String arrayToString(int[] arr)
    {
        StringBuffer sb = new StringBuffer();
        for(int i : arr)
        {
            sb.append(i);
        }
        return sb.toString();
    }
}
```

   
Q) Write a java program to find out occurance of 2's in a given number?  
   
Input:  
22  
   
Output:  
6 (2,12,20,21,22)  
   
   

```java
class Test 
{
    public static void main(String[] args) 
    {
        int n = 22;
        StringBuffer sb = new StringBuffer();
        for(int i=1;i<=n;i++)
        {
            sb.append(i);
        }
        int cnt = 0;
        for(int i=0;i<sb.length();i++)
        {
            if(sb.charAt(i) == '2')
            {
                cnt++;
            }
        }
        System.out.println(cnt);
    }
}
```

   
   
StringBuilder   
=============  
StringBuilder exactly same as StringBuffer with following differences.  
   
| StringBuffer | StringBuilder |
| --- | --- |
| Methods are synchronized. | Methods are not synchronized. |
| At a time only one thread is allocate<br>operate StringBuffer object. Hence<br>we can achieve thread safety. | Multiple threads are allowed to operate<br>StringBuilder object. Hence we can't achieve<br>thread safety. |
| Waiting time of threads will increase<br>effectively performance is low. | There is no waiting threads effectively<br>performance is high. |
| It is introduced in 1.0 version. | It is introduced in 1.5 version. |
   
   
Q) Write a java program to display reverse of a given number?  
   
input:  
123  
   
output:  
321  
   

```java
class Test 
{
    public static void main(String[] args) 
    {
        int n=123;
        String str = Integer.toString(n);
         
        StringBuilder sb = new StringBuilder(str);
        str = sb.reverse().toString();
         
        n = Integer.parseInt(str);
        System.out.println(n);
    }
}
```

   
Note:  
-----  
If our content is fixed then we need to use String.  
(It is a immutable object)  
   
If our content change frequently where thread safety is required then we need to use StringBuffer.  
(It is a mutable object)  
   
If our content change frequently where thread safety is not required then we need to use StringNuilder.  
(It is a mutable object)  
   
   
StringTokenizer   
================  
StringTokenizer class present in java.util package.  
   
It is used to tokenize the string based on delimeter.  
   
We can create StringTokenizer object as follow.  
ex:  

```java
StringTokenizer st = new StringTokenizer(String str,Regular Exp);
```

   
StringTokenizer class contains following methods.  
   
ex:  
public boolean hasMoreTokens()  
public String nextToken()  
public boolean hasMoreElements()          
public Object nextElement()  
public int countTokens()  
   
The String.split() method is the recommended approach for modern Java applications, while StringTokenizer is a legacy utility class   
   
ex:  
---  

```java
import java.util.StringTokenizer;
class Test 
{
    public static void main(String[] args) 
    {
        StringTokenizer st = new StringTokenizer("this is java class"," ");
        System.out.println(st.countTokens());
    }
}
```

   
ex:  
---  

```java
import java.util.StringTokenizer;
class Test 
{
    public static void main(String[] args) 
    {
        StringTokenizer st = new StringTokenizer("this is java class"," ");
        while(st.hasMoreTokens())
        {
            String s = st.nextToken();
            System.out.println(s);
        }
    }
}
```

   
ex:  
---  

```java
import java.util.StringTokenizer;
class Test 
{
    public static void main(String[] args) 
    {
        StringTokenizer st = new StringTokenizer("this is java class"," ");
        while(st.hasMoreElements())
        {
            String s = (String)st.nextElement();
            System.out.println(s);
        }
    }
}
```

   
ex:  
---  

```java
import java.util.StringTokenizer;
class Test 
{
    public static void main(String[] args) 
    {
        StringTokenizer st = new StringTokenizer("9,99,999",",");
        while(st.hasMoreElements())
        {
            String s = (String)st.nextElement();
            System.out.println(s);
        }
    }
}
```

   
   
   
Exception Handling   
==================  
Q) What is the difference between Exception and Error?  
   
Exception   
---------  
Exception is a problem for which we can provide solution programmatically.  
Exceptions will occur due to syntax errors.  
ex:  
ArithmeticException   
FileNotFoundException   
NullPointerException  
   
Error   
-----  
Error is a problem for which we can't provide solution programmatically.  
Errors will occur due to lack of system resources.  
ex:  
OutOfMemoryError   
StackOverFlowError  
LinkageError  
   
As a part of java application development it is a responsibility of a programmer to provide smooth termination for every java program.  
   
We have two types of terminations.  
   
1) Smooth termination / Graceful termination  
   
2) Abnormal termination   
   
1) Smooth termination  
--------------------  
During the program execution suppose if we are not getting any interruption in the middle of the program such type of termination is called smooth termination.  
   
ex:  
----  

```java
class Test 
{
    public static void main(String[] args) 
    {
        System.out.println("Smooth termination");
    }
}
```

   
2) Abnormal termination   
--------------------  
During the program execution suppose if we are getting some interruptions in the middle of the program such type of termination is called abnormal termination.  
   
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

o/p:  
R.E : ArithmeticException  
   
If any exception raised in our program we must and should handle that exception otherwise our program will terminate abnormally.  
   
Here exception will display name of the exception, description of the exception and line number of the exception.  
   
Exception   
=========  
It is unwanted , unexpected event which disturbs normal flow of a program.  
   
Exceptions always raised at runtime so they are also known as runtime events.  
   
The main objective of exception handling is to provide graceful termination.  
   
In java, exceptions are divided into two types.  
   
1) Predefined exceptions   
   
2) Userdefined exceptions   
   
1) Predefined exceptions   
------------------------  
Built-In exceptions are called predefined exceptions.  
   
It is categorized into two types.  
   
Diagram: class40.1  
   
i) Checked Exceptions  
----------------------  
Exceptions which are checked by the compiler at the time of compilation are called checked exceptions.  
ex:  
InterruptedException   
FileNotFoundException  
IOException   
   
ii) Unchecked Exceptions    
-----------------------  
Exceptions which are checked by the JVM at the time of runtime are called unchecked exceptions.  
ex:  
ArithmeticException  
ClassCastException   
IllegalArgumentException   
   
If any checked exception raised in our program we must and should handle that exception by using try and catch block.  
   
try block   
=========  
It is a block which contains risky code.  
   
It is associate with catch block and finally block.  
   
It is used to throw the exceptions in catch block.  
   
If exception raised in try block then it won't be executed.  
   
catch block   
===========  
It is a block which contains error handling code.  
   
It is always associate with try block.  
   
It is used to catch the exceptions which is thrown by try block.  
   
If there is no exception in try block then catch block won't be executed.  
   
A catch block will take exception name as parameter and that name must match exception class name.  
   
syntax:  
------  
try   
{  
-  
- // Risky Code   
-  
}  

```java
catch(Exception e)
{
```

-  
- // Error Handling Code  
-  
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
            System.out.println("catch-block");
        }
    }
}
```

o/p:  
try-block   
   
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
            System.out.println("catch-block");
        }
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
            System.out.println("stmt1");
            System.out.println(10/0);
            System.out.println("stmt3");
        }
        catch (ArithmeticException ae)
        {
            System.out.println("catch-block");
        }
    }
}
```

o/p:  
stmt1  
catch-block  
   
   
Q) Write a java program to display Hello World without using print stmt?  
   
   

```java
import java.io.*;
class Test 
{
    public static void main(String[] args) 
    {
        try
        {
            String str = "Hello World";
            System.out.write(str.getBytes());
        }
        catch (IOException ioe)
        {
            System.out.println("Exception Occured");
        }
    }
}
```

   
   
ex:  
---  

```java
import java.io.*;
class Test 
{
    //static block 
    static
    {
        System.out.println("static-block");
    }
     
    public static void main(String[] args) 
    {
        try
        {
            Class.forName("Test");                
        }
        catch (ClassNotFoundException cnfe)
        {
            System.out.println("Exception occured");
        }
    }
}
```

   
   
   
   
   
   
   
   
   
   
   
   
