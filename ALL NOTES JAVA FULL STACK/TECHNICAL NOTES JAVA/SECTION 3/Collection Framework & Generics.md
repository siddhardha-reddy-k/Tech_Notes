# Generics

- Arrays are typesafe. It means we can give guarantee that what type of elements are present in arrays.
- Collections are not typesafe. It means we can't provide guarantee that what type of elements are present in Collections.
- To overcome above limitations Sun Micro System introduced Generics concept in 1.5 version.
- The main objective of Generics is:

1. To make make Collections as typesafe.
2. To avoid typecasting problem.

java.util package: Arrays vs Collections

|   |   |
|---|---|
|Arrays|Collections|
|It is a collection of homogeneous data elements.|It is a collection of homogeneous and hetrogeneous data elements.|
|It is fixed in size.|It is growable in nature.|
|Performance point of view arrays are recommanded to use.|Memory point of view Collections are recommanded to use.|
|Arrays are not implemented based on data structure concept. So we can't expect any ready made method.|Collections are implemented based on data structure concept. So we can expect readymade methods.|
|It can hold primitive types and object types.|It can hold only object types.|
|It is typesafe.|It is not typesafe.|

## Collection Framework

- Collection framework defines several classes and interfaces to represent group of objects in a single entity.

## Collection Interface

- Collection is an interface which is present in java.util package.
- Collection is a root interface for entire Collection Framework.
- If we want to represent group of individual objects in a single entity then we need to use Collection interface.

## List Interface

- It is a child interface of Collection interface.
- If we want to represent group of individual objects in a single entity where duplicate objects are allowed and order is preserved then we need to use List interface.

## List.of() vs Arrays.asList()

|   |   |
|---|---|
|List.of()|Arrays.asList()|
|It is introduced in Java 9.|It is introduced in 1.2 version.|
|It gives immutable object.|It gives mutable object.|
|We can't add, remove and replace the elements.|We can't add, remove but we can replace the elements.|
|It does not allow null value.|It supports null value.|

## List Implementations

## ArrayList

- The underlying data structure is resizable array or growable array.
- Duplicate objects are allowed.
- Insertion order is preserved.
- Hetrogeneous objects are allowed.
- Null insertion is possible.
- It implements List, Serializable, Cloneable and RandomAccess inteface.

## LinkedList

- The underlying data structure is doubly LinkedList.
- Duplicates are allowed.
- Insertion order is preserved.
- Hetrogeneous objects are allowed.
- Null insertion is possible.
- It implements List, Serializable, Cloneable and Deque interface.

## ArrayList vs LinkedList

|   |   |
|---|---|
|ArrayList|LinkedList|
|The underlying data structure is resizable array or growable array.|The underlying data structure is doubly LinkedList.|
|It is best for storing and retrieving the data.|It is best for manipulating the data.|
|Memory address for ArrayList elements is contigeous.|Memory address for LinkedList elements is not contigeous.|
|When ArrayList is initialized a default capacity 10 is assigned to it.|There is no case of default capacity.|

## Vector

- The underlying data structure is resizable array or growable array.
- Duplicate objects are allowed.
- insertion order is preserved.
- Hetrogeneous objects are allowed.
- Null insertion is possible.
- Vector is synchronized. Hence it is thread safe.

## ArrayList vs Vector

|   |   |
|---|---|
|ArrayList|Vector|
|It is a non-legacy class.|It is a legacy class.|
|It is introduced in 1.2 version.|It is introduced in 1.0 version.|
|At a time multiple threads are allowed to operate ArrayList object. Hence it is not thread safe.|At a time only one thread is allowed to operate Vector object. Hence it is thred safe.|
|There is not waiting threads effectively performance is high.|There is a waiting threads effectively performance is low.|

## Stack

- It is a child class of Vector class.
- If we depend upon Last In First Out(LIFO) order then we need to use Stack.

## Set Interface

- It is a child interface of Collection interface.
- If we want to represent group of individual objects in a single entity where duplicate objects are not allowed and order is not preserved then we need to use Set interface.

## Set.of()

- It is introduced in Java 9.
- It gives immutable object.
- It does not allow duplicates.
- It does not accept null values.

## Set Implementations

## HashSet

- The underlying data structure is Hashtable.
- Duplicate objects are not allowed.
- Insertion order is not preserved.
- Hetrogeneous objects are allowed.
- Null insertion is possible.

## HashSet vs LinkedHashSet

|   |   |
|---|---|
|HashSet|LinkedHashSet|
|The underlying data structure is Hashtable.|The underlying data structure is Hashtable and LinkedList.|
|Insertion order is not preserved.|Insertion order is preserved.|
|It is introduced in 1.2 version.|It is introduced in 1.4 version.|

## TreeSet

- The underlying data structure Balanced Tree.
- Duplicate objects are not allowed.
- Insertion order is not preserved because it takes sorting order of an hashcode.
- Hetrogenous objects are not allowed otherwise we will ClassCastException.
- Null insertion is not possible otherwiser we will get NullPointerException.

## Comparable vs Comparator

|   |   |
|---|---|
|Comparable|Comparator|
|Comparable is an interface which is present in java.lang package.|Comparator is an interface which is present in java.util package.|
|Comparable interface contains only one method i.e compareTo() method.|Comparator interface contains following two methods i.e compare() and equals() method.|
|If we depend upon default natural sorting order then we need to use Comparable interface.|If we depend upon customized sorting order then we need to use Comparator interface.|

## Map Interface

- It is not a child interface of Collection interface.
- If we want to represent group of individual objects in key and value pair then we need to use Map interface.
- key and value both must be objects.
- Key can't be duplicate but value can be duplicate.
- Each key and value pair is called one-entry.

## Map.of()

- It is introduced in java 9.
- It gives immutable objects.
- key and value can't be null.

## Map Implementations

## HashMap

- The underlying data structure is Hashtable.
- Key can't be duplicate but value can be duplicate.
- Insertion order is not preserved because it takes hashcode of the key.
- Key and value both can be hetrogeneous.
- Key and value both can be null.

## HashMap vs LinkedHashMap

|   |   |
|---|---|
|HashMap|LinkedHashMap|
|The underlying data structure is Hashtable.|The underlying data structure is Hashtable and LinkedList.|
|Insertion is not preserved.|Insertion order is preserved.|
|It is introduced in 1.2 version.|It is introduced in 1.4 version.|

## TreeMap

- The underlying data structure is Red Black Tree.
- Key can't be duplicate but value can be duplicate.
- If we depend upon default natural sorting order then keys must be homogeneous and comparable.
- If we depend upon customized sorting order then keys must be hetrogeneous and non-comparable.
- Key can't be null but value can be null.

## Hashtable

- The underlying data structure is Hashtable.
- Key can't be duplicate but value can be duplicate.
- Insertion order is descending order of the key.
- Key and value both can be hetrogeneous.
- Key and value both can't be null.

Cursors are used to read objects one by one from Collections. There are three types of cursors in Java:

## 1) Enumeration

- Definition: It is used to read objects one by one from legacy Collection objects.
- Methods (2):

- public boolean hasMoreElements()
- public Object nextElement()

- Limitations:

- It is not a universal cursor (only works with legacy collections like Vector).
- Using Enumeration, we can perform read operations but not remove operations.

## 2) Iterator

- Definition: It is used to read objects one by one from any Collection object. Hence, it is a universal cursor.
- Methods (3):

- public boolean hasNext()
- public Object next()
- public void remove()

- Limitations:

- Enumeration and Iterator are used to read objects in the forward direction but not in the backward direction (they are not bi-directional cursors).
- Using Iterator, we can perform read and remove operations, but not adding and replacement of new objects.

## 3) ListIterator

- Definition: 5ListIterator is a child interface of Iterator. It is used to read objects one by one exclusively from List Collection objects.
- Capabilities: It overcomes Iterator's limitations by allowing bi-directional movement. Using ListIterator we can perform read, remove, adding, and replacement of new objects.
- Methods (9):

- Forward: hasNext(), next(), nextIndex()
- Backward: hasPrevious(), previous(), previousIndex()
- Operations: remove(), add(E), set€

## Technical Round Quick Comparison

|   |   |   |   |
|---|---|---|---|
|Feature|Enumeration|Iterator|ListIterator|
|Applicable to|Legacy Collections only|Any Collection (Universal)|List Collections only|
|Direction|Forward only|Forward only|Bi-directional (Forward & Backward)|
|Operations Allowed|Read|Read, Remove|Read, Remove, Add, Replace (Set)|
|Creation|v.elements()|c.iterator()|l.listIterator()|
