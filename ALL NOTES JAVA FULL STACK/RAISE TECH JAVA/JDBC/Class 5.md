SQL Injection Problem 
=====================
Along with input values if we pass special SQL instructions which change the behaviour of a query and behaviour of an application is called SQL injection problem.

Here special SQL instructions means comment in SQL (i.e --).

ex:
	Enter the username : raja'--
	Enter the password : pooja

	Valid Credentials 

While dealing with simple Statement object there is a chance of raising SQL injection problem.

To overcome this limitation we need to use PreparedStatement object.


userlist table 
==============
drop table userlist;
create table userlist(uname varchar2(10), pwd varchar2(10));
insert into userlist values('raja','rani');
insert into userlist values('king','kingdom');
commit;


ex:
---
package com.ihub.www;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;
import java.util.Scanner;

public class SQLInjProbApp 
{
	public static void main(String[] args)throws Exception  
	{
		Scanner sc = new Scanner(System.in);
		
		System.out.println("Enter the username :");
		String name = sc.next();
		
		System.out.println("Enter the password :");
		String pass = sc.next();
		
		//converting inputs according to SQL query 
		name="'"+name+"'";
		pass="'"+pass+"'";
		
		Class.forName("oracle.jdbc.driver.OracleDriver");
		Connection con = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE","system","admin");
		Statement st = con.createStatement();
		
		String qry = "select count(*) from userlist where uname="+name+" and pwd="+pass;
		
		ResultSet rs = st.executeQuery(qry);
		int result = 0;
		while(rs.next())
		{
			result = rs.getInt(1);
		}
		if(result==0)
			System.out.println("Invalid Credentials");
		else
			System.out.println("Valid Credentials");
		
		rs.close();
		st.close();
		con.close();
	}
}


Type1 JDBC Driver Architecture / JDBC-ODBC Bridge Driver 
=========================================================
Type1 JDBC driver is not designed to interact with database software directly.

It is designed to take the support of ODBC Driver and Vendor DB library to locate and interact with database software.

Diagram: jdbc5.1

Advantages:

> Using Type1 JDBC driver we can interact with any database software.

> It is a built-in driver of JDK.

Disadvantages:

> This driver performance is low. It is not suitable for medium and large scale 
  projects. Hence it is not a industry standard driver.

> To use Type1 JDBC driver we need to arrange ODBC driver and Vendor DB library 
  seperately.

> Since ODBC driver and Vendor DB library present at client side so it is not 
  suitable for untrusted applets to database communication.


Type2 JDBC Driver Architecture / Native API 
============================================
Type2 JDBC driver is not designed to interact with database software directly.

It is designed to take the support of Vendor DB library to locate and interact with database software.

Diagram: jdbc5.2

Advantages:

> Type2 JDBC driver will not take the support of ODBC driver.

> It gives better performance when compare to Type1 JDBC driver.

Disadvantages:

> This driver performance is quit slow. It is not suitable for medium and large 
  scale projects. Hence it is not a industry standard driver.

> To work with Type2 JDBC driver we need to arrange Vendor DB library seperately.

> Since Vendor DB library present at client side so it is not suitable for 
  untrusted applets to database communication.

> For every database we need to arrange Type2 JDBC driver seperately.


Type4 JDBC Driver Architecture / Native Protocol / Thin Driver
==============================================================
Type4 JDBC driver is not designed to take the support of ODBC driver and Vendor DB library. 

It is designed to locate and interact with database software directly.

Diagram: jdbc5.3

Advantages:

> This driver gives better performance when compare to Type1 and Type2 driver.

> It is developed by using java so it gives platform independency.

> It does not take the support of ODBC Driver and Vendor DB library.

> Since ODBC driver and Vendor DB library not present at client side so it is 
  suitable for untrusted applets to database communication.

> It is suitable for medium and large scale projects. Hence it is a industry 
  standard driver.

Disadvantages:

> It is not a built-in driver of JDK.

> For every database we need to arrange Type4 jdbc driver seperately.
