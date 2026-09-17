   
Import Statements  
=================  
A import keyword makes other classes and interfaces to visibility in a current class.  
   
Whenever we use import statements we should not use fully qualified name.  
   
We have three types of import statements in java.  
   
1) Explicit class import   
   
2) Implicit class import   
   
3) Static import   
   
1) Explicit class import   
------------------------  
This type of import statement is highly recommanded to use because it improves readability of our code.  
   
ex:  
---  

```java
import java.time.LocalDate;
import java.time.LocalTime;
class Test
{
    public static void main(String[] args)
    {
        LocalDate date = LocalDate.now();
        System.out.println(date);
 
        LocalTime time = LocalTime.now();
        System.out.println(time);        
    }
}
```

   
   
2) Implicit class import   
-----------------------  
This type of import statement is not recommanded to use because it reduce readability of our code.  
   
ex:  
---  

```java
import java.time.*;
class Test
{
    public static void main(String[] args)
    {
        LocalDateTime ldt = LocalDateTime.now();
        System.out.println(ldt);         
 
        LocalDate date = LocalDate.now();
        System.out.println(date);
 
        LocalTime time = LocalTime.now();
        System.out.println(time);        
    }
}
```

   
   
3) static import   
----------------  
Using static import we can call static members (static variables and static methods) directly.  
   
Often use of static import makes our program complex and unreadable.  
   
ex:  
---  
import static java.lang.System.*;  

```java
class Test
{
    public static void main(String[] args)
    {
        out.println("stmt1");
        out.println("stmt2");
        out.println("stmt3");        
    }
}
```

   
ex:  
---  
import static java.lang.System.*;  

```java
class Test
{
    public static void main(String[] args)
    {
        out.println("stmt1");
        exit(0);
        out.println("stmt3");        
    }
}
```

   
   
   
   
   
   
   
   
   
   
   
   
   
   
