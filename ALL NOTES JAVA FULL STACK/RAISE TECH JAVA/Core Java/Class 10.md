   
ex:5  
-----  

```java
class Test
{
    public static void main(String[] args)        
    {
        Test t = new Test();
        t.methodOne();
    }
    public void methodOne()
    {
        System.out.println("Instance-Method");
    }
}
```

   
   
2) static variables  
-------------------  
A value of a variable which is not varied(changes) from object to object is called static variable.  
   
Static variable allocates memory at the time of classloading and it will destroy at the time of classunloading. Hence scope of static variable is same as scope of .class file.  
   
Static variables store in method area.  
   
Static variable must and should declare immediately after the class using static keyword but not inside methods, blocks and constructors.  
   
Static variable we can access directly from instance area as well as from static area.  
   
Static variable we can access by using object reference and class name.  
   
ex:1  
-----  

```java
class Test
{
    //static variable 
    static int i = 10;
 
    public static void main(String[] args)        
    {
        System.out.println(i); // 10
 
        Test t = new Test();
        System.out.println(t.i); // 10 
 
        System.out.println(Test.i); // 10
    }
}
```

   
Note:  
-----  
If we won't initialize any value to static variable then JVM will initialized default values.  
   
ex:2  
----  

```java
class Test
{
    //static variable 
    static String s;
         
    public static void main(String[] args)        
    {
        System.out.println(s); // null
 
        Test t = new Test();
        System.out.println(t.s); // null 
 
        System.out.println(Test.s); // null 
    }
}
```

   
Note:  
-----  
In java, only one copy of static variable will be created and shared to multiple objects.  
   
ex:3  
----  

```java
class Test
{
    //static variable 
    static int i = 10;
         
    public static void main(String[] args)        
    {
        Test t1 = new Test();
        Test t2 = new Test();
        System.out.println(t1.i); // 10
        System.out.println(t2.i); // 10
        t1.i=100;
        System.out.println(t1.i); // 100
        System.out.println(t2.i); // 100        
    }
}
```

   
ex:4  
----  

```java
class Test
{
    public static void main(String[] args)        
    {
        methodOne();
 
        Test t = new Test();
        t.methodOne();
 
        Test.methodOne();        
    }
    public static void methodOne()
    {
        System.out.println("static method");
    }        
}
```

   
   
3) Local variables   
------------------  
To meet temperory requirements a programmer will declare some variables inside methods, blocks and constructors such type of variables are called local variables.  
   
Local variable allocates memory at the of execution block and it will destroy when  execution block is executed. Hence scope of local variable is same as scope of execution block where it is declared.  
   
Local variables store in Java Stack memory.  
   
ex:1  
----  

```java
class Test
{
    public static void main(String[] args)        
    {
        //local variable 
        int i = 10;
        System.out.println(i);                
    }        
}
```

   
Note:  
-----  
If we won't initialize any value to local variable then JVM won't initialized default values.  
   
ex:2  
----  

```java
class Test
{
    public static void main(String[] args)        
    {
        //local variable 
        int i;
        System.out.println(i);         // C.T.E         
    }        
}
```

   
Note:  
-----  
A local variable will accept only one modifier i.e final.  
   
ex:3  
---  

```java
class Test
{
    public static void main(String[] args)        
    {
        //local variable 
        final int i=10;
        System.out.println(i);                
    }        
}
```

   
   
   
Interview Question   
===================  
   
Jack and John both are best friends in a town. One day while going to school they saw one  beggar. Both have decided to assist a needy person. Jack gave 100 rupees of his school fee and John gave 50 rupees from his pocket money. Write a java program to find out total contribution they have done to help a poor guy.  
   
Approach1  
---------  

```java
class Test
{
    //instance variables 
    int a = 100;
    int b = 50;
     
    public static void main(String[] args)        
    {
        Test t = new Test();
        t.sum();        
    }        
    //non-static method 
    public void sum()
    {
        System.out.println(a+b);
    }
}
```

   
Approach2  
---------  

```java
class Test
{
    //static variables 
    static int a = 100;
    static int b = 50;
     
    public static void main(String[] args)        
    {
        sum();        
    }        
    //static method 
    public static void sum()
    {
        System.out.println(a+b);
    }
}
```

   
Approach3  
---------  

```java
class Test
{
    public static void main(String[] args)        
    {
        int a=100,b=50;
        System.out.println(a+b);
    }        
}
```

   
   
