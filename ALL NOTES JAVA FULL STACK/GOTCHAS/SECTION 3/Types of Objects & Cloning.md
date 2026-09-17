# Types of Objects in Java

- Immutable Objects: Cannot be changed after creation. If you attempt to modify it, Java automatically creates a completely new object to hold the changes. (Examples: String, Wrapper classes).
- Mutable Objects: Can be changed after creation. Any modifications are applied directly to the original object without creating a new one. (Examples: StringBuffer, StringBuilder).

## Object Cloning

Cloning is the process of creating an exact duplicate of an object. To enable cloning, a class must implement the Cloneable interface (a marker interface that contains no methods or constants) and utilize the clone() method from the Object class.

## Shallow Cloning vs. Deep Cloning

- Shallow Cloning: Creates an exact duplicate of the object reference. Both variables point to the exact same object in memory (meaning they will share the exact same hashCode). (Example: Test t2 = t1;).
- Deep Cloning: Creates an exact duplicate of the actual object. It allocates new memory for the duplicate, resulting in two completely independent objects (meaning they will have different hashCodes). This is achieved using the clone() method.
