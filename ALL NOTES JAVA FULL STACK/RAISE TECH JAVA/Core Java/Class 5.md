   
Java  
=====  
| Title | Info |
| --- | --- |
| Version | JDK-25 or JDK-26 |
| Creator | James Gosling |
| Vendor | Oracle Corporation (Sun Micro System) |
| Open source | Open source |
| Website | [www.oracle.com/in/java](<http://www.oracle.com/in/java>) |
| Tutorials | [www.geeksforgeeks.org](<http://www.geeksforgeeks.org>)<br>[www.tutorialspoint.com](<http://www.tutorialspoint.com>)<br>[www.w3schools.com](<http://www.w3schools.com>)<br>and etc. |
| Download link | [https://www.oracle.com/in/java/technologies/downloads/#jdk25-windows](<https://www.oracle.com/in/java/technologies/downloads/#jdk25-windows>) |
   
   
Steps to setup environment variables   
====================================  
step1:  
------  
Make sure JDK software installed successfully.  
   
step2:  
------  
Copy "bin" directory from "JAVA" home folder.  
ex:  
C:\Program Files\Java\jdk-25\bin  
   
step3:  
------  
Paste "bin" directory in environment variables.  
ex:  
Right click to This PC --> properties --> Advanced System Settings   
--> Environment variables --> Goto System variables -->   
click to new button -->  
| Title | Info |
| --- | --- |
| variable name | path |
| variable value | C:\Program Files\Java\jdk-25\bin; |
--> ok --> ok --> ok.  
   
step4:  
------  
Check environment setup done perfectly or not.  
ex:  
cmd> javap   
cmd> java  -version                   
   
Steps to develop first java application   
=======================================  
step1:  
------  
Create a "javaprog" folder inside "D" drive.  
   
step2:  
-----  
Open the notepad and write simple Hello World program.  
   
ex:  

```java
class Test
{
    public static void main(String[] args)
    {
        System.out.println("Hello World");
    }
}
```

step3:  
------  
Save above program with same name as class name inside "javaprog" folder.  
   
   
step4:  
------  
Open the command prompt from "javaprog" location.  
   
step5:  
-----  
Compile java program by using below command.  
ex:  
javac  Test.java  
|  
filename   
   
step6:  
-----  
Execute java program by using below command.  
ex:  
java    Test  
|  
classname   
   
Interview Questions   
===================  
   
Q) Is java platform dependent or independent ?   
   
Java is platform independent at byte code level.  
Hence it is also known as WORA- Write Once Run Anywhere.  
   
Diagram: class5.1  
![[attachments/image7.png]]  
   
Q) Is JVM platform dependent or independent?  
   
JVM is platform dependent.  
   
   
