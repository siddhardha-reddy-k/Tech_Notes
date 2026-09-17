   
Identifiers  
===========  
A name given to a program elements is called identifier.  
   
Here program elements means variable name, method name, class name, interface name, package name and constant name.  
   
ex:  

```java
class Test
{
    public static void main(String[] args)
    {
        int x = 10;
 
        System.out.println(x);
    }
}
```

   
Here Test,main,String,args,x,System and println() are identifiers.  
   
Rules to declare an identifiers  
-------------------------------  
Rule1:  
-----                  
Identifier will accept following characters.  
ex:          
A-Z  
a-z  
0-9  
_  
$  
   
Rule2:  
------  
If we take other characters then we will get compile time error.  
ex:  

```java
int  emp_id;      
int  emp$alary;
```

int  emp@no;  //invalid   
   
   
Rule3:  
-----  
Every identifier is a case sensitive.  
ex:  

```java
int  a;
int  A;
```

   
Rule4:  
-----  
Identifier must and should starts with alphabet,underscore or dollar symbol   
but not with digit.  
ex:  

```java
int  a1234;  
int  _abcd; 
int  $alary; 
```

int  1abcd;  //invalid           
   
Rule5:  
------  
We can't take reserved words as an identifier name.  
ex:  
int  if;  //invalid           
int  for; //invlaid   
int  public; //invalid   
   
Rule6:  
------  
There is no length limit for an identifier but it is not recommanded   
to take more then 15 characters.  
   
   
   
   
Reserved Words   
==============  
There are some identifiers which are reserved to associate some functionality of meaning such type of identifiers are called reserved words.  
   
Java supports 70 reserved words and it is classified into two types.  
   
Diagram: class7.1  
![[attachments/image10.png]]  
   
Used keywords with respect to flow control  
---------------------------------------------  
if  
else  
switch  
case  
default  
for  
while  
do  
break  
continue  
return  
   
Used keywords with respect to Access modifiers  
-----------------------------------------  
public  
private  
protected  
   
Used keywords with respect to classes and interfaces  
--------------------------------------  
class  
interface  
enum  
extends  
implements  
abstract  
final  
static  
strictfp  
sealed  
permits  
   
Used keywords with respect to exception handling   
---------------------------  
try  
catch  
finally  
throw  
throws  
assert  
   
Used keywords with respect to variables and methods  
--------------------------------  
void  
var  
new  
this  
super  
volatile  
transient  
synchronized  
   
Used keywords with respect to datatypes.  
----------------------------------------  
int  
long  
short  
byte  
float  
double  
char  
boolean  
   
   
Used keywords with respect to package  
---------------------------------------  
package  
import  
module  (Java 9+)  
   
   
Used keywords with respect to object and reference handling  
--------------------------------  
instanceof  
typeof   (reserved but unused in Java)  
yield    (Java 14+ switch expression)  
record   (Java 16+)  
native  
   
   
Used keywords with respect to misc reserved words   
--------------------------------------------  
requires  (Java 9 modules)  
exports   (Java 9 modules)  
opens     (Java 9 modules)  
uses      (Java 9 modules)  
provides  (Java 9 modules)  
with      (Java 9 modules)  
to        (Java 9 modules)  
non-sealed (Java 17+)  
   
   
   
   
Datatypes  
=========  
Datatype describes what type of value we want to store inside a variable.  
   
Datatype also tells how much memory has to be created for a variable.  
   
In java, datatypes are divided into two types.  
   
Diagram: class7.2          
![[attachments/image11.png]]  
   
byte  
-----  
It is a smallest datatype in java.  
   
| Title | Info |
| --- | --- |
| Size | 1 byte (8 bits) |
| Range | -128 to 127 (-2^7 to 2^7-1) |
   
ex:  
1) byte b = 10;  

```java
   System.out.println(b); 
```

   
2) byte b = 10.56;  
   System.out.println(b); // C.T.E   
   
3) byte b = 130;  
   System.out.println(b); // C.T.E   
   
   
short  
-----  
It is rarely used datatype in java.  
   
| Title | Info |
| --- | --- |
| Size | 2 bytes (16 bits) |
| Range | -32768 to 32767  (-2^15 to 2^15-1) |
   
ex:  
1) byte b = 10;  

```java
   short s = b;
```

           System.out.println(s); // 10  
   
2) short s = "Hi";  
   System.out.println(s); // C.T.E   
   
3) short s = true;  
           System.out.println(s); // C.T.E   
   
   
