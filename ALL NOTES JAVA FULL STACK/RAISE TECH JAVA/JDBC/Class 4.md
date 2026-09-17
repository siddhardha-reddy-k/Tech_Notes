Non-Select Queries 
==================

Q) Write a jdbc application to insert a record in to student table?

SQL Query :  insert into student values(104,'ramulu','pune'); 

ex:
---
package com.ihub.www;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.Statement;
import java.util.Scanner;

public class InsertApp
{
	public static void main(String[] args)throws Exception  
	{
		Scanner sc = new Scanner(System.in);
		
		System.out.println("Enter the student no :");
		int no = sc.nextInt();
		
		System.out.println("Enter the student name :");
		String name = sc.next();
		
		System.out.println("Enter the student address :");
		String add = sc.next();
		
		//converting inputs according to sql query
		name="'"+name+"'";
		add="'"+add+"'";
		
		Class.forName("oracle.jdbc.driver.OracleDriver");
		Connection con = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE","system","admin");
		Statement st = con.createStatement();
		
		String qry = "insert into student values("+no+","+name+","+add+")";
		
		int result = st.executeUpdate(qry);
		
		if(result==0)
			System.out.println("No Record Inserted");
		else
			System.out.println(result+" Record Inserted");
		
		st.close();
		con.close();
	}
}

Q) Write a jdbc application to update student name based on student number?

SQL Query : update student set sname='rani' where sno=104;

ex:
---
package com.ihub.www;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.Statement;
import java.util.Scanner;

public class UpdateApp 
{
	public static void main(String[] args)throws Exception  
	{
		Scanner sc = new Scanner(System.in);
		
		System.out.println("Enter the student no:");
		int no = sc.nextInt();
		
		System.out.println("Enter the student name :");
		String name =sc.next();
		
		//convert inputs according to SQL query
		name="'"+name+"'";
		
		Class.forName("oracle.jdbc.driver.OracleDriver");
		Connection con = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE","system","admin");
		Statement st = con.createStatement();
		
		String qry = "update student set sname="+name+" where sno="+no;

		int result = st.executeUpdate(qry);
		if(result==0)
			System.out.println("No Record Updated");
		else
			System.out.println(result+" Record Updated");
		
		st.close();
		con.close();
	}
}

Q) Write a jdbc application to delete student record based on student number?


SQL Query : delete from student where sno=104;

ex:
---
package com.ihub.www;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.Statement;
import java.util.Scanner;

public class DeleteApp 
{
	public static void main(String[] args)throws Exception  
	{
		Scanner sc = new Scanner(System.in);
		System.out.println("Enter the student number :");
		int no = sc.nextInt();
		
		Class.forName("oracle.jdbc.driver.OracleDriver");
		Connection con = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE","system","admin");
		Statement st = con.createStatement();
		
		String qry ="delete from student where sno="+no;
		
		int result = st.executeUpdate(qry);
		if(result==0)
			System.out.println("No Record Deleted");
		else
			System.out.println(result+" Record Deleted");
		
		st.close();
		con.close();
	}
}


Interview Question 
==================
Q) Write a JDBC application to create a student table?

package com.ihub.www;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.Statement;

public class CreateApp 
{
	public static void main(String[] args)throws Exception 
	{
		Class.forName("oracle.jdbc.driver.OracleDriver");
		Connection con = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE","system","admin");
		Statement st = con.createStatement();
		String qry ="create table student(sno number(3),sname varchar2(10),sadd varchar2(12))";
		st.executeUpdate(qry);
		System.out.println("Table Created");
		st.close();
		con.close();
	}
}


Q) Write a JDBC application to store student records in ArrayList?

Student.java
------------
package com.ihub.www;

public class Student
{
	private int sno;
	private String sname;
	private String sadd;
	
	public Student(int sno, String sname, String sadd) 
	{
		super();
		this.sno = sno;
		this.sname = sname;
		this.sadd = sadd;
	}

	@Override
	public String toString() {
		return sno+" "+sname+" "+sadd;
	}
	
}

ArrayListApp.java
------------------
package com.ihub.www;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;
import java.util.ArrayList;
import java.util.List;

public class ArrayListApp
{
	public static void main(String[] args)throws Exception  
	{
		Class.forName("oracle.jdbc.driver.OracleDriver");
		Connection con = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE","system","admin");
		Statement st = con.createStatement();
		String qry = "select * from student";
		ResultSet rs =st.executeQuery(qry);
		
		List<Student> list = new ArrayList<>();
		
		while(rs.next())
		{
			list.add(new Student(rs.getInt(1),rs.getString(2),rs.getString(3)));
		}
		
		list.forEach(System.out::println);
		
		rs.close();
		st.close();
		con.close();
	}
}


Standard procedure to develop jdbc application 
==============================================
package com.ihub.www;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;

public class StandardApp 
{
	public static void main(String[] args) 
	{
		final String DRIVER = "oracle.jdbc.driver.OracleDriver";
		final String URL="jdbc:oracle:thin:@localhost:1521:XE";
		final String USERNAME="system";
		final String PASSWORD="admin";
		final String QUERY ="select * from student";
		
		Connection con = null;
		Statement st = null;
		ResultSet rs = null;
		try
		{
			Class.forName(DRIVER);
			con = DriverManager.getConnection(URL,USERNAME,PASSWORD);
			st = con.createStatement();
			rs = st.executeQuery(QUERY);
			while(rs.next())
			{
	System.out.println(rs.getInt(1)+" "+rs.getString(2)+" "+rs.getString(3));
			}
			rs.close();
			st.close();
			con.close();
		}
		catch(Exception e)
		{
			e.printStackTrace();
		}
	}
}
