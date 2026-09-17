MIME Types 
==========
MIME stands for Multipurpose Internet Mail Extension.

MIME describes in how many formats we can display the output in servlets.

There are four formats to display the output in servlets.

1) text/html 
-----------
	It is used to display the output in HTML format.

2) text/xml 
------------
	It is used to display the output in XML format.

3) application/ms-word 
----------------------
	It is used to display the output in word format.

4) application/vnd.ms-excel
----------------------------
	It is used to display the output in excel format.
 



@WebServlet annotation 
======================
@WebServlet annotation introduced in Servlet 3.0.

@WebServlet annotation present in javax.servlet.annotation package.

It is a class level annotation.

It is used to declare the configuration of a servlets.




Deployment Directory Structure 
==============================
MIMEApp
|
|----Java Resources
|	|
	|------src
		|
		|---com.ihub.www
			|
			|---TestSrv1.java
			|---TestSrv2.java
			|---TestSrv3.java
			|---TestSrv4.java
|----WebContent
	|
	|---WEB-INF
		|
		|---web.xml 	
Note:
-----
In above application we need to add "servlet-api.jar" file in project build path.


TestSrv1.java
-------------
package com.ihub.www;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.GenericServlet;
import javax.servlet.ServletException;
import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;
import javax.servlet.annotation.WebServlet;

@WebServlet(urlPatterns = "/html", name = "TestSrv1")
public class TestSrv1 extends GenericServlet 
{
	public void service(ServletRequest req,ServletResponse res)throws ServletException,IOException
	{
		PrintWriter pw =res.getWriter();
		res.setContentType("text/html");
		
		pw.println("<table border='1'>");
		pw.println("<tr><th>No</th><th>Name</th><th>Address</th></tr>");
		pw.println("<tr><td>101</td><td>Alan</td><td>Florida</td></tr>");
		pw.println("<tr><td>102</td><td>Jose</td><td>Texas</td></tr>");
		pw.println("<tr><td>103</td><td>Mark</td><td>Chicago</td></tr>");
		pw.println("</table>");
		
		pw.close();
	}
}

TestSrv2.java
--------------
package com.ihub.www;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.GenericServlet;
import javax.servlet.ServletException;
import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;
import javax.servlet.annotation.WebServlet;

@WebServlet(urlPatterns = "/xml", name = "TestSrv2")
public class TestSrv2 extends GenericServlet 
{
	public void service(ServletRequest req,ServletResponse res)throws ServletException,IOException
	{
		PrintWriter pw =res.getWriter();
		res.setContentType("text/xml");
		
		pw.println("<table border='1'>");
		pw.println("<tr><th>No</th><th>Name</th><th>Address</th></tr>");
		pw.println("<tr><td>101</td><td>Alan</td><td>Florida</td></tr>");
		pw.println("<tr><td>102</td><td>Jose</td><td>Texas</td></tr>");
		pw.println("<tr><td>103</td><td>Mark</td><td>Chicago</td></tr>");
		pw.println("</table>");
		
		pw.close();
	}
}

TestSrv3.java
---------------
package com.ihub.www;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.GenericServlet;
import javax.servlet.ServletException;
import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;
import javax.servlet.annotation.WebServlet;

@WebServlet(urlPatterns = "/word", name = "TestSrv3")
public class TestSrv3 extends GenericServlet 
{
	public void service(ServletRequest req,ServletResponse res)throws ServletException,IOException
	{
		PrintWriter pw =res.getWriter();
		res.setContentType("application/ms-word");
		
		pw.println("<table border='1'>");
		pw.println("<tr><th>No</th><th>Name</th><th>Address</th></tr>");
		pw.println("<tr><td>101</td><td>Alan</td><td>Florida</td></tr>");
		pw.println("<tr><td>102</td><td>Jose</td><td>Texas</td></tr>");
		pw.println("<tr><td>103</td><td>Mark</td><td>Chicago</td></tr>");
		pw.println("</table>");
		
		pw.close();
	}
}


TestSrv4.java
-------------
package com.ihub.www;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.GenericServlet;
import javax.servlet.ServletException;
import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;
import javax.servlet.annotation.WebServlet;

@WebServlet(urlPatterns = "/excel", name = "TestSrv4")
public class TestSrv4 extends GenericServlet 
{
	public void service(ServletRequest req,ServletResponse res)throws ServletException,IOException
	{
		PrintWriter pw =res.getWriter();
		res.setContentType("application/vnd.ms-excel");
		
		pw.println("<table border='1'>");
		pw.println("<tr><th>No</th><th>Name</th><th>Address</th></tr>");
		pw.println("<tr><td>101</td><td>Alan</td><td>Florida</td></tr>");
		pw.println("<tr><td>102</td><td>Jose</td><td>Texas</td></tr>");
		pw.println("<tr><td>103</td><td>Mark</td><td>Chicago</td></tr>");
		pw.println("</table>");
		
		pw.close();
	}
}

web.xml
--------
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" id="WebApp_ID" version="4.0">
  <display-name>MIMEApp</display-name>
</web-app>	


request url
----------
	http://localhost:2525/MIMEApp/html 
	http://localhost:2525/MIMEApp/xml 
	http://localhost:2525/MIMEApp/word
	http://localhost:2525/MIMEApp/excel



Types of communication 
======================
We can communicate with servlet program in three ways.

1) Browser to servlet communication 

2) HTML to servlet communication 

3) Servlet to Servlet communication 

In browser to servlet communication we need to type request url in browser address.

Typing request url in browser address bar is quit complex.

To overcome this limitation we need to use HTML to servlet communication.

In HTML to servlet communication we can give the request to servlet program by using HTML based hyperlinks and form pages.

In HTML based hyperlink to servlet communication we need to type our request url as href url.
ex:
	<a href="http://localhost:2525/MIMEApp/html"> clickme </a>

In HTML based form page to servlet communication we need to type our request url as action url.
ex:
	<form action="http://localhost:2525/MIMEApp/html">
		-
		-
	</form>

A request which is generated by using hyperlink does not carry the data.

A request which is generated by using form page will carry the data.



HTML based Hyperlink to Servlet Communication 
==============================================
Diagram: servlet3.1

Deployment Directory Structure 
------------------------------
WishApp
|
|----Java Resources
	|	
	|------src
		|
		|---com.ihub.www
			|
			|---WishSrv.java
|
|---WebContent
	|
	|---index.html
	|---WEB-INF
		|
		|--web.xml 
Note:
-----
In above application we need to add "servlet-api.jar" file in project build path.

It is never recommanded to extends a class with GenericServlet class because it won't give HTTP protocol features.

It is recommanded to extends a class with HttpServlet  class because it gives HTTP protocol features.


index.html
----------
<center>
	<h1>
		<a href="test"> getMsg </a>
	</h1>
</center>

web.xml
-------
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" id="WebApp_ID" version="4.0">
  
  <display-name>WishApp</display-name>
  
  <welcome-file-list>
  	<welcome-file>index.html</welcome-file>
  </welcome-file-list>
  
</web-app>


WishSrv.java
----------
package com.ihub.www;

import java.io.IOException;
import java.io.PrintWriter;
import java.util.Calendar;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet(urlPatterns = "/test", name = "WishSrv")
public class WishSrv extends HttpServlet
{
	public void service(HttpServletRequest req,HttpServletResponse res)throws ServletException,IOException
	{
		PrintWriter pw =res.getWriter();
		res.setContentType("text/html");
		
		Calendar c = Calendar.getInstance();
		int h = c.get(Calendar.HOUR_OF_DAY);
		if(h<12)
			pw.println("<center><h1>Good Morning</h1></center>");
		else if(h<16)
			pw.println("<center><h1>Good Afternoon</h1></center>");
		else if(h<20)
			pw.println("<center><h1>Good Evening</h1></center>");
		else
			pw.println("<center><h1>Good Night</h1></center>");
		
		pw.close();
	}
}

Request url
------------
	http://localhost:2525/WishApp/
