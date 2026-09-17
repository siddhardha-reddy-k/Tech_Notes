   
Control statements   
==================  
Control statements enable the programmer to control the flow of the program.  
   
Control statements allow us to make decisions, to execute the code repeatedly and to jump from one section of code to another section.  
   
In java, we have three types of control statements.  
   
1) Decision Making statements   
   
2) Iteration statements   
   
3) Jump statements   
   
   
1) Decision Making statements  
-----------------------------  
Decision making statements are used to declare conditions in our program.  
   
Decision making statement is possible by using following ways.  
   
i) if stmt   
   
ii) if else stmt   
   
iii) if else if ladder   
   
iv) nested if stmt   
   
v) switch case   
   
   
i) if stmt   
==========  
It is used to execute the source code only if our condition is true.  
   
syntax:  
-------  

```java
if(condition)
{
```

-  
- // code to be execute   
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
         
        if(5>2)
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
        System.out.println("stmt1");
         
        if(!(5>2))
        {
            System.out.println("stmt2");
        }
         
        System.out.println("stmt3");
    }
}
```

o/p:  
stmt1  
stmt3  
   
ex:  
---  

```java
class Test  
{
    public static void main(String[] args) 
    {
        if((5>2) && (6<1))
            System.out.println("stmt1");
            System.out.println("stmt2");
            System.out.println("stmt3");
    }
}
```

o/p:  
stmt2  
stmt3  
   
   
Q) Write a java program to find out greatest of two numbers?  
   

```java
import java.util.Scanner;
class Test  
{
    public static void main(String[] args) 
    {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter two numbers :");
        int a = sc.nextInt(); // 5
        int b = sc.nextInt(); // 10
         
        if(a>b)
            System.out.println(a+" is greatest");
         
        if(b>a)
            System.out.println(b+" is greatest");
    }
}
```

   
Q) Write a java program to find out greatest of three numbers?  
   

```java
import java.util.Scanner;
class Test  
{
    public static void main(String[] args) 
    {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter three numbers :");
        int a = sc.nextInt(); // 5
        int b = sc.nextInt(); // 10
        int c = sc.nextInt(); // 2
         
        if((a>b) && (a>c))
            System.out.println(a+" is greatest");
         
        if((b>a) && (b>c))
            System.out.println(b+" is greatest");
         
        if((c>a) && (c>b))
            System.out.println(c+" is greatest");
    }
}
```

   
ii) if else stmt   
================  
It is used to execute the source code either our condition is true or false.  
   
syntax:  
-------  

```java
if(condition)
{
```

- //code to be execute if cond is true   
}  
else  
{  
- //code to be execute if cond is false  
}  
   
ex:  
---  

```java
class Test  
{
    public static void main(String[] args) 
    {
        System.out.println("stmt1");
         
        if(true)
        {
            System.out.println("stmt2");
        }
        else
        {
            System.out.println("stmt3");
        }
         
        System.out.println("stmt4");
    }
}
```

o/p:  
stmt1  
stmt2  
stmt4  
ex:  
---  

```java
class Test  
{
    public static void main(String[] args) 
    {
        System.out.println("stmt1");
         
        if(false)
        {
            System.out.println("stmt2");
        }
        else
        {
            System.out.println("stmt3");
        }
         
        System.out.println("stmt4");
    }
}
```

o/p:  
stmt1  
stmt3  
stmt4  
   
   
Q) Write a java program to find out given age is eligible to vote or not?  
   

```java
import java.util.Scanner;
class Test  
{
    public static void main(String[] args) 
    {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter the age :");
        int age = sc.nextInt();
         
        if(age>=18)
            System.out.println("U r eligible to vote");
        else
            System.out.println("U r not eligible to vote");
    }
}
```

   
Q) Write a java program to check given number is even or odd ?  
   

```java
import java.util.Scanner;
class Test  
{
    public static void main(String[] args) 
    {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter the number :");
        int n = sc.nextInt(); // 10 
     
        if(n%2==0)
            System.out.println("It is even number");
        else
            System.out.println("It is odd number");
         
    }
}
```

   
   
Q) Write a java program to find out given number is odd or not?  
   

```java
import java.util.Scanner;
class Test  
{
    public static void main(String[] args) 
    {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter the number :");
        int n = sc.nextInt(); // 10 
     
        if(n%2!=0)
            System.out.println("It is odd number");
        else
            System.out.println("It is not odd number");
         
    }
}
```

   
Q) Write a java program to check given number is positive or negative?  
   
   

```java
import java.util.Scanner;
class Test  
{
    public static void main(String[] args) 
    {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter the number :");
        int n = sc.nextInt(); // 10 
         
        if(n==0)
        {
            System.out.println("It is not a positive or negative number");
            System.exit(0);
        }
     
        if(n>0)
            System.out.println("It is positive number");
        else
            System.out.println("It is negative number");
         
    }
}
```

   
   
Q) John wants to buy new shoes. He visited a big showroom to purchase new shoes. But he has a myth that if shoe price divisible by 3 and 5 then only he can buy that shoe.  
Write a java program to find out john can buy the shoe or not?  
   
input:  
1500  
   
output:  
John can buy the shoe   
   

```java
import java.util.Scanner;
class Test  
{
    public static void main(String[] args) 
    {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter the show price:");
        int price = sc.nextInt(); 
         
        if((price%3==0) && (price%5==0))
            System.out.println("John can buy the shoe");
        else
            System.out.println("John can't buy the shoe");
    }
}
```

   
Q) Write a java program to find out given year is a leap year or not?  
   

```java
import java.util.Scanner;
class Test  
{
    public static void main(String[] args) 
    {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter the year:");
        int year = sc.nextInt(); 
         
        if(year%4==0 && year%100!=0 || year%400==0)
            System.out.println("It is a leap year");
        else
            System.out.println("It is not a leap year");
    }
}
```

   
   
Q) Write a java program to check given alphabet is a vowel or not?  
   

```java
import java.util.Scanner;
class Test  
{
    public static void main(String[] args) 
    {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter the alphabet:");
        char ch = sc.next().charAt(0); 
         
        if(ch=='a' || ch=='e' || ch=='i' || ch=='o' || ch=='u')
            System.out.println("It is a vowel");
        else
            System.out.println("It is not a vowel");
    }
}
```

   
   
3) if else if ladder   
===================  
It is used to execute the source code based on multiple conditions.  
   
syntax:  
-------  

```java
if(cond1)
{
```

- //code to be execute if cond1 is true   
}  
else if(cond2)  
{  
- //code to be execute if cond2 is true   
}  
else if(cond3)  
{  
- //code to be execute if cond3 is true   
}  
else  
{  
- //code to be execute if all conditions are false  
}  
   
   
ex:  
---  

```java
import java.util.Scanner;
class Test  
{
    public static void main(String[] args) 
    {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter the option :");
        int option = sc.nextInt();
         
        if(option==100)
            System.out.println("It is a police number");
        else if(option == 103)
            System.out.println("It is a enquiry number");
        else if(option == 108)
            System.out.println("It is a emergency number");
        else
            System.out.println("Invalid option");
         
    }
}
```

   
Q) Write a java program to find out given alphabet is a uppercase letter, lowercase letter, digit or a special symbol?  
   

```java
import java.util.Scanner;
class Test  
{
    public static void main(String[] args) 
    {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter the Alphabet :");
        char ch = sc.next().charAt(0); 
         
        if(Character.isUpperCase(ch))
            System.out.println("It is a uppercase letter");
        else if(Character.isLowerCase(ch))
            System.out.println("It is a lowercase letter");
        else if(Character.isDigit(ch))
            System.out.println("It is a digit");
        else
            System.out.println("It is a special symbol");
         
    }
}
```

   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
