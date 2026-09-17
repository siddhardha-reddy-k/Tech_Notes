   
Q) Write a java program to display the output in a given format?  
   
input:  
abababa   

```java
// 
```

output:  
aba   
   

```java
class Test 
{
    public static void main(String[] args) 
    {
        String str = "abababa";
        str = str.replaceAll("aba","a");
        System.out.println(str);
    }
}
```

   
Q) Write a java program to delete the word in a given string?  
   
Input:   
str = this is java class  
word = is  
   
Output:  
th java class   
   
   

```java
class Test 
{
    public static void main(String[] args) 
    {
        String str = "this is java class";
        String word = "is";
        str = str.replaceAll("is","");
        System.out.println(str); 
    }
}
```

   
Q) Write a java program on trim() method?  
   
Input:  
str = " raise tech "  
Output:  
raise tech  
   
   

```java
class Test 
{
    public static void main(String[] args) 
    {
        String str = " raise tech ";
        System.out.println(str.length()); // 12
        str = str.trim();
        System.out.println(str.length()); // 10
        System.out.println(str);
    }
}
```

   
Q) Write a java program to display number of digits, sum of digits and it is even or odd?  
   
Input:  
NEX123  
Output:  
| Title | Info |
| --- | --- |
| Number of digits | 3 |
| Sum of digits | 6 |
It is even number   
   
   

```java
class Test 
{
    public static void main(String[] args) 
    {
        String str = "NEX123";
        String digits = str.replaceAll("[^0-9]","");
        System.out.println("No of digits :"+digits.length()); // 3
        int sum = 0;
        for(int i=0;i<digits.length();i++)
        {
            int n = Character.getNumericValue(digits.charAt(i));        
            sum+=n;
        }
        System.out.println("Sum of digits :"+sum);
        System.out.println((sum%2==0)?"It is even number":"It is odd number");
    }
}
```

   
   
Q) Write a java program to perform right rotation of a given string?  
   
input:  
str = raisetech   
cnt = 2  
output:  
isetechra  
   
   

```java
class Test 
{
    public static void main(String[] args) 
    {
        String str ="raisetech"; 
        int cnt = 2;
         
        String word1 = str.substring(cnt);
        String word2 = str.substring(0,cnt);
         
        str = word1+word2;
         
        System.out.println(str);
    }
}
```

Regex grouping  

```java
class Test {
    public static void main(String[] args) {
        String str = "raisetech";
        System.out.println(str.replaceAll("(.{2})(.*)", "$2$1"));
    }
}
```

   
   
Q) Write a java program to insert a word in a given string?  
   
input:  
str = "JavaStudents"  
insert = "For"  
index = 4  
Output:  
JavaForStudents   
   

```java
class Test 
{
    public static void main(String[] args) 
    {
        String str ="JavaStudents";
        String insert = "For";
        int index = 4; 
         
        String word1 = str.substring(0,index); // Java
        String word2 = str.substring(index); // Students
         
        str = word1+insert+word2;
        System.out.println(str);
    }
}
```

Regex grouping  

```java
class Test {
    public static void main(String[] args) {
        String str = "JavaStudents";
        str = str.replaceAll("(.{4})(.+)", "$1For$2");
        System.out.println(str);
    }
}
```

   
   
   
Q) Write a java program to display the string in a given format?  
   
input:  
abc.txt  
   
output:  
txt   
   

```java
class Test 
{
    public static void main(String[] args) 
    {
        String str ="abc.txt";
        int index = str.indexOf('.');        
        System.out.println(str.substring(index+1));
    }
}
```

regexWay  

```java
class Test {
    public static void main(String[] args) {
        String str = "abc.txt";
        System.out.println(str.replaceAll(".*\\.", ""));
    }
}
```

   
   
   
Q) Write a java program to sort the string?                  
   
Input:  
daceb  
output:  
abcde  
   

```java
import java.util.Arrays;
class Test 
{
    public static void main(String[] args) 
    {
        String str ="daceb";
        char[] carr = str.toCharArray(); 
        Arrays.sort(carr); 
        str = new String(carr);
        System.out.println(str); 
    }
}
```

   
Q) Write a java program to check given string is Anagram or not?  
   
Input:  
silent           
listen   
   
Output:  
It is a anagram string           
   
   

```java
import java.util.Arrays;
class Test 
{
    public static void main(String[] args) 
    {
        String s1 = "silent";         
        String s2 = "listen";
         
        char[] carr1 = s1.toCharArray();
        char[] carr2 = s2.toCharArray();
         
        Arrays.sort(carr1); // e i l n s t 
        Arrays.sort(carr2); // e i l n s t
         
        s1 = new String(carr1);
        s2 = new String(carr2);
         
        if(s1.equals(s2))
            System.out.println("It is a Anagram string");
        else
            System.out.println("It is not a Anagram string");
    }
}
```

**Time complexity:** O(n log n) — dominated by the sort.  
**Space:** O(n)  
   
   
**Dsa Way, Time complexity:** O(n), Space : O(n)  

```java
public class Test {
    public static void main(String[] args) {
        String str1 = "silent";
        String str2 = "listen";
        if (str1.length() != str2.length()) {
            System.out.println("Its Not an anagram");
        } else {
            int[] freq = new int[26];
            for (int i = 0; i < str1.length(); i++) {
                freq[str1.charAt(i) - 'a']++;
                freq[str2.charAt(i) - 'a']--;
            }
            boolean isAnagram = true;
            for (int f : freq) {
                if (f != 0) {
                    isAnagram = false;
                }
            }
            System.out.println((isAnagram) ? "Its an Anagram" : "its not an Anagram");
        }
    }
}
```

   
   
   
Q) Write a java program to display highest int number from given string?  
   
Input:  
1kg apple for 100 rupees and 2kg mangoes for 200 rupees  
   
Output:  
200  
   
   

```java
class Test 
{
    public static void main(String[] args) 
    {
        String str = "1kg apple for 100 rupees and 2kg mangoes for 200 rupees";
        String[] sarr  = str.split("\\D+");
         
        int max = Integer.MIN_VALUE;
         
        for(String s : sarr)
        {
            int n = Integer.parseInt(s);
            if(n>max)
            {
                max = n;
            }
        }
        System.out.println(max);
    }
}
```

   
Q) John has purchased a new laptop for his office work. His child started to frame sentences using words . John wants to write one program to find out the longest word created by his child.  
   
Input:  
cat apple elephant ball                   
   
Output:  
elephant   
   
   
   

```java
class Test 
{
    public static void main(String[] args) 
    {
        String str = "cat apple elephant ball";
        String[] sarr  = str.split(" ");
         
        int max = sarr[0].length();
        String result = "";
         
        for(String s : sarr)
        {
            if(s.length() > max)
            {
                max = s.length();
                result = s;
            }
        }
        System.out.println(result);
    }
}
```

   
   
Q) Write a java program to display reverse of a string?  
   
Input:  
hello   
   
output:  
olleh   
   

```java
class Test 
{
    public static void main(String[] args) 
    {
        String str = "hello";
         
        String rev = "";
         
        for(int i=str.length()-1;i>=0;i--)
        {
            rev += str.charAt(i);        
        }
         
        System.out.println(rev);
    }
}
```

   
   
Q) Write a java program to check given string is palindrome or not?  
   
input:  
racar   
   
output:  
It is a palindrome string   
   
   
   

```java
class Test 
{
    public static void main(String[] args) 
    {
        String str = "racar";
         
        String rev = "";
         
        for(int i=str.length()-1;i>=0;i--)
        {
            rev += str.charAt(i);        
        }
         
        if(str.equals(rev))
            System.out.println("It is a palindrome string");
        else
            System.out.println("It is not a palindrome string");
    }
}
```

   

```java
public class Test {
    public static void main(String[] args) {
        String str = "racar";
        int left = 0, right = str.length() - 1;
        boolean isPalindrome = true;
        while (left < right) {
            if (str.charAt(left) != str.charAt(right)) {
                isPalindrome = false;
                break;
            }
            left++;
            right--;
        }
        System.out.println(isPalindrome ? "It is a palindrome string" : "It is not a palindrome string");
    }
}
```

TC - O(1);  
   
   
   
Q) Write a java program to display reverse of a sentence?  
   
input:  
this is java class   
   
output:  
class java is this   
   
   

```java
class Test 
{
    public static void main(String[] args) 
    {
        String str = "this is java class";
         
        String[] sarr = str.split(" ");
         
        String rev = "";
         
        for(int i=sarr.length-1;i>=0;i--)
        {
            rev += sarr[i]+" ";        
        }
        System.out.println(rev.trim());
    }
}
```

   
Using collections  

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
import java.util.Collections;
public class Test {
    public static void main(String[] args) {
        String str = "this is java class";
        String[] strSplit = str.split(" ");
        List<String> words = new ArrayList<>(Arrays.asList(strSplit));
        Collections.reverse(words);
        str = String.join(" ", words);
        System.out.println(str);
    }
}
```

   
   
Q) Write a java program to reverse of a word in a sentence?  
   
input:  
This is java class  
   
output:  
sihT si avaj ssalc                   
   
   
   

```java
class Test 
{
    public static void main(String[] args) 
    {
        String str = "This is java class";
         
        String[] sarr = str.split(" ");
         
        String result = "";
         
        for(String s : sarr) // T h i s 
        {
            String rev = "";
            for(int i=s.length()-1;i>=0;i--)
            {
                rev += s.charAt(i);
            }
            result += rev+" ";
        }
        System.out.println(result.trim());
    }
}
```

   
Better version using StringBuilder:  

```java
class Test {
    public static void main(String[] args) {
        String str = "This is java class";
        String[] sarr = str.split(" ");
        StringBuilder result = new StringBuilder();
        
        for(int i = 0; i < sarr.length; i++) {
            String rev = new StringBuilder(sarr[i]).reverse().toString();
            result.append(rev);
            if(i != sarr.length-1) result.append(" ");
        }
        System.out.println(result.toString());
    }
}
```

   
   
Q) Write a java program to display each word starting letter in uppercase?  
   
input:  
this is java class  
output:  
This Is Java Class   
   
   
   

```java
class Test 
{
    public static void main(String[] args) 
    {
        String str = "this is java class";
         
        String[] sarr = str.split(" ");
         
        String result = "";
         
        for(String s : sarr)
        {
            String first = s.substring(0,1).toUpperCase();
            String second = s.substring(1);
            s = first+second;
            result += s+" ";        
        }
        str = result.trim();
        System.out.println(str);
    }
}
```

   
   
   
Assignment  
----------  
Q) Write a java program to display the string in a given format?  
   
input:  
IhuBTalEnt  
output:  
iHUbtALeNT  
   

```java
class Test {
    public static void main(String[] args) {
        String str = "IhuBTalEnt";
        String result = "";
        
        for(int i = 0; i < str.length(); i++) {
            char ch = str.charAt(i);
            if(Character.isUpperCase(ch)) {
                result += Character.toLowerCase(ch);
            } else {
                result += Character.toUpperCase(ch);
            }
        }
        System.out.println(result);
    }
}
```

   
   
Write a program to count vowels and consonants in a string.  
Input: "programming" → Output: Vowels: 3, Consonants: 8  
   
   

```java
public class Test {
    public static void main(String[] args) {
        String str1 = "programming";
        int vowelsCount = 0;
        int constantsCount = 0;
        for (int i = 0; i < str1.length(); i++) {
            char c = str1.charAt(i);
            String s = "" + c;
            if (s.matches("[aeiou]")) {
                vowelsCount++;
            } else if (s.matches("[^aeiou]")) {
                constantsCount++;
            }
        }
        System.out.println(vowelsCount + " " + constantsCount);
    }
}
```

   
2nd method  
   

```java
public class Test {
    public static void main(String[] args) {
        String str1 = "programming";
        int vowelsCount = 0;
        int consonantsCount = 0;
        for (int i = 0; i < str1.length(); i++) {
            char c = str1.charAt(i);
            if ("aeiouAEIOU".indexOf(c) != -1) {
                vowelsCount++;
            } else if (Character.isLetter(c)) {
                consonantsCount++;
            }
        }
        System.out.println(vowelsCount + " " + consonantsCount);
    }
}
```

   
   
   
Q) Write a java program to display palindrome string?  
   
input:  
racar is madam for students  
   
output:  
racar madam   
   

```java
class Test {
    public static void main(String[] args) {
        String str = "racar is madam for students";
        String[] words = str.split(" ");
        String result = "";
        
        for(String w : words) {
            String rev = new StringBuilder(w).reverse().toString();
            if(w.equals(rev)) {
                result += w + " ";
            }
        }
        System.out.println(result.trim());
    }
}
```

   
   
   
   
