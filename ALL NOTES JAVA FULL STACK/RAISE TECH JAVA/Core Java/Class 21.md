   
2) Iteration statement   
======================  
Iteration statement is used to execute the source code repeatedly.  
   
Iteration statement is possible by using LOOPS.  
   
We have four types of loops in java.  
   
i) do while loop  
   
ii) while loop   
   
iii) for loop  
   
iv) for each loop - enhanced for loop   
   
i) do while loop  
================  
It executes the source code how long our condition is true.  
   
syntax:  
-------  
do   
{  
-  
- //code to be execute  
-  
}while(condition);  
   
ex:  
---  

```java
class Test  
{
    public static void main(String[] args) 
    {
        int i = 1;
        do
        {
            System.out.print(i+" "); // infinite 1 
        }
        while(i<=10);
    }
}
```

   
Note:  
-----  
In do while loop, our code will execute atleast for one time either our condition   
is true or false.  
   
ex:  
---  

```java
class Test  
{
    public static void main(String[] args) 
    {
        int i = 11;
        do
        {
            System.out.print(i+" "); // 11
        }
        while(i<=10);
    }
}
```

   
   
Q) Write a java program to display 10 natural numbers?  
   

```java
class Test  
{
    public static void main(String[] args) 
    {
        int i=1;
        do
        {
            System.out.print(i+" ");//1 2 3 4 5 6 7 8 9 10
             
            i++;
        }
        while (i<=10);
    }
}
```

   
   
Q) Write a java program to perform sum of 10 natural numbers?  
   

```java
class Test  
{
    public static void main(String[] args) 
    {
        int i=1,sum=0;
        do
        {
            sum = sum + i;
             
            i++;
        }
        while (i<=10);
         
        System.out.println(sum);
    }
}
```

   
Q) Write a java program to find out factorial of a given number?  
   
Input:  
5  
   
Output:  
120 (5*4*3*2*1)  
   
   

```java
import java.util.Scanner;
class Test  
{
    public static void main(String[] args) 
    {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter the number :");
        int n = sc.nextInt(); // 5
         
        int i=n,fact=1;
        do
        {
            fact = fact * i;
            i--;
        }
        while (i>=1);
        System.out.println(fact);
    }
}
```

   
Q) Write a java program to display multiplication table of a given number?  
   
Input:  
5  
   
Output:  
5 * 1 = 5  
-  
-  
5 * 10 = 50   
   
   

```java
import java.util.Scanner;
class Test  
{
    public static void main(String[] args) 
    {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter the number :");
        int n = sc.nextInt(); // 5
         
        int i=1;
        do
        {
            System.out.println(n+" * "+i+" = "+n*i);
             
            i++;
        }
        while (i<=10);
    }
}
```

   
ii) while loop   
==============  
It executes the source code how long our condition is true.  
   
syntax:  
-------  

```java
while(condition)
{
```

-  
- //code to be execute   
-  
}  
   
   
ex:  
---  

```java
class Test  
{
    public static void main(String[] args) 
    {
        int i = 1;
        while(i<=10)
        {
            System.out.print(i+" "); // infinite 1 
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
        int i = 11;
        while(i<=10)
        {
            System.out.print(i+" "); // nothing/ no output
        }
    }
}
```

   
   
Q) Write a java program to perform sum of digits of a given number ?  
   
input:  
123  
output:  
6 (1+2+3)  
   
   

```java
import java.util.Scanner;
class Test  
{
    public static void main(String[] args) 
    {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter the number :");
        int n = sc.nextInt(); // 123
         
        int rem , sum = 0;
        while(n>0)
        {
            rem = n%10;
            sum = sum + rem;
            n = n/10;
        }
        System.out.println(sum);        
    }
}
```

   
   
Q) Write a java program to find out special number?  
   
Input:  
798  
   
Output:  
6  
   
   

```java
import java.util.Scanner;
class Test  
{
    public static void main(String[] args) 
    {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter the number :");
        int n = sc.nextInt(); // 987
         
        while(n>9)
        {
            int rem , sum = 0;
            while(n>0)
            {
                rem = n%10;
                sum = sum + rem;
                    n = n/10;
            }
            n = sum;
        }
        System.out.println(n);
    }
}
```

   
   
Q) Write a java program to find out given number is armstrong or not?  
   
Input:  
153  
   
Output:  
It is a Armstrong number   
1*1*1+5*5*5+3*3*3 = 1 + 125 + 27 = 153  
   
ex:  
---  

```java
import java.util.Scanner;
class Test  
{
    public static void main(String[] args) 
    {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter the number :");
        int n = sc.nextInt(); // 153
         
        int temp = n;
         
        int rem, sum =0;
        while(n>0)
        {
            rem = n%10;
            sum = sum + rem * rem * rem;
            n = n/10;
        }
        if(temp == sum)
            System.out.println("It is a Armstrong number");
        else
            System.out.println("It is not a Armstrong number");
    }
}
```

   
Q) Write a java program to display reverse of a given number?  
   
input:  
123  
output:  
321  
   
   

```java
import java.util.Scanner;
class Test  
{
    public static void main(String[] args) 
    {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter the number :");
        int n = sc.nextInt(); // 123
         
        int rem, rev=0;
        while(n>0)
        {
            rem = n%10;
            rev = rev * 10 + rem;
            n = n/10;
        }
        System.out.println(rev);
    }
}
```

   
   
Q) Write a java program to find out given number is palindrome or not?  
   
Input:  
121  
   
Output:  
It is a palindrome number   
   
   

```java
import java.util.Scanner;
class Test  
{
    public static void main(String[] args) 
    {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter the number :");
        int n = sc.nextInt(); // 123
         
        int temp = n;
         
        int rem, rev=0;
        while(n>0)
        {
            rem = n%10;
            rev = rev * 10 + rem;
            n = n/10;
        }
        if(temp == rev)
            System.out.println("It is a palindrome number");
        else
            System.out.println("It is not a palindrome number");
    }
}
```

   
Assignment   
==========  
Q) Write a java program to display 10 natural numbers using while loop?  
   
Q) Write a java program to perform sum of 10 natural numbers using while loop?  
   
Q) Write a java program to find out factorial of a given number using while loop?  
   
   
   
   
   
   
   
   
   
   
   
   
   
   
