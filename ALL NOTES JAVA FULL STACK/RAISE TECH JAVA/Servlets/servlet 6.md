ServletContext object 
=====================
ServletContext is an interface which is present in javax.servlet package.

ServletContext object is created by web container for every web application.

ServletContext object is used to read configuration information from web.xml file which is global.

We can create ServletContext object as follow.

ex:
	ServletConfig config = getServletConfig();
	ServletContext context = config.getServletContext();

	or 

	ServletContext context = getServletContext();

ServletContext interface contains following methods.


1) public String getInitParameter(String name)
---------------------------------------
	It returns initialized parameter value based on parameter name.

2) public Enumeration getInitParameterNames()
--------------------------------------------
	It returns Enumeration of initialized parameters.

3) public void setAttribute(String name,Object object)
----------------------------------
	It is used to add the attributes to context.

4) public String getAttribute(String name)
------------------------------------------
	It is used to read the attributes from context.

5) public void removeAttribute(String name) 
-----------------------------------------	
	It is used to remove the attributes from context.

Deployment Directory Structure 
------------------------------
ContextApp
|
|---Java Resources
	|
	|------src
		|
		|---com.ihub.www
			|
			|---TestSrv.java
|---WebContent
	|
	|---index.html 
	|---WEB-INF
		|
		|---web.xml 
Note:
-----
In above application we need to add "servlet-api.jar " file in project build path.


index.html
----------
<center>
	<h1>
		<a href="test"> clickMe </a>
	</h1>
</center>

web.xml 
-------
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" id="WebApp_ID" version="4.0">
  <display-name>ContextApp</display-name>
  
  <welcome-file-list>
  	<welcome-file>index.html</welcome-file>
  </welcome-file-list>
  
  
  <context-param>
  		<param-name>driver</param-name>
  		<param-value>oracle.jdbc.driver.OracleDriver</param-value>
  </context-param>
  <context-param>
  		<param-name>url</param-name>
  		<param-value>jdbc:oracle:thin:@localhost:1521:XE</param-value>
  </context-param>
  
</web-app>

TestSrv.java
-------------
package com.ihub.www;

import java.io.IOException;
import java.io.PrintWriter;
import java.util.Enumeration;

import javax.servlet.ServletContext;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet(urlPatterns = "/test", name = "TestSrv")
public class TestSrv extends HttpServlet 
{
	protected void doGet(HttpServletRequest req,HttpServletResponse res)throws ServletException,IOException
	{
		PrintWriter pw =res.getWriter();
		res.setContentType("text/html");
		
		ServletContext context = getServletContext();
		
		pw.println(context.getInitParameter("driver")+"<br>");
		pw.println(context.getInitParameter("url")+"<br>");
		
		Enumeration<String> e = context.getInitParameterNames();
		while(e.hasMoreElements())
		{
			String s = e.nextElement();
			pw.println(s+"<br>");
		}
		
		context.setAttribute("username", "system");
		context.setAttribute("password", "admin");
		
		pw.println(context.getAttribute("username")+"<br>");
		pw.println(context.getAttribute("password")+"<br>");
		
		context.removeAttribute("username");
		context.removeAttribute("password");
		pw.close();
	}
}

Request url
-------------
	http://localhost:2525/ContextApp/

Servlet to Servlet Communication 
=================================
Servlet to servlet communication is also known as servlet chaining.

Servlet to servlet communication is possible by using following ways.

1) Forwarding the request 

2) Including the response 

3) Send Redirection 


4) Forwarding the request 
-------------------------
In forwarding the request, the output of source servlet program will be discarded and output of destination servlet program goes to browser window as dynamic response.

To forward the request , we need to use RequestDispatcher object.

RequestDispatcher is an interface which is present in javax.servlet package.

We can create RequestDispatcher object as follow.
ex:
	RequestDispatcher rd = req.getRequestDispatcher("url");
	rd.forward(req,res);



2) Including the response
-------------------------
In including the response, the output of source servlet program and destination servlet program combinely go to browser window as dynamic response. 

To include the response , we need to use RequestDispatcher object.

RequestDispatcher is an interface which is present in javax.servlet package.

We can create RequestDispatcher object as follow.
ex:
	RequestDispatcher rd = req.getRequestDispatcher("url");
	rd.include(req,res);


Deployment Directory Structure 
-------------------------------
STSApp1
|
|---Java Resources
	|
	|-------src
		|
		|---com.ihub.www
			|
			|---TestSrv1.java
			|---TestSrv2.java
|---WebContent
	|
	|---form.html
	|---WEB-INF
		|
		|---web.xml 
Note:
------
In above application we need to add "servlet-api.jar" file in project build path.

form.html
---------

<form action="test1">
	
	<table align="center">
		<tr>
			<td>UserName:</td>
			<td><input type="text" name="t1"/></td>
		</tr>
		<tr>
			<td>Password:</td>
			<td><input type="password" name="t2"/></td>
		</tr>
		<tr>
			<td><input type="reset" value="reset"/></td>
			<td><input type="submit" value="login"/></td>
		</tr>
	</table>
	
</form>

web.xml
--------
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" id="WebApp_ID" version="4.0">
  
  <display-name>STSApp1</display-name>
  
  <welcome-file-list>
  	<welcome-file>form.html</welcome-file>
  </welcome-file-list>
  
</web-app>


TestSrv1.java
--------------
package com.ihub.www;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.RequestDispatcher;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet(urlPatterns = "/test1", name = "TestSrv1")
public class TestSrv1 extends HttpServlet
{
	protected void doGet(HttpServletRequest req,HttpServletResponse res)throws ServletException,IOException
	{
		PrintWriter pw =res.getWriter();
		res.setContentType("text/html");
		
		//reading form data 
		String name = req.getParameter("t1");
		String pass = req.getParameter("t2");
		
		if(pass.equals("admin"))
		{
			RequestDispatcher rd = req.getRequestDispatcher("test2");
			rd.forward(req, res);
		}
		else
		{
			pw.println("<center><b style='color:red'>Invalid! username or password</b></center>");
			RequestDispatcher rd = req.getRequestDispatcher("form.html");
			rd.include(req, res);
		}
		pw.close();
	}
}

TestSrv2.java
-------------
package com.ihub.www;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet(urlPatterns = "/test2", name = "TestSrv2")
public class TestSrv2 extends HttpServlet
{
	protected void doGet(HttpServletRequest req,HttpServletResponse res)throws ServletException,IOException
	{
		PrintWriter pw =res.getWriter();
		res.setContentType("text/html");
		
		pw.println("<center><h1>Login Done Successfully</h1></center>");
		pw.close();
	}
}

Request url
------------
	http://localhost:2525/STSApp1/
