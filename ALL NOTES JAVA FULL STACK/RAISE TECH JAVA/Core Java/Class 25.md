   
Various ways to declare methods in java  
=======================================  
There are four ways to declare methods in java.  
   
1) No returntype with No argument method   
2) No returntype with argument method   
3) With returntype with No argument method  
4) With returntype with argument method  
   
1) No returntype with No argument method  
----------------------------------------  
If there is no arguments then we need to ask input values inside callie method.  
   
ex:  
---  

```java
import java.util.Scanner;
class Test  
{
    public static void main(String[] args) 
    {
        //caller method 
        sum();
    }
    //callie method 
    public static void sum()
    {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter the two numbers :");
        int a = sc.nextInt();//10
        int b = sc.nextInt();//20 
        int c = a + b;
        System.out.println("Sum of two numbers is ="+c);
    }
}
```

   
   
2) No returntype with argument method   
-------------------------------------  
If we have arguments then we need to ask input values inside main method.  
Number of arguments depend upon number of inputs.  
   
ex:  
---  

```java
import java.util.Scanner;
class Test 
{
    public static void main(String[] args)
    {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter two numbers :");
        int a = sc.nextInt();//10
        int b = sc.nextInt();//20
         
        //caller method 
        sum(a,b);
    }
    //callie method
    public static void sum(int a,int b)
    {
        int c = a + b;
        System.out.println("Sum of two numbers is ="+c);
    }
}
```

   
3) With returntype with No argument method  
------------------------------------------  
A returntype is completely depend upon output datatype.  
At a time we can only one value.  
   
ex:  
--  

```java
import java.util.Scanner;
class Test 
{
    public static void main(String[] args)
    {
        //caller method 
        int k = sum();
        System.out.println("Sum of two numbers is ="+k);
    }
    //callie method 
    public static int sum()
    {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter two numbers :");
        int a = sc.nextInt(); // 10
        int b = sc.nextInt(); // 20 
        int c = a + b;
        return c;
    }
}
```

   
   
4) With returntype with argument method  
---------------------------------------  

```java
import java.util.Scanner;
class Test 
{
    public static void main(String[] args)
    {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter two numbers :");
        int a = sc.nextInt();//50
        int b = sc.nextInt();//20
         
        //caller method
        System.out.println("sum of two numbers is = "+sum(a,b));
    }
    //callie method 
    public static int sum(int a,int b)
    {
        int c = a + b;
        return c;
    }
}
```

   
Q) Write java program to find out given number is even or odd?  
   

```java
class Test 
{
    public static void main(String[] args)
    {
        //code here 
    }
     
    public static boolean find(int n)
    {
        //code here         
    }
}
```

   
solution   
--------  

```java
import java.util.Scanner;
class Test 
{
    public static boolean find(int n)
    {
        if(n%2==0)
            return true;
        else 
            return false;
    }
     
    public static void main(String[] args)
    {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter the number :");
        int n = sc.nextInt(); // 10
         
        //caller method 
        if(find(n))
            System.out.println("It is even number");
        else
            System.out.println("It is odd number");
    }
}
```

   
Recursion   
=========  
Recursion is a programming technique which breaks down complex problem into sub-problems.  
   
A method which call itself for many number of times is called recursion.   
   
Recursion is similar to loopings so whenever we use recursion we should not use loops.  
   
Q) Write a java program to display 10 natural numbers without using loops?  
   
   

```java
class Test 
{
    public static void main(String[] args)
    {
        //caller method
        display(1);
    }
    //callie method 
    public static void display(int i)
    {
        if(i<=10)
        {
            System.out.print(i+" ");
            display(i+1);
        }
    }
}
```

   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
