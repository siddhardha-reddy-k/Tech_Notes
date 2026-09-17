Eclipse 
=======
IDE		:	JEE 

Vendor		:	Eclipse Foundation

Environment	:	Java  

Website		:	www.eclipse.org

Format		:	Zip 

Download link	:

https://drive.google.com/file/d/1c8TAX048EjAubIFByqZ0DzWZI3oKuauR/view?usp=drive_link


Steps to develop first JDBC application to read the records from student table
===============================================================================
step1:
------
	Create a student table with records.
	ex:
		drop table student;
		create table student(sno number(3),
					sname varchar2(10),
						sadd varchar2(12));	
		insert into student values(101,'raja','hyd');
		insert into student values(102,'ravi','delhi');
		insert into student values(103,'ramana','vizag');
		commit;
		select * from student;

step2:
------
	Launch eclipse IDE by choosing workspace location.

step3:
------
	Create a Java project i.e IH-JAVA-056.
	ex:
		File --> New --> Project --> Java Project --> Next 
		Project Name : IH-JAVA-056 --> Next --> Finish (Don't create, No).	
step4:
-----	
	Add ojdbc14.jar file in project build path.
	Note:
		C:\oraclexe\app\oracle\product\10.2.0\server\jdbc\lib

	ex:
		Right click to IH-JAVA-056 project --> Build path --> 
		Configure build path --> Libararies --> classpath -->
		add external jars --> select ojdbc14.jar file --> open 
		--> apply and close.

step5:
------
	Create a "com.ihub.www" package inside "src" folder.
	ex:
		right click to src folder --> new --> package -->
		Name : com.ihub.www --> finish.

step6:
-----
	Create a SelectApp1.java file inside "com.ihub.www" package.
	ex:
		Right click to com.ihub.www package --> new --> class -->
		class name : SelectApp1 --> Finish. 

SelectApp1.java
---------------
package com.ihub.www;

//ctrl + shift + o 
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;

public class SelectApp1 
{
	public static void main(String[] args)throws Exception  
	{
		Class.forName("oracle.jdbc.driver.OracleDriver");
		Connection con = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE","system","admin");
		Statement st = con.createStatement(); 
		String qry = "select * from student";
		ResultSet rs = st.executeQuery(qry);
		while(rs.next())
		{
			System.out.println(rs.getInt(1)+" "+rs.getString(2)+" "+rs.getString(3));
		}
		rs.close();
		st.close();
		con.close();
	}
}

step7:
-------
	Run JDBC application.


Q) Write a JDBC application to select student name and student address from student table?

package com.ihub.www;

//ctrl + shift + o 
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;

public class SelectApp1 
{
	public static void main(String[] args)throws Exception  
	{
		Class.forName("oracle.jdbc.driver.OracleDriver");
		Connection con = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE","system","admin");
		Statement st = con.createStatement(); 
		String qry = "select sname,sadd from student";
		ResultSet rs = st.executeQuery(qry);
		while(rs.next())
		{
			System.out.println(rs.getString(1)+" "+rs.getString(2));
		}
		rs.close();
		st.close();
		con.close();
	}
}


Q) Write a jdbc application to select student name from student table?

package com.ihub.www;

//ctrl + shift + o 
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;

public class SelectApp1 
{
	public static void main(String[] args)throws Exception  
	{
		Class.forName("oracle.jdbc.driver.OracleDriver");
		Connection con = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE","system","admin");
		Statement st = con.createStatement(); 
		String qry = "select sname from student";
		ResultSet rs = st.executeQuery(qry);
		while(rs.next())
		{
			System.out.println(rs.getString(1));
		}
		rs.close();
		st.close();
		con.close();
	}
}


Q) Write a jdbc application to select student name and student address based on student number?

package com.ihub.www;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;
import java.util.Scanner;

public class SelectApp2 
{
	public static void main(String[] args)throws Exception  
	{
		Scanner sc = new Scanner(System.in);
		System.out.println("Enter the student no :");
		int n = sc.nextInt();
		
		Class.forName("oracle.jdbc.driver.OracleDriver");
		Connection con = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE","system","admin");
		Statement st = con.createStatement();
		String qry="select sname,sadd from student where sno="+n;
		ResultSet rs = st.executeQuery(qry);
		
		int cnt=0;
		while(rs.next())
		{
			System.out.println(rs.getString(1)+" "+rs.getString(2));
			cnt=1;
		}
		if(cnt==0)
			System.out.println("No Rows Selected");
		
		rs.close();
		st.close();
		con.close();
	}
}
