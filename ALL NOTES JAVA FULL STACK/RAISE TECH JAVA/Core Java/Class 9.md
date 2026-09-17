   
Q) Is java purely object oriented or not ?  
   
No, Java will not consider as purely object oriented programming language because java does not support many OOPS concepts like multiple inheritance, operator overloading and more ever we depends upon primitive datatypes which are non-objects.  
   
   
Q) Write a java program to display range of int datatype?  
   

```java
class Test
{
    public static void main(String[] args)
    {
        System.out.println(Integer.BYTES);
        System.out.println(Integer.SIZE);
    }
}
```

   
   
Q) Write a java program to find out size of short datatype?  
   

```java
class Test
{
    public static void main(String[] args)
    {
        System.out.println(Short.BYTES);
        System.out.println(Short.SIZE);
    }
}
```

   
Q) Write a java program to display range of short datatype?  
   

```java
class Test
{
    public static void main(String[] args)
    {
        System.out.println(Short.MIN_VALUE);
        System.out.println(Short.MAX_VALUE);
    }
}
```

   
   
Q) Write a java program to display range of int datatype?  
   

```java
class Test
{
    public static void main(String[] args)
    {
        System.out.println(Integer.MIN_VALUE);
        System.out.println(Integer.MAX_VALUE);
    }
}
```

   
   
Q) Write a java program to display range of char datatype?  
   

```java
class Test
{
    public static void main(String[] args)
    {
        System.out.println((int)Character.MIN_VALUE);
        System.out.println((int)Character.MAX_VALUE);
    }
}
```

   
   
Types of variables  
==================  
A name given to a memory location is called variable.  
   
Purpose of variable is used to store the data.  
   
In java, variables are divided into two types.  
   
1) Primitive variables  
----------------------  
It is used to represent primitive values.  
   
2) Reference variables   
----------------------  
It is used to represent object reference.          
ex:  

```java
Student s = new Student();
```

|  
reference variable   
   
Based on the position and execution these variables are divided into three types.  
   
1) Instance variables / Non-static variables   
   
2) Static variables / Global variables   
   
3) Local variables / Temperory variables   
   
   
   
## 1. Development (Source Code)  
- **Writing:** You write code in a text editor or IDE.  
- **Saving:** Files are saved with the .java extension. [[1](<https://www.scaler.com/topics/java/how-java-program-works/>), [2](<https://www.fusion-institute.com/java-programming-structure-explained-for-beginners-guide>), [3](<https://www.aegissofttech.com/insights/what-is-java-technology/>), [4](<https://www.wscubetech.com/resources/c-programming/first-program>), [5](<https://hyperskill.org/university/java/java-for-beginners>)]  
## 2. Compilation (Build Time)  
- **Command:** Run javac MyClass.java in the terminal.  
- **Compiler:** The Java Compiler (javac) checks for syntax errors.  
- **Bytecode:** If clean, it generates platform-independent .class files (bytecode). [[1](<https://medium.com/@piyalahmed/this-is-how-to-run-a-pdf-file-as-a-java-program-b3cc0bfa2527>), [2](<https://stackoverflow.com/questions/65355383/how-do-i-run-a-java-program-in-the-terminal-using-short-form>), [3](<https://smartprogramming.in/tutorials/java/how-java-works>), [4](<https://medium.com/@roopa.kushtagi/journey-through-java-execution-from-loader-to-memory-model-3e37809a6f6f>), [5](<https://codefinity.com/blog/What-Is-the-Java-Virtual-Machine-(JVM)-and-How-Does-It-Work%3F>)]  
## 3. Execution (Run Time)  
- **Command:** Run java MyClass to start the JVM.  
- **Class Loading:** The ClassLoader loads, links, and initializes the .class file.  
- **Memory Setup:** JVM allocates memory areas (Heap, Stack, Method Area).  
- **Execution Engine:** The JVM reads bytecode and converts it to machine instructions.  
- **JIT Compiler:** The Just-In-Time compiler speeds up the program by compiling hot code.  
- **Output:** Your program runs and outputs results. [[1](<https://nachoiborraies.github.io/java/md/en/01a.html>), [2](<https://www.reddit.com/r/AskProgramming/comments/s0qtox/what_exactly_is_a_programming_language_what_is/>), [3](<https://www.edureka.co/blog/java-virtual-machine/>), [4](<https://www.turing.com/interview-questions/java>), [5](<https://medium.com/@sunil17bbmp/java-classloader-explained-how-it-works-with-real-examples-ff8f22793270>)]  
   
   
   
1) Instance variables  
---------------------  
A value of a variable which is varied (changes) from object to object is called instance variable.   
   
Instance variable allocates memory at the time of object creation and it will destroy at the time of object destruction. Hence scope of instance variable is same as scope of an object.  
   
Instance variables store in heap area as a part of an object.  
   
Instance variable must and should declare immediately after the class but not inside methods, blocks and constructors.  
   
Instance variable we can access directly from instance area but we can't access   
directly from static area.  
   
To access instance variable from static area we need to create object reference.  
   
ex:1  
----  

```java
class Test
{
    //instance variable 
    int i = 10;
 
    public static void main(String[] args)
    {
        System.out.println(i);        // C.T.E         
    }
}
```

   
ex:2  
----  

```java
class Test
{
    //instance variable 
    int i = 10;
 
    public static void main(String[] args)
    {
        Test t = new Test();
        System.out.println(t.i);        
    }
}
```

   
Note:  
----  
If we won't initialize any value to instance variable then JVM will initialized default values.  
   
ex:3  
----  

```java
class Test
{
    //instance variable 
    boolean b;
     
    public static void main(String[] args)
    {
        Test t = new Test();
        System.out.println(t.b); // false         
    }
}
```

   
Note:  
-----  
In java, For every object a seperate copy of instance variable will be created.  
   
ex:4  
----  

```java
class Test
{
    //instance variable 
    int i = 10;
     
    public static void main(String[] args)
    {
        Test t1 = new Test();
        Test t2        = new Test();
 
        System.out.println(t1.i);//10
        System.out.println(t2.i);//10
 
        t1.i=100;
 
        System.out.println(t1.i); //100
        System.out.println(t2.i); //10
 
 
 
```
