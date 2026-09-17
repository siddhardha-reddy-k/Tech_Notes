   
EditPlus Editor   
================  
Download link :  [https://www.editplus.com/download.html](<https://www.editplus.com/download.html>)  
   
   
Java Basic Programs  
======================  
   
   
Q) Write a java program to perform sum of two numbers?  
   

```java
import java.util.Scanner;
class Example1 
{
    public static void main(String[] args) 
    {
        Scanner sc = new Scanner(System.in);
         
        System.out.println("Enter the first number :");
        int a = sc.nextInt();//10
         
        System.out.println("Enter the second number :");
        int b = sc.nextInt();//20
         
        int c = a + b;
         
        System.out.println("sum of two numbers is ="+c);
    }
}
```

   
   
Q) Write a java program to find out square of a given number?  
   
Input:  
5  
   
Output:  
25  
   
   

```java
import java.util.Scanner;
class Example2
{
    public static void main(String[] args) 
    {
        Scanner sc = new Scanner(System.in);
         
        System.out.println("Enter the number :");
        int n = sc.nextInt();//5
         
        int square = n*n;
         
        System.out.println("Square of a given number is ="+square);
    }
}
```

   
   
Q) Write a java program to find out cube of a given number?  
   
input:  
5  
   
output:  
125  
   
   

```java
import java.util.Scanner;
class Example3
{
    public static void main(String[] args) 
    {
        Scanner sc = new Scanner(System.in);
         
        System.out.println("Enter the number :");
        int n = sc.nextInt(); // 5 
         
        int cube = (int)Math.pow(n,3);
         
        System.out.println("Cube of a given numebr is ="+cube);
    }
}
```

   
   
   
Q) Write a java program to find out area of a circle?  
   
Input:  
5  
Output:  
78.5  
   

```java
import java.util.Scanner;
class Example4
{
    public static void main(String[] args) 
    {
        Scanner sc = new Scanner(System.in);
         
        System.out.println("Enter the radius :");
        int r = sc.nextInt(); // 5 
         
        double area = 3.14d * Math.pow(r,2);
         
        System.out.println("Area of a circle is = "+area);
    }
}
```

   
   
Q) Write a java program to find out perimeter of a circle?  
   
Input:  
5  
   
Output:  
31.42  
   
   

```java
import java.util.Scanner;
class Example5
{
    public static void main(String[] args) 
    {
        Scanner sc = new Scanner(System.in);
         
        System.out.println("Enter the radius :");
        int r = sc.nextInt(); // 5 
         
        double perimeter = 2 * Math.PI * r; 
         
        System.out.printf("Perimeter of a circle is = %.2f",perimeter);
    }
}
```

   
   
Q) Write a java program to find out swapping of two numbers ?  
   
input:  
a=10, b=20  
   
output:  
Before swapping a=10 and b=20  
After swapping a=20 and b=10  
   

```java
import java.util.Scanner;
class Example6
{
    public static void main(String[] args) 
    {
        Scanner sc = new Scanner(System.in);
         
        System.out.println("Enter two numbers :");
        int a = sc.nextInt(); //10
        int b = sc.nextInt(); //20
         
        System.out.println("Before swapping a="+a+" and b="+b);
         
        //logic
        int temp = a;
        a = b;
        b = temp;
         
        System.out.println("After swapping a="+a+" and b="+b);
    }
}
```

   
   
Q) Write a java program to find out swapping of two numbers without using third variable?  
   
input:  
a=10, b=20  
   
output:  
Before swapping a=10 and b=20  
After swapping a=20 and b=10  
   
   

```java
import java.util.Scanner;
class Example7
{
    public static void main(String[] args) 
    {
        Scanner sc = new Scanner(System.in);
         
        System.out.println("Enter two numbers :");
        int a = sc.nextInt(); //10
        int b = sc.nextInt(); //20
         
        System.out.println("Before swapping a="+a+" and b="+b);
         
        //logic
        a = a + b;
        b = a - b;
        a = a - b;
         
        System.out.println("After swapping a="+a+" and b="+b);
    }
}
```

   
   
   
Q)  
There is one running race between different participants. So in that race two partners need to finish the race. There is four rounds of race in that each lane length is 100m.So in that one participant will cover 30% of the lane length and another partner will cover remaining length of lane. So print each participant covers distance in that race.  
   

```java
import java.util.Scanner;
class Example8
{
    public static void main(String[] args) 
    {
        int lane = 100;
        int rounds = 4;
        int firstParticipantPercent = 30;
         
        int firstParticipant = lane * rounds * firstParticipantPercent/100;
        int secondParticipant = lane * rounds - firstParticipant;
         
    System.out.println("First partcipant covered "+firstParticipant+" distance");
    System.out.println("Second partcipant covered "+secondParticipant+" distance");
    }
}
```

   
Q)  
Alice is planning to organize a contest with 4 players in each team.   
   
There are two types of players named Experienced and Freshers.   
To make the contest unbiased Alice wants to have a team in such a way that each team must   
contain at least 1 Experienced and 1 Fresher.  
You are given N the number of Experienced and M the number of Freshers.   
Your task is to determine the maximum number of team formations possible.  
Example:  
   
Input:  
5 5  
Output:  
2  
   
Input:  
10  1  
   
Output:   
1  
   
ex:  
---  

```java
import java.util.Scanner;
class Example9
{
    public static void main(String[] args) 
    {
        int N=10, M=1;
         
        int teams = Math.min((N+M)/4, Math.min(N,M));
         
        System.out.println(teams);
    }
}
```

   
   
   
Q) Write a java program to accept date of birth of a person and find out his age?  
   
   

```java
import java.time.LocalDate;
import java.time.Period;
class Example10
{
    public static void main(String[] args) 
    {
        LocalDate dob = LocalDate.of(2004,2,8);
        LocalDate curr_date = LocalDate.now();
         
        Period p = Period.between(dob,curr_date);
         
        int age = p.getYears();
         
        System.out.println("You are "+age+" years old");
    }
}
```

   
   
   
   
Q)A car travels 120 km in 2 hours.  
Write a Java program to calculate the average speed of the car.  
   
formulea :   

```java
average speed = distance/time;
```

   
   
   

```java
class Example11
{
    public static void main(String[] args) 
    {
        int distance = 120;
        int time = 2;
         
        int average_speed = distance/time;
         
        System.out.println(average_speed);
    }
}
```

   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
