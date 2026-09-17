   
Q) Write a java program to display array elements in sorting order?  
   
Input:  
6 1 9 2 7 5  
   
output:  
1 2 5 6 7 9   
   
   

```java
import java.util.Arrays;
class Test 
{
    public static void main(String[] args) 
    {
        int[] arr = {6,1,9,2,7,5};
         
        Arrays.sort(arr);
         
        for(int i : arr)
        {
            System.out.print(i+" ");
        }
    }
}
```

   
   
Q) Write a java program to display array elements in sorting order without using sort() method?  
   
Input:  
6 1 9 2 7 5  
   
output:  
1 2 5 6 7 9   
   
   

```java
class Test 
{
    public static void main(String[] args) 
    {
        int[] arr = {6,1,9,2,7,5};
         
        for(int i=0;i<arr.length-1;i++)
        {
            if(arr[i] > arr[i+1])
            {
                int temp = arr[i];
                arr[i] = arr[i+1];
                arr[i+1] = temp;
                 
                i=-1;
            }
        }
         
        //display elements 
        for(int i : arr)
        {
            System.out.print(i+" ");
        }
    }
}
```

   
   
Q) Write a java program to display array elements in descending order without using sort() method?  
   
Input:  
6 1 9 2 7 5  
   
output:  
9 7 6 5 2 1   
   
   

```java
class Test 
{
    public static void main(String[] args) 
    {
        int[] arr = {6,1,9,2,7,5};
         
        for(int i=0;i<arr.length-1;i++)
        {
            if(arr[i] < arr[i+1])
            {
                int temp = arr[i];
                arr[i] = arr[i+1];
                arr[i+1] = temp;
                 
                i=-1;
            }
        }
         
        //display elements 
        for(int i : arr)
        {
            System.out.print(i+" ");
        }
    }
}
```

   
   
   
Q) Write a java program to display highest element from given array?  
   
Input:  
6 1 9 2 7 5  
   
output:  
9  
   

```java
import java.util.Arrays;
class Test 
{
    public static void main(String[] args) 
    {
        int[] arr = {6,1,9,2,7,5};
         
        Arrays.sort(arr);
         
        System.out.println(arr[arr.length-1]);
    }
}
```

   
   
   
Q) Write a java program to display highest element from given array without using sort() method?  
   
Input:  
6 1 9 2 7 5  
   
output:  
9  
   
   

```java
class Test 
{
    public static void main(String[] args) 
    {
        int[] arr = {6,1,9,2,7,5};
         
        int big = arr[0];
         
        for(int i=0;i<arr.length;i++)
        {
            if(arr[i] > big)
            {
                big = arr[i];
            }
        }
        System.out.println(big);
    }
}
```

   
   
   
Q) Write a java program to display Least element from given array without using sort() method?  
   
Input:  
6 1 9 2 7 5  
   
output:  
1  
   
   

```java
class Test 
{
    public static void main(String[] args) 
    {
        int[] arr = {6,1,9,2,7,5};
         
        int small = arr[0];
         
        for(int i=0;i<arr.length;i++)
        {
            if(arr[i] < small)
            {
                small = arr[i];
            }
        }
        System.out.println(small);
    }
}
```

   
   
Q) Write a java program to display three highest elements from given array?  
   
   
Input:  
5 9 2 6 8 3 7   
   
Output:  
9 8 7   
   
   

```java
class Test 
{
    public static void main(String[] args) 
    {
        int[] arr = {5,9,2,6,8,3,7};
         
        int firstElement = Integer.MIN_VALUE;
        int secondElement = Integer.MIN_VALUE;
        int thirdElement = Integer.MIN_VALUE;
         
        for(int i : arr)
        {
            if(i > firstElement)
            {
                thirdElement = secondElement; 
                secondElement = firstElement;
                firstElement = i;
            }
            else if(i>secondElement)
            {
                thirdElement = secondElement;
                secondElement = i;
            }
            else if(i>thirdElement)
            {
                thirdElement = i;
            }
        }
        System.out.println(firstElement+" "+secondElement+" "+thirdElement);
    }
}
```

   
   
Q) Write a java program to display unique elements from given array?  
   
input:  
5 9 1 2 6 9 7 7 5 4   
   
output:  
1 2 6 4   
   

```java
class Test 
{
    public static void main(String[] args) 
    {
        int[] arr = {5,9,1,2,6,9,7,7,5,4};
         
        for(int i=0;i<arr.length;i++)
        {
            int cnt = 0;
             
            for(int j=0;j<arr.length;j++)
            {
                if(arr[i]==arr[j])
                {
                    cnt++;
                }
            }
            if(cnt==1)
                System.out.print(arr[i]+" ");
        }
    }
}
```

   
   
   
Q) Write a java program to find out most repeating element from given array?  
   
Input:  
2 8 1 2 9 2 1 2 6 2 5   
   
 Output:  
2 repeating for 5 times   
   
   

```java
class Test 
{
    public static void main(String[] args) 
    {
        int[] arr = {2,8,1,2,9,2,1,2,6,2,5};
         
        int element=0;
        int maxCount=0;
         
        for(int i=0;i<arr.length;i++)
        {
            int cnt = 0;
             
            for(int j=0;j<arr.length;j++)
            {
                if(arr[i]==arr[j])
                {
                    cnt++;
                }
            }
             
            if(cnt>maxCount)
            {
                maxCount = cnt;
                element = arr[i];
            }
        }
        System.out.println(element+" repeating for "+maxCount+" times");
    }
}
```

   
   
Q) Write a java program to seggregate array elements?  
   
Input:  
1 0 1 0 0 1 1 0 1 0  
   
output:  
0 0 0 0 0 1 1 1 1 1  
   
   
Approach1  
---------  

```java
import java.util.Arrays;
class Test 
{
    public static void main(String[] args) 
    {
        int[] arr = {1,0,1,0,0,1,1,0,1,0};
        Arrays.sort(arr);
        System.out.println(Arrays.toString(arr));
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
        int[] arr = {1,0,1,0,0,1,1,0,1,0};
 
        int index=0;
        for(int i=0;i<arr.length;i++)
        {
            if(arr[i]==0)
            {
                int temp = arr[i];
                arr[i] = arr[index];
                arr[index] = temp;
                 
                index++;
            }
        }
        //display 
        for(int i : arr)
        {
            System.out.print(i+" ");
        }
    }
}
```

   
   
Q) Write a java program to display pair of elements equals to sum=10?  
   
Input:  
arr = 7 2 3 1 6 5 4  
sum = 10  
Output:  
7 3  
6 4   
   
   

```java
class Test 
{
    public static void main(String[] args) 
    {
        int[] arr = {7,2,3,1,6,5,4};
        int sum = 10;
 
        for(int i=0;i<arr.length;i++)
        {
            for(int j=i+1;j<arr.length;j++)
            {
                if(arr[i]+arr[j] == sum)
                {
                    System.out.println(arr[i]+" "+arr[j]);
                }
            }
        }
    }
}
```

   
   
   
   
Q) Write a java program to display triple of elements equals to sum=10?  
   
Input:  
arr = 7 2 3 1 6 5 4  
sum = 10  
Output:  
7 2 1   
2 3 5   
3 1 6  
1 5 4   
   
   

```java
class Test 
{
    public static void main(String[] args) 
    {
        int[] arr = {7,2,3,1,6,5,4};
        int sum = 10;
 
        for(int i=0;i<arr.length;i++)
        {
            for(int j=i+1;j<arr.length;j++)
            {
                for(int k=j+1;k<arr.length;k++)
                {
                    if(arr[i]+arr[j]+arr[k] == sum)
                    {
                    System.out.println(arr[i]+" "+arr[j]+" "+arr[k]);
                    }
                }
            }
        }
    }
}
```

   
   
Assignment   
==========  
Q) Write a java program to shift all 0's to end of the array?  
   
input:  
6 0 2 0 9 0 4   
   
output:  
6 2 9 4 0 0 0    
   
   
