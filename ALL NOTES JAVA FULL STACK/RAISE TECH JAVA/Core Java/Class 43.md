   
Various ways to provide inputs in java  
======================================  
There are following ways to provide inputs in java.  
   
1) Command line argument   
   
2) BufferedReader class   
   
3) Console class   
   
4) Scanner class   
   
   
1) Command line argument   
------------------------  

```java
class Test  
{
    public static void main(String[] args) 
    {
        String name = args[0];
        System.out.println("Welcome :"+name);
    }
}
```

javac   Test.java  
java    Test  JackMa  
   
   
2) BufferedReader class  
-----------------------  

```java
import java.io.*;
class Test  
{
    public static void main(String[] args)throws IOException  
    {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        System.out.println("Enter the name :");
        String name = br.readLine();
        System.out.println("Welcome :"+name);
    }
}
```

   
3) Console class   
-----------------  

```java
import java.io.*;
class Test  
{
    public static void main(String[] args)throws IOException  
    {
        Console c = System.console();
        System.out.println("Enter the name :");
        String name = c.readLine();
        System.out.println("Welcome :"+name);
    }
}
```

   
4) Scanner class   
--------------  

```java
import java.util.*;
class Test  
{
    public static void main(String[] args)  
    {
        Scanner sc = new Scanner(System.in);
         
        System.out.println("Enter the student no :");
        int no = sc.nextInt();
         
        System.out.println("Enter the student name :");
        String name = sc.next();
         
        System.out.println("Enter the student fee :");
        double fee = sc.nextDouble();
         
        System.out.println(no+" "+name+" "+fee);
 
    }
}
```

   
Serialization   
=============  
A process of storing object data into a file is called serialization..  
   
Converting object state to file state is called serialization.  
   
To perform serialization we required ObjectOutputStream and FileOutputStream.  
   
We can perform serialization only for serialized objects.  
   
To create serialized object our class must implements Serializable interface.  
   
Serializable is a marker interface which does not have any methods and constants.  
   
By using Serializable interface we will get some ability to do by JVM.  
   
Diagram: class43.1  
![[attachments/image29.png]]  
ex:  
---  

```java
import java.io.*;
class Person implements Serializable
{
    private String name;
    private int age;
    Person(String name,int age)
    {
        this.name = name;
        this.age = age;
    }
    public String toString()
    {
        return name+" "+age; 
    }
}
class Test 
{
    public static void main(String[] args)
    {
        Person p = new Person("Alan",28);
        try(ObjectOutputStream ostream = 
            new ObjectOutputStream(new FileOutputStream("abc.ser"));)
        {
            ostream.writeObject(p);
            System.out.println("Serialization Done");
        }
        catch (IOException ioe)
        {
            ioe.printStackTrace();
        }
    }
}
```

   
   
Deserialization   
=============  
A process of taking the data from a file and representing an object is called deserialization.  
   
Converting file state to object state is called deserialization.  
   
To perform deserialization we required ObjectInputStream and FileInputStream.  
   
We can perform deserialization only for serialized objects.  
   
To create serialized object our class must implements Serializable interface.  
   
Serializable is a marker interface which does not have any methods and constants.  
   
By using Serializable interface we will get some ability to do by JVM.  
   
Diagram: class43.2  
![[attachments/image29.png]]  
ex:  
---  

```java
import java.io.*;
class Person implements Serializable
{
    private String name;
    private int age;
    Person(String name,int age)
    {
        this.name = name;
        this.age = age;
    }
    public String toString()
    {
        return name+" "+age; 
    }
}
class Test 
{
    public static void main(String[] args)
    {
         
        try(ObjectInputStream istream = 
            new ObjectInputStream(new FileInputStream("abc.ser"));)
        {
            Person p = (Person) istream.readObject();
            System.out.println(p);
        }
        catch (IOException | ClassNotFoundException e)
        {
            e.printStackTrace();
        }
    }
}
```

   
   
Singleton class   
===============  
It is a design pattern which ensures that a class must have only one instance.  
   
A class which allows us to create only one object is called singleton class.  
   
To create a singleton class we required private constructor and static method.  
   
The main purpose of singleton class is we can control object creations, save some memory and maintain consistency cross the application.  
   
ex:  
---  

```java
import java.util.*;
class Singleton 
{
    static Date date = null;
    private Singleton()
    {
        System.out.println("constructor");
    }
    public static Date getInstance()
    {
        if(date==null)
        {
            date = new Date();
        }
        return date;
    }
}
class Test 
{
    public static void main(String[] args)
    {
        Date d1 = Singleton.getInstance();
        System.out.println(d1);
        System.out.println(d1.hashCode());
         
        Date d2 = Singleton.getInstance();
        System.out.println(d2);
        System.out.println(d2.hashCode());
    }
}
```

   
Generics   
========  
Arrays are typesafe.  
It means we can give guarantee that what type of elements are present in arrays.  
ex:  

```java
int[] arr = new int[3];
arr[0] = 10;
arr[1] = 20;
```

   
If requirement is there to store string values then it is recommanded to use String[] array.  
ex:  

```java
String[] sarr = new String[10];
sarr[0] = "Hi";
sarr[1] = "Bye";
```

sarr[2] = 10;    // Invalid   
   
At the time of retrieving the data we don't need to perform typecasting.  
ex:  

```java
String[] sarr = new String[10];
sarr[0] = "Hi";
sarr[1] = "Bye";
```

-  
-          

```java
String val1 = sarr[0];        
```

   
Collections are not typesafe.  
   
It means we can't provide guarantee that what type of elements are present in Collections.  
   
If requirement is there to store string values then it is never recommanded to use ArrayList because we won't get any compile time error or runtime error but sometimes our program get failure.  
   
ex:  

```java
ArrayList al = new ArrayList();
al.add("Hi");
al.add("Bye");
al.add(10);
```

   
At the time of retrieving the data from Collections compulsary we need to perform typecasting.  
   
ex:  

```java
ArrayList al = new ArrayList();
al.add("Hi");
al.add("Bye");
al.add(10);
```

-  
-  

```java
String val1 = (String)al.get(0);
```

   
To overcome above limitations Sun Micro System introduced Generics concept in 1.5 version.  
   
The main objective of Generics is  
   
1) To make make Collections as typesafe.  
   
2) To avoid typecasting problem.   
   
   
java.util package  
=================  
   
Q) What is the difference between Arrays and Collections ?   
   
| Arrays | Collections |
| --- | --- |
| It is a collection of homogeneous<br>data elements. | It is a collection of homogeneous and<br>hetrogeneous data elements. |
| It is fixed in size. | It is growable in nature. |
| Performance point of view arrays are<br>recommanded to use. | Memory point of view Collections are<br>recommanded to use. |
| Arrays are not implemented based on<br>data structure concept. So we can't<br>expect any ready made method. | Collections are implemented based on<br>data structure concept. So we can expect<br>readymade methods. |
| It can hold primitive types and<br>object types. | It can hold only object types. |
| It is typesafe. | It is not typesafe. |
   
   
