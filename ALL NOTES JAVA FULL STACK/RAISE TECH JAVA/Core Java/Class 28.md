   
Q) Write a java program to set all 0's to last of an array?  
   
input:  
2 0 1 9 0 5 0  
output:  
2 1 9 5 0 0 0  
   
   
   

```java
class Test 
{
    public static void main(String[] args) 
    {
        int[] arr = {2,0,1,9,0,5,0};
         
        int pos = 0;
        for(int i=0;i<arr.length;i++)
        {
            if(arr[i]!=0)
            {
                int temp = arr[i];
                arr[i] = arr[pos];
                arr[pos] = temp;
                 
                pos++;
            }
        }
         
        //display the elements
        for(int i : arr)
        {
            System.out.print(i+" ");
        }
         
    }
}
```

   
   
Q) Write a java program to reverse the array without using another array?  
   
Input:  
4 9 1 3 6 2  
   
Output:  
2 6 3 1 9 4   
   
   

```java
class Test {
    public static void main(String[] args) {
        int[] arr = { 4, 9, 1, 3, 6, 2 };
        int countStart = 0;
        int countEnd = arr.length - 1;
        for (int i = 0; i < arr.length / 2; i++) {
            int temp = arr[countStart];
            arr[countStart] = arr[countEnd];
            arr[countEnd] = temp;
            countStart++;
            countEnd--;
        }
        for (int i : arr) {
            System.out.print(i + " ");
        }
    }
}
```

   
   
   
   

```java
class Test {
    public static void main(String[] args) {
        int[] arr = { 4, 9, 1, 3, 6, 2 };
        int left = 0;
        int right = arr.length - 1;
        while (left < right) {
            int temp = arr[left];
            arr[left] = arr[right];
            arr[right] = temp;
            left++;
            right--;
        }
        for (int i : arr) {
            System.out.print(i + " ");
        }
    }
}
```

   
   

```java
class Test 
{
    public static void main(String[] args) 
    {
        int[] arr = {4,9,1,3,6,2};
         
        int left = 0;
        int right = arr.length-1;
         
        for(int i=0;i<arr.length;i++)
        {
            if(left<right)
            {
                int temp = arr[left];
                arr[left]= arr[right];
                arr[right]=temp;
                 
                left++;
                right--;
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

   
   
Q) Write a java program to display array elements which are greater to its immediate predecessor and successor and consider first and last element having only one neighbour?  
   
input:  
7 2 5 32 4 12 90    
   
output:  
7 32 90   
   
   

```java
class Test 
{
    public static void main(String[] args) 
    {
        int[] arr = {7,2,5,32,4,12,90};
         
        //first element
        if(arr[0]>arr[1])
        {
            System.out.print(arr[0]+" ");
        }
         
        //middle elements
        for(int i=1;i<arr.length-2;i++)
        {
            if(arr[i]>arr[i-1] && arr[i]>arr[i+1])
            {
                System.out.print(arr[i]+" ");
            }
        }
         
        //last element
        if(arr[arr.length-1]>arr[arr.length-2])
        {
            System.out.print(arr[arr.length-1]+" ");
        }
    }
}
```

   
   
   
Q) Write a java program to display all missing elements from given array?  
   
input:  
1 4 2 9   
   
output:  
3 5 6 7 8   
   
   

```java
import java.util.Arrays;
class Test 
{
    public static void main(String[] args) 
    {
        int[] arr = {1,4,2,9};
         
        Arrays.sort(arr); 
         
        for(int i=0;i<arr.length-1;i++)
        {
            int current = arr[i];
            int next = arr[i+1];
             
            while((current+1)<next)
            {
                System.out.print((current+1)+" ");
                current++;
            }
        }
    }
}
```

   
   
Q) Write a java program to display distinct elements from given array?  
   
input:  
5 9 1 3 7 6 9 3 4 2 2  
   
output:  
5 9 1 3 7 6 4 2  
   
   
   

```java
class Test 
{
    public static void main(String[] args) 
    {
        int[] arr = {5,9,1,3,7,6,9,3,4,2,2};
         
        for(int i=0;i<arr.length;i++)
        {
            int cnt = 0;
             
            for(int j=0;j<i;j++)
            {
                if(arr[i]==arr[j])
                {
                    cnt++;
                    break;
                }
            }
            if(cnt==0)
                System.out.print(arr[i]+" ");
        }
    }
}
```

   
   
Q) Write a java program to merge two arrays and display them in sorting order?  
   
input:  
5 1 3 2 4   
9 6 8 7 10  
output:  
1 2 3 4 5 6 7 8 9 10  
   
   

```java
import java.util.Arrays;
class Test 
{
    public static void main(String[] args) 
    {
        int[] arr1 = {5,1,3,2,4}; 
        int[] arr2 = {9,6,8,7,10};
         
        int size1 = arr1.length;//5
        int size2 = arr2.length;//5
 
        arr1 = Arrays.copyOf(arr1,size1+size2);
         
        int index=0;
        for(int i = size1;i<arr1.length;i++)
        {
            arr1[i] = arr2[index++];
        }
         
        //sorting
        Arrays.sort(arr1);
         
        //display
        for(int i : arr1)
        {
            System.out.print(i+" ");
        }
    }
}
```

   
   
Q) Write a java program to insert element in a given index?  
   
Input:  
arr = 7 2 8 1 9 4   
index = 3  
insert = 100  
Output:  
7 2 8 100 1 9 4  
   
   

```java
import java.util.Arrays;
class Test 
{
    public static void main(String[] args) 
    {
        int[] arr = {7,2,8,1,9,4}; 
        int index = 3;
        int insert = 100;
     
        arr = Arrays.copyOf(arr,arr.length+1);
         
        //shifting elements
        for(int i=arr.length-1;i>=index;i--)
        {
            arr[i] = arr[i-1];
        }
        arr[index]=insert;
         
        for(int i : arr)
        {
            System.out.print(i+" ");
        }
    }
}
```

   
   
Q) Write a java program to display leader elements from given array?  
   
Input:  
2 8 72 9 34 6 12  
   
Output:  
72 34 12  
   

```java
class Test 
{
    public static void main(String[] args) 
    {
        int[] arr = {2,8,72,9,34,6,12}; 
     
        for(int i=0;i<arr.length;i++)
        {
            boolean flag=true;
             
            for(int j=i+1;j<arr.length;j++)
            {
                if(arr[i]>arr[j])
                {
                    continue;
                }
                else
                {
                    flag=false;
                    break;
                }
            }
            if(flag==true)
                System.out.print(arr[i]+" ");
        }
    }
}
```

   
Assignments  
==========  
Q) Write a java program to display duplicate elements from given array?  
   
input:  
4 8 2 9 6 1 2 4 7   
   
output:  
4 2   
   
   
Q) Write a java program to remove the element from given array?  
   
input:  
arr = 7 9 4 5 8 1   
index = 2  
output:  
7 9 5 8 1   
   
   
