   
synchronized block   
==================  
If we want to perform synchronization on specific resource of a program then we need to use synchronized block.  
   
If we keep all the code inside synchronized block then it acts like a synchronized method.  
   
ex:  
---  

```java
class Table
{
    public void printTable(int n)
    {
        synchronized(this)
        {
            for(int i=1;i<=5;i++)
            {
                System.out.println(n*i);
                try
                {
                    Thread.sleep(2000);
                }
                catch (InterruptedException ie)
                {
                    ie.printStackTrace();
                }
            }
        }
    }
}
class MyThread1 extends Thread
{
    Table t;
    MyThread1(Table t)
    {
        this.t = t;
    }
    public void run()
    {
        t.printTable(5);
    }
}
class MyThread2 extends Thread
{
    Table t;
    MyThread2(Table t)
    {
        this.t = t;
    }
    public void run()
    {
        t.printTable(10);
    }
}
class Test 
{
    public static void main(String[] args) 
    {
        Table obj = new Table();
        MyThread1 t1 = new MyThread1(obj);
        MyThread2 t2 = new MyThread2(obj);
        t1.start();
        t2.start();
    }
}
```

   
static synchronization   
======================  
In static synchronization the lock will be on class not on object.  
   
If we declare any static method as synchronized then it is called static synchronization.  
   
ex:  
---  

```java
class Table
{
    public static synchronized void printTable(int n)
    {
        for(int i=1;i<=5;i++)
        {
            System.out.println(n*i);
            try
            {
                Thread.sleep(2000);
            }
            catch (InterruptedException ie)
            {
                ie.printStackTrace();
            }
        }
    }
}
class MyThread1 extends Thread
{
    public void run()
    {
        Table.printTable(5);
    }
}
class MyThread2 extends Thread
{
    public void run()
    {
        Table.printTable(10);
    }
}
class Test 
{
    public static void main(String[] args) 
    {
        MyThread1 t1 = new MyThread1();
        MyThread2 t2 = new MyThread2();
        t1.start();
        t2.start();
    }
}
```

   
Inter-Thread Communication   
==========================  
Inter-thread communication is possible by using wait(), notify() and notifyAll() method.  
   
A thread which is waiting for notification has to call wait() method.  
   
A thread which is giving notficaion has to call notify() or notifyAll() method.  
   
A wait(),notify() and notifyAll() method present in Object class.  
   
To call wait(), notify() and notifyAll() we required synchronized area.  
   
If we call wait() method thread will release the lock immediately and goes to waiting state.  
   
If we call notify() and notifyAll() method thread will release the lock but not immediately.  
   
Except wait(), notify() and notifyAll() method there is no other way to release the lock.  
   
ex:  
---  

```java
class MyThread extends Thread
{
    int total = 0;
    public void run()
    {
        synchronized(this)
        {
            System.out.println("Child started calculation ");
             
            for(int i=1;i<=10;i++)
            {
                total += i;
            }
            System.out.println("Child giving notification");
            this.notify();
        }
    }
}
class Test 
{
    public static void main(String[] args)throws InterruptedException
    {
        MyThread t = new MyThread();
        t.start();
        synchronized(t)
        {
            System.out.println("Main method waiting for notification");
            t.wait();
            System.out.println("Main method got notification");
            System.out.println(t.total);
        }
    }
}
```

   
DeadLock in Java  
================  
Deadlock will occur in a situation where first thread is waiting for object lock which is acquired by another thread and that thread is waiting for object lock which is acquired by first thread. Here both the threads are ready to release the lock but nobody will release this situation is called deadlock in java.  
   
ex:  
---  

```java
class Test 
{
    public static void main(String[] args)
    {
        final String res1="Hi";
        final String res2="Bye";
         
        //Anonymous inner class
        Thread t1 = new Thread()
        {
            public void run()
            {
                synchronized(res1)
                {
                    System.out.println("Thread1: Locking Resource1");
                    synchronized(res2)
                    {
                        System.out.println("Thread1: Locking Resource2");
                    }
                }
            }
        };
         
        //Anonymous inner class
        Thread t2 = new Thread()
        {
            public void run()
            {
                synchronized(res2)
                {
                    System.out.println("Thread2: Locking Resource2");
                    synchronized(res1)
                    {
                    System.out.println("Thread2: Locking Resource1");
                    }
                }
            }
        };
        t1.start();
        t2.start();
    }
}
```

   
   
   
Java 8 Features   
===============  
   
   
Functional interface   
===================  
Functional interface introduced in Java 8.  
   
Interface which contains only one abstract method is called functional interface.  
   
It can have any number of default methods, static methods and private methods.  
   
It is also known as SAM or Single Abstract Method interface.  
   
The main objective of functional interface is to achieve functional programming.  
ex:  
a = f1(){}   
   
f1(f2(){})  
{  
}  
   
We have following list of functional interfaces in java.  
ex:  

```java
Comparable         ->        compareTo()
Comparator        ->        compare() 
Runnable         ->        run() 
ActionListener         ->        actionPerformed()  
```

and etc.  
   
@FunctionalInterface annotation is to declare functional interface which is optional.  
   
ex:  
---  

```java
@FunctionalInterface
interface ATM 
{
    void deposit();
}
class ATMImpl implements ATM
{
    @Override
    public void deposit()
    {
        System.out.println("Deposit Method");
    }
}
class Test 
{
    public static void main(String[] args)
    {
        ATM atm = new ATMImpl();
        atm.deposit();
    }
}
```

   
   
ex:  
---  

```java
@FunctionalInterface
interface ATM 
{
    void deposit();
}
class Test 
{
    public static void main(String[] args)
    {
        ATM atm = new ATM()
        {
            public void deposit()
            {
                System.out.println("Deposit Method");
            }
        };
        atm.deposit();
    }
}
```

   
Lamda Expression   
================  
Lamda expression introduced in Java 8.  
   
Lamda expression is used to concise the code.  
   
We can use lamda expression when we have functional interface.  
   
The main objective of lamda expression is to achieve functional programming.  
   
Lamda expression consider as method.  
   
Lamda expression does not allow name, returntype and modifier.  
   
ex:  
Java Method  
----------  
public void m1()  
{  

```java
    System.out.println("M1-Method");
}
```

   
Lamda Expression   
--------------          
()->  
{  

```java
    System.out.println("M1-Method");
};
```

   
ex:  
----  

```java
@FunctionalInterface
interface ATM 
{
    void deposit();
}
class Test 
{
    public static void main(String[] args)
    {
        ATM atm = ()->{
            System.out.println("Deposit Method");
        };
        atm.deposit();                
    }
}
```

   
ex:  
---  

```java
@FunctionalInterface
interface ATM 
{
    void deposit(int amt);
}
class Test 
{
    public static void main(String[] args)
    {
        ATM atm = (amt)->{
            System.out.println("Deposit Amount :"+amt);
        };
        atm.deposit(10000);                
    }
}
```

   
ex:  
---  

```java
@FunctionalInterface
interface ATM 
{
    String deposit(int amt);
}
class Test 
{
    public static void main(String[] args)
    {
        ATM atm = (amt)->{
            return "Deposit Amount :"+amt;
        };
        System.out.println(atm.deposit(20000));                
    }
}
```

   
   
Default methods  
================  
Default methods in interface introduced in Java 8.  
   
Java provides facility to declare the methods and tagged with default keyword.  
   
Default methods are non-abstract methods.  
   
Default methods we can override.  
   
ex:  
---  

```java
interface Animal
{
    public abstract void sound();
     
    default void eat()
    {
        System.out.println("Animals eat");
    }
}
class Dog implements Animal 
{
    @Override
    public void sound()
    {
        System.out.println("Bow Bow");
    }
}
class Test 
{
    public static void main(String[] args)
    {
        Animal a = new Dog();
        a.sound();
        a.eat();
    }
}
```

   
ex:  
---  

```java
interface Animal
{
    public abstract void sound();
     
    default void eat()
    {
        System.out.println("Animals eat");
    }
}
class Dog implements Animal 
{
    @Override
    public void sound()
    {
        System.out.println("Bow Bow");
    }
    @Override
    public void eat()
    {
        System.out.println("Pedigree");
    }
}
class Test 
{
    public static void main(String[] args)
    {
        Animal a = new Dog();
        a.sound();
        a.eat();
    }
}
```

   
static methods   
================  
Static methods in interface introduced in Java 8.  
   
Java provides facility to declare methods and tagged with static keyword.  
   
Static methods are non-abstract methods.  
   
Static methods we can't override.  
   
ex:  
---  

```java
interface Draw
{
    static void circle()
    {
        System.out.println("Circle");
    }
}
class Test 
{
    public static void main(String[] args)
    {
        Draw.circle();
    }
}
```

   
Assignment   
==========  
Explain diamond problem in java?  
   
   
