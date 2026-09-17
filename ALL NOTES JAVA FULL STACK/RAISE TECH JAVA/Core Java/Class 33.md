   
Method Overloading   
==================  
Having same method name with different parameters/signatures in a single class is called method overloading.  
   
Methods which are present in a class are called overloaded methods.  
   
Method resolution will taken care by a compiler based on reference type.  
   
Method overloading reduces complexity of the programming.  
   
ex:  
   

```java
class ECOI 
{
    //overloaded methods 
    public void search(int epicNo)
    {
        System.out.println("Details Found via epicNo");
    }
    public void search(String details)
    {
        System.out.println("Details Found via details");
    }
    public void search(long phoneNo)
    {
        System.out.println("Details Found via phoneNo");
    }
}
class Voter
{
    public static void main(String[] args)
    {
        ECOI ecoi = new ECOI();
        ecoi.search(1234);
        ecoi.search("Niyaz");
        ecoi.search(99999L);
    }
}
```

   
   
Q) Can we overload main method in java?  
   
Yes, we can overload main method in java but JVM always execute main method with String[] parameter only.  
   
ex:  
---  
   

```java
class Test
{
    public static void main(String[] args)
    {
        System.out.println("String-array arg");
    }
    public static void main(int[] iargs)
    {
        System.out.println("int-array arg");
    }
}
```

   
   
Method Overriding   
=================  
Having same method name with same parameters in two different classes is called method overriding.  
   
Methods which are present in parent class are called overridden methods.  
   
Methods which are present in child class are called overriding methods.  
   
Method resolution will taken care by JVM based on runtime object.  
   
ex:  
---  

```java
class Parent 
{
    //overridden methods 
    public void property()
    {
        System.out.println("Land+House+Gold");
    }
    public void marry()
    {
        System.out.println("Trisha");
    }
}
class Child extends Parent
{
    //overriding methods 
    @Override
    public void marry()
    {
        System.out.println("Rashmika");
    }
}
class Test 
{
    public static void main(String[] args)
    {
        Parent p = new Parent();
        p.property(); // Land+House+Gold
        p.marry(); // Trisha 
         
        Child c = new Child();
        c.property(); // Land+House+Gold
        c.marry();    // Rashmika 
         
        Parent p1 = new Child();
        p1.property(); // Land+House+Gold
        p1.marry(); // Rashmika 
    }
}
```

   
If we declare any method as final then overriding of that method is not possible.  
   
ex:  
---  

```java
class Parent 
{
    //overridden methods 
    public void property()
    {
        System.out.println("Land+House+Gold");
    }
    public final void marry()
    {
        System.out.println("Trisha");
    }
}
class Child extends Parent
{
    //overriding methods 
    @Override
    public void marry()
    {
        System.out.println("Rashmika");
    }
}
class Test 
{
    public static void main(String[] args)
    {
        Parent p = new Parent();
        p.property(); // Land+House+Gold
        p.marry(); // Trisha 
         
        Child c = new Child();
        c.property(); // Land+House+Gold
        c.marry();    // Rashmika 
         
        Parent p1 = new Child();
        p1.property(); // Land+House+Gold
        p1.marry(); // Rashmika 
    }
}
```

   
Method Hiding   
=============  
Method hiding exactly same as method overriding with following differences.  
   
| Method overriding | Method Hiding |
| --- | --- |
| Methods must be non-static. | Methods must be static. |
| Method resolution will taken care<br>by JVM based on runtime object. | Method resolution will taken care<br>by compiler based on reference type. |
| It is also known as runtime polymorphism,<br>dynamic polymorphism or late binding. | It is also known as compile time<br>polymorphism, static polymorphism or<br>early binding. |
   
ex:  
---  

```java
class Parent 
{
    public static void property()
    {
        System.out.println("House-Not For Sale");
    }
}
class Child extends Parent 
{
    public static void property()
    {
        System.out.println("House-For Sale");
    }
}
class Test 
{
    public static void main(String[] args)
    {
        Parent p = new Child();
        p.property(); // House-Not For Sale 
    }
}
```

   
   
Q) Can we override main method in java?  
   
No, we can't override main method in java because it is static.  
   
   
Polymorphism   
============  
Polymorphism has taken from Greek word.  
   
Here poly means many and morphism means forms.  
   
The ability to represent in different forms is called polymorphism.  
   
The main objective of polymorphism is to provide flexibility.  
   
Diagram: class33.1  
![[attachments/image21.png]]  
   
In java, polymorphism divided into two types.  
   
1) Compile time polymorphism   
   
2) Runtime polymorphism   
   
1) Compile time polymorphism   
----------------------------  
A polymorphism which exhibits at compile time is called compile time polymorphism.  
   
It is also known as static polymorphism or early binding.  
   
Method resolution will taken care by a compiler based on reference type.  
   
ex:  
Method overloading   
Method hiding   
   
2) Runtime polymorphism   
------------------------  
A polymorphism which exhibits at runtime is called runtime polymorphism.  
   
It is also known as dynamic polymorphism or late binding.  
   
Method resolution will taken care by JVM based on runtime object.  
   
ex:  
Method Overriding  
   
Diagram: class33.2  
![[attachments/image22.png]]  
   
this keyword   
============  
A this keyword is a java keyword which is used to refer current class object reference.  
   
We can utilize this keyword in following ways.  
   
1) To refer current class variables   
   
2) To refer current class methods   
   
3) To refer current class constructors  
   
   
1) To refer current class variables  
------------------------------------  

```java
class A 
{
    //current class variable 
    int i=10;
    int j=20;
     
    A(int i,int j)
    {
        System.out.println(i+" "+j); // 100  200
        System.out.println(this.i+" "+this.j); // 10   20
    }
}
class Test 
{
    public static void main(String[] args)
    {
        A a = new A(100,200);
    }
}
```

   
2) To refer current class methods   
----------------------------------  

```java
class A 
{
    public void methodOne()
    {
        System.out.println("MethodOne");
        this.methodTwo();
    }
    public void methodTwo()
    {
        System.out.println("MethodTwo");
    }
}
class Test 
{
    public static void main(String[] args)
    {
        A a = new A();
        a.methodOne();
    }
}
```

   
3) To refer current class constructors  
--------------------------------------  
   

```java
class A 
{
    A()
    {
        System.out.println("0-arg const");
    }
    A(int i)
    {
        this();
        System.out.println("int-arg const");
    }
    A(double d)
    {
        this(10);
        System.out.println("double-arg const");
    }
}
class Test 
{
    public static void main(String[] args)
    {
        A a = new A(10.5d);
    }
}
```

   
super keyword   
=============  
A super keyword is a java keyword which is used to refer super class object reference.  
   
We can utilize super keyword in following ways.  
   
1) To refer super class variables   
   
2) To refer super class methods   
   
3) To refer super class constructors  
   
1) To refer super class variables  
---------------------------------  

```java
class A 
{
    int i=10;
    int j=20;
}
class B extends A 
{
    int i=100;
    int j=200;
    B(int i,int j)
    {
        System.out.println(this.i+" "+this.j); // 100 200
        System.out.println(i+" "+j); // 1000 2000
        System.out.println(super.i+" "+super.j); // 10 20
    }
}
class Test 
{
    public static void main(String[] args)
    {
        B b  = new B(1000,2000);
    }
}
```

   
2) To refer super class methods   
-------------------------------  

```java
class A 
{
    public void methodOne()
    {
        System.out.println("MethodOne");
    }
}
class B extends A 
{
    public void methodTwo()
    {
        super.methodOne();
        System.out.println("MethodTwo");
    }
}
class Test 
{
    public static void main(String[] args)
    {
        B b  = new B();
        b.methodTwo();
    }
}
```

   
3) To refer super class constructors  
------------------------------------  

```java
class A 
{
    A()
    {
        System.out.println("A-const");
    }
}
class B extends A 
{
    B()
    {
        super();
        System.out.println("B-const");
    }
}
class Test 
{
    public static void main(String[] args)
    {
        new B();
    }
}
```

   
   
