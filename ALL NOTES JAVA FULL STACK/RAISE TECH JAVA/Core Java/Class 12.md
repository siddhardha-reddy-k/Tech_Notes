   
Main method   
===========  
Our program contains main method or not. Either it is properly declared or not. It is not a responsibility of a compiler to check. It is a duty of a JVM to check for main method always at runtime. If JVM won't find main method then it will throw one runtime error called main method not found.  
   
JVM always look for main method with below signature.  
ex:  

```java
public static void main(String[] args)
```

   
Before Java 21 , If we perform any changes in above signature then we will get runtime error called main method not found.  
   
Since Java 21, we can perform following changes in main method.  
   
1) public modifier is optional.  
   ex:  

```java
static void main(String[] args)
```

   
   
2) We can declare instance main method.  
   ex:  
public void main(String[] args)  
   
3) We can declare String[] in following acceptable formats.  
   ex:  

```java
public static void main(String[] args)
public static void main(String  []args)
public static void main(String args[])
```

   
4) We can replace String[] with var-arg parameter.  
   ex:  

```java
public static void main(String... args)        
```

   
   
5) We can change args with any java valid identifier.  
   ex:  

```java
public static void main(String[] ihub)
```

   
   
6) Declaration of String[] args is optional.   
   ex:  

```java
public static void main()        
```

   
   
   
   
Q) Explain main method in Java?  
   
public  
------  
JVM wants to call main method anywhere.  
   
static   
-------  
JVM wants to call main method without using object reference.  
   
void   
----  
Main method does not return anything to JVM.  
   
main  
----  
It is a identifier given to a main method.  
   
String[] args  
------------  
It is a command line argument.  
   
Command Line Arguments   
=====================  
Arguments which are passing through command prompt such type of arguments are called command line arguments.  
   
In command line arguments, we need to pass our inputs at runtime command.  
   
ex:  
java  -version   
java  Test.java  
git   status  
and etc.  
   
   
Program:  
-------  
javac   Test.java  
java    Test  101  Alan  M  1000.0  
|   |    |    |_____ args[3]  
|   |    |__________ args[2]  
|   |_______________ args[1]  
|___________________ args[0]  
ex:  
   

```java
class Test
{
    public static void main(String[] args)
    {
        System.out.println(args[0]);
        System.out.println(args[1]);
        System.out.println(args[2]);
        System.out.println(args[3]);                
    }
}
```

   
   
Note:  
-----  
Using command line argument we can read input values.  
   
ex:  
---  

```java
class Test
{
    public static void main(String[] args)
    {
        String fname = args[0];
        String lname = args[1];
        System.out.println(fname+lname);        
    }
}
```

javac   Test.java  
java    Test   Alan Morries   
   
   
