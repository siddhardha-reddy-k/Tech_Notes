   
Bitwise XOR operator (^)  
------------------------  
Bitwise XOR operator deals with binary numbers.  
   
Truth table   
-----------  
T        T        = F  
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
        int a = 10, b = 15;
        int c = a ^ b;
        System.out.println(c);  // 5 
    }
}
/*
    10 - 1010
    15 - 1111
    ---------
    ^  - 0101  <----
     
    1*1 + 0*2 + 1*4 + 0*8
     
    1 + 0 + 4 + 0  = 5
*/
```

   
Bitwise NOT operator (~)  
-------------------------  
syntax:  
------  
-(n+1)  
   
ex:  
---  

```java
class Test  
{
    public static void main(String[] args) 
    {
        int i = ~10;
        System.out.println(i); // -11
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
        int i = ~(-21);
        System.out.println(i); // 20
    }
}
```

   
   
Q) Write a java program to find out given number is even or odd?  
   

```java
import java.util.Scanner;
class Test  
{
    public static void main(String[] args) 
    {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter the number :");
        int n = sc.nextInt(); // 10 
         
        String result = ((n&1)==0)?"It is even number":"It is odd number";        
        System.out.println(result);
    }
}
/*
    10 - 1010
    1  - 0001
    ---------
    &  - 0000
*/
```

   
   
5) Logical operators   
====================  
   
Logical AND operator (&&)  
-------------------------  
Logical AND operator deals with boolean values either true or false.  
   
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
        System.out.println(true && true); // true 
        System.out.println(true && false); // false 
        System.out.println(false && true); // false 
        System.out.println(false && false); // false 
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
        boolean b = (5>2) && (6<10);
        System.out.println(b); // true 
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
        boolean b = (5>2) && (6<1);
        System.out.println(b); // false 
    }
}
```

   
Logical OR operator (||)  
------------------------  
Logical OR operator deals with boolean values either true or false.  
   
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
        boolean b = (5>6) || (6<10);
        System.out.println(b); // true 
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
        boolean b = (5>6) || (6<1);
        System.out.println(b); // false 
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
        boolean b = (5>20) || (6<10) && (10==10);
        System.out.println(b); // true
    }
}
```

   
   
   
Logical NOT operator (!)  
-----------------------  
Logical NOT operator deals with binary numbers either true or false.  
   
ex:  
---  

```java
class Test  
{
    public static void main(String[] args) 
    {
        boolean b = !(5>2);
        System.out.println(b); // false
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
        boolean b = !(5>20);
        System.out.println(b); // true
    }
}
```

   
6) Relational operators   
=======================  
   
ex:  
---  

```java
class Test  
{
    public static void main(String[] args) 
    {
        System.out.println(10 > 20); // false 
        System.out.println(10 >= 20); // false 
         
        System.out.println(10 < 20); // true 
        System.out.println(10 <= 20); // true 
                 
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
        System.out.println(10 == 10); // true 
        System.out.println(10 == 20); // false
         
        System.out.println(10 != 20); // true 
        System.out.println(10 != 10); // false        
    }
}
```

   
7) Shift operators   
===================  
   
Right shift operator(>>)  
------------------------  

```java
class Test  
{
    public static void main(String[] args) 
    {
        int i = 10 >> 2;
        System.out.println(i); // 10/2*2 = 10/4 = 2
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
        int i = 100 >> 4;
        System.out.println(i); // 100/2*2*2*2 = 100/16 = 6
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
        int i = 10 >> 6;
        System.out.println(i); // 10/2*2*2*2*2*2 = 10/64 = 0
    }
}
```

   
Left Shift operator (<<)  
------------------------  
ex:  
---  

```java
class Test  
{
    public static void main(String[] args) 
    {
        int i = 10 << 4;
        System.out.println(i); // 10 * (2*2*2*2)  = 10*16 = 160
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
        int i = 100 << 2;
        System.out.println(i); // 100 * (2*2) = 100*4 = 400
    }
}
```

   
8) Unary operators   
===================  
   
   
Increment/Decrement operators (++/--)  
-------------------------------------  
We have two types of increment operators.  
   
1) Post Increment   
ex:  
i++;  
   
2) Pre Increment   
ex:  
++i;  
   
We have two types of decrement operators.  
   
1) Post Decrement   
ex:  
i--;  
   
2) Pre Decrement   
ex:  
--i;  
   
   
Post Increment/Decrement   
------------------------  
Rule1: First Take    
Rule2: Then Change   
   
ex:  
---  

```java
class Test  
{
    public static void main(String[] args) 
    {
        int i = 10;
         
        i++;
         
        System.out.println(i); // 11
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
        System.out.println(i++); // 10
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
        int j = i++;
        System.out.println(i+" "+j); // 11  10
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
        int j = i--;
        System.out.println(i+" "+j); // 9  10
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
        int j = i++ + i++; // 10 + 11
        System.out.println(i+" "+j); // 12  21
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
        int j = i-- + i-- + i--; // 10 + 9 + 8 
        System.out.println(i+" "+j); // 7  27
    }
}
```

   
Pre Increment/Decrement   
-----------------------  
Rule1: First Change   
Rule2: Then Take   
   
   
ex:  
---  

```java
class Test  
{
    public static void main(String[] args) 
    {
        int i = 10;
        ++i;
        System.out.println(i); // 11
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
        System.out.println(++i); // 11
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
        int j = ++i;
        System.out.println(i+" "+j); // 11  11
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
        int j = --i + --i; // 9 + 8 
        System.out.println(i+" "+j); // 8  17
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
        int i = 100;
         
        100++;
         
        System.out.println(i); // C.T.E 
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
        System.out.println((++i)++); // C.T.E 
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
        System.out.println(i++ + ++i); // 10+12 = 22
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
        byte b = 127;
         
        b++;
         
        System.out.println(b); // -128
    }
}
```

   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
