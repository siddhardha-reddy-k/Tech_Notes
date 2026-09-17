   
iv) for each loop   
==================  
It is also known as enhanced for loop.  
   
It is used to iterate the elements/objects from arrays/Collections.  
   
syntax:  
-------  

```java
for(variable_name : array_name)
{
```

-  
- //code to be execute  
-  
}  
   
ex:  
---  

```java
class Test  
{
    public static void main(String[] args) 
    {
        int[] arr = {10,20,30,40};
         
        for(int i : arr)
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
        List<Integer> list = List.of(6,8,2,9,1);
         
        for(int i : list)
        {
            System.out.print(i+" ");
        }
    }
}
```

   
3) Jump Statement   
=================  
Jump statement is used to jump from one section of code to another section.  
   
We have three jump statements in java.  
   
i) break stmt   
   
ii) continue stmt   
   
iii) return stmt   
   
   
i) break stmt  
=============  
It is used to break the execution of loops and switch case.  
For conditional statements we can use if condition.  
syntax:  
-------  

```java
break;
```

   
ex:  
---  

```java
class Test  
{
    public static void main(String[] args) 
    {
        System.out.println("stmt1");
        break;
        System.out.println("stmt2");
    }
}
```

o/p:  
C.T.E : break outside switch or loop  
   
ex:  
---  

```java
class Test  
{
    public static void main(String[] args) 
    {
        System.out.println("stmt1");
        if(false)
        {
            break;
        }
        System.out.println("stmt2");
    }
}
```

o/p:  
C.T.E : break outside switch or loop  
   
ex:  
---  

```java
class Test  
{
    public static void main(String[] args) 
    {
        for(int i=1;i<=10;i++)
        {
            if(i==5)
            {
                break;
            }
             
            System.out.print(i+" ");//1 2 3 4 
        }
    }
}
```

   
   
ii) continue stmt   
=================  
It is used to continue the execution of loops.  
For conditional statement we can use if condition.  
syntax:  
-------  

```java
continue;
```

   
ex:  
---  

```java
class Test  
{
    public static void main(String[] args) 
    {
        System.out.println("stmt1");
        continue;
        System.out.println("stmt2");
    }
}
```

o/p:  
C.T.E : continue outside of loop  
   
ex:  
---  

```java
class Test  
{
    public static void main(String[] args) 
    {
        System.out.println("stmt1");
        if(true)
        {
            continue;
        }
        System.out.println("stmt2");
    }
}
```

o/p:  
C.T.E : continue outside of loop  
   
ex:  
---  

```java
class Test  
{
    public static void main(String[] args) 
    {
        for(int i=1;i<=10;i++)
        {
            if(i==5)
            {
                continue;
            }
            System.out.print(i+" ");// 1 2 3 4 6 7 8 9 10
        }
    }
}
```

   
iii) return stmt   
================  
It is used to exit from method.  
It contains optional value.  
   
syntax:  
-------  

```java
return <value>;
```

   
ex:  
---  

```java
import java.util.Scanner;
class Test  
{
    public static void main(String[] args) 
    {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter the option :");
        int option = sc.nextInt();
         
        if(option==100)
            System.out.println("It is a police number");
        else if(option == 103)
            System.out.println("It is a enquiry number");
        else if(option==108)
            System.out.println("It is a emergency number");
        else
            return;
    }
}
```

   
   
Loop Patterns   
=============  
   
1)  
   

```java
1 1 1 1
2 2 2 2
3 3 3 3
4 4 4 4 
```

   

```java
class Test  
{
    public static void main(String[] args) 
    {
        //rows
        for(int i=1;i<=4;i++)
        {
            //cols
            for(int j=1;j<=4;j++)
            {
                System.out.print(i+" ");
            }
            //new line 
            System.out.println();
        }
    }
}
```

   
2)  

```java
1 2 3 4
1 2 3 4
1 2 3 4
1 2 3 4
```

   

```java
class Test  
{
    public static void main(String[] args) 
    {
        //rows
        for(int i=1;i<=4;i++)
        {
            //cols
            for(int j=1;j<=4;j++)
            {
                System.out.print(j+" ");
            }
            //new line 
            System.out.println();
        }
    }
}
```

   
   
3)  

```java
* * * * 
* * * *
* * * * 
* * * * 
```

   

```java
class Test  
{
    public static void main(String[] args) 
    {
        //rows
        for(int i=1;i<=4;i++)
        {
            //cols
            for(int j=1;j<=4;j++)
            {
                System.out.print("* ");
            }
            //new line 
            System.out.println();
        }
    }
}
```

   
   
4)   
   

```java
* * * * 
*     *
*     *
* * * * 
```

   

```java
class Test  
{
    public static void main(String[] args) 
    {
        //rows
        for(int i=1;i<=4;i++)
        {
            //cols
            for(int j=1;j<=4;j++)
            {
                if(i==1 || i==4 || j==1 || j==4)
                    System.out.print("* ");
                else
                    System.out.print("  ");
            }
            //new line 
            System.out.println();
        }
    }
}
```

   
5)   
   

```java
* - - - 
- * - - 
- - * - 
- - - * 
```

   

```java
class Test  
{
    public static void main(String[] args) 
    {
        //rows
        for(int i=1;i<=4;i++)
        {
            //cols
            for(int j=1;j<=4;j++)
            {
                if(i==j)
                    System.out.print("* ");
                else
                    System.out.print("- ");
            }
            //new line 
            System.out.println();
        }
    }
}
```

   
6)  

```java
* - - - *
- * - * - 
- - * - - 
- * - * -
* - - - *
```

   

```java
class Test  
{
    public static void main(String[] args) 
    {
        //rows
        for(int i=1;i<=5;i++)
        {
            //cols
            for(int j=1;j<=5;j++)
            {
                if(i==j || i+j==6)
                    System.out.print("* ");
                else
                    System.out.print("- ");
            }
            //new line 
            System.out.println();
        }
    }
}
```

   
7)   

```java
    *
    *
* * * * * 
    *
    * 
```

   

```java
class Test  
{
    public static void main(String[] args) 
    {
        //rows
        for(int i=1;i<=5;i++)
        {
            //cols
            for(int j=1;j<=5;j++)
            {
                if(i==3 || j==3)
                    System.out.print("* ");
                else
                    System.out.print("  ");
            }
            //new line 
            System.out.println();
        }
    }
}
```

   
8)  
4 4 4 4 4 4 4  
4 3 3 3 3 3 4  
4 3 2 2 2 3 4  
4 3 2 1 2 3 4  
4 3 2 2 2 3 4       
4 3 3 3 3 3 4  
4 4 4 4 4 4 4  
   
   

```java
class Test  
{
    public static void main(String[] args) 
    {
        int n=4, size=7;
         
        for(int i=0;i<size;i++)
        {
            for(int j=0;j<size;j++)
            {
                int result = n - Math.min(Math.min(i,j), Math.min(size-i-1,size-j-1));
                System.out.print(result+" ");
            }
            //new line 
            System.out.println();
        }
    }
}
```

   
   
   
Left Side Loop Patterns  
=======================  
1)  
1  
2 2   
3 3 3   
4 4 4 4  
   
   

```java
class Test  
{
    public static void main(String[] args) 
    {
        //rows 
        for(int i=1;i<=4;i++)
        {
            //cols
            for(int j=1;j<=i;j++)
            {
                System.out.print(i+" ");        
            }
            //new line 
            System.out.println();
        }
    }
}
```

   
2)   
   
4 4 4 4   
3 3 3  
2 2   
1   
   
   

```java
class Test  
{
    public static void main(String[] args) 
    {
        //rows 
        for(int i=4;i>=1;i--)
        {
            //cols
            for(int j=1;j<=i;j++)
            {
                System.out.print(i+" ");
            }
            //new line 
            System.out.println();
        }
    }
}
```

   
   
3)   
   

```java
*
* * 
* * * 
* * * *
```

   

```java
class Test  
{
    public static void main(String[] args) 
    {
        //rows 
        for(int i=1;i<=4;i++)
        {
            //cols
            for(int j=1;j<=i;j++)
            {
                System.out.print("* ");
            }
            //new line 
            System.out.println();
        }
    }
}
```

   
4)  
   

```java
* * * * 
* * * 
* * 
* 
```

   
   

```java
class Test  
{
    public static void main(String[] args) 
    {
        //rows 
        for(int i=4;i>=1;i--)
        {
            //cols
            for(int j=1;j<=i;j++)
            {
                System.out.print("* ");
            }
            //new line 
            System.out.println();
        }
    }
}
```

   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
