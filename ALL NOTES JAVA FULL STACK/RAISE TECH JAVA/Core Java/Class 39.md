   
   
Q) Write a java program to display the string in a given format?  
   
Input:  
H2ow Ar3e Hello1 Yo4u  
   
Output:  
Hello How Are You  
   
   

```java
class Test  
{
    public static void main(String[] args) 
    {
        String str = "H2ow Ar3e Hello1 Yo4u";
        String[] words = str.split(" ");
        String[] result = new String[words.length];
         
        for(String word :words)
        {
            int position=0;
            String text="";
             
            for(char ch : word.toCharArray())
            {
                if(Character.isDigit(ch))
                {
                    position = ch - '0';
                }
                else
                {
                    text += ch;
                }        
            }
            result[position-1] = text;
        }
         
        for(String s : result)
        {
            System.out.print(s+" ");
        }
    }
}
```

Regex -   

```java
class Test {
    public static void main(String[] args) {
        String str = "H2ow Ar3e Hello1 Yo4u";
        String[] strArray = str.split(" ");
        String[] wordsArr = new String[strArray.length];
        for (String w : strArray) {
            String word = w.replaceAll("\\d", "");
            int num = Integer.parseInt(w.replaceAll("\\D", ""));
            wordsArr[num - 1] = word;
        }
        for (String word : wordsArr) {
            System.out.print(word + " ");
        }
    }
}
```

  
   
Q) Write a java program to display unique and duplicate characters from given string?  
   
Input:  
messissippi  
   
Output:  
| Title | Info |
| --- | --- |
| Unique characters | mesip |
| Duplicate characters | sip |
   
   

```java
class Test  
{
    public static void main(String[] args) 
    {
        String str = "messissippi";
        String unique="";
        String duplicates="";
         
        for(int i=0;i<str.length();i++)
        {
            String current = Character.toString(str.charAt(i));
            if(unique.contains(current))
            {
                if(!duplicates.contains(current))
                {
                    duplicates+=current;
                    continue;
                }
                else
                {
                    continue;
                }
            }
            unique+=current;
        }
        System.out.println("Unique Characters : "+unique);
        System.out.println("Duplicate Characters :"+duplicates);
    }
}
```

Using LinnkedHashSet  

```java
import java.util.*;
class Test {
    public static void main(String[] args) {
        String str = "messissippi";
        Set<Character> seen = new LinkedHashSet<>();
        Set<Character> duplicates = new LinkedHashSet<>();
        
        for(char ch : str.toCharArray()) {
            if(!seen.add(ch)) {          // add() returns false if already present
                duplicates.add(ch);
            }
        }
        
        System.out.println("Unique Characters : " + seen);
        System.out.println("Duplicate Characters : " + duplicates);
    }
}
 
 
```

   
Q) Write a java program to encode the string?  
   
input:  
1106  
   
Output:  
AAJF  
   

```java
class Test  
{
    public static void main(String[] args) 
    {
        String str = "1106";
        for(int i=0;i<str.length();i++)
        {
            int n = Character.getNumericValue(str.charAt(i));
            if(n>0)
            {
                System.out.print((char)('A'+n-1));
            }
            else
            {
                int k = Integer.parseInt(str.substring(i-1,i+1));
                System.out.print((char)('A'+k-1));
            }
        }
    }
}
```

   
Q) Write a java program to decode the string?  
   
input:  
AAJF  
   
Output:  
1106  
   
   

```java
class Test  
{
    public static void main(String[] args) 
    {
        String str = "AAJF";
        for(int i=0;i<str.length();i++)
        {
            char ch = str.charAt(i);
             
            int n = ch - 'A' + 1;
             
            if(Integer.toString(n).contains("0"))
            {
                System.out.print(n%10);
            }
            else
            {
                System.out.print(n);
            }
        }
    }
}
```

   
Q) Write a java program to display the string in a given format?  
   
Input:  
A1B2C3D4  
Output:  
ABBCCCDDDD  
   
   

```java
class Test  
{
    public static void main(String[] args) 
    {
        String str = "A1B2C3D4";
        for(int i=0;i<str.length();i++)
        {
                 
            if(Character.isAlphabetic(str.charAt(i)))
            {
                System.out.print(str.charAt(i));
            }
            else
            {
                int n = Character.getNumericValue(str.charAt(i));
                for(int k=1;k<n;k++)
                {
                    System.out.print(str.charAt(i-1));
                }
            }
        }
    }
}
```

MyOwnLoop  
   

```java
class Test {
    public static void main(String[] args) {
        String str = "A1B2C3D4";
        for (int i = 0; i < str.length(); i += 2) {
            char c = str.charAt(i);
            int n = Character.getNumericValue(str.charAt(i + 1));
            for (int j = 0; j < n; j++) {
                System.out.print(c);
            }
        }
    }
}
```

   
   
Q) Write a java program to display the string in a given format?  
   
Input:  
ABBCCCDDDD  
Output:  
A1B2C3D4  
   
   

```java
class Test  
{
    public static void main(String[] args) 
    {
        String str = "ABBCCCDDDD";
        int cnt = 1;
        String result = "";
             
        for(int i=0;i<str.length();i++)
        {
            if(i<str.length()-1 && str.charAt(i) == str.charAt(i+1))
            {
                cnt++;
            }
            else
            {
                result += str.charAt(i);
                result += cnt;
                cnt = 1;
            }
        }
        System.out.println(result);
    }
}
```

   
StringBuffer   
============  
If our content change frequently then it is never recommanded to use String because for every change a new object will be created.  
   
To overcome this limitation Sun Micro System introduced StringBuffer concept.  
   
In StringBuffer, all the required changes will be done in a same object.  
   
Constructors  
------------  
   
1) StringBuffer sb = new StringBuffer()  
--------------------------------------  
It creates empty StringBuffer object with default initial capacity of 16.  
   
If capacity reaches to maximum capacity then new capacity will be created with below formulea.  
ex:  

```java
new capacity = current_capacity+1 * 2;
```

   
ex:  

```java
class Test  
{
    public static void main(String[] args) 
    {
        StringBuffer sb = new StringBuffer();
        System.out.println(sb.capacity());// 16
         
        sb.append("abcdefghijklmnop");
        System.out.println(sb.capacity());// 16
         
        sb.append("qr");
        System.out.println(sb.capacity()); // 16+1*2=34
    }
}
```

   
2) StringBuffer sb = new StringBuffer(int capacity)  
-------------------------------------------------  
It creates StringBuffer object with specified initial capacity.  
   
ex:  
--  

```java
class Test  
{
    public static void main(String[] args) 
    {
        StringBuffer sb = new StringBuffer(19);
        System.out.println(sb.capacity());// 19
         
    }
}
```

   
3) StringBuffer sb = new StringBuffer(String s)  
------------------------------------------  
It creates StringBuffer object equivalent to String.  
   
Here capacity will be created with below formulea.  
   
ex:  
capacity = s.length() + 16  
   
   
ex:  
----  

```java
class Test  
{
    public static void main(String[] args) 
    {
        StringBuffer sb = new StringBuffer("raisetech");
        System.out.println(sb.capacity());// 9+16 = 25
         
    }
}
```

   
   
Q) Write a java program to display reverse of a string?  
   
input:  
hello  
   
output:  
olleh   
   
ex:  
---  

```java
class Test  
{
    public static void main(String[] args) 
    {
        String str = "hello";
        StringBuffer sb = new StringBuffer(str);
        String rev = sb.reverse().toString();
        System.out.println(rev);
    }
}
```

   
Q) Write a java program to check given string is palindrome or not?  
   

```java
class Test  
{
    public static void main(String[] args) 
    {
        String str = "racar";
        StringBuffer sb = new StringBuffer(str);
        String rev = sb.reverse().toString();
        if(str.equals(rev))
            System.out.println("It is a palindrome string");
        else
            System.out.println("It is not a palindrome string");
    }
}
```

   
Q) Write a java program to insert a given word in a string?  
   
input:  
str = "JavaStudents"  
word = "For"  
index = 4  
   
Output:  
JavaForStudents  
   
   

```java
class Test  
{
    public static void main(String[] args) 
    {
        String str = "JavaStudents";
        String word = "For";
        int index = 4;
 
        StringBuffer sb = new x(str);
        str = sb.insert(index,word).toString();
        System.out.println(str);
    }
}
```

   
Assignment   
==========  
Q) Write a java program to display the string in a given format?  
   
input:  
XYZ  
output:  
XY  
XZ  
YX  
YZ  
ZX  
ZY   
   

```java
class Test {
    public static void main(String[] args) {
        String str = "XYZ";
        
        for(int i = 0; i < str.length(); i++) {
            for(int j = 0; j < str.length(); j++) {
                if(i != j) {
                    System.out.println("" + str.charAt(i) + str.charAt(j));
                }
            }
        }
    }
}
```

   
   
Q) Write a java program to convert number to words?  
   
Input:  
125  
   
Output:  
One Hundred Twenty Five   
   
   
   

```java
class Test {
    public static void main(String[] args) {
        int num = 125;
        String[] ones = { "", "One", "Two", "Three", "Four", "Five", "Six", "Seven", "Eight", "Nine",
                "Ten", "Eleven", "Twelve", "Thirteen", "Fourteen", "Fifteen", "Sixteen",
                "Seventeen", "Eighteen", "Nineteen" };
        String[] tens = { "", "", "Twenty", "Thirty", "Forty", "Fifty", "Sixty", "Seventy", "Eighty", "Ninety" };
        String result = "";
        int hundreds = num / 100;
        int remainder = num % 100;
        if (hundreds > 0) {
            result += ones[hundreds] + " Hundred ";
        }
        if (remainder < 20) {
            result += ones[remainder];
        } else {
            result += tens[remainder / 10] + " " + ones[remainder % 10];
        }
        System.out.println(result.trim());
    }
}
```

   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
