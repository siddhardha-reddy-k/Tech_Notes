   
Abstraction   
===========  
Hiding internal implementation and highlighting the set of services is called abstraction.   
   
The best example of abstraction is GUI ATM machine where bank people will hide internal implementation and highlights set of services like banking, withdrawl, mini statement and etc.  
   
Using abstract classes and interfaces we can implements abstraction.  
   
The main advantages of abstraction are.  
   
1) It gives security because it hides internal implementation.  
   
2) Enhancement becomes more easy because without effecting enduser they can perform   
   any changes in our internal system.  
   
3) It provides flexibility to enduser to use the system.  
   
4) It improves maintainability of an application.  
   
   
Encapsulation   
=============  
The process of encapsulatin  
g or grouping variables and it's associate methods in a single entity is called encapsulation.  
   
   
Diagram: class31.1  
![[attachments/image16.png]]  
   
A class is said to be encapsulated class if it supports data hiding and abstraction.  
   
Abstraction is used to hide the data and encapsulation is used to protect the data.  
   
In encapsulation for every variable we need to write setter and getter methods.  
   
The main advantages of encapsulation are   
   
1) It gives security.  
   
2) Enhancement becomes more easy.  
   
3) It provides flexibility to the enduser.  
   
4) It improves maintainability of an application.  
   
The main disadvantage of encapsulation is it will increase the length of our code and slow down the execution process.  
   
ex:  
---  

```java
class Student
{
    //current class variables 
    private int studId;
    private String studName;
    private double studFee;
     
    //setter method 
    public void setStudId(int studId)
    {
        this.studId = studId;
    }
    public void setStudName(String studName)
    {
        this.studName = studName;
    }
    public void setStudFee(double studFee)
    {
        this.studFee = studFee;
    }
     
    //getter methods 
    public int getStudId()
    {
        return studId;
    }
    public String getStudName()
    {
        return studName;
    }
    public double getStudFee()
    {
        return studFee;
    }
}
class Test
{
    public static void main(String[] args)
    {
        Student s = new Student();
        s.setStudId(101);
        s.setStudName("Alan");
        s.setStudFee(10000d);
         
        System.out.println("Student Id : "+s.getStudId());
        System.out.println("Student Name : "+s.getStudName());
        System.out.println("Student Fee : "+s.getStudFee());
    }
}
```

   
   
Q) What is the difference between Abstraction and Encapsulation ?  
   
| Abstraction | Encapsulation |
| --- | --- |
| Hiding internal implementation and<br>highlighting the set of services is<br>called abstraction. | The process of encapsulating or grouping<br>variables and it's associate methods in a<br>single entity is called encapsulation. |
| The best example of abstraction<br>is ATM Machine. | The best example of encapsulation is<br>Capsule. |
| Using abstract classes and interfaces<br>we can implements abstraction. | Using access modifiers we can implements<br>encapsulation. |
| It is a process of gaining the<br>information. | It is process of containing the information. |
| It is used to hide the data. | It is used to protect the data. |
| It solves the issue at design level. | It solves the issue at implementation level. |
   
   
   
   
Q) What is the difference between POJO and Java Bean class?  
   
| POJO | Java Bean |
| --- | --- |
| It can't be serialized. | It can be serialized. |
| It may or may not have constructor. | At must have atleast zero argument constructor. |
| Fields can have any visibility. | Fields can have only private visibility. |
| It can't extend other classes. | It can extends. |
| It can't implement other interfaces. | It can implements. |
| It can't use other annotations. | It can use. |
   
   
Is-A relationship   
=================  
Is-A relationship is also known as inheritance.  
   
Using "extends" keywords we can implements Is-A relationship.  
   
The main objective of Is-A relationship is to provide reusability.   
   
ex:  
A dog is a animal and animal is a dog  
A laptop is a computer and computer is a laptop  
A ravi is a human and human is a ravi          
   
   
ex:  
---  

```java
class Animal
{
    public void eat()
    {
        System.out.println("Eat Method");
    }
}
class Dog extends Animal 
{
    public void sleep()
    {
        System.out.println("Sleep Method");
    }
}
class Test 
{
    public static void main(String[] args)
    {
        Animal a = new Animal();
        a.eat();
         
        Dog d = new Dog();
        d.eat();
        d.sleep();
         
        Animal a1 = new Dog();
        a1.eat();
         
        Dog d1 = new Animal();  // C.T.E  
    }
}
```

   
conclusion   
----------  
Whatever properties are there with parent that comes to child. But whatever properties   
are ther with child that never comes to parent.  
   
A parent reference can hold child object but child reference can't hold parent object.  
   
   
Inheritance   
===========  
It is a mechanism in which one class inherits the properties of another class.  
   
Deriving a class in the presence of existing class is called inheritance.  
   
The main objective of inheritance is to provide reusability.  
   
Diagram: class31.2  
![[attachments/image17.png]]  
   
In java, We have five types of inheritance.  
   
1) Single Level Inheritance   
   
2) Multi-Level Inheritance   
   
3) Multiple Inheritance   
   
4) Hierarchical Inheritance   
   
5) Hybrid Inheritance   
   
   
