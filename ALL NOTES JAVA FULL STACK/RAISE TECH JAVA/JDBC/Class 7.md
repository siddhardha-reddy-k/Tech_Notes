Solution for SQL Injection problem 
===================================
package com.ihub.www;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.util.Scanner;

public class SolForSqlInjProb 
{
	public static void main(String[] args)throws Exception  
	{
		Scanner sc = new Scanner(System.in);
		
		System.out.println("Enter the username :");
		String name = sc.next();
		
		System.out.println("Enter the password :");
		String pass = sc.next();
		
		Class.forName("oracle.jdbc.driver.OracleDriver");
		Connection con = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE","system","admin");
		
		String qry = "select count(*) from userlist where uname=? and pwd=?";
		
		PreparedStatement ps = con.prepareStatement(qry);
		
		//set the values 
		ps.setString(1, name);
		ps.setString(2, pass);
		
		//execute 
		ResultSet rs = ps.executeQuery();
		int result=0;
		while(rs.next())
		{
			result = rs.getInt(1);
		}
		if(result==0)
			System.out.println("Invalid Credentials");
		else
			System.out.println("Valid Credentials");
		
		rs.close();
		ps.close();
		con.close();
	}
}

DatabaseMetaData 
================
DatabaseMetaData is an interface which is present in java.sql package.

DatabaseMetaData provides metadata of a database.

DatabasetMetaData gives information about database product name, database product version, database driver name, database driver version, database username and etc.

We can create DatabaseMetaData object by using getMetaData() method of Connection object.
ex:
	DatabaseMetaData dbmd = con.getMetaData();

ex:
---
package com.ihub.www;

import java.sql.Connection;
import java.sql.DatabaseMetaData;
import java.sql.DriverManager;

public class DBMDApp 
{
	public static void main(String[] args)throws Exception  
	{
		Class.forName("oracle.jdbc.driver.OracleDriver");
		Connection con = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE","system","admin");
		DatabaseMetaData dbmd = con.getMetaData();
		System.out.println(dbmd.getDatabaseProductName());
		System.out.println(dbmd.getDatabaseProductVersion());
		System.out.println(dbmd.getDriverName());
		System.out.println(dbmd.getDriverVersion());
		System.out.println(dbmd.getUserName());
		con.close();
	}
}

ResultSetMetaData 
=================
ResultSetMetaData is an interface which is present in java.sql package.

ResultSetMetaData provides metadata of a table.

ResultSetMetaData gives information about number of columns,name of the columsn, type of columns, size of columns and etc.

We can create ResultSetMetaData object by using getMetaData() method of ResultSet object.

ex:	
	ResultSetMetaData rs = rs.getMetaData();

ex:
---
package com.ihub.www;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.ResultSetMetaData;
import java.sql.Statement;

public class RSMDApp 
{
	public static void main(String[] args)throws Exception  
	{
		Class.forName("oracle.jdbc.driver.OracleDriver");
		Connection con = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE","system","admin");
		Statement st = con.createStatement();
		String qry = "select * from student";
		ResultSet rs = st.executeQuery(qry);
		
		ResultSetMetaData rsmd = rs.getMetaData();
		
		System.out.println(rsmd.getColumnCount());
		System.out.println(rsmd.getColumnName(1));
		System.out.println(rsmd.getColumnTypeName(2));
		System.out.println(rsmd.getColumnDisplaySize(2));
		
		rs.close();
		st.close();
		con.close();
	}
}

Working with Date values 
=========================
While dealing with DOB, DOA, DOR, DOD we need to insert and retrieve date values.

It is never recommanded to pass date values in the form of string because we can't compare two dates.

Every database software supports different date pattern.
ex:
	oracle - dd-MMM-yy
	mysql  - yyyy-MM-dd 

Using simple Statement object we can't insert date values to query parameters.

To overcome this limitation we need to use PreparedStatement object.

A java.util.Date class object is not suitable to perform database operation.

A java.sql.Date class object is suitable to perform datbase operation.

Once JDBC driver gets date value then it will insert in the pattern which is supported by underlying database software.

Diagram: jdbc7.1

With respect to the diagram:

1) Enduser gives data value in the form String.

2) A parse() method of SimpleDateFormat class converts String date to 
   java.util.Date class object.

3) Our application converts java.util.Date class object to java.sql.Date class object.

4) A ps.setDate(-,-) method is used to set the date value to query parameter.

5) Once JDBC driver gets date value then it will insert in the pattern which is supported
   by underlying database software.

emp1 table 
===========
drop table emp1;
create table emp1(eid number(3),ename varchar2(10),edoj date);


DateInsertApp.java
------------------
package com.ihub.www;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.text.SimpleDateFormat;
import java.util.Scanner;

public class DateInsertApp 
{
	public static void main(String[] args)throws Exception  
	{
		Scanner sc = new Scanner(System.in);
		
		System.out.println("Enter the employee id :");
		int id = sc.nextInt(); 
		
		System.out.println("Enter the employee name :");
		String name = sc.next();
		
		System.out.println("Enter the DOJ (dd-MM-yyyy) :");
		String sdoj = sc.next();
		
		//converting string date to util date 
		SimpleDateFormat sdf = new SimpleDateFormat("dd-MM-yyyy");
		java.util.Date udoj = sdf.parse(sdoj);
		
		//converting util date to SQl date.
		long ms = udoj.getTime();
		java.sql.Date sqldoj = new java.sql.Date(ms);
		
		Class.forName("oracle.jdbc.driver.OracleDriver");
		Connection con = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE","system","admin");
		
		String qry  = "insert into emp1 values(?,?,?)";
		
		PreparedStatement ps = con.prepareStatement(qry);
		
		//set the values 
		ps.setInt(1, id);
		ps.setString(2, name);
		ps.setDate(3, sqldoj);
		
		//execute
		int result = ps.executeUpdate();
		if(result==0)
			System.out.println("No record Inserted");
		else
			System.out.println("Record Inserted");
		
		ps.close();
		con.close();
	}
}

DateRetrieveApp.java
--------------------
package com.ihub.www;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;
import java.text.SimpleDateFormat;

public class DateRetrieveApp 
{
	public static void main(String[] args)throws Exception  
	{
		Class.forName("oracle.jdbc.driver.OracleDriver");
		Connection con = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE","system","admin");
		Statement st = con.createStatement();
		String qry = "select * from emp1";
		ResultSet rs = st.executeQuery(qry);
		while(rs.next())
		{
			int id = rs.getInt(1);
			String name = rs.getString(2);
			java.sql.Date sqldoj = rs.getDate(3);
			
			//converting sql date to util date 
			java.util.Date udoj = (java.util.Date) sqldoj;
			
			//converting util date to string date 
			SimpleDateFormat sdf = new SimpleDateFormat("dd-MM-yyyy");
			String sdoj = sdf.format(udoj);
			
			System.out.println(id+" "+name+" "+sdoj);
		}
		
		rs.close();
		st.close();
		con.close();
	}
}

String program 
==============
package com.ihub.www;

public class StringApp 
{
	public static void main(String[] args)
	{
		String str="hello1";
		
		if(str.matches("[A-Za-z]+"))
			System.out.println("All are alphabets");
		else
			System.out.println("All are not alphabets");
	}
}


ex:
---
package com.ihub.www;

public class StringApp 
{
	public static void main(String[] args)
	{
		String[] sarr = {"apple","banana","cat"};
		
		String result = String.join(" | ", sarr);
		
		System.out.println(result);
	}
}

Assignment 
==========
Q) Write a jdbc application to read the records from student table using PreparedStatement object.
