   
History of Java  
===============  
In 1990, Sun Micro System company took one project to develop a software called consumer electronic device which can be controlled by a remote like a setup box.  
That time project as called Stealth project and later it is renamed to Green project.  
   
James Gosling, Mike Sharadin, Patrick Naughton were there to develop the project and they have met in a place called Aspan/Colarado to start the work with Graphic System. James Gosling decided to use C and C++ languages to develop the project but the problem what they have faced is C and C++ languages are system dependent. Then James Gosling decided why don't we create our own programming language which is system independent.   
   
In 1991, they have developed a programming language called OAK. OAK is a national tree for many countries like Germany, France, USA and etc. Late in 1995 they have renamed OAK to JAVA. Java is a island of an Indonasia where first coffee of seed was produced and during the development of project they were consuming lot of coffee's. Hence symbol of java is a cup of coffee with saucer.  
   
   
Interview Questions   
===================  
Q) Who is the creator of Java?  
   
James Gosling   
   
Q) In which year java was developed?  
   
In 1995  
   
Q) Java originally known as ___ ?  
   
OAK   
   
   
Q) What is the difference between JDK, JRE and JVM ?  
   
JDK   
----  
JDK stands for Java Development Kit.  
   
It is a installable software which consist Java Runtime Environment (JRE), Java Virtual Machine (JVM), compiler (javac), interpreter(java), an archiever (.jar). document generator (javadoc) and other tools needed for java application development.  
   
JRE  
----  
JRE stands for Java Runtime Environment.  
JRE is a part of a JDK which provides very good environment to run java applications only.  
   
   
JVM   
----  
JVM stands for Java Virtual Machine.  
JVM is a part of JRE which is used to execute our program line by line procedure and converts byte code to machine code.  
   
   
Diagram: class6.1  
![[attachments/image8.png]]  
   
   
Internal Architecture of JVM   
============================  
Diagram: class6.2  
![[attachments/image9.png]]  
Java application contains java code instructions. One if we compiled, java code instructions convert to byte code instructions in .class file.  
   
JVM invokes one module called classloader/subsystem to load all the byte code instructions from .class file. The work of classloader is to check these byte code instructions are proper or not. If they are not proper then it will refuse the execution. If they are proper then it will allocate memory.   
   
We have five types of memories in java.  
   
1) Method Area   
-------------  
It contains code of a class, code of a variable and code of a method.  
   
2) Heap   
--------  
Our object creation will store in heap area.  
   
3) Java Stack  
--------------  
Java methods store in method area. But to execute those methods we required some memory and that memory is allocated in Java Stack.   
   
4) PC Register   
--------------  
It is a program counter register which is used to track the address of instructions.  
   
5) Native Method Stack   
-----------------------  
Java methods execute in method area.  
Similarly native methods execute in native method stack.  
But to execute native methods we required one program called Native method interfacae.  
   
   
Execution Engine   
----------------  
Execution engine contains interpreter and JIT compiler.  
Whenever JVM loads byte code instructions from .class file. It simultenously uses interpreter and JIT compiler.  
   
Interpreter is used to execute our program line by line procedure.  
   
JIT compiler is used to increase the execution speed of our program.  
   
Finally, JVM converts byte code to machine code.  
   
   
Interview Questions   
===================  
   
Q) A .class file contains which code ?  
   
byte code   
   
   
Q) Which package consider as default package in java?  
   
java.lang package  
   
   
Q) How many memories are there in java?  
   
We have five memories in java.  
   
1) Method Area   
2) Heap   
3) JAva Stack   
4) PC Register   
5) Native Method Stack   
   
   
Q) What is Native method in java?  
   
Method which is developed by using some other language is called native method.  
But we can't execute native methods in java directly, we required a program called Native method interface and all native methods store in native method stack memory.   
   
   
Q) What is JIT compiler?  
   
JIT compiler is a part of a JVM which is used to increase the execution speed of our program.  
   
   
Assignment  
==========  
1) What is Java?  
2) Features of Java?  
3) JDK vs JRE vs JVM?  
4) which package consider as default package in java?  
5) How many memories are there in java?  
6) What is JIT compiler   
7) What is Native method in java?  
   
   
