   
Types of cursors in java  
========================  
Cursors are used to read objects one by one from Collections.  
   
We have three types of cursors.  
   
1) Enumeration   
   
2) Iterator   
   
3) ListIterator   
   
1) Enumeration  
--------------  
It is used to read objects one by one from legacy Collection objects.  
   
Enumeration interface contains following two methods.  
ex:  
public boolean hasMoreElements()  
public Object nextElement()   
   
We can create Enumeration object as follow.  
ex:  

```java
Enumeration e = v.elements();
```

   
ex:  
---  

```java
import java.util.*;
class Test 
{
    public static void main(String[] args) 
    {
        Vector<Integer> v = new Vector<>();
        for(int i=1;i<=10;i++)
        {
            v.add(i);
        }
        Enumeration e = v.elements();
        while(e.hasMoreElements())
        {
            int i = (Integer)e.nextElement();
            System.out.println(i);
        }
    }
}
```

   
Limitations with Enumeration   
----------------------------  
Enumeration is used to read object one by one from legacy Collection objects. Hence it is not a universal cursor.  
   
Using Enumeration we can perform read operation but not remove operation.  
   
To overcome above limitation we need to use Iterator.  
   
   
2) Iterator   
--------------  
It is used to read objects one by one from any Collection object. Hence it is a universal cursor.  
   
Using Iterator we can perform read and remove operations.  
   
We can create Iterator object as follow.  
   
ex:  

```java
Iterator itr = al.iterator();
```

   
Iterator interface contains following three methods.  
ex:  
public boolean hasNext()          
public Object next()  
public void remove()  
   
ex:  
---  

```java
import java.util.*;
class Test 
{
    public static void main(String[] args) 
    {
        ArrayList<Integer> al = new ArrayList<>();
        for(int i=1;i<=10;i++)
        {
            al.add(i);
        }
        Iterator itr = al.iterator();
        while(itr.hasNext())
        {
            int i = (Integer)itr.next();
            if(i%2==0)
                System.out.print(i+" ");
            else
                itr.remove();
        }
        System.out.println("\n"+al); //[2,4,6,8,10]
    }
}
```

   
Limitations with Iterator  
------------------------  
Enumeration and Iterator is used to read objects in forward direction but not in backward direction. Hence they are not bi-directional cursors.  
   
Using Iterator we can perform read and remove operation but not adding and replacement of new objects.  
   
To overcome this limitation Sun Micro System introduced ListIterator.   
   
   
3) ListIterator   
---------------  
ListIterator is a child interface of Iterator.  
   
It is used to read objects one by one from List Collection objects.  
   
Using ListIterator we can perform read, remove  , adding and replacement of new objects.  
   
We can create ListIterator object as folow.  
ex:  

```java
ListIterator litr = al.listIterator();
```

   
ListIterator interface contains following 9 methods.  
ex:  
public boolean hasNext()  
public Object next()  
public void remove()  
public boolean hasPrevious()  
public Object previous()  
public int nextIndex()  
public int previousIndex()   
public void add(E)   
public void set(E)  
   
ex:  
---  

```java
import java.util.*;
class Test 
{
    public static void main(String[] args) 
    {
        ArrayList<String> al = new ArrayList<>();
        al.add("venki");
        al.add("bala");
        al.add("nag");
        al.add("chiru");
 
        ListIterator litr = al.listIterator();
        while(litr.hasNext())
        {
            String s = (String) litr.next();
            System.out.println(s); 
        }
    }
}
```

   
   
ex:  
---  

```java
import java.util.*;
class Test 
{
    public static void main(String[] args) 
    {
        ArrayList<String> al = new ArrayList<>();
        al.add("venki");
        al.add("bala");
        al.add("nag");
        al.add("chiru");
 
        ListIterator litr = al.listIterator(al.size());
        while(litr.hasPrevious())
        {
            String s = (String) litr.previous();
            System.out.println(s); 
        }
    }
}
```

   
ex:  
---  

```java
import java.util.*;
class Test 
{
    public static void main(String[] args) 
    {
        ArrayList<String> al = new ArrayList<>();
        al.add("venki");
        al.add("bala");
        al.add("nag");
        al.add("chiru");
 
        ListIterator litr = al.listIterator();
        while(litr.hasNext())
        {
            String s = (String) litr.next();
            if(s.equals("bala"))
            {
                litr.remove();
            }
        }
        System.out.println(al);
    }
}
```

   
ex:  
---  

```java
import java.util.*;
class Test 
{
    public static void main(String[] args) 
    {
        ArrayList<String> al = new ArrayList<>();
        al.add("venki");
        al.add("bala");
        al.add("nag");
        al.add("chiru");
 
        ListIterator litr = al.listIterator();
        while(litr.hasNext())
        {
            String s = (String) litr.next();
            if(s.equals("chiru"))
            {
                litr.add("pavan");
            }
        }
        System.out.println(al);
    }
}
```

   
ex:  
---  

```java
import java.util.*;
class Test 
{
    public static void main(String[] args) 
    {
        ArrayList<String> al = new ArrayList<>();
        al.add("venki");
        al.add("bala");
        al.add("nag");
        al.add("chiru");
 
        ListIterator litr = al.listIterator();
        while(litr.hasNext())
        {
            String s = (String) litr.next();
            if(s.equals("venki"))
            {
                litr.set("ram");
            }
        }
        System.out.println(al);
    }
}
```

   
   
Multi-Threading   
===============  
   
Q) What is the difference between Thread and Process ?   
   
Thread   
--------  
It is a leight weight sub-process.  
ex:  
Screen Share   
Chat Box   
Audio   
Video  
and etc.  
   
We can run multiple threads concurrently.  
One thread can communicate with another thread.  
   
Process  
--------  
It is a collection of threads.  
ex:  
Zoom Meeting   
   
We can run multiple process concurrently.  
One process can't communicate with another process because they are   
independent to each other.  
   
   
Multi-tasking   
=============  
Executing several tasks simultenously such concept is called multitasking.  
   
We have two types of multitasking.  
   
1) Thread based multitasking  
----------------------------  
Executing several tasks simultenously where each task is a same part of a program such type of tasking is called thread based multitasking.  
It is best suitable for programmatic level.  
   
2) Process based multitasking  
-----------------------------  
Executing several tasks simultenously where each task is a independent process such type of tasking is called process based multitasking.  
It is best suitable for OS level.  
   
   
Multi-Threading   
===============  
Executing severals threads simultenously such concept is called multithreading.  
   
In multithreading only 10% of work should be done by a programmer and 90% of work will be done by a JAVA API.  
   
The main important application area of multithreading are   
   
1) To implements multimedia graphics  
   
2) To develop video games   
   
3) To develop animations  
   
   
Ways to create a thread in java   
=============================  
There are two ways to create a thread in java.  
   
1) By extending Thread class   
   
2) By implementing Runnable interface   
   
   
1) By extending Thread class  
----------------------------  

```java
class MyThread extends Thread 
{
    public void run()
    {
        for(int i=1;i<=5;i++)
        {
            System.out.println("Child-Thread");
        }
    }
}
class Test
{
    public static void main(String[] args)
    {
        //instantiate a thread 
        MyThread t = new MyThread();
         
        //start a thread 
        t.start();
         
        for(int i=1;i<=5;i++)
        {
            System.out.println("Parent-Thread");
        }
    }
}
```

   
case1: Thread Schedular   
-----------------------  
If multiple threads are waiting for execution which thread has to be executed will decided by thread schedular.  
   
What algorithm, behaviour or mechanism used by thread schedular is depend upon JVM vendor.   
   
Hence we can't expect any execution order or exact output in multithreading.  
   
   
case2: What is difference between t.start() and t.run()   
---------------------------------------------------------  
If we invoke t.start() method, a new thread will be created which is responsible to execute run() method automatically.  
   
ex:  
--  

```java
class MyThread extends Thread 
{
    public void run()
    {
        for(int i=1;i<=5;i++)
        {
            System.out.println("Child-Thread");
        }
    }
}
class Test
{
    public static void main(String[] args)
    {
        //instantiate a thread 
        MyThread t = new MyThread();
         
        //start a thread 
        t.start();
         
        for(int i=1;i<=5;i++)
        {
            System.out.println("Parent-Thread");
        }
    }
}
```

   
   
If we invoke t.run() method, no new thread will be created but run() method will execute just like a normal method.  
   
ex:  
--  

```java
class MyThread extends Thread 
{
    public void run()
    {
        for(int i=1;i<=5;i++)
        {
            System.out.println("Child-Thread");
        }
    }
}
class Test
{
    public static void main(String[] args)
    {
        //instantiate a thread 
        MyThread t = new MyThread();
         
        //no new thread 
        t.run();
         
        for(int i=1;i<=5;i++)
        {
            System.out.println("Parent-Thread");
        }
    }
}
```

   
case3: if we won't ovreride run() method   
---------------------------------------  
If we won't override run() method then start() method executes Thread class run() method automatically which is empty implementation. Hence we won't get any output from child thread.  
   
ex:  
---  

```java
class MyThread extends Thread 
{
     
}
class Test
{
    public static void main(String[] args)
    {
        //instantiate a thread 
        MyThread t = new MyThread();
         
        //start thread 
        t.start();
         
        for(int i=1;i<=5;i++)
        {
            System.out.println("Parent-Thread");
        }
    }
}
```

   
case4: If we overload run() method   
-------------------------------  
If we overload run() method then Thread class start() method always execute run() method with no argument only.  
   
ex:  
---  

```java
class MyThread extends Thread 
{
    public void run()
    {
        System.out.println("0-arg method");
    }
    public void run(int i)
    {
        System.out.println("int-arg method");
    }
}
class Test
{
    public static void main(String[] args)
    {
        //instantiate a thread 
        MyThread t = new MyThread();
         
        //start thread 
        t.start();
         
        for(int i=1;i<=5;i++)
        {
            System.out.println("Parent-Thread");
        }
    }
}
```

   
case5: Thread Life Cycle   
------------------------  
Diagram: class47.1  
![[attachments/image33.png]]  
Once if we create a thread object then our thread is in new or born state.  
   
Once if we call t.start() method then our thread is in ready or runnable state.  
   
If thread schedular allocates to CPU then our thread goes to running state.  
   
Once run() method execution is completed then our thread enters to dead sate.  
   
   
2) By implementing Runnable interface  
-------------------------------------  

```java
class MyRunnable implements Runnable 
{
    public void run()
    {
        for(int i=1;i<=5;i++)
        {
            System.out.println("child-thread");
        }
    }
}
class Test 
{
    public static void main(String[] args)
    {
        MyRunnable r = new MyRunnable();
         
        Thread t = new Thread(r); // r is a targetable interface 
         
        t.start();
        for(int i=1;i<=5;i++)
        {
            System.out.println("Parent-thread");
        }
    }
}
```

   
   
