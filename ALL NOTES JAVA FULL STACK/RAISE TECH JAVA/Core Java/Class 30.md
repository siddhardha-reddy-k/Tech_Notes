   
Multi-Dimensional Array   
=======================  
If array contains more than two dimensions is called multi-dimensional array.  
   
Multi-dimensional array is used to store the data in structured and tabular format.  
   
We can declare and create multi-dimensional array as follow.  
   
ex:  
      base rows  
|  |    
         int[][][] arr = new int[2][3][3];  
      |  
    columns  
   
Here we can store 18 elements   
   
We can initialized multi-dimensional array as follow.  
   
ex:  
int[][][] arr = {  
{  
{1,2,3},{4,5,6},{7,8,9}  
},  
{  
{1,2,3},{4,5,6},{7,8,9}  
}  
};  
   
ex:  
----  

```java
class Test  
{
    public static void main(String[] args) 
    {
        int[][][] arr = {{{1,2,3},{4,5,6},{7,8,9}},{{1,2,3},{4,5,6},{7,8,9}}};
                         
        for(int i=0;i<arr.length;i++)
        {
            for(int j=0;j<arr[i].length;j++)
            {
                for(int k=0;k<arr[i][j].length;k++)
                {
                    System.out.print(arr[i][j][k]+" ");
                }
                //new line 
                System.out.println();
            }
            //new line 
            System.out.println();
        }
                         
    }
}
```

   
Jagged Array   
============  
Jagged array is also known as array of arrays.  
It is a multi-dimensional array where each row contains different column size.  
   
ex:  
---  

```java
class Test  
{
    public static void main(String[] args) 
    {
        int[][] arr = {
                            {1,2,3,4},
                            {5,6},
                            {7,8,9}
                        };
                         
        for(int i=0;i<arr.length;i++)
        {
            for(int j=0;j<arr[i].length;j++)
            {
                System.out.print(arr[i][j]+" ");
            }
            //newline 
            System.out.println();
        }
                         
    }
}
```

   
Anonymous Array   
==============  
Sometimes we will declare an array without name such type of namesless array is called anonymous array.  
   
The main objective of anonymous array is just for instance use.  
   
We can declare anonymous array as follow.  
ex:  
new int[]{10,20,30};  
new int[][]{{1,2,3},{4,5,6},{7,8,9}};  
   
ex:  
---  

```java
class Test  
{
    public static void main(String[] args) 
    {
        //caller method 
        System.out.println(sum(new int[]{10,20,30}));
    }
    //callie method 
    public static int sum(int[] arr)
    {
        int sum = 0;
        for(int i : arr)
        {
            sum += i;
        }
        return sum;
    }
}
```

   
   
OOPS   
=====  
OOPS stands for Object Oriented Programming System.  
   
OOPS concept introduced to deal with real world entities using programming language.  
   
A language is said to be object oriented if it supports following features.  
ex:  
class  
object   
abstraction -   
Encapsulation   
Inheritance and   
Polymorphism   
   
   
class  
=====  
A class is a blue print of an object.  
ex:  
Design   
Template   
   
It is a logical entity.  
   
It is a collection of objects.  
   
A class will accept following modifiers.  
ex:  
default   
public   
final   
abstract   
sealed   
non-sealed   
   
We can declare a class as follow.  
ex:  
optional   
|  
Modifier class  class_name  <extends>   parent_class_name   
    <implements> interface_name  
{  
   
}  
   
object  
======  
It is a output come of a blue print.  
   
It is a instance of a class.  
   
Here instance means allocating memory for our data members.  
   
It is a physical entity.  
   
It is a collection of properties and behaviours.  
   
ex:  
Dog          
|          
|-----------------|  
| Properties | Behaviours |
| --- | --- |
| > Name<br>> Color<br>> Breed<br>> Weight<br>> Height<br>and etc. | > Eating<br>> Playing<br>> Sleeping<br>> Barking<br>and etc. |
   
It is possible to create more than one object in a single class.  
   
We can create object as follow.  
   
syntax:  
------  

```java
class_name  reference_variable = new constructor();
```

ex:  

```java
Test t = new Test();
```

   
ex:  
---  

```java
class Test  
{
    public static void main(String[] args) 
    {
        Test t1 = new Test();
        Test t2 = new Test();
         
        System.out.println(t1.hashCode());
        System.out.println(t2.hashCode());
         
        System.out.println(t1); // Test@Hexadecimalvalue
        System.out.println(t2.toString()); // Test@Hexadecimalvalue 
    }
}
```

   
   
Q) What is hash code in java?  
   
For every object JVM creates a unique identification number i.e hash code.  
   
To read hash code of an object we need to use hashCode() method.  
   
A hashCode() method present in Object class.  
   
Diagram: class30.1  
![[attachments/image15.png]]  
   
   
Q) What is toString() method in java?  
   
Whenever we are trying to display any object reference directly or indirectly toString() method will be executed.  
   
A toString() method present in Object class.  
   
ex:  
---  

```java
class Test  
{
    public static void main(String[] args) 
    {
        Test t = new Test();
        System.out.println(t); // Test@Hexadecimalnumber 
        System.out.println(t.toString()); // Test@Hexadecimalnumber 
         
        int[] arr = {10,20,30};
        System.out.println(arr); // [I@Hexadecimalnumber
        System.out.println(arr.toString()); // [I@Hexadecimalnumber
    }
}
```

   
ex:  
---  

```java
class Test  
{
    public static void main(String[] args) 
    {
        Test t = new Test();
        System.out.println(t);
        System.out.println(t.toString());
    }
     
    @Override
    public String toString()
    {
        return "Hello World";
    }
}
```

   
   
Q) What is the difference between class and object ?   
   
| class | object |
| --- | --- |
| To declare a class we used "class"<br>keyword. | To declare object we used "new"<br>keyword. |
| It is a blue print of an object. | It is a instance of a class. |
| It is a logical entity. | It is a physical entity. |
| It is a collection of objects. | It is a collection of properties<br>and behaviours. |
| It can't be modified. | It can be modified. |
| It can't be redeclared. | It can be redeclared. |
   
   
Data Hiding   
===========  
The process of hiding object data from unauthorized access is called data hiding.  
   
Using "private" modifier we can achieve data hiding concept.  
   
The main objective of data hiding is to provide security.  
   
ex:  
---  

```java
class Account 
{
    private double balance = 10000d;
}
class Student
{
    public static void main(String[] args)
    {
        Account acc = new Account();
        System.out.println(acc.balance);
    }
}
```

   
   
