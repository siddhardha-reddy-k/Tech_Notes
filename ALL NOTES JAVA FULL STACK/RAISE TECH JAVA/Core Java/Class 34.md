   
Interface  
=========  
It is a blue print of a class and it is a collection of abstract methods, default methods, static methods and private methods.  
   
Abstract methods are incomplete methods because they end with semicolon and don't have any body.  
ex:  
void methodOne();  
   
It is not possible to create object for interfaces.  
   
To write the implementation for abstract methods we will use implementation class.  
   
It is possible to create object for implementation class because it contains method with body.  
   
Every abstract method is a public and abstract.  
ex:  

```java
public abstract void methodOne();
```

   
Interface contains only constants i.e public static final.  
   
syntax:  
------  

```java
interface  interface_name
{
    -
    - // abstract methods 
    - // default methods 
    - // static methods 
    - // private methods 
    - // constants 
    -
}
```

   
If we depend upon service requirement specification then we need to use interface.  
   
Diagram: class34.1  
![[attachments/image23.png]]  
ex:  
---  

```java
interface Animal
{
    public abstract void eat();
}
class Dog implements Animal 
{
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
        a.eat();
    }
}
```

   
ex:  
--  

```java
interface Animal
{
    public abstract void eat();
}
class Test 
{
    public static void main(String[] args)
    {
        //Anonymous inner class
        Animal a = new Animal()
        {
            public void eat()
            {
                System.out.println("Pedigree");
            }
        };
        a.eat();
    }
}
```

   
If interface contains four methods then we need to override all methods otherwise we will get compile time error.  
   
ex:  
---  

```java
interface A
{
    void view();
    public void show();
    abstract void see();
    public abstract void display();
}
class B implements A 
{
    @Override
    public void view()
    {
        System.out.println("View Method");
    }
    @Override
    public void show()
    {
        System.out.println("Show Method");
    }
    @Override
    public void see()
    {
        System.out.println("See Method");
    }
    @Override
    public void display()
    {
        System.out.println("Display Method");
    }
}
class Test 
{
    public static void main(String[] args)
    {
        A a = new B();
        a.view();
        a.show();
        a.see();
        a.display();
    }
}
```

   
A class can't extends more then one class.  
But interface can extends more then one interface.  
   
ex:  
---  

```java
interface A 
{
    void methodOne();
}
interface B 
{
    void methodTwo();
}
interface C extends A,B 
{
    void methodThree();
}
class D implements C 
{
    @Override
    public void methodOne()
    {
        System.out.println("MethodOne");
    }
    @Override
    public void methodTwo()
    {
        System.out.println("MethodTwo");
    }
    @Override
    public void methodThree()
    {
        System.out.println("MethodThree");
    }
}
class Test 
{
    public static void main(String[] args)
    {
        C c = new D();
        c.methodOne();
        c.methodTwo();
        c.methodThree();
    }
}
```

   
Multiple Inheritance   
-------------------  

```java
interface Dog 
{
    public abstract void eat();
}
interface Cat
{
    public abstract void eat();
}
class Animal implements Dog,Cat
{
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
        Animal a = new Animal();
        a.eat();
    }
}
```

   
ex:  
---  

```java
interface Dog 
{
    public abstract void eat();
}
interface Cat
{
    public abstract void eat();
}
class Animal implements Dog,Cat
{
    @Override
    public void eat()
    {
        System.out.println("Milk");
    }
}
class Test 
{
    public static void main(String[] args)
    {
        Animal a = new Animal();
        a.eat();
    }
}
```

   
A class can implements more than one interface.  
   
ex:  
--  

```java
interface Father 
{
    float HT = 6.2f;
    void height();
}
interface Mother
{
    float HT = 5.8f;
    void height();
}
class Child implements Father,Mother 
{
    public void height()
    {
        float height = (Father.HT+Mother.HT)/2;
        System.out.println("Child Height : "+height);
    }
}
class Test 
{
    public static void main(String[] args)
    {
        Child c = new Child();
        c.height();
    }
}
```

   
   
   
   
   
   
