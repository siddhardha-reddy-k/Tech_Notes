   
Arrays  
======  
In a normal variable we can store only one value at a time.  
   
To store more mote than one value in a single variable we need to use arrays.  
   
Array is a collection of homogeneous data elements.  
   
The main advantages of arrays are   
   
1) We can represent multiple elements using single variable name.  
   ex:  

```java
int[] arr={10,20,30};
```

   
2) Performance point of view arrays are recommanded to use.   
   
The main disadvantages of arrays are   
   
1) Arrays are fixed in size. Once if we create an array there is no chance of   
   increasing or decreasing the size of an array.  
   
2) To use array concept in advanced we should know what is the size of an array   
   which is always not possible.  
   
In java, arrays are classified into three types.  
   
1) Single Dimensional Array   
   
2) Double Dimensional Array   
   
3) Multi-Dimensional Array   
   
Array Declaration   
-----------------  
At the time of array declaration we should not specify array size.  
ex:  
            Array  
|-----------------------------------|-------------------------|  
Single Dimensional Array        Double Dimensional Array        Multi-Dimensional Array  
   
int[] arr;                        int[][] arr;                        int[][][] arr;  
int []arr;                        int [][]arr;                        int [][][]arr;  
int arr[];                        int arr[][];                        int arr[][][];  
int[] []arr;                        int[][] []arr;  
int[] arr[];                        int[][] arr[];  
int []arr[];                        int[] [][]arr;  
int[] arr[][];  
int[] []arr[];  
int [][]arr[];  
int []arr[][];  
   
Array Creation   
--------------  
In java, every array consider as an object.Hence we will use new keyword to create an array.  
ex:  

```java
int[] arr = new int[3];
```

   
Rules to constructor an array   
----------------------------  
Rule1:  
-----  
At the time of array creation compulsary we need to specify array size.  
ex:  

```java
int[] arr = new int[3];
```

int[] arr = new int[]; // C.T.e Array dimension missing   
   
Rule2:  
------  
It is legal to have an array size with zero.  
ex:  

```java
int[] arr = new int[0];
System.out.println(arr.length);
```

   
Rule3:  
-----  
We can't take negative number as an array size otherwise we will get   
runtime exception called NegativeArraySizeException.  
ex:  

```java
int[] arr = new int[-3];
```

   
Rule4:  
------  
The allowed datatype for an array size is byte,short,int and char.  
If we take other datatypes then we will get compile time erorr.  
ex:  

```java
byte b = 10;
int[] arr = new int[b];
```

   

```java
int[] arr = new int['a'];
```

   

```java
int[] arr = new int[10.5d];
```

   
   
Rule5:  
-----          
The maximum length we can take for an array size is maximum length of int.  
ex:  

```java
int[] arr = new int[2147483647];
```

   
Array initialization   
--------------------  
Once if we create an array , every array element is initialized with default values.  
   
If we are not happy with default values then we can change with customized values.  
   
ex:  

```java
int[] arr = new int[3];
arr[0] = 10;
arr[1] = 20;
arr[2] = 30;
```

arr[3] = 40; // R.E ArrayIndexOutOfBoundsException  
   
Diagram: class26.1  
![[attachments/image14.png]]  
   
Array declaration, creation and intialization using single line   
---------------------------------------------------------------  
   
int[] arr;  

```java
arr = new int[3];
arr[0]=10;
arr[1]=20;
arr[2]=30;        ==> int[] arr = {10,20,30};        
```

==> char[] arr = {'a','b','c'};  
==> String[] arr = {"Hi","Hello","Bye"};  
   
   
   
Q) What is the difference between length and length() ?   
   
length   
------  
It is a final variable which is applicable for arrays.  
It returns size of an array.  
ex:  

```java
int[] arr = new int[3];
System.out.println(arr.length);
```

   
length()  
--------  
It is a predefined method which is applicable for String objects.  
It returns number of characters present in string.  
ex:  

```java
String s = "hello";
```

System.out.println(s.length());//5    
   
   
Single Dimensional Array Programs   
=================================  
   
Q) Write a java program to accept array elements and display them?  
   

```java
import java.util.Scanner;
class Test  
{
    public static void main(String[] args) 
    {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter the array size :");
        int size = sc.nextInt(); // 3
         
        int[] arr = new int[size];
         
        //inserting elements
        for(int i=0;i<arr.length;i++)
        {
            System.out.println("Enter the element :");
            arr[i] = sc.nextInt();
        }
         
        //printing elements 
        for(int i=0;i<arr.length;i++)
        {
            System.out.print(arr[i]+" ");
        }
    }
}
```

   
Q) Write a java program to display array elements from given array?  
   
ex:  
4 9 1 3 7 2   
   

```java
class Test  
{
    public static void main(String[] args) 
    {
        int[] arr = {4,9,1,3,7,2};
         
        for(int i=0;i<arr.length;i++)
        {
            System.out.print(arr[i]+" ");
        }
    }
}
```

   
Approach2  
---------  

```java
class Test  
{
    public static void main(String[] args) 
    {
        int[] arr = {4,9,1,3,7,2};
         
        //for each loop
        for(int i : arr)
        {
            System.out.print(i+" ");
        }
    }
}
```

   
   
   
   
   
   
   
Q) Write a java program to display array elements in reverse order?  
   
Input  
4 9 1 3 7 2   
   
Output:  
2 7 3 1 9 4   
   
   

```java
class Test  
{
    public static void main(String[] args) 
    {
        int[] arr = {4,9,1,3,7,2};
         
        for(int i=arr.length-1;i>=0;i--)
        {
            System.out.print(arr[i]+" ");
        }
    }
}
```

   
Q) Write a java program to display sum of array elements?  
   
Input:  
4 9 1 3 7 2   
   
Output:  
26  
   

```java
class Test  
{
    public static void main(String[] args) 
    {
        int[] arr = {4,9,1,3,7,2};
         
        int sum = 0;
         
        for(int i : arr)
        {
            sum += i;
        }
         
        System.out.println(sum);
    }
}
```

   
   
   
Q) Write a java program to copy array elements?  
   
Input:  
4 9 1 3 7 2   
   
   

```java
class Test  
{
    public static void main(String[] args) 
    {
        int[] arr = {4,9,1,3,7,2};
         
        int[] newArr = new int[arr.length];
         
        newArr = arr;
         
        for(int i : newArr)
        {
            System.out.print(i+" ");
        }
    }
}
```

   
Q) Write a java program to display even elements from given array?  
   
Input:  
4 9 1 3 7 2   
Output:  
4 2   
   

```java
class Test  
{
    public static void main(String[] args) 
    {
        int[] arr = {4,9,1,3,7,2};
         
        for(int n : arr)
        {
            if(n%2==0)
            {
                System.out.print(n+" ");
            }
        }
    }
}
```

   
Q) Write a java program to display prime elements from given array?  
   
input:  
9 2 6 5 12 7   
   
output:  
2 5 7   
   

```java
class Test  
{
    public static void main(String[] args) 
    {
        int[] arr = {9,2,6,5,12,7};
         
        for(int n : arr)
        {
            boolean flag = true;
            for(int i=2;i<=n/2;i++)
            {
                if(n%i==0)
                {
                    flag = false;
                    break;
                }
            }
            if(flag==true)
                System.out.print(n+" ");
        }
    }
}
```

   
Assignment  
==========  
Q) Write a java program to display array elements in sorting order?  
   
input:  
5 1 9 2 7 4  
output:  
1 2 4 5 7 9   
   
   
