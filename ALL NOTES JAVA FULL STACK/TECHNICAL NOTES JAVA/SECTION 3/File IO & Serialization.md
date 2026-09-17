# File Handling (java.io.File)

The File class represents file and directory pathnames. Instantiating a File object does not immediately create a physical file on the disk; it merely checks if the file exists or creates a reference to it.

- exists(): Checks if the file or directory already exists.
- createNewFile(): Creates a new physical file if it does not already exist.
- mkdir(): Creates a new directory.

## Character Streams

## FileWriter & FileReader

These classes communicate directly with physical files to handle character-oriented data.

|   |   |   |   |
|---|---|---|---|
|Class|Purpose|Key Methods|Limitations|
|FileWriter|Writes character data into a file.|write(int), write(char[]), write(String), flush(), close().|Requires manual insertion of line separators (\n).|
|FileReader|Reads character data from a file.|read() (returns unicode value, -1 if end), read(char[]), close().|Reads character by character, which is not convenient.|

## BufferedWriter & BufferedReader

To overcome the limitations of FileWriter and FileReader, these classes provide enhanced reading and writing capabilities. They cannot communicate with files directly and require the support of a Writer or Reader object.

|   |   |   |
|---|---|---|
|Class|Purpose|Key Enhancements|
|BufferedWriter|Enhanced character writing.|Introduces the newLine() method to insert a new line into a file.|
|BufferedReader|Enhanced character reading.|Introduces the readLine() method to read data line-by-line rather than character-by-character.|

## PrintWriter

PrintWriter is an enhanced writer used to write character-oriented data into a file.

- It can communicate directly with a file or take the support of a Writer object.
- The main advantage over FileWriter and BufferedWriter is that it allows inserting any type of data, especially primitive data.
- Provides convenient methods like print() and println() for int, char, String, double, and boolean data types.

## Byte Streams

Byte streams are used to handle data in the form of byte streams.

- FileOutputStream: Used to insert the data in the form of byte of streams.
- FileInputStream: Used to read the data in the form of byte of streams.

## Various Ways to Provide Input in Java

## There are following ways to provide inputs in Java:

- Command Line Argument: Input is captured directly via the String[] args array in the main method.
- BufferedReader Class: Uses new BufferedReader(new InputStreamReader(System.in)) to read input line-by-line.
- Console Class: Uses System.console().readLine() to read input directly from the console.
- Scanner Class: Uses new Scanner(System.in) and provides specific methods like nextInt(), next(), and nextDouble() to parse input types.

## Serialization & Deserialization

## Serialization

- Definition: A process of storing object data into a file, or converting object state to file state.
- Implementation: Requires ObjectOutputStream and FileOutputStream.
- Requirement: We can perform serialization only for serialized objects. To create a serialized object, the class must implement the Serializable marker interface.

## Deserialization

- Definition: A process of taking the data from a file and representing an object, or converting file state to object state.
- Implementation: Requires ObjectInputStream and FileInputStream.
- Requirement: Similar to serialization, it requires the class to implement the Serializable marker interface. It utilizes the readObject() method to reconstruct the object.
