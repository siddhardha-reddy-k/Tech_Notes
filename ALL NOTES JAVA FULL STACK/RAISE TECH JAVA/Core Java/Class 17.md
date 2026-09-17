   
Operators   
=========  
Operator is a symbol which is used to perform some operations on operands.  
ex:  

```java
c = a + b;
```

   
Here a,b and c are operands.  
Here + and = are operators.  
   
We have following list of operators in java.  
   
1) Arithmetic operators   
2) Assignment operators   
3) Ternary operators/Conditional operators   
4) Bitwise operators   
5) Logical operators   
6) Relational operators   
7) Shift operators   
8) Unary operators   
   
1) Arithmetic operators   
-----------------------  
   
Operator Precedence   
-------------------  
No        operators  
---        ---------  
1         *, / , %   
2        +, -   
3        << , >>  
   
ex:  
---  

```java
class Test 
{
    public static void main(String[] args) 
    {
        int i = 10*5+10/3+10%2+6/10+7%20+6*5-20;
        System.out.println(i);
    }
}
/*
    10*5+10/3+10%2+6/10+7%20+6*5-20
     
    50+10/3+10%2+6/10+7%20+30-20
     
    50+3+10%2+0+7%20+30-20
     
    50+3+0+0+7+30-20
     
    90 - 20 
     
    70
*/
```

   
ex:  
---  

```java
class Test 
{
    public static void main(String[] args) 
    {
        int i = 5 + 10 / 2;
        System.out.println(i); // 10 
    }
}
```

   
2) Assignment operators  
-----------------------  
   
ex:  
---  

```java
class Test 
{
    public static void main(String[] args) 
    {
         int i = 10;
         
         i = 20;
         
         i = 30;
         
         System.out.println(i); // 30
    }
}
```

Note:  
-----  
Reinitialization is possible in java.  
   
   
ex:  
---  

```java
class Test 
{
    public static void main(String[] args) 
    {
         final int i = 10;
         
         i = 20;
         
         i = 30;
         
         System.out.println(i); // C.T.E  
    }
}
```

Note:  
-----  
We can't modify final vairable.  
   
   
ex:  
---  

```java
class Test 
{
    static int i = 10;
    public static void main(String[] args) 
    {
        int i = 100;
        System.out.println(i); // 100
    }
}
```

Note:  
-----          
Here priority goes to local variable.  
   
ex:  
---  

```java
class Test 
{
    public static void main(String[] args) 
    {
        int i = 1,2,3,4,5;
        System.out.println(i); // C.T.E 
    }
}
```

Note:  
-----  
We can't assign multiple values.  
   
ex:  
---  

```java
class Test 
{
    public static void main(String[] args) 
    {
        int i,j;
         
        i = j = 10;
         
        System.out.println(i+" "+j); //10  10
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
        int i = 10;
         
        i+=5; // i = i + 5 
         
        System.out.println(i); // 15
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
        int i = 10;
         
        i-=20; // i = i - 20 
         
        System.out.println(i); // -10
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
         
        i*=5; // i = i * 5 
         
        System.out.println(i); // 50
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
         
        i/=3; // i = i / 3;
         
        System.out.println(i); // 3
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
         
        i%=3; // i = i % 3;
         
        System.out.println(i); // 1 
    }
}
```

   
3) Ternary operators / Conditional operators   
-----------------------------------------  
syntax:  
------  
(condition)?value1:value2;  
   
ex:  
---  

```java
class Test 
{
    public static void main(String[] args) 
    {
        String str = (1)?"Hi":"Bye";
        System.out.println(str); // C.T.E 
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
        int i = (5>2)?1:0;
        System.out.println(i); // 1
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
        char ch = (5>7)?'T':'F';
        System.out.println(ch); // F 
    }
}
```

   
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
         
         int max = (a>b)?a:b;
         System.out.println(max+" is greatest");
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
         
         int max = (a>b)?((a>c)?a:c):((b>c)?b:c);
         System.out.println(max+" is greatest"); 
    }
}
```

   
   
How to convert decimal number to binary number   
----------------------------------------------  
   
10 - decimal number   
1010 - binary number   
   
2|10  
         ---- 0  
2|5   
         ---- 1   
2|2    
 ---- 0   
  1                  
   
   
How to convert binary number to decimal number   
----------------------------------------------  
   
1010 - binary number   
10   - decimal number   
   
   
1010 <----  
   
0*1 + 1*2 +  0*4 + 1*8  
   
 0  + 2 + 0 + 8  = 10   
   
   
4) Bitwise operators   
--------------------  
   
Bitwise AND operator (&)  
------------------------  
Bitwise AND operator deals with binary numbers.  
   
Truth table   
-----------  
T        T        = T  
T        F        = F  
F        T        = F   
F        F        = F   
   
ex:  
---  

```java
class Test 
{
    public static void main(String[] args) 
    {
        int a=10,b=15;
        int c = a & b;
        System.out.println(c); //10
    }
}
/*
    10 - 1010
    15 - 1111
    ---------
    &  - 1010  <---
     
    0*1 + 1*2 + 0*4  + 1*8 
     
    0 + 2 + 0 + 8 = 10
*/
```

   
Bitwise OR operator (|)  
-----------------------  
Bitwise OR operator deals with binary numbers.  
   
Truth table   
-----------  
T        T        = T  
T        F        = T  
F        T        = T  
F        F        = F   
   
ex:  
---  

```java
class Test 
{
    public static void main(String[] args) 
    {
        int a=10,b=5;
        int c = a | b;
        System.out.println(c); // 15
    }
}
/*
    10 - 1010
    5  - 0101
    ----------
    |  - 1111 <----
     
    1*1 +  1*2 + 1*4 + 1*8
     
    1 + 2 + 4 + 8 = 15
*/
```

   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
