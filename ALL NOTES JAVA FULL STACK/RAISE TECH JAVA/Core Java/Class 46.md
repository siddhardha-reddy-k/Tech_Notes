   
Q) What is the difference between Comparable and Comparator interface?  
   
Comparable   
-----------  
Comparable is an interface which is present in java.lang package.  
   
Comparable interface contains only one method i.e compareTo() method.  
   
If we depend upon default natural sorting order then we need to use Comparable interface.  
   
ex:  
obj1.compareTo(obj2)  
   
It returns -ve if obj1 comes before obj2.  
It returns +ve if obj1 comes after obj2.  
It returns 0 if both objects are same.  
   
ex:  
---  

```java
class Test  
{
    public static void main(String[] args) 
    {
        System.out.println("A".compareTo("Z")); // -25
        System.out.println("Z".compareTo("A")); // 25
        System.out.println("K".compareTo("K")); // 0 
    }
}
```

   
   
   
Comparator   
----------  
Comparator is an interface which is present in java.util package.  
   
Comparator interface contains following two methods i.e compare() and equals() method.  
   
If we depend upon customized sorting order then we need to use Comparator interface.  
   
Implementation of compare() method is mandatory.  
ex:  
public int compare(Object obj1,Object obj2)  
   
It returns +ve if obj1 comes before obj2.  
It returns -ve if obj1 comes after obj2.  
It returns 0 if both objects are same.  
   
But implementation of equals() method is optional because it is available to the class through inheritance.  
   
ex:  
---  

```java
import java.util.*;
class Test  
{
    public static void main(String[] args) 
    {
        TreeSet<Integer> ts = new TreeSet<>(new MyComparator());
        ts.add(5);
        ts.add(1);
        ts.add(10);
        System.out.println(ts);//[10,5,1]
    }
}
class MyComparator implements Comparator 
{
    public int compare(Object obj1,Object obj2)
    {
        Integer i1 = (Integer)obj1;
        Integer i2 = (Integer)obj2;
 
        if(i1<i2)
            return 1;
        else if(i1>i2)
            return -1;
        else 
            return 0;
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
        TreeSet<Integer> ts = new TreeSet<>(new MyComparator());
        ts.add(5);
        ts.add(1);
        ts.add(10);
        System.out.println(ts);//[1,5,10]
    }
}
class MyComparator implements Comparator 
{
    public int compare(Object obj1,Object obj2)
    {
        Integer i1 = (Integer)obj1;
        Integer i2 = (Integer)obj2;
 
        if(i1<i2)
            return -1;
        else if(i1>i2)
            return 1;
        else 
            return 0;
    }
}
```

   
Q) Write a java program to compare two dates?  
   

```java
import java.time.*;
class Test  
{
    public static void main(String[] args) 
    {
        LocalDate date1 = LocalDate.now();
        LocalDate date2 = LocalDate.of(2026,1,26);
         
        if(date1.compareTo(date2)<0)
            System.out.println("date2 is greatest");
        else if(date1.compareTo(date2)>0)
            System.out.println("date1 is greatest");
        else
            System.out.println("Both are same");
    }
}
```

   
   
Map   
====  
It is not a child interface of Collection interface.  
   
If we want to represent group of individual objects in key and value pair then we need to use Map interface.  
   
key and value both must be objects.  
   
Key can't be duplicate but value can be duplicate.  
   
Each key and value pair is called one-entry.  
   
Diagram: class46.1  
![[attachments/image32.png]]  
   
Map.of()  
========  
It is introduced in java 9.  
It gives immutable objects.  
key and value can't be null.  
   
ex:  
---  

```java
import java.util.*;
class Test  
{
    public static void main(String[] args) 
    {
        Map<Integer,String> map = Map.of(1,"one",6,"six",9,"nine",4,"four");
        System.out.println(map);
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
        Map<Integer,String> map = Map.of(1,"one",6,"six",9,"nine",4,"four");
         
        for(Map.Entry<Integer,String> entry : map.entrySet())
        {
            System.out.println(entry.getKey()+"="+entry.getValue());
        }
         
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
        Map<Integer,String> map = Map.of(1,"one",6,"six",9,"nine",4,"four");
         
        map.put(9,"nine");
         
        for(Map.Entry<Integer,String> entry : map.entrySet())
        {
            System.out.println(entry.getKey()+"="+entry.getValue());
        }
         
    }
}
```

o/p:  
R.E UnsupportedOperationException  
   
ex:  
--  

```java
import java.util.*;
class Test  
{
    public static void main(String[] args) 
    {
        Map<Integer,String> map = Map.of(1,"one",6,"six",9,"nine",4,"four",null,null);
         
        for(Map.Entry<Integer,String> entry : map.entrySet())
        {
            System.out.println(entry.getKey()+"="+entry.getValue());
        }
         
    }
}
```

o/p:  
R.E NullPointerException   
   
   
   
   
HashMap  
=======  
The underlying data structure is Hashtable.  
   
Key can't be duplicate but value can be duplicate.  
   
Insertion order is not preserved because it takes hashcode of the key.  
   
Key and value both can be hetrogeneous.  
   
Key and value both can be null.  
   
ex:  
---  

```java
import java.util.*;
class Test  
{
    public static void main(String[] args) 
    {
        HashMap hm = new HashMap();
        hm.put(1,"one");
        hm.put(9,"nine");
        hm.put(5,"five");
        hm.put(7,"seven");
        System.out.println(hm);// {1=one, 5=five, 7=seven, 9=nine}
         
        hm.put(1,"gogo");
        System.out.println(hm);// {1=gogo, 5=five, 7=seven, 9=nine}
         
        hm.put("six",6);
        System.out.println(hm);//{1=gogo, six=6, 5=five, 7=seven, 9=nine}
         
        hm.put(null,null);
        System.out.println(hm);//{null=null, 1=gogo, six=6, 5=five, 7=seven, 9=nine}
         
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
        HashMap hm = new HashMap();
        hm.put(1,"one");
        hm.put(9,"nine");
        hm.put(5,"five");
        hm.put(7,"seven");
         
        Set s = hm.keySet();
        System.out.println(s); // [1, 5, 7, 9]
         
        Collection c = hm.values();
        System.out.println(c); // [one, five, seven, nine]
         
        Set s1 = hm.entrySet();
        System.out.println(s1);//[1=one, 5=five, 7=seven, 9=nine]
    }
}
```

   
   
   
   
   
LinkedHashMap   
=============  
It is a child class of HashMap class.  
LinkedHashMap exactly same as HashMap class with following differences.  
   
| HashMap | LinkedHashMap |
| --- | --- |
| The underlying data structure is<br>Hashtable. | The underlying data structure is<br>Hashtable and LinkedList. |
| Insertion is not preserved. | Insertion order is preserved. |
| It is introduced in 1.2 version. | It is introduced in 1.4 version. |
   
ex:  
---  

```java
import java.util.*;
class Test  
{
    public static void main(String[] args) 
    {
        LinkedHashMap lhm = new LinkedHashMap();
        lhm.put(1,"one");
        lhm.put(9,"nine");
        lhm.put(5,"five");
        lhm.put(7,"seven");
        System.out.println(lhm);// {1=one,9=nine,5=five,7=seven}
         
        lhm.put(1,"gogo");
        System.out.println(lhm);// {1=gogo,9=nine,5=five,7=seven}
         
        lhm.put("six",6);
        System.out.println(lhm);//{1=gogo,9=nine,5=five,7=seven,six=6}
         
        lhm.put(null,null);
        System.out.println(lhm);//{1=gogo,9=nine,5=five,7=seven,six=6,null=null}
         
    }
}
```

   
TreeMap   
========  
The underlying data structure is Red Black Tree.  
   
Key can't be duplicate but value can be duplicate.  
   
If we depend upon default natural sorting order then keys must be homogeneous and comparable.  
   
If we depend upon customized sorting order then keys must be hetrogeneous and non-comparable.  
   
Key can't be null but value can be null.  
   
ex:  
--  

```java
import java.util.*;
class Test  
{
    public static void main(String[] args) 
    {
        TreeMap<Integer,String> tm = new TreeMap<>();
        tm.put(5,"five");
        tm.put(1,"one");
        tm.put(10,"ten");
        System.out.println(tm); //{1=one, 5=five, 10=ten}
         
        tm.put(1,"gogo");
        System.out.println(tm); //{1=gogo, 5=five, 10=ten}
         
        tm.put(6,null);
        System.out.println(tm); //{1=gogo, 5=five, 6=null, 10=ten}
         
        tm.put(null,"four");
        System.out.println(tm); // R.E NullPointerException
    }
}
```

   
   
Hashtable   
===========  
The underlying data structure is Hashtable.  
   
Key can't be duplicate but value can be duplicate.  
   
Insertion order is descending order of the key.  
   
Key and value both can be hetrogeneous.  
   
Key and value both can't be null.  
   
ex:  
---  

```java
import java.util.*;
class Test  
{
    public static void main(String[] args) 
    {
        Hashtable ht =new Hashtable();
        ht.put("one",1);
        ht.put("ten",10);
        ht.put("five",5);
        System.out.println(ht);//{ten=10, five=5, one=1}
         
        ht.put("one",100);
        System.out.println(ht);//{ten=10, five=5, one=100}
         
        ht.put(6,"six");
        System.out.println(ht);//{ten=10, five=5, 6=six, one=100}
         
        ht.put(null,null);
        System.out.println(ht);// R.E NullPointerException
    }
}
```

   
   
   
Q) Write a java program to display number of occurance of a given string?  
   
input:  
this is is java java class  
   
output:  
this=1  is=2  java=2  class=1  
   
   

```java
import java.util.*;
class Test  
{
    public static void main(String[] args) 
    {
        String str = "this is is java java class";
        String[] sarr = str.split(" ");
        Map<String,Integer> map = new LinkedHashMap<>();
        for(String s : sarr)
        {
            if(map.containsKey(s))
            {
                map.put(s,map.get(s)+1);
            }
            else
            {
                map.put(s,1);
            }
        }
        for(Map.Entry<String,Integer> entry : map.entrySet())
        {
            System.out.print(entry.getKey()+"="+entry.getValue()+" ");
        }
    }
}
```

   
   
Q) Write a java program to display number of occurance of character ?  
   
input:  
java  
   
output:  
j=1 a=2 v=1  
   
   
   

```java
import java.util.*;
class Test  
{
    public static void main(String[] args) 
    {
        String str = "java";
        char[] carr = str.toCharArray();
        Map<Character,Integer> map = new LinkedHashMap<>();
        for(char ch : carr)
        {
            if(map.containsKey(ch))
            {
                map.put(ch,map.get(ch)+1);
            }
            else
            {
                map.put(ch,1);
            }
        }
        for(Map.Entry<Character,Integer> entry : map.entrySet())
        {
            System.out.print(entry.getKey()+"="+entry.getValue()+" ");
        }
    }
}
```

   
   
   
   
