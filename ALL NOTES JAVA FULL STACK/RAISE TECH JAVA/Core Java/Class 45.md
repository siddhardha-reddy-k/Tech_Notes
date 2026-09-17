   
ex:  
---  

```java
import java.util.*;
class Test  
{
    public static void main(String[] args) 
    {
        LinkedList<String> ll1 = new LinkedList<>();
        ll1.add("one");
        ll1.add("two");
        ll1.add("three");
        System.out.println(ll1);//[one,two,three]
         
        LinkedList<String> ll2 = new LinkedList<>();
        ll2.add("raja");
        System.out.println(ll2); // [raja]
         
        ll2.addAll(ll1);
        System.out.println(ll2); // [raja,one,two,three]
         
        System.out.println(ll2.containsAll(ll1)); // true 
         
        ll2.removeAll(ll1);
        System.out.println(ll2); // [raja]
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
        LinkedList<String> ll = new LinkedList<>();
        ll.add("one");
        ll.add("two");
        ll.add("three");
        System.out.println(ll);//[one,two,three]
         
        ll.addFirst("gogo");
        ll.addLast("jojo");
        System.out.println(ll);//[gogo,one,two,three,jojo]
         
        System.out.println(ll.getFirst()); // gogo 
        System.out.println(ll.getLast()); // jojo
         
        ll.removeFirst();
        ll.removeLast();
        System.out.println(ll);//[one, two, three]
    }
}
```

   
   


   
Q) What is the difference between ArrayList and LinkedList ?   
 
| ArrayList                                                             | LinkedList                                                |
| --------------------------------------------------------------------- | --------------------------------------------------------- |
| The underlying data structure is resizable array or growable array.   | The underlying data structure is doubly LinkedList.       |
| It is best for storing and retrieving the data.                       |  It is best for manipulating the data.                    |
| Memory address for ArrayList elements is contigeous.                  | Memory address for LinkedList elements is not contigeous. |
| When ArrayList is initialized a default capacity 10 is assigned to it | There is no case of default capacity.                     |
   
   
   
Vector   
=======  
The underlying data structure is resizable array or growable array.  
   
Duplicate objects are allowed.  
   
insertion order is preserved.  
   
Hetrogeneous objects are allowed.  
   
Null insertion is possible.  
   
Vector is synchronized. Hence it is thread safe.  
ex:  
---  

```java
import java.util.*;
class Test  
{
    public static void main(String[] args) 
    {
        Vector<Integer> v = new Vector<>();
        System.out.println(v.capacity());//10
         
        for(int i=1;i<=10;i++)
        {
            v.addElement(i);
        }
        System.out.println(v); //[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
         
        System.out.println(v.firstElement());//1
        System.out.println(v.lastElement());//10
         
        v.removeElement(5);
        System.out.println(v);//[1, 2, 3, 4, 6, 7, 8, 9, 10]
         
        v.removeAllElements();
        System.out.println(v); // []
    }
}
```

   
Stack   
=====  
It is a child class of Vector class.  
   
If we depend upon Last In First Out(LIFO) order then we need to use Stack.  
   
constructor  
-----------          

```java
Stack s = new Stack();
```

   
Methods  
-------  
   
1) push(E)   
----------  
It is used to push the element into stack.  
   
2) pop()  
--------  
It is used to pop the element from stack.  
   
3) peek()  
---------  
It is used to return toppest element from stack without removal.  
   
4) isEmpty()  
----------  
It is used to check stack is empty or not.  
   
5) search(E)   
-----------  
It returns offset value if element is found otherwise it returns -1.  
   
ex:  
---  

```java
import java.util.*;
class Test  
{
    public static void main(String[] args) 
    {
        Stack<String> s = new Stack<>();
        s.push("A");
        s.push("B");
        s.push("C"); 
        System.out.println(s); // [A,B,C]
         
        s.pop();
        System.out.println(s);//[A,B]
         
        System.out.println(s.peek());// B 
         
        System.out.println(s.isEmpty()); // false 
         
        System.out.println(s.search("Z")); // -1
         
        System.out.println(s.search("A")); // 2 
    }
}
```

   
   
Q) What is the difference between ArrayList and Vector?  
   
| ArrayList | Vector |
| --- | --- |
| It is a non-legacy class. | It is a legacy class. |
| It is introduced in 1.2 version. | It is introduced in 1.0 version. |
| At a time multiple threads are allowed<br>to operate ArrayList object. Hence<br>it is not thread safe. | At a time only one thread is allowed<br>to operate Vector object. Hence<br>it is thred safe. |
| There is not waiting threads effectively<br>performance is high. | There is a waiting threads effectively<br>performance is low. |
   
   
   
Set   
====  
It is a child interface of Collection interface.  
   
If we want to represent group of individual objects in a single entity where duplicate objects are not allowed and order is not preserved then we need to use Set interface.  
   
Diagram: class45.1  
![[attachments/image31.png]]  
   
   
Set.of()  
=========  
It is introduced in Java 9.  
   
It gives immutable object.  
   
It does not allow duplicates.  
   
It does not accept null values.  
   
ex:  
--  

```java
import java.util.*;
class Test  
{
    public static void main(String[] args) 
    {
        Set<Integer> set = Set.of(7,2,9,1,5);
        System.out.println(set);
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
        Set<Integer> set = Set.of(7,2,9,1,5);
        set.add(100);
        System.out.println(set);
    }
}
```

o/p:  
R.E UnsupportedOperationException  
   
ex:  
---  

```java
import java.util.*;
class Test  
{
    public static void main(String[] args) 
    {
        Set<Integer> set = Set.of(7,2,9,1,5,1,2);
        System.out.println(set);
    }
}
```

o/p:  
R.E : IllegalArgumentException  
   
ex:  
---  

```java
import java.util.*;
class Test  
{
    public static void main(String[] args) 
    {
        Set<Integer> set = Set.of(7,2,9,1,5,null);
        System.out.println(set);
    }
}
```

o/p:  
R.E NullPointerException  
   
   
HashSet  
========  
The underlying data structure is Hashtable. (Instance of HashMap, uses only key parameter, with dummy arguments for values parameter)  
   
Duplicate objects are not allowed.  
   
Insertion order is not preserved.  
   
Hetrogeneous objects are allowed.  
   
Null insertion is possible.  
   
ex:  
---  

```java
import java.util.*;
class Test  
{
    public static void main(String[] args) 
    {
        HashSet hs = new HashSet();
        hs.add("one");
        hs.add("nine");
        hs.add("five");
        hs.add("seven");
        System.out.println(hs); // [nine, one, seven, five]
         
        hs.add("one");
        System.out.println(hs); // [nine, one, seven, five]
         
        hs.add(10);
        System.out.println(hs); // [nine, one, seven, 10, five]
         
        hs.add(null);
        System.out.println(hs); // [null, nine, one, seven, 10, five]
    }
}
```

   
   
Q) What is the difference between HashSet and LinkedHashSet ?  
   
| HashSet | LinkedHashSet |
| --- | --- |
| The underlying data structure is<br>Hashtable. | The underlying data structure is<br>Hashtable and LinkedList. |
| Insertion order is not preserved. | Insertion order is preserved. |
| It is introduced in 1.2 version. | It is introduced in 1.4 version. |
   
ex:  
---  

```java
import java.util.*;
class Test  
{
    public static void main(String[] args) 
    {
        LinkedHashSet lhs = new LinkedHashSet();
        lhs.add("one");
        lhs.add("nine");
        lhs.add("five");
        lhs.add("seven");
        System.out.println(lhs); // [one,nine,five,seven]
         
        lhs.add("one");
        System.out.println(lhs); // [one,nine,five,seven]
         
        lhs.add(10);
        System.out.println(lhs); // [one,nine,five,seven,10]
         
        lhs.add(null);
        System.out.println(lhs); // [one,nine,five,seven,10,null]
    }
}
```

   
TreeSet  
=======  
The underlying data structure Balanced Tree.  
   
Duplicate objects are not allowed.  
   
Insertion order is not preserved because it takes sorting order of an hashcode.  
   
Hetrogenous objects are not allowed otherwise we will ClassCastException.  
   
Null insertion is not possible otherwiser we will get NullPointerException.  
   
ex:  
---  

```java
import java.util.*;
class Test  
{
    public static void main(String[] args) 
    {
        TreeSet ts = new TreeSet();
        ts.add(5);
        ts.add(1);
        ts.add(10);
        ts.add(7);
        System.out.println(ts); // [1, 5, 7, 10]
         
        ts.add(1);
        System.out.println(ts); // [1,5,7,10]
         
        //ts.add("Hi");
        //System.out.println(ts); // R.E ClassCastException
         
        //ts.add(null);
        //System.out.println(ts); // R.E NullPointerException
    }
}
```

   
Interview Question   
==================  
Q) Write a java program to display distinct elements from given array?  
   
input:  
2 7 9 1 2 5 5 3 9  
   
output:  
2 7 9 1 5 3   
   
   

```java
import java.util.*;
class Test  
{
    public static void main(String[] args) 
    {
        int[] arr = {2,7,9,1,2,5,5,3,9};
         
        Set<Integer> set = new LinkedHashSet<>();
         
        for(int i : arr)
        {
            set.add(i);
        }
         
        for(int i : set)
        {
            System.out.print(i+" ");
        }
    }
}
```

   
   
Q) Write a java program to display intersect elements from given list?  
   
Input:  
list1 = HTML JAVA CSS SPRING JAVASCRIPT  
list2 = JAVASCRIPT PYTHON  DJANGO  CSS  HTML  
   
Output:  
HTML CSS JAVASCRIPT   
   
   

```java
import java.util.*;
class Test  
{
    public static void main(String[] args) 
    {
        List<String> list1 = new ArrayList<>();
        list1.add("HTML");
        list1.add("JAVA");
        list1.add("CSS");
        list1.add("SPRING");
        list1.add("JAVASCRIPT");
         
        List<String> list2 = new ArrayList<>();
        list2.add("JAVASCRIPT");
        list2.add("PYTHON");
        list2.add("DJANGO");
        list2.add("CSS");
        list2.add("HTML");
     
        list1.retainAll(list2);
        System.out.println(list1);
    }
}
```

   
   
