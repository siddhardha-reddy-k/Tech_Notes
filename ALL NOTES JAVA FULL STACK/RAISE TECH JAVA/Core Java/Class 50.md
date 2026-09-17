   
Stream API   
==========  
Stream API introduced in Java 8.  
   
Stream API present in java.util.stream package.  
   
It allows functional style programming which makes our code simple and elegant.  
   
It is used to process the objects/data.  
   
It is used to perform bulk operations on Collections.  
   
ex:  
---  

```java
import java.util.*;
import java.util.stream.*;
class Test  
{
    public static void main(String[] args) 
    {
        List<Integer> marks = List.of(56,49,71,67,84);
         
        //add 10 grace marks 
        List<Integer> newMarks = marks.stream()
                    .map(i -> i + 10).collect(Collectors.toList());
         
        System.out.println(newMarks);
    }
}
```

   
   
ex:  
---  

```java
import java.util.*;
import java.util.stream.*;
class Test  
{
    public static void main(String[] args) 
    {
        List<Integer> list = List.of(6,9,1,7,4);
         
        //display even elements 
        List<Integer> newList = list.stream().filter(i -> i%2==0).collect(Collectors.toList());
         
        System.out.println(newList);
    }
}
```

   
ex:  
---  

```java
import java.util.*;
import java.util.stream.*;
class Test  
{
    public static void main(String[] args) 
    {
        List<Integer> list = List.of(6,9,1,7,4);
         
        //counting even elements 
        long cnt = list.stream().filter(i -> i%2==0).count();
         
        System.out.println(cnt);
    }
}
```

   
ex:  
---  

```java
import java.util.*;
import java.util.stream.*;
class Test  
{
    public static void main(String[] args) 
    {
        List<Integer> list = List.of(6,9,1,7,4);
         
        //sort the list 
        List<Integer> newList = list.stream().sorted().toList();
         
        System.out.println(newList);
    }
}
```

   
ex:  
---  

```java
import java.util.*;
import java.util.stream.*;
class Test  
{
    public static void main(String[] args) 
    {
        List<Integer> list = List.of(6,9,1,7,4);
         
        //descending the list 
        List<Integer> newList = list.stream().sorted(Comparator.reverseOrder()).toList();
         
        System.out.println(newList);
    }
}
```

   
ex:  
---  

```java
import java.util.*;
import java.util.stream.*;
class Test  
{
    public static void main(String[] args) 
    {
        List<Integer> list = List.of(6,9,1,7,4);
         
        //highest element
        long max = list.stream().max((i1,i2)->i1.compareTo(i2)).get();
         
        System.out.println(max);
    }
}
```

   
ex:  
---  

```java
import java.util.*;
import java.util.stream.*;
class Test  
{
    public static void main(String[] args) 
    {
        List<Integer> list = List.of(6,9,1,7,4);
         
        //least element
        long min = list.stream().min((i1,i2)->i1.compareTo(i2)).get();
         
        System.out.println(min);
    }
}
```

   
Q) Write a java program to display distinct elements from list using stream API?  
   

```java
import java.util.*;
import java.util.stream.*;
class Test  
{
    public static void main(String[] args) 
    {
        List<Integer> list = List.of(1,6,7,2,6,9,9,4);
         
        //distinct elements 
        List<Integer> newList = list.stream().distinct().toList();
         
        System.out.println(newList);
    }
}
```

   
Q) Write a java progarm to concatinate two list and display in sorting order?  
   
input:  
5 8 9 7 10  
1 4 3 2 6  
   
output:  
1 2 3 4 5 6 7 8 9 10  
   
   

```java
import java.util.*;
import java.util.stream.*;
class Test  
{
    public static void main(String[] args) 
    {
        List<Integer> list1 = List.of(5,8,9,7,10);
        List<Integer> list2 = List.of(1,4,3,2,6);
         
        List<Integer> newList = Stream.concat(list1.stream(),list2.stream()).sorted().toList();
         
        System.out.println(newList);
    }
}
```

   
Q) Write a java program to marge two maps?  
   
input:  
{1=5, 3=10, 4=9, 6=20}  
{2=8, 1=10, 6=9, 7=4}  
   
output:  
{1=15, 2=8, 3=10, 4=9, 6=29, 7=4}  
   

```java
import java.util.*;
import java.util.stream.*;
class Test  
{
    public static void main(String[] args) 
    {
        Map<Integer,Integer> map1 = Map.of(1,5, 3,10, 4,9, 6,20);
        Map<Integer,Integer> map2 = Map.of(2,8, 1,10, 6,9, 7,4);
         
        Map<Integer,Integer> result = new HashMap<>();
         
        result.putAll(map1);
 
        for(Map.Entry<Integer,Integer> entry : map2.entrySet())
        {
            result.merge(entry.getKey(), entry.getValue(),Integer::sum);
        }
         
        System.out.println(result);                
    }
}
```

   
   
Q) Write a java program to convert list of Map ?  
   
Input:  
list = [apple, banana, orange, mango]  
   
Output:  
{apple=1, banana=2, orange=3, mango=4}  
   
   

```java
import java.util.*;
import java.util.stream.*;
class Test  
{
    public static void main(String[] args) 
    {
        List<String> list = List.of("apple", "banana", "orange", "mango");
         
        Map<String,Integer> map = new LinkedHashMap<>();
         
        for(int i=0;i<list.size();i++)
        {
            map.put(list.get(i), i+1);
        }
 
        System.out.print(map);
    }
}
```

   
forEach() method   
================  
The forEach() method introduced in Java 8.  
   
It is used to iterate objects from Collections.  
   
ex:  
---  

```java
import java.util.*;
class Test  
{
    public static void main(String[] args) 
    {
        List<String> list = List.of("apple", "banana", "orange", "mango");
         
        list.forEach(e -> System.out.println(e));                
    }
}
```

   
ex:  
---  

```java
import java.util.*;
class Test  
{
    public static void main(String[] args) 
    {
        Set<Integer> set = Set.of(7,9,1,4,6);
        set.forEach(e -> System.out.println(e));                
    }
}
```

   
ex:  
---  

```java
import java.util.*;
class Test  
{
    public static void main(String[] args) 
    {
        Map<Integer,String> map = Map.of(1,"one",2,"two",3,"three");
        map.forEach((key,value) -> System.out.println(key+"="+value));        
    }
}
```

   
   
Method Reference (::)   
=====================  
Method reference introduced in Java 8.  
   
Method reference is a special type of lamda expression.  
   
It is a concise way to call existing methods.  
   
ex:  
---  

```java
import java.util.*;
class Test  
{
    public static void main(String[] args) 
    {
        List<Integer> list = List.of(7,9,1,3,5);
        list.forEach(System.out::println);
    }
}
```

   
ex:  
--  

```java
import java.util.*;
class Test  
{
    public static void main(String[] args) 
    {
        Map<Integer,String> map = Map.of(1,"one",2,"two",3,"three");
        map.forEach(Test::entry);
    }
     
    public static void entry(Integer key,String value)
    {
        System.out.println(key+"="+value);
    }
}
```

   
Q) When java throws NullPointerException ?  
   
If our code attempts to read object reference which is not initialized then we will get NullPointerException.  
   
ex:  

```java
ArrayList al = null;
System.out.println(al.get(0));
```

   
ex:  

```java
int[] arr = null;
System.out.println(arr[0]);
```

   
ex:  

```java
MyThread t = null;
synchronized(t)
{
}
```

   
   
Optional   
=========  
Optional class introduced in Java 8.  
   
Optional class present in java.util package.  
   
Optional class is used to perform null checks gracefully.  
   
There are three ways to create Optional class object.  
   
ex:  
Optional optional = Optional.empty()  
Optional optional = Optional.of()  
Optional optional = Optional.ofNullable()   
   
ex:  
---  

```java
import java.util.*;
class Test  
{
    public static void main(String[] args) 
    {
        Optional optional = Optional.empty();
        System.out.println(optional);
 
    }
}
```

   
ex:  
---  

```java
import java.util.*;
class Test  
{
    public static void main(String[] args) 
    {
        String str = "raisetech";
        Optional optional = Optional.of(str);
        System.out.println(optional);
 
    }
}
```

   
ex:  
---  

```java
import java.util.*;
class Test  
{
    public static void main(String[] args) 
    {
        String str = null;
        Optional optional = Optional.of(str);
        System.out.println(optional);
 
    }
}
```

   
ex:  
--  

```java
import java.util.*;
class Test  
{
    public static void main(String[] args) 
    {
        String str = "raisetech";
        Optional<String> optional = Optional.ofNullable(str);
        System.out.println(optional.orElse("Value Not Found"));
 
    }
}
```

   
ex:  
---  

```java
import java.util.*;
class Test  
{
    public static void main(String[] args) 
    {
        String str = null;
        Optional<String> optional = Optional.ofNullable(str);
        System.out.println(optional.orElse("Value Not Found"));
 
    }
}
```

   
ex:  
----  

```java
import java.util.*;
class Test  
{
    //instance variable 
    int i = 200;
     
    public static void main(String[] args) 
    {
        Test t = null;
        Optional optional = Optional.ofNullable(t);
        if(!optional.isPresent())
        {
            t = new Test();
        }
        System.out.println(t.i);
    }
}
```

   
Sealed classes   
==============  
   
ex:  
---  
sealed class A permits B    
{  
public void m1()  
{  

```java
        System.out.println("M1-Method");
    }
}
final class B extends A  
{
    public void m2()
    {
        System.out.println("M2-Method");
    }
}
class Test 
{
    public static void main(String[] args)
    {
        B b = new B();
        b.m1();
        b.m2();
    }
}
```

   
ex:  
---  
sealed class A permits B    
{  
public void m1()  
{  

```java
        System.out.println("M1-Method");
    }
}
non-sealed class B extends A  
{
    public void m2()
    {
        System.out.println("M2-Method");
    }
}
class Test 
{
    public static void main(String[] args)
    {
        B b = new B();
        b.m1();
        b.m2();
    }
}
```

   
ex:  
---  
sealed class A permits B    
{  
public void m1()  
{  

```java
        System.out.println("M1-Method");
    }
}
sealed class B extends A  
{
    public void m2()
    {
        System.out.println("M2-Method");
    }
}
final class C extends B 
{
    public void m3()
    {
        System.out.println("M3-Method");
    }
}
class Test 
{
    public static void main(String[] args)
    {
        B b = new B();
        b.m1();
        b.m2();
         
        C c = new C();
        c.m1();
        c.m2();
        c.m3();
    }
}
```
