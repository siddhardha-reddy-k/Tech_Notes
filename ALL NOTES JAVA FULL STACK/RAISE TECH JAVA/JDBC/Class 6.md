JDBC Connection Pool 
====================
It is a factory containing set of readily available JDBC Connection object before actual being used.

JDBC Connection pool represent connectivity with same database software.

Diagram: jdbc6.1

Advantages:

> With minimum number of connection object we can interact with multiple clients.

> It gives reusable JDBC Connection objects.

> A programmer is not responsible to create, manage and destory JDBC Connection 
  object. A JDBC Connection pool is responsible.

Type3 JDBC Driver Architecture / Net Protocol 
=============================================
A web server, proxy server or IDE's server contains JDBC Connection pool.

Type3 JDBC driver is not designed to interact with database software directly.

It is designed to interact with web server, proxy server or IDE's server to get one reusable JDBC Connection object from Connection pool. 

Diagram: jdbc6.2


With respect to the diagram
----------------------------
> Web Server or Proxy Server or IDE's server interacts with database software to
  get some JDBC Connection objects in JDBC connection pool.

> Using Type3 driver we interacts with web server or proxy server or IDE's server   
  to get one resuable JDBC Connection object from JDBC connection pool.

> Our application uses JDBC Connection object to create other JDBC connection
  objects.

> Once if we call con.close(), Connection object goes back to JDBC Connection pool.

Q) Types of JDBC Connection objects ? 

We have two types of JDBC Connection objects.

1) Direct JDBC Connection object 
-------------------------------
A JDBC Connection object which is created by the user based on the application requirements is called direct JDBC Connection object.
ex:
	Class.forName("driver-class-name");
	Connection con = DriverManager.getConnection("url","username","password");

2) Pooled JDBC Connection object
---------------------------------
A JDBC Connection object which is gathered from JDBC Connection pool.



Q) Types of Statement objects in JDBC?

We have three Statement objects in JDBC.

1) Simple Statement object 
-----------------------
It is an object of underlying supplied java class which implements java.sql.Statement interface.

2) PreparedStatement object 
--------------------------
It is an object of underlying supplied java class which implements java.sql.PreparedStatement interface.

3) CallableStatement object 
---------------------------
It is an object of underlying supplied java class which implements java.sql.CallableStatement interface.

Limitations with Simple Statement object 
========================================

1) It is not suitable to execute same query for multiple times with same or 
   different values.

2) It raises SQL injection problem.

3) Framing query with variables is quit complex.

4) We can't use string values without any conversion.

5) It does not allow us to insert date values to database table column.

6) It does not allow us to insert LOB values to database table column.

To overcome above limitations we need to use PreparedStatement object.


Working with PreparedStatement object
=====================================
step1:
------
	Create a query with placeholders or parameters.
	ex:
		String qry = "insert into student values(?,?,?)";

step2:
------
	Convert SQL query to pre-compiled SQL query.
	ex:	
		PreparedStatement ps = con.prepareStatement(qry);

step3:
-----
	Set the values to query parameters.
	ex:	
		ps.setInt(1,no);
		ps.setString(2,name);
		ps.setString(3,add);

step4:
-----
	Execute pre-compiled SQL Query.
	ex:
		ps.executeUpdate();

step5:
------
	Close PreparedStatement object.
	ex:
		ps.close();

Q) Write a JDBC application to insert a record into student table?

package com.ihub.www;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.util.Scanner;

public class PSInsertApp 
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
		
		Class.forName("oracle.jdbc.driver.OracleDriver");
		Connection con = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE","system","admin");
		
		String qry = "insert into student values(?,?,?)";
		
		PreparedStatement ps = con.prepareStatement(qry);
		
		//set the values
		ps.setInt(1, no);
		ps.setString(2, name);
		ps.setString(3, add);
		
		//execute 
		int result = ps.executeUpdate();
		
		if(result==0)
			System.out.println("No Record Inserted");
		else
			System.out.println("Record Inserted");
		
		ps.close();
		con.close();
	}
}


Q) Write a JDBC application to update student name based on student number?


package com.ihub.www;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.util.Scanner;

public class PSUpdateApp
{
	public static void main(String[] args)throws Exception  
	{
		Scanner sc = new Scanner(System.in);
		System.out.println("Enter the student no :");
		int no = sc.nextInt();
		
		System.out.println("Enter the student name :");
		String name = sc.next();
		
		Class.forName("oracle.jdbc.driver.OracleDriver");
		Connection con = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE","system","admin");
		
		String qry = "update student set sname=? where sno=?";
		
		PreparedStatement ps = con.prepareStatement(qry);
		
		//set the values
		ps.setString(1, name);
		ps.setInt(2,no);
		
		int result = ps.executeUpdate();
		
		if(result==0)
			System.out.println("No Record Updated");
		else
			System.out.println("Record Updated");
		
		ps.close();
		con.close();
	}
}


Q) Write a JDBC Application to delete student record based on student number?

package com.ihub.www;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.util.Scanner;

public class PSDeleteApp 
{
	public static void main(String[] args)throws Exception 
	{
		Scanner sc = new Scanner(System.in);
		System.out.println("Enter the student no :");
		int no = sc.nextInt();
		
		Class.forName("oracle.jdbc.driver.OracleDriver");
		Connection con = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE","system","admin");
		
		String qry = "delete from student where sno=?";
		
		PreparedStatement ps = con.prepareStatement(qry);
		
		//set the values
		ps.setInt(1, no);
		
		//execute 
		int result = ps.executeUpdate();
		
		if(result==0)
			System.out.println("No Record Deleted");
		else
			System.out.println("Record Deleted");
		
		ps.close();
		con.close();
	}
}
