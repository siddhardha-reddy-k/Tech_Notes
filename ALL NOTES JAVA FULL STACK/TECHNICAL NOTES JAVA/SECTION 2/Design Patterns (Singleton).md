# Singleton Class

- Definition: It is a design pattern which ensures that a class must have only one instance.
- Concept: A class which allows us to create only one object is called singleton class.
- Requirements: To create a singleton class we required private constructor and static method.
- Purpose: The main purpose of singleton class is we can control object creations, save some memory and maintain consistency cross the application.

```java
import java.util.*;  

class Singleton  
{  
        static Date date = null;  
        private Singleton()  
        {  

                System.out.println("constructor");  

        }  
        public static Date getInstance()  
        {  
                if(date==null)  
                {  

                        date = new Date();  

                }  

                return date;  

        }  
}  
class Test  
{  
        public static void main(String[] args)  
        {  

                Date d1 = Singleton.getInstance();  
                System.out.println(d1);  
                System.out.println(d1.hashCode());  
                  
                Date d2 = Singleton.getInstance();  
                System.out.println(d2);  
                System.out.println(d2.hashCode());  

        }  
}
```
