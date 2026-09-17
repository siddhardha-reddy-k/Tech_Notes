   
java.io package  
===============  
   
File   
=====  
   

```java
File f = new File("abc.txt");
```

   
It will check "abc.txt" file already exist or not. If already exist then it simply refers to that file. if it is not exist then it won't create physical file.  
   
ex:  
---  

```java
import java.io.*;
class Test 
{
    public static void main(String[] args) 
    {
        File f = new File("abc.txt");
        System.out.println(f.exists()); // False 
    }
}
```

   
Using File object we can create a physical file.  
   
ex:  
---  

```java
import java.io.*;
class Test 
{
    public static void main(String[] args) 
    {
        try
        {
            File f = new File("abc.txt");
            System.out.println(f.exists()); // false
         
            f.createNewFile();
            System.out.println(f.exists()); // true 
        }
        catch (IOException ioe)
        {
            ioe.printStackTrace();
        }
         
    }
}
```

   
Using File object we can create a directory.  
   
ex:  
---  

```java
import java.io.*;
class Test 
{
    public static void main(String[] args) 
    {
        File f = new File("raisetech");
        System.out.println(f.exists()); // false 
         
        f.mkdir();
        System.out.println(f.exists()); // true 
    }
}
```

   
   
Q) Write a java program to create "cricket123" folder and inside that folder create "abc.txt" file?  
   
ex:  
---  

```java
import java.io.*;
class Test 
{
    public static void main(String[] args)throws IOException 
    {
        File f1 = new File("cricket123");
        f1.mkdir();
         
        File f2 = new File("cricket123","abc.txt");
        f2.createNewFile();
         
        System.out.println("Please check the location");
    }
}
```

   
   
FileWriter   
==========  
It is used to insert character oriented data into a file.  
   
constructor  
-----------  

```java
FileWriter fw = new FileWriter(File f); 
```

   
FileWrite can communicate with file directly.  
ex:  

```java
FileWriter fw = new FileWriter("aaa.txt");
```

   
If file is not available then it will create a physical file.  
   
Methods  
-------  
1) write(int ch)  
---------------  
It is used to insert single character into a file.  
   
2) write(char[] ch)  
-----------------  
It is used to insert collection of characters into a file.  
   
3) write(String s)  
-----------------  
It is used to insert string into a file.  
   
4) flush()  
---------  
It gives guarantee that last character of a file is also inserted.  
   
5) close()   
----------  
It is used to FileWriter object.  
   
   
ex:  
--  

```java
import java.io.*;
class Test 
{
    public static void main(String[] args)
    {
        try(FileWriter fw = new FileWriter("aaa.txt");)
        {
            fw.write(98); // b
            fw.write("\n");
             
            char[] ch = {'a','b','c'};
            fw.write(ch);
            fw.write("\n");
             
            fw.write("raise\ntech");
            fw.flush();
            System.out.println("Please check the location");
        }
        catch (IOException ioe)
        {
            ioe.printStackTrace();
        }
    }
}
```

   
   
FileReader   
==========  
It is used to read character oriented data from a file.  
   
constructor  
-----------  

```java
FileReader fr = new FileReader(File f);
```

   
FileReader can communicate with file directly.  
ex:  

```java
FileReader fr = new FileReader("aaa.txt");
```

   
Methods  
-------  
1) read()  
---------  
It reads next character from a file and returns unicode value.   
If next character is not available then it will return -1.    
   
2) read(char[] ch)  
------------  
It reads collection of characters from a file.  
   
3) close()  
---------  
It is used to clsoe FileReader object.  
   
ex:  
---  

```java
import java.io.*;
class Test 
{
    public static void main(String[] args)
    {
        try(FileReader fr = new FileReader("aaa.txt");)
        {
            int i = fr.read();
            while(i!=-1)
            {
                System.out.print((char)i);
                i = fr.read();
            }
        }
        catch (IOException ioe)
        {
            ioe.printStackTrace();
        }
    }
}
```

   
ex:  
---  

```java
import java.io.*;
class Test 
{
    public static void main(String[] args)
    {
        try(FileReader fr = new FileReader("aaa.txt");)
        {
            char[] carr = new char[50];
             
            fr.read(carr);
             
            for(char ch : carr)
            {
                System.out.print(ch);
            }
        }
        catch (IOException ioe)
        {
            ioe.printStackTrace();
        }
    }
}
```

   
Limitations with FileWriter and FileReader   
==========================================  
While writing data using FileWriter object we need to insert line sperators (\n) which is very headache for the programmer.  
   
While reading the data using FileReader object we need to read character by character which is not convenient to the programmer.  
   
To overcome above limitations Sun Micro System introduced BufferedWriter and BufferedReader.  
   
   
BufferedWriter   
=============  
It is used to insert character oriented data into a file.  
   
constructor  
------------  

```java
BufferedWriter bw = new BufferedWriter(Writer w);
```

   
BufferedWriter can't communicate with file directly. It takes the support of writer object.  
ex:  

```java
BufferedWriter bw = new BufferedWriter(new FileWriter("bbb.txt"));
```

   
If that file is not available then it will create a physical file.  
   
Methods  
-------  
1) write(int ch)  
--------------  
It is used to insert single character into a file.  
   
2) write(char[] ch)  
-----------------  
It is used to insert collection of characters into a file.  
   
3) write(String s)  
--------------  
It is used to insert string into a file.  
   
4) flush()  
-----------  
It gives guarantee that last character of a file is also inserted.  
   
5) close()   
-----------  
It is used to close BufferedWriter object.  
   
6) newLine()  
----------  
It is used to insert new line in to a file.  
   
ex:  
---  

```java
import java.io.*;
class Test 
{
    public static void main(String[] args)
    {
        try(BufferedWriter bw = new BufferedWriter(new FileWriter("bbb.txt"));)
        {
            bw.write(98); // b 
            bw.newLine();
             
            char[] ch = {'a','b','c'};
            bw.write(ch);
            bw.newLine();
             
            bw.write("raisetech");
            bw.flush();
            System.out.println("Please check the location");
        }
        catch (IOException ioe)
        {
            ioe.printStackTrace();
        }
    }
}
```

   
   
   
BufferedReader   
=============  
It is a enhanced reader to read character oriented data into a file.  
   
constructor  
------------  

```java
BufferedReader br = new BufferedReader(Reader r);
```

   
BufferedReader can't communicate with file directly. It takes the support of reader object.  
ex:  

```java
BufferedReader br = new BufferedReader(new FileReader("bbb.txt"));
```

   
The main advantage of BufferedReader over FileReader is we can read the data line by line instead of character by character.  
   
Methods  
--------  
1) read()  
-------  
It reads next character from a file and returns unicode value.  
If next character is not available then it will return -1.  
   
2) read(char[] ch)  
--------------  
It reads collection of characters from a file.  
   
3) close()   
---------  
It is used to close BufferedReader object.  
   
4) readLine()   
-----------  
It is used to read next line from a file. If next line is not available   
thne it will return null.  
ex:  
--  

```java
import java.io.*;
class Test 
{
    public static void main(String[] args)
    {
        try(BufferedReader br = new BufferedReader(new FileReader("bbb.txt"));)
        {
            String line = br.readLine();
            while(line!=null)
            {
                System.out.println(line);
                line = br.readLine();
            }
        }
        catch (IOException ioe)
        {
            ioe.printStackTrace();
        }
    }
}
```

   
PrintWriter  
============  
It is a enhanced writer to write character oriented data into a file.  
   
constructor  
-----------  
PrintWriter pw = new PrintWriter(File f)  
PrintWriter pw = new PrintWriter(Writer w)  
   
PrintWriter can communicate with file directly and it will take the support of writer object also.  
ex:  

```java
PrintWriter pw = new PrintWriter("ccc.txt");
```

or  

```java
PrintWriter pw = new PrintWriter(new FileWriter("ccc.txt"));
```

   
If that file is not available then it will create a physical file.  
   
The main advantage of PrintWriter over FileWriter and BufferedWriter is we can insert any type of data. Specially when we want to insert primitive data then we need to use Printwriter.  
   
   
   
Methods  
--------  
write(int ch)  
write(char[] ch)  
write(String s)  
flush()  
close()   
   
print(int i)  
print(char ch)  
print(String s)  
print(double d)  
print(boolean b)  
   
println(int i)  
println(char ch)  
println(String s)  
println(double d)  
println(boolean b)  
   
   
   
ex:  
---  

```java
import java.io.*;
class Test 
{
    public static void main(String[] args)
    {
        try(PrintWriter pw =new PrintWriter("ccc.txt");)
        {
            pw.write(98); // b
            pw.println(98); // 98
            pw.println('a'); // a 
            pw.println(true); // true 
            pw.println(10.5d); // 10.5
            pw.println("Hi");
            pw.flush();
            System.out.println("Please check the location");
        }
        catch (IOException ioe)
        {
            ioe.printStackTrace();
        }
    }
}
```

   
   
FileOutputStream   
----------------  
It is used to insert the data in the form of byte of streams.  
   
FileInputStream   
-------------  
It is used to read the data in the form of byte of streams.  
   
   
Q) Write a java program to copy the data from one file to another file?  
   
input:  
-----  
source.txt   
----------  
a  
ab  
abc  
abcd   
   
ex:  
---  

```java
import java.io.*;
class Test 
{
    public static void main(String[] args)throws IOException
    {
        FileInputStream fis = new FileInputStream("source.txt");
        FileOutputStream fos = new FileOutputStream("destination.txt");
         
        int byteReads = 0;
        byte[] barr = new byte[50];
         
        while((byteReads = fis.read(barr))!=-1)
        {
            fos.write(barr,0,byteReads);
        }
        fis.close();
        fos.close();
        System.out.println("Please check the location");
    }
}
```

   
Assignment   
========  
Q) Write a java program to write and read the data into a file.  
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
