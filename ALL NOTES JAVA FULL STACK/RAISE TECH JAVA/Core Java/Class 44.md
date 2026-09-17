   
Collection Framework   
====================  
Collection framework defines several classes and interfaces to represent group of objects in a single entity.  
   
ex:  
| Java | C++ |
| --- | --- |
| Collection<br>Collection Framework | Containers<br>STL (Standard Template Library) |
   
   
Collection   
==========  
Collection is an interface which is present in java.util package.  
   
Collection is a root interface for entire Collection Framework.  
   
If we want to represent group of individual objects in a single entity then we need to use Collection interface.  
   
Collection interface contains following methods which are available for entire Collection objects.  
   
ex:  
cmd> javap   java.util.Collection   
   

```java
  public abstract int size();
  public abstract boolean isEmpty();
  public abstract boolean contains(java.lang.Object);
  public abstract java.util.Iterator<E> iterator();
  public abstract java.lang.Object[] toArray();
  public abstract <T> T[] toArray(T[]);
  public default <T> T[] toArray(java.util.function.IntFunction<T[]>);
  public abstract boolean add(E);
  public abstract boolean remove(java.lang.Object);
  public abstract boolean containsAll(java.util.Collection<?>);
  public abstract boolean addAll(java.util.Collection<? extends E>);
  public abstract boolean removeAll(java.util.Collection<?>);
  public default boolean removeIf(java.util.function.Predicate<? super E>);
  public abstract boolean retainAll(java.util.Collection<?>);
  public abstract void clear();
```

  and etc.  
   
   
List   
=====  
It is a child interface of Collection interface.  
   
If we want to represent group of individual objects in a single entity where duplicate objects are allowed and order is preserved then we need to use List interface.  
   
Diagram: class44.1  
![[attachments/image30.png]]  
   
Q) What is the difference between List.of() and Arrays.asList() method?  
   
List.of()  
=========  
It is introduced in Java 9.  
It gives immutable object.  
We can't add, remove and replace the elements.  
It does not allow null value.  
   
ex:  
---  

```java
import java.util.*;
class Test  
{
    public static void main(String[] args) 
    {
        List<Integer> list = List.of(1,6,2,9,4);
         
        for(int i : list)
        {
            System.out.print(i+" ");
        }
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
        List<Integer> list = List.of(1,6,2,9,4);
         
        list.add(10);
         
        for(int i : list)
        {
            System.out.print(i+" ");
        }
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
        List<Integer> list = List.of(1,6,2,9,4);
         
        list.remove(6);
         
        for(int i : list)
        {
            System.out.print(i+" ");
        }
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
        List<Integer> list = List.of(1,6,2,9,4);
         
        list.set(1,100);
         
        for(int i : list)
        {
            System.out.print(i+" ");
        }
    }
}
```

   
o/p:  
R.E UnsupportedOperationException  
   
ex:  
----  

```java
import java.util.*;
class Test  
{
    public static void main(String[] args) 
    {
        List<Integer> list = List.of(1,6,2,9,4,null);
        System.out.println(list);
    }
}
```

   
o/p:  
R.E NullPointerException  
   
   
Arrays.asList()  
===============  
It is introduced in 1.2 version.  
It gives mutable object.  
We can't add, remove but we can replace the elements.  
It supports null value.  
   
ex:  
---  

```java
import java.util.*;
class Test  
{
    public static void main(String[] args) 
    {
        List<Integer> list = Arrays.asList(7,2,9,1,5);
        for(int i : list)
        {
            System.out.print(i+" ");
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
        List<Integer> list = Arrays.asList(7,2,9,1,5);
        list.add(100);
        for(int i : list)
        {
            System.out.print(i+" ");
        }
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
        List<Integer> list = Arrays.asList(7,2,9,1,5);
        list.remove(2);
        for(int i : list)
        {
            System.out.print(i+" ");
        }
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
        List<Integer> list = Arrays.asList(7,2,9,1,5);
        list.set(1,100);
        for(int i : list)
        {
            System.out.print(i+" ");
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
        List<Integer> list = Arrays.asList(7,2,9,1,5,null);
        System.out.print(list);
    }
}
```

   
   
Q) Write a java program to sort the list?  
   
input:  
5 9 1 2 7   
   
output:  
1 2 5 7 9   
   
   

```java
import java.util.*;
class Test  
{
    public static void main(String[] args) 
    {
        List<Integer> list = Arrays.asList(5,9,1,2,7);
         
        Collections.sort(list);
         
        System.out.println(list);
    }
}
```

   
Q) Write a java program to make our list as synchronized(thread safe)?  
   
   

```java
import java.util.*;
class Test  
{
    public static void main(String[] args) 
    {
        //Non-synchronized list
        // Not thread safe.
        List<Integer> list = List.of(5,9,1,2,7);
         
        //converting to synchronized list
        // thread safe
        List<Integer> newList = Collections.synchronizedList(list);
         
        System.out.println(newList);
         
    }
}
```

   
Q) Write a java program to reverse the list?  
   
input:  
this is java class   
   
output:  
class java is this   
   
   

```java
import java.util.*;
class Test  
{
    public static void main(String[] args) 
    {
        List<String> list = Arrays.asList("this","is","java","class");
         
        Collections.reverse(list);
         
        System.out.println(list);
         
    }
}
```

   
   
ArrayList   
=========  
The underlying data structure is resizable array or growable array.  
   
Duplicate objects are allowed.  
   
Insertion order is preserved.  
   
Hetrogeneous objects are allowed.  
   
Null insertion is possible.  
   
It implements List, Serializable, Cloneable and RandomAccess inteface.  
   
ex:  
---  

```java
import java.util.*;
class Test  
{
    public static void main(String[] args) 
    {
        ArrayList al = new ArrayList();
        al.add("one");
        al.add("two");
        al.add("three");
        System.out.println(al); // [one, two, three]
         
        al.add("one");
        System.out.println(al); // [one,two,three,one]
         
        al.add(10);
        System.out.println(al); // [one,two,three,one,10]
         
        al.add(null);
        System.out.println(al); // [one,two,three,one,10,null]
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
        ArrayList<String> al = new ArrayList<>();
        al.add("one");
        al.add("two");
        al.add("three");
        System.out.println(al); // [one, two, three]
         
        al.add("one");
        System.out.println(al); // [one,two,three,one]
         
        al.add(null);
        System.out.println(al); // [one,two,three,one,null]
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
        ArrayList<String> al = new ArrayList<>();
        al.add("one");
        al.add("two");
        al.add("three");
        System.out.println(al); // [one, two, three]
         
        al.remove(1);
        System.out.println(al); // [one,three]
         
        al.clear();
        System.out.println(al); // []
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
        ArrayList<String> al = new ArrayList<>();
        al.add("one");
        al.add("two");
        al.add("three");
     
        for(int i=0;i<al.size();i++)
        {
            String s = al.get(i);
            System.out.println(s);
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
        List<Integer> list= new ArrayList<>();
        list.add(10);
        list.add(20);
        list.add(30);
         
        System.out.println(list.isEmpty()); // false 
         
        System.out.println(list.indexOf(20)); // 1 
         
        System.out.println(list.contains(10)); // true 
    }
}
```

   
LinkedList   
=========  
The underlying data structure is doubly LinkedList.  
   
Duplicates are allowed.  
   
Insertion order is preserved.  
   
Hetrogeneous objects are allowed.  
   
Null insertion is possible.  
   
It implements List, Serializable, Cloneable and Deque interface.  
   
ex:  
---  

```java
import java.util.*;
class Test  
{
    public static void main(String[] args) 
    {
        LinkedList ll = new LinkedList();
        ll.add("one");
        ll.add("two");
        ll.add("three");
        System.out.println(ll); //[one,two,three]
         
        ll.add("one");
        System.out.println(ll); //[one,two,three,one]
         
        ll.add(10);
        System.out.println(ll); // [one,two,three,one,10]
         
        ll.add(null);
        System.out.println(ll); // [one,two,three,one,10,null]
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
        System.out.println(ll); //[one,two,three]
         
        ll.add("one");
        System.out.println(ll); //[one,two,three,one]
     
        ll.add(null);
        System.out.println(ll); // [one,two,three,one,null]
    }
}
```

   
   
