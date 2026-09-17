   
Double Dimensional Array   
========================  
Double dimensional is a combination of rows and columns.  
   
Double dimensional array is implemented based on array of arrays approach but not matrix form.  
   
The main objective of double dimensional array is memory utilization.  
   
Double dimensional array is used to develop business oriented applications, gaming applications, matrix type of applications.  
   
We can declare and create double dimensional array as follow.  
   
ex:                                  
    rows columns   
      |  |  
int[][] arr = new int[3][3];  
   
Here we can store 9 elements.  
   
We can initialize double dimensional array as follow.  
ex:  
int[][] arr = {{1,2,3},{4,5,6},{7,8,9}};  
   
   
Q) Write a java program to display array elements in matrix form?  
   

```java
import java.util.Scanner;
class Test  
{
    public static void main(String[] args) 
    {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter the rows :");
        int rows = sc.nextInt(); //3
        System.out.println("Enter the columns :");
        int cols = sc.nextInt(); //3
         
        int[][] arr = new int[rows][cols];
         
        //insert elements 
        for(int i=0;i<rows;i++)
        {
            for(int j=0;j<cols;j++)
            {
                System.out.println("Enter the element :");
                arr[i][j] = sc.nextInt();
            }
        }
         
        //display elements  
        for(int i=0;i<rows;i++)
        {
            for(int j=0;j<cols;j++)
            {
                System.out.print(arr[i][j]+" ");
            }
            //new line 
            System.out.println();
        }
    }
}
```

   
   
Q) Write a java program to display array elements from double dimensional array?  
   
Input:  
1 2 3   
4 5 6   
7 8 9   
   
   

```java
class Test  
{
    public static void main(String[] args) 
    {
        int[][] matrix = {{1,2,3},{4,5,6},{7,8,9}};        
         
        for(int[] arr : matrix)
        {
            for(int i : arr)
            {
                System.out.print(i+" ");
            }
            //new line 
            System.out.println();
        }
    }
}
```

   
   
Q) Write a java program to perform sum of diagonal elements ?  
   
Input:  
1 2 3   
4 5 6   
7 8 9   
Output:  
15  
   
   

```java
class Test  
{
    public static void main(String[] args) 
    {
        int[][] matrix = {{1,2,3},{4,5,6},{7,8,9}};        
         
        int rows = matrix.length;
        int cols = matrix[0].length;
         
        int sum = 0;
        for(int i=0;i<rows;i++)
        {
            for(int j=0;j<cols;j++)
            {
                if(i==j)
                {
                    sum += matrix[i][j];
                }
            }
        }
        System.out.println(sum);
    }
}
```

   
   
Q) Write a java program to perform sum of upper triangle elements?  
   
Input:  
1 2 3   
4 5 6   
7 8 9   
Output:  
11  
   

```java
class Test  
{
    public static void main(String[] args) 
    {
        int[][] matrix = {{1,2,3},{4,5,6},{7,8,9}};        
         
        int rows = matrix.length;
        int cols = matrix[0].length;
         
        int sum = 0;
        for(int i=0;i<rows;i++)
        {
            for(int j=0;j<cols;j++)
            {
                if(i<j)
                {
                    sum += matrix[i][j];
                }
            }
        }
        System.out.println(sum);
    }
}
```

   
Q) Write a java program to perform sum of lower triangle elements?  
   
Input:  
1 2 3   
4 5 6   
7 8 9   
Output:  
19  
   

```java
class Test  
{
    public static void main(String[] args) 
    {
        int[][] matrix = {{1,2,3},{4,5,6},{7,8,9}};        
         
        int rows = matrix.length;
        int cols = matrix[0].length;
         
        int sum = 0;
        for(int i=0;i<rows;i++)
        {
            for(int j=0;j<cols;j++)
            {
                if(i>j)
                {
                    sum += matrix[i][j];
                }
            }
        }
        System.out.println(sum);
    }
}
```

   
   
Q) Write a java program to display transpose of a matrix?  
   
Input:  
1 2 3  
4 5 6  
7 8 9  
   
Output:  
1 4 7  
2 5 8  
3 6 9  
   

```java
class Test  
{
    public static void main(String[] args) 
    {
        int[][] matrix = {{1,2,3},{4,5,6},{7,8,9}};        
         
        int rows = matrix.length;
        int cols = matrix[0].length;
         
        int[][] transpose =  new int[rows][cols];
         
        for(int i=0;i<rows;i++)
        {
            for(int j=0;j<cols;j++)
            {
                transpose[j][i]=matrix[i][j];        
            }
        }
         
        //display elements 
        for(int[] arr : transpose)
        {
            for(int i  : arr)
            {
                System.out.print(i+" ");
            }
            //new line
            System.out.println();
        }
    }
}
```

   
Q) Write a java program to sort the array elements?  
   
input:  
7 9 1  
2 6 8  
3 5 4  
   
output:  
1 2 3  
4 5 6  
7 8 9   
   
   

```java
import java.util.Arrays;
class Test  
{
    public static void main(String[] args) 
    {
        int[][] matrix = {{7,9,1},{2,6,8},{3,5,4}};
         
        int rows = matrix.length;
        int cols = matrix[0].length;
         
        int[] flatArr = new int[rows*cols];
         
        //converting double dimensional array to single dimensional 
        int index = 0;
        for(int i=0;i<rows;i++)
        {
            for(int j=0;j<cols;j++)
            {
                flatArr[index++] = matrix[i][j];
            }
        }
         
        //sorting 
        Arrays.sort(flatArr);
         
        //converting single dimensional array to double dimensional array 
        int idx = 0;
        for(int i=0;i<rows;i++)
        {
            for(int j=0;j<cols;j++)
            {
                matrix[i][j] = flatArr[idx++];
                System.out.print(matrix[i][j]+" ");
            }
            //new line 
            System.out.println();
        }
    }
}
```

   
Q) Write a java program to display array elements in spiral form?  
   
Input:  
1 2 3   
4 5 6   
7 8 9   
   
output:  
1 2 3 6 9 8 7 4 5   
   
   

```java
import java.util.Arrays;
class Test  
{
    public static void main(String[] args) 
    {
        int[][] matrix = {{1,2,3},{4,5,6},{7,8,9}};
 
        int top = 0;
        int bottom = matrix.length-1;
        int left = 0;
        int right = matrix[0].length-1;
         
        while(true)
        {
            if(left>right)
            {
                break;
            }
            for(int i=left;i<=right;i++)
            {
                System.out.print(matrix[top][i]+" ");
            }
            top++;
             
            if(top>bottom)
            {
                break;
            }
            for(int i=top;i<=bottom;i++)
            {
                System.out.print(matrix[i][right]+" ");
            }
            right--;
             
            if(left>right)
            {
                break;
            }
            for(int i=right;i>=left;i--)
            {
                System.out.print(matrix[bottom][i]+" ");
            }
            bottom--;
             
            if(top>bottom)
            {
                break;
            }
            for(int i=bottom;i>=top;i--)
            {
                System.out.print(matrix[i][left]+" ");
            }
            left++;
        }
    }
}
```

   
   
