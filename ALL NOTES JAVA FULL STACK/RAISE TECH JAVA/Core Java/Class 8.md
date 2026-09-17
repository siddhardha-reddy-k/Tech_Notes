   
int   
====  
It is mostly used datatype in java.  
   
| Title | Info |
| --- | --- |
| Size | 4 bytes (32 bits) |
| Range | -2147483648 to 2147483647 (-2^31 to 2^31-1) |
   
ex:  
1) int i = 10.5;  
           System.out.println(i); // C.T.E   
   
2) int i = true;  
           System.out.println(i); // C.T.E   
   
3) int i = "Hi";  
   System.out.println(i); // C.T.E   
   
4) int i = 'a';  
   System.out.println(i); // 97  
   
Note:  
----  
In java, every character has universal unicode value.  
ex:  
A = 65   
a = 97   
   
   
long   
====  
If int datatype is not enough to hold large value then we need to use long datatype.  
   
| Title | Info |
| --- | --- |
| Size | 8 bytes (64 bits) |
| Range | (-2^63 to 2^63-1) |
   
ex:  
1) long l = "true";  
   System.out.println(l); // C.T.E   
   
2) long l = 'A';  
   System.out.println(l); // 65  
   
3) long l = 10.56;  
   System.out.println(l); // C.T.E   
   
   
   
| float | double |
| --- | --- |
| If we need 4 to 6 decimal point of accuracy<br>then we need to use float. | If we need 14 to 16 decimal point of<br>accuracy then we need to use double. |
| Size : 4 bytes (32 bits) | Size : 8 bytes (64 bits) |
| Range : -3.4e38 to 3.4e38 | Range : -1.7e308 to 1.7e308 |
| To declare a float value we need to suffix<br>with 'f' or 'F'.<br>ex:<br>10.56f | To declare a double value we need to<br>suffix with 'd' or 'D'.<br>ex:<br>10.56d |
   
   
   
ex:  
---  
1) float f = 10.56f;  
   System.out.println(f); // 10.56  
   
2) float f = "Hi";  
   System.out.println(f); // C.T.E   
   
3) float f = 'a';  
   System.out.println(f); // 97.0  
   
4) float f = true;  
   System.out.println(f); // C.T.E   
   
5) float f = 10;  
   System.out.println(f); // 10.0          
   
ex:  
---  
1) double d = 10.56d;  
   System.out.println(d); // 10.56  
   
2) double d = "Hi";  
   System.out.println(d); // C.T.E   
   
3) double d = 'a';  
   System.out.println(d); // 97.0  
   
4) double d = true;  
   System.out.println(d); // C.T.E   
   
5) double d = 10;  
   System.out.println(d); // 10.0  
   
boolean   
=======  
It is used to represent boolean values either true or false.  
   
| Title | Info |
| --- | --- |
| Size | (Not Applicable) |
| Range | (Not Applicable) |
   
ex:  
1) boolean b = "true";  
   System.out.println(b); // C.T.E   
   
2) boolean b = TRUE;  
   System.out.println(b); // C.T.E  
   
3) boolean b = true;  
   System.out.println(b); // true   
   
   
char   
=====  
It is a single character which is enclosed in a single quotation.  
   
| Title | Info |
| --- | --- |
| Size | 2 bytes (16 bits) |
| Range | 0 to 65535 |
   
ex:  
---  
1) char ch = 'a';  
   System.out.println(ch); // a  
     
2) char ch = 65;  
   System.out.println(ch); // A  
   
3) char ch = 65.0;  
   System.out.println(ch); // C.T.E   
   
4) char ch = "A";  
   System.out.println(ch); // C.T.E   
   
5) char ch = 'ab';  
   System.out.println(ch); // C.T.E   
   
Diagram: class8.1  
   
![[attachments/image12.png]]  
   
   
   
