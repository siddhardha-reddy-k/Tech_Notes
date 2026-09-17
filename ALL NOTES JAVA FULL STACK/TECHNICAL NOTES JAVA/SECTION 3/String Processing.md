# String in Java

A String is a collection of characters enclosed in double quotes.

1. Immutability Strings in Java are immutable. This means once a String object is created, it cannot be modified. If you attempt to change its value, the JVM will not modify the original object; instead, it will create a completely new object to hold the changed value.

## 2. Comparison: == vs .equals()

- == Operator: Used for reference/address comparison. It checks if two variables point to the exact same object in memory. (Example: new String("raise") == new String("raise") returns false because they are two different objects in memory).
- .equals() Method: Used for content comparison. It checks if the actual text inside the objects is exactly the same (it is case-sensitive). (Example: s1.equals(s2) returns true if both contain "raise").

3. Memory Allocation (Heap vs. SCP) When you create a String using the new keyword (e.g., new String("raise")), Java creates two objects:

- One in the Heap area (which your variable reference points to).
- One in the String Constant Pool (SCP) area.

## Rules of the String Constant Pool (SCP):

- No Duplicates: Object creation in the SCP is optional. The JVM first checks if an object with the same content already exists in the SCP. If it does, it reuses it. If not, it creates a new one.
- Garbage Collection: Even if SCP objects lose all their references, the Garbage Collector cannot touch them.
- Lifecycle: SCP objects are only destroyed when the JVM terminates or shuts down completely.

## String Methods

- length(): Gets the character count. Example: "hi".length() outputs 2

- toUpperCase(): Converts to capital letters. Example: "hi".toUpperCase() outputs "HI"
- toLowerCase(): Converts to small letters. Example: "HI".toLowerCase() outputs "hi"
- concat(): Joins two strings together. Example: "a".concat("b") outputs "ab"

- matches(): Checks if the string matches a regex pattern. Example: "12".matches("\\d+") outputs true
- split(): Breaks the string into an array based on a delimiter. Example: "a b".split(" ") outputs ["a", "b"]
- join(): Merges strings or an array with a separator. Example: String.join("-", "a", "b") outputs "a-b"

- equals(): Checks for exact content match (case-sensitive). Example: "a".equals("A") outputs false
- equalsIgnoreCase(): Checks for content match ignoring case. Example: "a".equalsIgnoreCase("A") outputs true

- charAt(): Gets the character at a specific index position. Example: "abc".charAt(1) outputs 'b'
- replaceAll(): Replaces text using a regex pattern. Example: "a1b".replaceAll("\\d", "") outputs "ab"

- trim(): Removes starting and ending spaces. Example: " a ".trim() outputs "a"

- substring(): Extracts a part of the string starting from an index. Example: "abc".substring(1) outputs "bc"
- indexOf(): Finds the first index position of a character or word. Example: "abc".indexOf('b') outputs 1
- toCharArray(): Converts the string into a character array. Example: "ab".toCharArray() outputs ['a', 'b']
- contains(): Checks if a sequence of characters exists inside the string. Example: "abc".contains("b") outputs true

## StringBuffer

Overview: Unlike String (which creates a new object for every change), StringBuffer allows changes to be made within the same object. It is a mutable sequence of characters, heavily recommended when string content changes frequently.

### Key Features:

- Thread Safety: All methods are synchronized. Only one thread can operate on it at a time, making it thread-safe but slower due to thread waiting times.
- Version: Introduced in Java 1.0.
- Capacity Logic:

- Default capacity is 16.
- When max capacity is reached, the new capacity is calculated as: (current_capacity + 1) * 2.

- If initialized with a String, capacity is: string.length() + 16.

### Constructors:

- StringBuffer(): Creates an empty object with a default capacity of 16.
- StringBuffer(int capacity): Creates an empty object with a specified initial capacity.
- StringBuffer(String s): Creates an object pre-filled with the specified string.

### Extracted Methods:

- capacity(): Returns the current allocated memory (capacity) of the buffer.
- append(String/int): Adds the specified data to the end of the current sequence.
- reverse(): Reverses the entire sequence of characters.
- insert(int index, String word): Inserts a word at the specified index position.
- charAt(int index): Returns the character at the specified index.
- length(): Returns the total number of characters currently in the buffer.
- toString(): Converts the StringBuffer object back into a standard, immutable String.
- delete(int index, int Index); sb.delete(1, 3); Hlo for Hello
- replace(int index, int Indexd, String "String"); sb.replace(1, 3, "Java"); HJavalo

## StringBuilder

Overview: StringBuilder is exactly the same as StringBuffer in functionality and methods, but it is designed for single-threaded environments.

### Key Differences from StringBuffer:

- Thread Safety: Methods are not synchronized. Multiple threads can operate on it simultaneously, meaning it is not thread-safe.
- Performance: Because there is no waiting time for threads, its performance is much higher than StringBuffer.
- Version: Introduced later, in Java 1.5.

Methods: It uses the exact same methods as StringBuffer (e.g., reverse(), append(), toString()).

## StringTokenizer

Overview: Present in the java.util package, StringTokenizer is used to break a string into smaller pieces (tokens) based on a specific delimiter (like a space or a comma). Note: This is considered a legacy utility class. For modern Java applications, using the String.split() method is recommended instead.

### Constructor:

- StringTokenizer(String str, String delimiter): Creates a tokenizer for the given string, using the specified delimiter to split it.

### Extracted Methods:

- countTokens(): Returns the total number of tokens (pieces) available.
- hasMoreTokens(): Returns a boolean (true/false) checking if there are any more tokens left to process.
- nextToken(): Returns the next available token as a String.
- hasMoreElements(): Functions identically to hasMoreTokens(), but returns a boolean.
- nextElement(): Functions identically to nextToken(), but returns an Object instead of a String (requires casting, e.g., (String) st.nextElement()).

## Summary of Usage (The Golden Rule)

- String: Use when content is fixed (Immutable).
- StringBuffer: Use when content changes frequently AND thread safety is required (Mutable, Synchronized, Slower).
- StringBuilder: Use when content changes frequently AND thread safety is NOT required (Mutable, Not Synchronized, Faster).
