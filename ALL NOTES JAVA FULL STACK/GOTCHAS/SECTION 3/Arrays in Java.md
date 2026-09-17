# Java Arrays Overview

An array is a collection of homogeneous data elements, allowing you to store multiple values in a single variable rather than using separate variables for each value.

## Pros & Cons

- Advantages: Represents multiple elements under one variable name and is highly recommended for performance.
- Disadvantages: Fixed in size (cannot grow or shrink once created) and requires you to know the exact size you need in advance.

Types of Arrays Single Dimensional, Double Dimensional, and Multi-Dimensional.

## Array Lifecycle & Rules

- Declaration: You must not specify the size during declaration. (e.g., int[] arr; or int arr[];).
- Creation: Because arrays are treated as objects in Java, they are created using the new keyword. (e.g., arr = new int[3];).

- Rule 1: You must specify the size during creation.
- Rule 2: An array size of 0 is completely legal.
- Rule 3: Providing a negative size will cause a runtime NegativeArraySizeException.
- Rule 4: The array size must be a byte, short, int, or char. (Decimals cause a Compile Time Error).
- Rule 5: The maximum allowed size is the maximum value of an int (2147483647).

- Initialization: Arrays automatically get default values upon creation. You can override these using the index (e.g., arr[0] = 10;). Accessing an index outside the array size throws an ArrayIndexOutOfBoundsException.
- One-Line Shortcut: You can declare, create, and initialize simultaneously: int[] arr = {10, 20, 30};.

## length vs length()

- length: A predefined final variable used specifically for arrays to return their size (e.g., arr.length).

- length(): A predefined method used specifically for String objects to return the number of characters (e.g., s.length()).

## Jagged Array

- Definition: Also known as an "array of arrays." It is a multi-dimensional array where each row can have a different number of columns (a different column size).
- Structure: Instead of a perfect rectangular grid, the rows are uneven. For example, row 0 might have 4 elements, row 1 might have 2 elements, and row 2 might have 3 elements.
- Iteration: When looping through a jagged array, you must check the specific length of each row dynamically (e.g., using arr[i].length for the inner column loop) to avoid out-of-bounds errors.

## Anonymous Array

- Definition: A nameless array declared without assigning it to a variable.
- Purpose: Used strictly for instant or one-time use. It is highly useful when you need to pass an array directly as an argument to a method without needing to store it for future use.
- Declaration: Created and initialized on the fly using the new keyword and providing the values immediately.

- Single Dimensional Example: new int[]{10, 20, 30};
- Double Dimensional Example: new int[][]{{1, 2}, {3, 4, 5}};
