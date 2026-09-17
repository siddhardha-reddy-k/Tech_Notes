   
Q)   
   
A frog falls into a 10-meter-deep well. Every day, the frog jumps up 2 meters but rollback for 1 meter at the end of the day. Write a Java program to determine how many days it will take for the frog to come out of the well.  
   
   

```java
class Test  
{
    public static void main(String[] args) 
    {
        int wellLength = 10;
        int jumps = 2;
        int rollback = 1;
         
        int currentPosition = 0;
        int days = 0;
        while(currentPosition<wellLength)
        {
            currentPosition += jumps;
            if(currentPosition>wellLength)
            {
                break;
            }
            currentPosition -= rollback;
            days++;
        }
        System.out.println("In "+days+" days frog will come out of the well");
    }
}
```

   
Q) Write a java program to find out reverse of a given number ?  
   
input:  
123  
output:  
ThreeTwoOne  
   
   

```java
import java.util.Scanner;
class Test  
{
    public static void main(String[] args) 
    {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter the number :");
        int n = sc.nextInt(); // 123
         
        while(n>0)
        {
            switch(n%10)
            {
                case 0 : System.out.print("Zero"); break;
                case 1 : System.out.print("One"); break;
                case 2 : System.out.print("Two"); break;
                case 3 : System.out.print("Three"); break;
                case 4 : System.out.print("Four"); break;
                case 5 : System.out.print("Five"); break;
                case 6 : System.out.print("Six"); break;
                case 7 : System.out.print("Seven"); break;
                case 8 : System.out.print("Eight"); break;
                case 9 : System.out.print("Nine"); break;
            }
            n = n/10;
        }        
    }
}
```

   
iii) for loop   
=============  
It is used to execute the source code how long our condition is true.  
   
syntax:  
-------  

```java
for(initialization;condition;incrementation/decrementation)
{
```

-  
- //code to be execute  
-  
}  
   
Note:  
-----  
   
If number of iterations are known by the user then we need to use for loop.  
   
If number of iterations are not known by the user then we need to use while loop.  
   
If number of iterations are not known by the user but code must execute atleast for one time then we need to use do while loop.  
   
ex:  
---  

```java
class Test  
{
    public static void main(String[] args) 
    {
        for(int i=1;i<=10;i++)
        {
            System.out.print(i+" ");//1 2 3 4 5 6 7 8 9 10
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
        for(int i=1;i<=10;i++)
        {
            if(i%2==0)
            {
                System.out.print(i+" "); // 2 4 6 8 10
            }
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
        int cnt = 0;
        for(int i=1;i<=10;i++)
        {
            if(i%2!=0)  // 1 3 5 7 9 
            {
                cnt++;
            }
        }
        System.out.println(cnt);//5
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
        for(int i=1;i<=10;i++)
        {
            if(i%2==0) 
            {
                System.out.print(i+" "); // 2 6 10
                i+=2;
            }
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
        for(;;)
        {
            System.out.print("Hello "); // infinite Hello 
        }
    }
}
```

   
Q) Write a java program to find out given number is prime or not?  
   
Input:  
5  
   
Output:  
It is a prime number   
   
   

```java
import java.util.Scanner;
class Test  
{
    public static void main(String[] args) 
    {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter the number :");
        int n = sc.nextInt(); // 10
         
        boolean flag = true;
        for(int i=2;i<=n/2;i++)
        {
            if(n%i==0)
            {
                flag = false;
                break;
            }
        }
        if(flag==true)
            System.out.println("It is a prime number");
        else
            System.out.println("It is not a prime number");
    }
}
```

   
   
Q) Write a java program to display prime numbers from 1 to 100?  
   
Output:  
2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41,   
43, 47, 53, 59, 61, 67, 71, 73, 79, 83, 89, 97  
   
   

```java
class Test  
{
    public static void main(String[] args) 
    {
        for(int n=2;n<=100;n++)
        {
            boolean flag = true;
            for(int i=2;i<=n/2;i++)
            {
                if(n%i==0)
                {
                    flag = false;
                    break;
                }
            }
            if(flag==true)
                System.out.print(n+" ");
        }
     
    }
}
```

   
   
   
   
Q) Write a java program to find out given number is perfect or not?  
   
Input:  
6  
   
Output:  
It is a perfect number   
   

```java
import java.util.Scanner;
class Test  
{
    public static void main(String[] args) 
    {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter the number :");
        int n = sc.nextInt(); // 6 
         
        int sum = 0;
        for(int i=1;i<n;i++)
        {
            if(n%i==0)    
            {
                sum += i;
            }
        }
        if(n==sum)
            System.out.println("It is a perfect number");
        else
            System.out.println("It is not a perfect number");
    }
}
```

   
   
Q) Write a java program to find out fibonacci series of a given number?  
   
input:  
6  
   
output:  
0 1 1 2 3 5 8  
   

```java
import java.util.Scanner;
class Test  
{
    public static void main(String[] args) 
    {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter the number :");
        int n = sc.nextInt(); // 6 
         
        int a=0,b=1,c;
        System.out.print(a+" "+b+" ");
         
        for(int i=2;i<=n;i++)
        {
            c = a + b;
            System.out.print(c+" ");
            a = b;
            b = c;
        }
    }
}
```

   
   
Q) Write a java program to find out GCD (Greatest Common Divisor) of two numbers?  
   
input:  
12    18  
   
output:  
6  
   
   

```java
class Test  
{
    public static void main(String[] args) 
    {
        int a=12, b=18;
        int gcd = 0;
        for(int i=1;i<=a && i<=b;i++)
        {
            if((a%i==0) && (b%i==0))
            {
                gcd = i;
            }
        }
        System.out.println("GCD of two numbers is ="+gcd);
    }
}
```

   
   
Assignments   
===========  
1. Monkey Climbing a Tree  
   
A monkey is trying to climb a 20-meter tree. Every day it climbs 4 meters and every night it slips down 2 meters. Write a Java program to find out how many days the monkey takes to reach the top.  
   

```java
public class Test {
    public static void main(String[] args) {
        int treeHeight = 20;
        int perDayClimb = 4;
        int perNightSlip = 2;
        int currentHeight = 0;
        int dayCount = 0;
        while (currentHeight < treeHeight) {
            dayCount++;
            currentHeight += perDayClimb;
            if (currentHeight >= treeHeight) {
                break;
            }
            currentHeight -= perNightSlip;
        }
        System.out.println("It takes " + dayCount + " days.");
    }
}
```

   
2. Water Tank Filling  
   
A water tank can hold 1000 liters of water. Every hour, 150 liters are poured into the tank, while 30 liters leak out. Write a Java program to determine how many hours it will take to fill the tank.  
   
   
   

```java
public class Test {
    public static void main(String[] args) {
        int waterTankCapcity = 1000;
        int perHourFilled = 150;
        int perHourLeaked = 30;
        int currentWaterInTheTank = 0;
        int hours = 0;
        while (currentWaterInTheTank < waterTankCapcity) {
            hours++;
            currentWaterInTheTank += perHourFilled;
            if (currentWaterInTheTank >= waterTankCapcity) {
                break;
            }
            currentWaterInTheTank -= perHourLeaked;
        }
        System.out.println("It takes " + hours + " to fill the tank.");
    }
}
```

   
   
   
3. Saving Money  
   
Rahul has a goal of saving ₹10,000. Every month, he saves ₹1,200 but spends ₹200 on entertainment. Write a Java program to calculate how many months it will take Rahul to achieve his goal.  
   
   

```java
public class Test {
    public static void main(String[] args) {
        int goal = 10000;
        int spend = 200;
        int save = 1200;
        int currentSavings = 0;
        int monthsCount = 0;
        while (currentSavings < goal) {
            monthsCount++;
            currentSavings += save;
            if (currentSavings >= goal) {
                break;
            }
            currentSavings -= spend;
        }
        System.out.println("it takes " + monthsCount + " months.");
    }
}
// 10000 - 1200;
// 8800 / 1200 = 8.8
// 1000 * 8 = 8000;
// 9th month = 8000+1200 -> 9200 - 200 = 9000
// 10th month = 9000 + 1200 = 10200;
```

   
   
4. Elevator Problem  
   
An elevator starts from the ground floor and needs to reach the 25th floor. Every trip, it goes up 5 floors but comes down 1 floor before going up again. Write a Java program to determine how many trips are required.  
   
   

```java
public class Test {
    public static void main(String[] args) {
        int target = 25;
        int goesUp = 5;
        int comesDown = 1;
        int currentFloor = 0;
        int trips = 0;
        while (currentFloor < target) {
            trips++;
            currentFloor += goesUp;
            if (currentFloor >= target) {
                break;
            }
            currentFloor -= comesDown;
        }
        System.out.println(trips);
    }
}
```

   
   
5. Battery Charging  
   
A mobile phone battery is at 0%. It charges by 18% every hour but loses 3% due to background apps. Write a Java program to determine how many hours are required to reach 100% charge.  
   
   
   

```java
public class Test {
    public static void main(String[] args) {
        int target = 100;
        int chargePerHour = 18;
        int chargeLost = 3;
        int currentBattery = 0;
        int hours = 0;
        while (currentBattery < target) {
            hours++;
            currentBattery += chargePerHour;
            if (currentBattery >= target) {
                break;
            }
            currentBattery -= chargeLost;
        }
        System.out.println(hours);
    }
}
```

   
   
   
