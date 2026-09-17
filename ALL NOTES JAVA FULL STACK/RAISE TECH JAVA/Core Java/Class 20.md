   
Q) Write a java program to accept six marks of a student then find out total,average and grade?  
   
i) If average is greater than equals to 70 then A grade.  
   
ii) If average is greater than equals to 50 then B grade.  
   
iii) If average is greater than equals to 35 then C grade.  
   
iv) if average is less than 35 then failed.  
   
   
ex:  
---  

```java
import java.util.Scanner;
class Test  
{
    public static void main(String[] args) 
    {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter the six marks of a student :");
        int m1 = sc.nextInt();
        int m2 = sc.nextInt();
        int m3 = sc.nextInt();
        int m4 = sc.nextInt();
        int m5 = sc.nextInt();
        int m6 = sc.nextInt();
         
        int total = m1+m2+m3+m4+m5+m6;
        System.out.println("Total :"+total);
         
        double average = (double)total/6;
        System.out.printf("Average : %.2f"+average);
         
        if(average>=70)
            System.out.println("Grade : A grade");
        else if(average>=50)
            System.out.println("Grade : B grade");
        else if(average>=35)
            System.out.println("Grade : C grade");
        else
            System.out.println("Grade : Failed");
         
    }
}
```

   
iv) nested if stmt   
==================  
If stmt contains another if stmt is called nested if stmt.  
   
syntax:  
------  

```java
if(condition)
{
    if(condition)
    {
```

-  
- //code to be execute   
-  
}  
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
            if(true)
            {
                System.out.println("stmt3");
            }
            System.out.println("stmt4");
        }
        System.out.println("stmt5");
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
        System.out.println("stmt1");                
        if(5>20)
        {
            System.out.println("stmt2");
            if(true)
            {
                System.out.println("stmt3");
            }
            System.out.println("stmt4");
        }
        System.out.println("stmt5");
    }
}
```

o/p:  
stmt1  
stmt5  
   
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
            if(false)
            {
                System.out.println("stmt3");
            }
            System.out.println("stmt4");
        }
        System.out.println("stmt5");
    }
}
```

   
o/p:  
stmt1  
stmt2  
stmt4  
stmt5  
   
   
Q) Write a java program to find out given number is positive or negative using nested if stmt?  
   

```java
import java.util.Scanner;
class Test  
{
    public static void main(String[] args) 
    {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter the number :");
        int n = sc.nextInt(); // 5
         
        if(n!=0)
        {
            if(n>0)
            {
                System.out.println("It is a positive number");
                System.exit(0);
            }        
            System.out.println("It is a negative number");
        }
    }
}
```

   
   
   
  
Input:  
Enter total weight of items : 11  
Enter shipping destination  : domestic  
   
Output:  
Total Shipping Cost : 1100  
5kg(500) + 6kg(600)  
   
   
Output:  
Total Shipping Cost : 2700  
5kg(1000) + 6kg(1200) + 500  
   
ex:  
---  

```java
import java.util.Scanner;
class Test  
{
    public static void main(String[] args) 
    {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter total weight of items :");
        int weight = sc.nextInt(); //11
        System.out.println("Enter shipping destination :");
        String destination = sc.next().toLowerCase(); // domestic 
         
        int cost = 0;
         
        if(destination.equals("domestic"))
        {
            if(weight<=5)
            {
                cost = 500;
            }
            else
            {
                cost = 500 + (weight-5)*100;
            }
        }
        else if(destination.equals("international"))
        {
            if(weight<=5)
            {
                cost = 1000;
            }
            else if(weight>5 && weight<=10)
            {
                cost = 1000 + (weight-5)*200;
            }
            else
            {
                cost = 1000 + (weight-5)*200 + 500;
            }
        }
        System.out.println("Total Shipping Cost : "+cost);
    }
}
```

   
   
switch case   
===========  
It is used to execute the source code based on multiple conditions.  
   
It is similar to if else if ladder.  
   
syntax:  
------          

```java
switch(expression)
{
```

case value1 : //code to be execute  

```java
      break stmt;
```

   
case value2 : //code to be execute  

```java
      break stmt; 
```

   
-  
-  
default            : //code to be execute if all cases are false.  
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
        int option = sc.nextInt(); // 108 
         
        switch(option)
        {
            case 100 :        System.out.println("It is a police number");
                        break;
            case 103 :        System.out.println("It is a enquiry number");
                        break;
            case 108 :        System.out.println("It is a emergency number");
                        break;
            default  :  System.out.println("Invalid option");
        }
    }
}
```

   
Note:  
-----  
Declaration of break statement is optional.If we won't define break statement then from where our condition is satisfied from there all cases will be executed that state is called "Fall Through State" of switch case.  
   
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
        int option = sc.nextInt(); // 108 
         
        switch(option)
        {
            case 100 :        System.out.println("It is a police number");
                        //break;
            case 103 :        System.out.println("It is a enquiry number");
                        //break;
            case 108 :        System.out.println("It is a emergency number");
                        //break;
            default  :  System.out.println("Invalid option");
        }
    }
}
```

   
Note:  
-----  
The allowed datatype for switch case are byte,short,int,char and string.  
   
   
Q) Write a java program to find out given alphabet is a vowel or cosonent?  
   

```java
 import java.util.Scanner;
class Test  
{
    public static void main(String[] args) 
    {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter the Alphabet :");
        char ch = sc.next().charAt(0);
         
        //convert character to lowercase 
        ch = Character.toLowerCase(ch);
         
        switch(ch)
        {
            case 'a' : System.out.println("It is a vowel"); break;
            case 'e' : System.out.println("It is a vowel"); break;
            case 'i' : System.out.println("It is a vowel"); break;
            case 'o' : System.out.println("It is a vowel"); break;
            case 'u' : System.out.println("It is a vowel"); break;
            default  : System.out.println("It is a consonent");
        }
    }
}
```

   
Approach2  
---------  

```java
import java.util.Scanner;
class Test  
{
    public static void main(String[] args) 
    {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter the Alphabet :");
        char ch = sc.next().charAt(0);
         
        //convert character to lowercase 
        ch = Character.toLowerCase(ch);
         
        switch(ch)
        {
            case 'a' : 
            case 'e' : 
            case 'i' : 
            case 'o' : 
            case 'u' : System.out.println("It is a vowel"); break;
            default  : System.out.println("It is a consonent");
        }
    }
}
```

   
Approach3  
--------  

```java
import java.util.Scanner;
class Test  
{
    public static void main(String[] args) 
    {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter the Alphabet :");
        char ch = sc.next().charAt(0);
         
        //convert character to lowercase 
        ch = Character.toLowerCase(ch);
         
        switch(ch)
        {
        case 'a','e','i','o','u' -> System.out.println("It is a vowel");
        default  -> System.out.println("It is a consonent");
        }
    }
}
```

   
yield  
======  
A yield keyword introduced in Java 14.  
   
It is used to return the value from case block within the switch expression.  
   
   

```java
import java.util.Scanner;
class Test  
{
    public static void main(String[] args) 
    {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter the Day of a Week :");
        int day = sc.nextInt(); // 4
         
        String result = switch(day)
        {
            case 1,2,3,4,5 -> { yield "weekday"; }
            case 6,7 -> {yield "weekend"; }
            default -> {yield "invalid day"; }
        };
        System.out.println(result);
    }
}
```

   
   
var keyword  
==========  
A var keyword introduced in Java 10.  
It is used to enables local variable type inference.  
   
ex:  
---  

```java
class Test  
{
    public static void main(String[] args) 
    {
        var i = "Hi";
        System.out.println(i); 
    }
}
```

   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
