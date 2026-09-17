   
5)  
   

```java
1 
1 # 2
1 # 2 # 3
1 # 2 # 3 # 4
```

   

```java
class Test  
{
    public static void main(String[] args) 
    {
        for(int i=1;i<=4;i++)
        {
            for(int j=1;j<=i;j++)
            {
                if(j==1)
                    System.out.print(j);
                else
                    System.out.print(" # "+j);
            }
            //new line 
            System.out.println();
        }
    }
}
```

   
   
6)  
   

```java
1
2 1 
1 2 3 
4 3 2 1 
```

   

```java
class Test  
{
    public static void main(String[] args) 
    {
        for(int i=1;i<=4;i++)
        {
            if(i%2!=0)
            {
                for(int j=1;j<=i;j++)
                {.
                    System.out.print(j+" ");
                }
                //new line 
                System.out.println();
            }
            else
            {
                for(int j=i;j>=1;j--)
                {
                    System.out.print(j+" ");
                }
                //new line 
                System.out.println();
            }
        }
    }
}
```

   
7)  

```java
2
4  6 
8  10  12
14 16  18  20
```

   

```java
class Test  
{
    public static void main(String[] args) 
    {
        int n=2;
         
        for(int i=1;i<=4;i++)
        {
            for(int j=1;j<=i;j++)
            {
                System.out.print(n+" ");
                n+=2;
            }
            //new line 
            System.out.println();
        }
    }
}
```

   
   
8)  
   

```java
2
3  5 
7  11 13
17 19 23 29
```

   

```java
class Test  
{
    public static void main(String[] args) 
    {
        int n=2;
         
        for(int i=1;i<=4;i++)
        {
            for(int j=1;j<=i;j++)
            {
                while(true)
                {
                    boolean flag = true;
                    for(int k=2;k<=n/2;k++)
                    {
                        if(n%k==0)
                        {
                            flag=false;
                            break;
                        }
                    }
                    if(flag==true)
                    {
                        System.out.print(n+" ");
                        n++;
                        break;
                    }
                    else
                    {
                        n++;
                    }
                }
            }
            //new line 
            System.out.println();
        }
    }
}
```

   
Right Side Loop Patterns   
========================  
1)  

```java
      1
    2 2
  3 3 3 
4 4 4 4
```

   
   

```java
class Test  
{
    public static void main(String[] args) 
    {
        for(int i=1;i<=4;i++)
        {
            //space
            for(int j=4;j>i;j--)
            {
                System.out.print("  ");
            }
             
            //elements
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

```java
4 4 4 4 
  3 3 3 
    2 2 
      1
class Test  
{
    public static void main(String[] args) 
    {
        for(int i=4;i>=1;i--)
        {
            //space
            for(int j=4;j>i;j--)
            {
                System.out.print("  ");
            }
             
            //elements
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
        for(int i=1;i<=4;i++)
        {
            //space
            for(int j=4;j>i;j--)
            {
                System.out.print("  ");
            }
             
            //elements
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

   
Pyramid Loop Patterns  
=====================  
   
1)   

```java
      1
    1 2 1
  1 2 3 2 1 
1 2 3 4 3 2 1 
```

   

```java
class Test  
{
    public static void main(String[] args) 
    {
        for(int i=1;i<=4;i++)
        {
            //space
            for(int j=4;j>i;j--)
            {
                System.out.print("  ");
            }
             
            //left side 
            for(int j=1;j<=i;j++)
            {
                System.out.print(j+" ");
            }
             
            //right side 
            for(int j=i-1;j>=1;j--)
            {
                System.out.print(j+" ");
            }
            //new line 
            System.out.println();
        }
    }
}
```

   
   
2)   

```java
    
1 2 3 4 3 2 1
  1 2 3 2 1 
    1 2 1 
      1
```

   

```java
class Test  
{
    public static void main(String[] args) 
    {
        for(int i=4;i>=1;i--)
        {
            //space
            for(int j=4;j>i;j--)
            {
                System.out.print("  ");
            }
             
            //left side 
            for(int j=1;j<=i;j++)
            {
                System.out.print(j+" ");
            }
             
            //right side 
            for(int j=i-1;j>=1;j--)
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
      * 
    * * * 
  * * * * * 
* * * * * * * 
```

   

```java
class Test  
{
    public static void main(String[] args) 
    {
        for(int i=1;i<=4;i++)
        {
            //space
            for(int j=4;j>i;j--)
            {
                System.out.print("  ");
            }
             
            //left side 
            for(int j=1;j<=i;j++)
            {
                System.out.print("* ");
            }
             
            //right side 
            for(int j=i-1;j>=1;j--)
            {
                System.out.print("* ");
            }
            //new line 
            System.out.println();
        }
    }
}
```

   
Q) Write a java program to display below loop pattern?  
   

```java
1             1
1 2         2 1 
1 2 3     3 2 1
1 2 3 4 4 3 2 1
```

   

```java
class Test  
{
    public static void main(String[] args) 
    {
        int rows = 4;
         
        for(int i=1;i<=rows;i++)
        {
            //left side 
            for(int j=1;j<=i;j++)
            {
                System.out.print(j+" ");
            }
             
            //space
            for(int j=1;j<=(rows-i)*2;j++)
            {
                System.out.print("  ");
            }
             
            //right side 
            for(int j=i;j>=1;j--)
            {
                System.out.print(j+" ");
            }
            //new line 
            System.out.println();
        }
    }
}
```

   
Q) Write a java program to display below loop pattern?  
   

```java
6 5 4 3 2 1
 6 5 4 3 2
  6 5 4 3 
   6 5 4 
    6 5   
     6
```

   
   

```java
class Test  
{
    public static void main(String[] args) 
    {
        for(int i=1;i<=6;i++)
        {
            //space
            for(int j=1;j<i;j++)
            {
                System.out.print(" ");
            }
            //elements
            for(int j=6;j>=i;j--)
            {
                System.out.print(j+" ");
            }
            //new line 
            System.out.println();
        }
    }
}
```

   
Q) Write a java program to display below loop pattern?  
   

```java
     *
    * * 
   * * * 
  * * * * 
 * * * * * 
* * * * * *
```

   

```java
class Test  
{
    public static void main(String[] args) 
    {
        for(int i=6;i>=1;i--)
        {
            //space
            for(int j=1;j<i;j++)
            {
                System.out.print(" ");
            }
            //elements
            for(int j=6;j>=i;j--)
            {
                System.out.print("* ");
            }
            //new line 
            System.out.println();
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
        for(int i=0;i<5;i++)
        {
            //space
            for(int j=4;j>i;j--)
            {
                System.out.print(" ");
            }
            for(int k=0;k<=i;k++)
            {
                System.out.print("* ");
            }
            //new line 
            System.out.println();
        }
    }
}
```

   
   
   
Q) Write a java program to display pascal triangle?  
   

```java
    1 
   1 1
  1 2 1
 1 3 3 1
1 4 6 4 1
```

   

```java
class Test  
{
    public static void main(String[] args) 
    {
        for(int i=0;i<5;i++)
        {
            //space
            for(int j=4;j>i;j--)
            {
                System.out.print(" ");
            }
            int result = 1;
            for(int k=0;k<=i;k++)
            {
                System.out.print(result+" ");
                result = result * (i-k)/(k+1);
            }
            //new line 
            System.out.println();
        }
    }
}
```

   
   
Assignment  
==========  
A water tank can hold 1000 liters of water. Every hour, 150 liters are poured into the tank, while 30 liters leak out. Write a Java program to determine how many hours it will take to fill the tank.  
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
