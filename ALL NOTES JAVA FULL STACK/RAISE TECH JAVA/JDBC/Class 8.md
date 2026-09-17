Working with LOB values
=======================
Files are known as LOB's.

We have two types of LOB's.

1) BLOB (Binary Large Object)
----------------------------
	ex:
		Images, Audio, Video, Avi file and etc.

2) CLOB (Character Large Object)
--------------------------------
	ex:
		Text file, Advanced text file and etc.

Using simple Statement object we can place LOB values to query parameters.

To overcome this limitation we need to use PreparedStatement object.

We can set the LOB values to query parameter by using following methods.
ex:
	ps.setBLOB(-,-,-) / ps.setBinaryStream(-,-,-)
	ps.setCLOB(-,-,-) / ps.setCharacterStream(-,-,-)

emp2 table 
===========
drop table emp2;
create table emp2(eid number(3),ename varchar2(10),ephoto BLOB);


PhotoInsertApp.java
-------------------
package com.ihub.www;

import java.io.File;
import java.io.FileInputStream;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.util.Scanner;

public class PhotoInsertApp 
{
	public static void main(String[] args)throws Exception  
	{
		Scanner sc = new Scanner(System.in);
		
		System.out.println("Enter the employee id :");
		int id = sc.nextInt();
		
		System.out.println("Enter the employee name :");
		String name = sc.next();
		
		//find and locate a photo 
		File f = new File("src/com/ihub/www/srinivasa.jfif");
		FileInputStream fis = new FileInputStream(f); 
		
		Class.forName("oracle.jdbc.driver.OracleDriver");
		Connection con = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE","system","admin");
	
		String qry = "insert into emp2 values(?,?,?)";
		
		PreparedStatement ps = con.prepareStatement(qry);
		
		//set the values
		ps.setInt(1, id);
		ps.setString(2, name);
		ps.setBinaryStream(3, fis, (int)f.length());
		
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

PhotoRetrieveApp.java
---------------------
package com.ihub.www;

import java.io.FileOutputStream;
import java.io.InputStream;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;

public class PhotoRetrieveApp 
{
	public static void main(String[] args)throws Exception  
	{
		Class.forName("oracle.jdbc.driver.OracleDriver");
		Connection con = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE","system","admin");
		Statement st = con.createStatement();
		String qry = "select * from emp2";
		ResultSet rs = st.executeQuery(qry);
		while(rs.next())
		{
			InputStream is = rs.getBinaryStream(3);
			FileOutputStream fos = new FileOutputStream("D:\\sudheer.jpg");
			int byteReads = 0;
			byte[] buff = new byte[100];
			
			while((byteReads = is.read(buff))!=-1)
			{
				fos.write(buff, 0 , byteReads);
			}
			fos.close();
		}
		System.out.println("Please check the location");
		rs.close();
		st.close();
		con.close();
	}
}

Working with properties file 
============================
In regular intervals, DBA will change username and password for security reason. 

It is never recommanded to pass database properties directly to the application.

It is always recommanded to read database properties from properties file.

A properties file contains key and value pair.

dbdetails.properties 
--------------------
driver=oracle.jdbc.driver.OracleDriver 
url=jdbc:oracle:thin:@localhost:1521:XE 
username=system 
password=admin 

PropertiesApp.java
-------------------
package com.ihub.www;

import java.io.FileInputStream;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;
import java.util.Properties;

public class PropertiesApp 
{
	public static void main(String[] args)throws Exception  
	{
		//find and locate properties file 
		FileInputStream fis = new FileInputStream("src/com/ihub/www/dbdetails.properties");
		
		// Create Properties class object 
		Properties p = new Properties();
		
		//loading data from file to class
		p.load(fis);
		
		//reading data from properties class
		String s1 = p.getProperty("driver");
		String s2 = p.getProperty("url");
		String s3 = p.getProperty("username");
		String s4 = p.getProperty("password");
		
		Class.forName(s1);
		Connection con = DriverManager.getConnection(s2,s3,s4);
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

JDBC Flexible Application 
=========================
In JDBC, Connection object consider as heavy weight object.

It is never recommanded to create Connection object for every JDBC application.

It is recommanded to create a seperate class which returns Connection object.

DBConnection.java
-----------------
package com.ihub.www;

import java.sql.Connection;
import java.sql.DriverManager;

public class DBConnection 
{
	static Connection con = null;
	
	private DBConnection(){}
	
	public static Connection getConnection()
	{
			try
			{
				Class.forName("oracle.jdbc.driver.OracleDriver");
				if(con==null)
				{
					con = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE","system","admin");
				}
			}
			catch(Exception e)
			{
				e.printStackTrace();
			}
			return con;
	}
}



FlexibleApp.java
-----------------
package com.ihub.www;

import java.sql.Connection;
import java.sql.DriverManager;

public class DBConnection 
{
	static Connection con = null;
	
	private DBConnection(){}
	
	public static Connection getConnection()
	{
			try
			{
				Class.forName("oracle.jdbc.driver.OracleDriver");
				if(con==null)
				{
					con = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE","system","admin");
				}
			}
			catch(Exception e)
			{
				e.printStackTrace();
			}
			return con;
	}
}


Thin-Client/Fat-Server Application 
==================================
Every JDBC application consider as thin-client/fat-server application.

Diagram: jdbc8.1

To create a thin-client/fat-server application we need to keep business logic and persistence logic in database software in the form of stored PL/SQL procedures and functions. 

To deal with stored PL/sQL procedures and functions we need to use CallableStatement object.

PL/SQL Procedure 
================
create or replace procedure first_proc(A IN number,B IN number,C OUT number)
is
begin 
C:=a+b;
end;
/

ex:
---

package com.ihub.www;

import java.sql.CallableStatement;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.Types;

public class CallableStmtApp1 
{
	public static void main(String[] args)throws Exception 
	{
		Class.forName("oracle.jdbc.driver.OracleDriver");
		Connection con = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE","system","admin");
		CallableStatement cst = con.prepareCall("{CALL first_proc(?,?,?)}");
		
		//register OUT parameter 
		cst.registerOutParameter(3, Types.INTEGER);
		
		//set the values to IN parameter
		cst.setInt(1, 10);
		cst.setInt(2, 20);
		
		//execute 
		cst.execute();
		
		//gather the result
		int result = cst.getInt(3);
		
		System.out.println("Sum of two numbers ="+result);
		
		cst.close();
		con.close();
	}
}

PL/SQL function 
---------------
create or replace function ret_sum(A number,B number)
return number
is
c number;
begin
C:=A+B;
return C;
end;
/

ex:
---
package com.ihub.www;

import java.sql.CallableStatement;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.Types;

public class CallableStmtApp2
{
	public static void main(String[] args)throws Exception  
	{
		Class.forName("oracle.jdbc.driver.OracleDriver");
		Connection con = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE","system","admin");
		CallableStatement cst = con.prepareCall("{?=call ret_sum(?,?)}");
		
		//register OUT parameter
		cst.registerOutParameter(1, Types.INTEGER);
		
		//set the IN parameters
		cst.setInt(2, 30);
		cst.setInt(3, 40);
		
		//execute 
		cst.execute();
		
		//gather the reult 
		int result = cst.getInt(1);
		
		System.out.println("sum of two numbers is ="+result);
		
		cst.close();
		con.close();
	}
}
