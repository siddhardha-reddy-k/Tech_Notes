   
System.out.println()  
====================  
It is a output statement in java.  
   
Whenever we want to display any user defined statements, data or expression then we need to use output statement in java.  
   
syntax:  
-------          
static variable   
|  
System.out.println()  
|                |  
predefined        predefined method  
final class           
   
Diagram: class13.1  
![[attachments/image13.png]]  
   
ex:  
---  

```java
class Test
{
    public static void main(String[] args)
    {
        System.out.print("IHUB");
        System.out.print("TALENT");        
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
        System.out.println("IHUB");
        System.out.println("TALENT");        
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
        double d = 10.123456789d;
        System.out.printf("%.2f",d); 
    }
}
```

   
Various ways to print the output in java  
----------------------------------------  
   
1) custom message  
   ex:  

```java
System.out.println("Hi");
```

   
2) int a=10;   
   ex:  

```java
System.out.println(a);
System.out.println("The value is ="+a);
System.out.println(a+" is the value");
```

   
3) int a=10,b=20;  
   ex:  

```java
System.out.println(a+" "+b);
System.out.println(a+" and "+b);
System.out.println(a+","+b);
```

   
4) int a=1,b=2,c=3;  
   ex:  

```java
System.out.println(a+" "+b+" "+c);
```

   
   
Fully Qualified Name   
====================  
Sometimes we will declare a class or interface along with package name such concept is called fully qualified name.  
ex:  
java.io.File(C)   
java.util.Iterator(I)   
   
Fully qualified name improves readability of our code.  
   
ex:  

```java
class Test
{
    public static void main(String[] args)
    {
        java.util.Date d = new java.util.Date();
        System.out.println(d);          
    }
}        
```

   
Note:  
-----  
We will use fully qualified name when a classes or interfaces   
present in two difference packages and we required both of them in our   
program.  
ex:  
java.util.Date  
java.sql.Date  
   
ex:  
---  

```java
class Test
{
    public static void main(String[] args)
    {
        java.util.Date d = new java.util.Date();
        int h = d.getHours();
        int m = d.getMinutes();
        int s = d.getSeconds();
        System.out.println(h+" : "+m+" : "+s);          
    }
}
```

   
   
