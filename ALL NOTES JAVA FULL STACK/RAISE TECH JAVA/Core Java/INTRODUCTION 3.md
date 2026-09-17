   
Escape Characters or Escape Sequences  
=====================================  
Escape characters are used to design our output in neat and clean manner.  
   
Escape characters start with back slash(\) followed by a character.  
ex:  
\n  
   
Mostly escape characters are placed inside output statement in java.  
ex:  

```java
System.out.println("\n");
```

   
We have following list of escape characters in java.  
   
1) \n (new line)  
   
2) \t (horizontal tab)  
   
3) \b (back space)  
   
4) \r (carriage return)  
   
5) \f (form feeding)  
   
6) \\ (back slash)  
   
7) \" (double quote)  
   
8) \' (single quote)  
   
and etc.  
   
1) \n (new line)  
----------------  

```java
class Siddu
{
    public static void main(String[] args)
    {
        System.out.println("IHUB\nTALENT");
    }        
}
```

o/p:  
IHUB  
TALENT  
   
2) \t (horizontal tab)  
----------------------  

```java
class Sahil
{
    public static void main(String[] args)
    {
        System.out.println("IHUB\tTALENT");
    }        
}
```

o/p:  
IHUB        TALENT  
   
3) \b (back space)  
------------------  

```java
class Pranish
{
    public static void main(String[] args)
    {
        System.out.println("IHUBTAL\bENT");        
    }
}
```

o/p:  
IHUBTAENT  
   
ex:  
---  

```java
class Vandik
{
    public static void main(String[] args)
    {        
        System.out.println("IHUB\b\b\bTALENT");
    }
}
```

o/p:  
ITALENT  
   
   
4) \r (carriage return)  
-----------------------  

```java
class Hari
{
    public static void main(String[] args)
    {
        System.out.println("IHUB\rTALENT");
    }
}
```

o/p:  
TALENT  
   
ex:  
---  

```java
class Radhika
{
    public static void main(String[] args)
    {
        System.out.println("TALENT\rIHUB");
    }
}
```

o/p:  
IHUBNT  
   
5) \f (form feeding)  
---------------------  

```java
class Laxmi 
{
    public static void main(String[] args)
    {
        System.out.println("I\fLove\fJava");
    }
}
```

o/p:  
I  
 Love  
     Java  
   
6) \\ (back slash)  
-------------------  

```java
class Ranga
{
    public static void main(String[] args)
    {
        System.out.println("IHUB\\TALENT");
    }
}
```

o/p:  
IHUB\TALENT  
   
C program   
=========  
Q) Write a c program to display %d ?  
   

```java
void main()
{
    clrscr();
     
    printf("%%d"); // %d
 
    getch();
}
```

   
7) \" (double quote)  
--------------------  

```java
class Saniya
{
    public static void main(String[] args)
    {
        System.out.println("I love \"java\" programming");
    }
}
```

o/p:  
I love "java" programming  
   
   
8) \' (single quote)  
--------------------  

```java
class Sai
{
    public static void main(String[] args)
    {
        System.out.println("I love 'java' programming");        
        System.out.println("I love \'java\' programming");
 
    }
}
```

o/p:  
I love 'java' programming  
I love 'java' programming  
   
Screening Test   
==============  
Q) What will be the output of below snippet ?   
   

```java
class Example
{
    public static void main(String[] args)
    {
        System.out.print("\nkj");
        System.out.print("\bpi");
        System.out.print("\rha");
    }
}
```

o/p:  
hai   
   
   
