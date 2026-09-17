HTML based form page to servlet communication 
=============================================
Diagram: servlet4.1

Deployment Directory Structure 
------------------------------
VoteApp
|
|---Java Resources
	|
	|------src
		|
		|---com.ihub.www
			|
			|---VoteSrv.java
|---WebContent
	|
	|----form.html
	|----WEB-INF
		|
		|----web.xml 
Note:
-----
In above application we need to add "servlet-api.jar" file in project build path.		
We can send the request to servlet program in two methodologies.

1) GET Methodology 
-----------------
	It carries limited amount of data.

2) POST Methodology 
------------------
	It carries unlimited amount of data.

While working HttpServlet , it is never recommanded to use service(-,-) because it is not designed according to HTTP protocol.

It is recommanded to use doXxx(-,-) methods because they have designed according to HTTP protocol.

We have following seven doXxx(-,-) methods.
ex:
	doGet(-,-)
	doPost(-,-)
	doPut(-,-)
	doHead(-,-)
	doDelete(-,-)
	doOption(-,-)
	doTrace(-,-)

Prototype of doXxx(-,-) method
------------------------------
protected void doGet(HttpServletRequest req,HttpServletResponse res)throws 
				ServletException,IOException
{
		
}
	
form.html
---------

<form action="test" method="GET">
	
	<table align="center">
		<tr>
			<td>Name:</td>
			<td><input type="text" name="t1"/></td>
		</tr>
		<tr>
			<td>Age:</td>
			<td><input type="text" name="t2"/></td>
		</tr>
		<tr>
			<td><input type="reset" value="reset"/></td>
			<td><input type="submit" value="submit"/></td>
		</tr>	
	</table>
	
</form>		

web.xml
-------
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" id="WebApp_ID" version="4.0">
  
  <display-name>VoteApp</display-name>
  
  <welcome-file-list>
  	<welcome-file>form.html</welcome-file>
  </welcome-file-list>
  
</web-app>

VoteSrv.java
-------------
package com.ihub.www;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet(urlPatterns = "/test", name = "VoteSrv")
public class VoteSrv extends HttpServlet
{
	protected void doGet(HttpServletRequest req,HttpServletResponse res)throws ServletException,IOException 
	{
		PrintWriter pw = res.getWriter();
		res.setContentType("text/html");
		
		//reading form data 
		String name = req.getParameter("t1");
		String sage = req.getParameter("t2");
		
		//convert string age to int age 
		int age = Integer.parseInt(sage);
		
		if(age<18)
			pw.println("<center><h1 style='color:red'>"+name+" U r not eligible to vote </h1></center>");
		else
			pw.println("<center><h1 style='color:green'>"+name+" U r eligible to vote </h1></center>");
		
		pw.close();
	}
}

Request url
----------
	http://localhost:2525/VoteApp/




Servlet to Database Communication 
=================================
Diagram: servlet4.2

Deployment Directory Structure 
------------------------------
DBApp
|
|----Java Resources
	|
	|------src
		|
		|---com.ihub.www
			|
			|---TestSrv.java
|----WebContent
	|
	|---form.html	
	|---WEB-INF
		|
		|------web.xml 	
		|------lib
			|
			|---ojdbc14.jar
Note:
-----
In above project we need to add "servlet-api.jar" and "ojdbc14.jar" file in project build path.

student table 
==============
drop table student;
create table student(sno number(3),sname varchar2(10),sadd varchar2(12));

form.html
---------

<form action="test" method="GET">
	
	<table align="center">
		<tr>
			<td>No:</td>
			<td><input type="text" name="t1"/></td>
		</tr>
		<tr>
			<td>Name:</td>
			<td><input type="text" name="t2"/></td>
		</tr>
		<tr>
			<td>Address:</td>
			<td><input type="text" name="t3"/></td>
		</tr>
		<tr>
			<td><input type="reset" value="reset"/></td>
			<td><input type="submit" value="submit"/></td>
		</tr>
	</table>
	
</form>

web.xml
-------
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" id="WebApp_ID" version="4.0">
  
  <display-name>DBApp</display-name>
  
  <welcome-file-list>
  	<welcome-file>form.html</welcome-file>
  </welcome-file-list>
  
</web-app>

TestSrv.java
-------------
package com.ihub.www;

import java.io.IOException;
import java.io.PrintWriter;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet(urlPatterns = "/test", name="TestSrv")
public class TestSrv extends HttpServlet
{
	protected void doGet(HttpServletRequest req,HttpServletResponse res)throws ServletException,IOException
	{
		PrintWriter pw =res.getWriter();
		res.setContentType("text/html");
		
		//reading form data 
		String sno = req.getParameter("t1");
		int no = Integer.parseInt(sno);
		String name = req.getParameter("t2");
		String add = req.getParameter("t3");
		
		//store the data into database 
		Connection con = null;
		PreparedStatement ps = null;
		int result = 0;
		String qry = null;
		try
		{
			Class.forName("oracle.jdbc.driver.OracleDriver");
			con = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE","system","admin");
			qry = "insert into student values(?,?,?)";
			ps = con.prepareStatement(qry);
			//set the values 
			ps.setInt(1, no);
			ps.setString(2, name);
			ps.setString(3, add);
			//execute 
			result = ps.executeUpdate();
			if(result==0)
				pw.println("<center><h1>Record Not Inserted</h1></center>");
			else
				pw.println("<center><h1>Record Inserted</h1></center>");
			
			ps.close();
			con.close();
		}
		catch(Exception e)
		{
			pw.println(e);
		}
		
	}
}

Request url
-----------
	http://localhost:2525/DBApp/
