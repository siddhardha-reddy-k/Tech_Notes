   
Types of objects in java  
========================  
We have two types of objects in java.  
   
1) Immutable object   
   
2) Mutable object   
   
1) Immutable object   
-------------------  
After object creation if we perform any changes then for every change a new object will be created such type of object is called immutable object.  
   
ex:  
String and Wrapper class   
   
2) Mutable object   
-----------------  
After object creation if we perform any changes then all the required changes will be done in a same object such type of object is called mutable object.  
ex:  
StringBuffer and StringBuilder   
   
   
Cloning   
=======  
The process of creating exact duplicate object is called cloning.  
   
We can perform cloning only for cloneable objects.  
   
To create a cloneable object our class must implements Cloneable interface.  
   
A Cloneable is a marker interface which does not have any methods and constants.  
   
To perform cloning we will use clone() method of Object class.  
ex:  

```java
protected native Object clone() throws CloneNotSupportedException
```

   
ex:  
---  

```java
class Test implements Cloneable 
{
    int i = 10;
     
    public static void main(String[] args)throws CloneNotSupportedException
    {
        Test t1 = new Test();
        System.out.println(t1.i); // 10
        System.out.println(t1.hashCode());//480971771
         
        Test t2 = (Test)t1.clone();
        System.out.println(t2.i); // 10
        System.out.println(t2.hashCode());//1095293768
    }
}
```

   
Q) What is the difference between shallow cloning and deep cloning?  
   
Shallow Cloning   
---------------  
The process of creating exact duplicate object reference is called shallow cloning.  
   
ex:  
---  

```java
class Test 
{
    int i = 10;
     
    public static void main(String[] args)
    {
        Test t1 = new Test();
        System.out.println(t1.i); // 10
        System.out.println(t1.hashCode());//124407148
         
        Test t2 = t1;
        System.out.println(t2.i); // 10
        System.out.println(t2.hashCode());//124407148
    }
}
```

Diagram: class37.1  
![[attachments/image24.png]]  
   
   
Deep Cloning   
------------  
The process of creating exact duplicate object is called deep cloning.  
![[attachments/image25.png]]  
ex:  
---  

```java
class Test implements Cloneable
{
    int i = 10;
     
    public static void main(String[] args)throws CloneNotSupportedException 
    {
        Test t1 = new Test();
        System.out.println(t1.i); // 10
        System.out.println(t1.hashCode());//1881129850
         
        Test t2 = (Test)t1.clone();
        System.out.println(t2.i); // 10
        System.out.println(t2.hashCode());//1095293768
    }
}
```

   
String   
======  
It is a collection of characters which is enclosed in a double quotation.  
   
case1:  
------  
Once if we create a string object we can perform any changes if we perform any changes then for every change a new object will be created such behaviour is called immutability of an object.  
   
Diagram : class37.3  
![[attachments/image26.png]]  
case2:  
------  
What is the difference between == and .equals() method?  
   
==  
----  
It is used for reference or address comparision.  
It is used to compare primitive types and object types.  
   
ex:  
--  

```java
class Test 
{
    public static void main(String[] args)
    {
        String s1 = new String("raise");
        String s2 = new String("raise");
        System.out.println(s1 == s2); // false
    }
}
```

   
.equals()  
---------  
It is used for content comparision and it is a case sensitive.  
   
ex:  
---  

```java
class Test 
{
    public static void main(String[] args)
    {
        String s1 = new String("raise");
        String s2 = new String("raise");
        System.out.println(s1.equals(s2));
    }
}
```

   
case3:  
------  
Once if we create a String object two objects will be created. One is on heap and another is on SCP(String Constant Pool) area. But reference points to heap area only.  
   
Diagram: class37.4  
![[attachments/image27.png]]  
   
Object creations in SCP area is always optional. First JVM will check is there any object is created with same content or not. If it is created then it simply refers to that object. If it is not created then JVM creates a new object. Hence there is no chance of having duplicate objects in SCP area.  
   
Even though SCP objects do not have any reference , garbage collector can't access them.   
   
SCP objects will destroy automatically whenever JVM shutdowns or terminated.  
   
Diagram: class37.5  
![[attachments/image28.png]]  
   
   
String Important Programs  
=========================  
Q) Write a java program to find out length of a string?  
   
input:  
hello   
   
output:  
5  
   

```java
class Test 
{
    public static void main(String[] args)
    {
        String str = "hello";
        int len = str.length();
        System.out.println(len);
    }
}
```

   
Q) Write a java program to convert lowercase to uppercase string?  
   
input:  
raisetech  
   
output:  
RAISETECH   
   

```java
class Test 
{
    public static void main(String[] args)
    {
        String str = "raisetech";
        str = str.toUpperCase();
        System.out.println(str);
    }
}
```

   
Q) Write a java program to convert uppercase to lowercase string?  
   
input:  
RAISETECH  
   
output:  
raisetech  
   

```java
class Test 
{
    public static void main(String[] args)
    {
        String str = "RAISETECH";
        str = str.toLowerCase();
        System.out.println(str);
    }
}
```

   
Q) Write a java program to concatinate two strings?  
   
input:  
raise  
tech   
output:  
raisetech   
   

```java
class Test 
{
    public static void main(String[] args)
    {
        String s1 = "raise";
        String s2 = "tech";
        String result = s1.concat(s2);
        System.out.println(result);
    }
}
```

   
   
Q) Write a java program to check string contains only alphabets? //[a-zA-z]  
   
input:  
abcd  
   
output:  
TRUE   
   
   

```java
class Test 
{
    public static void main(String[] args)
    {
        String str = "abcd1";
        if(str.matches("^[A-Za-z]+")) //^ is optional it’s the same without it
            System.out.println("TRUE");
        else
            System.out.println("FALSE");
    }
}
```

   
Q) Write a java program to check string contains only digits?  
   
input:  
1234  
   
output:  
TRUE  
   
   

```java
class Test 
{
    public static void main(String[] args)
    {
        String str = "1234a";
        if(str.matches("\\d+"))
            System.out.println("TRUE");
        else
            System.out.println("FALSE");
    }
}
```

   
Q) Write a java program on join() method?  
   
Input:  
this is java class  
   
output:  
this,is,java,class  
   
   

```java
class Test 
{
    public static void main(String[] args)
    {
        String str = "this is java class";
        String newStr = str.join(",",str.split(" "));
        System.out.println(newStr);
    }
}
```

   
Q) Write a java program to check two strings are equal or not?  
   
input:  
raise   
tech   
   
output:  
Both are not equal   
   
   

```java
class Test 
{
    public static void main(String[] args)
    {
        String s1 = "raise";
        String s2 = "raise";
        if(s1.equals(s2))
            System.out.println("Both are equals");
        else
            System.out.println("Both are not equals");
    }
}
```

   
   
Q) Write a java program to check two strings are equal or not?  
   
input:  
raise   
RAISE  
   
output:  
Both are equals   
   

```java
class Test 
{
    public static void main(String[] args)
    {
        String s1 = "raise";
        String s2 = "RAISE";
        if(s1.equalsIgnoreCase(s2))
            System.out.println("Both are equals");
        else
            System.out.println("Both are not equals");
    }
}
```

   
   
Q) Write a java program to display the characters from given string?  
   
input:  
raise  
   
output:  
r  
a   
i   
s   
e  
   

```java
class Test 
{
    public static void main(String[] args)
    {
        String str = "raise";
     
        for(int i=0;i<str.length();i++)
        {
            System.out.println(str.charAt(i));
        }
    }
}
```

   
Q) Write a java program to remove special characters from given string?  
   
input:  
R@ai_s#eTe^c&h  
   
Output:  
RaiseTech   
   
   

```java
class Test 
{
    public static void main(String[] args)
    {
        String str = "R@Ai_S#eTe^c&h";
     
        str = str.replaceAll("[^A-Za-z0-9]","");
         
        System.out.println(str);
    }
}
```

   
   
Q) Write a java program to remove spaces from given string?  
   
input:  
R ais e Te ch   
   
Output:  
RaiseTech   
   
   
Approach1  
--------  

```java
class Test 
{
    public static void main(String[] args)
    {
        String str = "R ais e Te ch";
     
        str = str.replaceAll("[^A-Za-z0-9]","");
         
        System.out.println(str);
    }
}
```

   
Approach2  
---------  

```java
class Test 
{
    public static void main(String[] args)
    {
        String str = "R ais e Te ch";
     
        str = str.replaceAll("\\s","");
         
        System.out.println(str);
    }
}
```

   
Q) Write a java program to concatinate two strings?  
   
Input:  
Raise12  
Tech28  
Output:  
RaiseTech40  
   
   

```java
class Test 
{
    public static void main(String[] args)
    {
        String s1 = "Raise12";
        String s2 = "Tech28";
         
        String word1 = s1.replaceAll("[^A-Za-z]","");
        int num1 = Integer.parseInt(s1.replaceAll("[^0-9]",""));
         
        String word2 = s2.replaceAll("[^A-Za-z]","");
        int num2 = Integer.parseInt(s2.replaceAll("[^0-9]",""));
         
        String word = word1 + word2;
        int  num = num1 + num2;
         
        System.out.println(word+num);
    }
}
```

   
   
