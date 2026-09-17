3) Send Redirection 
===================
It is used to send the request to the application which is present in same server or different server.

It is used to send the response or errors to other resources.

To perform send redirection we need to use sendRedirect() method of HttpServletResponse object.
ex:
	res.sendRedirect(url);

Deployment Directory Structure 
------------------------------
STSApp2
|
|---Java Resources
	|
	|-----src
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
In above application we need to add "servlet-api.jar" file in project build path.

index.html
----------
<center>
	<h1>
		<a href="test?t1=flights"> Flights </a>
	</h1>
	<h1>
		<a href="test?t1=hotels"> Hotels </a>
	</h1>
	<h1>
		<a href="test?t1=railways"> Trains </a>
	</h1>
</center>

web.xml
--------
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" id="WebApp_ID" version="4.0">
 
  <display-name>STSApp2</display-name>
 
  <welcome-file-list>
  	<welcome-file>index.html</welcome-file>
  </welcome-file-list>
 
</web-app>

TestSrv.java
-------------
package com.ihub.www;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet(urlPatterns = "/test",name = "TestSrv")
public class TestSrv extends HttpServlet
{
	protected void doGet(HttpServletRequest req,HttpServletResponse res)throws ServletException,IOException
	{
		PrintWriter pw =res.getWriter();
		res.setContentType("text/html");
		
		//reading request parameter 
		String value = req.getParameter("t1");
		
		res.sendRedirect("https://www.makemytrip.com/"+value);
		
		pw.close();
		
	}
}

Request url
----------
	http://localhost:2525/STSApp2/



Servlet Filters 
===============
Filter is an object which is executed at the time of preprocessing and postprocessing of the request.

Diagram: servlet7.1

Filter is to perform filtering task such as

1) To count number of request coming to the application.

2) To perform form validation.

3) To perform encyrption and descryption.

Like Servlets , Filter having it's own API called Filter API.

A javax.servlet package gave three interfaces for Filter API.

1) Filter 

2) FilterChain 

3) FilterConfig 


1)Filter Interface
================
For creating any filter, we must and should implements the Filter interface.

Filter interface provides the following 3 life cycle methods for filter.


i)public void init(FilterConfig config)
----------------------------------
	
	IT is used to initialize the filter.
	It invokes only once .


ii)public void doFilter(HttpServletRequest req,HttpServletResponse res,FilterChain chain)
----------------------------------------------------------
	This method is invoked every time when user request to any resources to which
	the filter is mappend.

	IT is used to perform filtering task.	
	
iii)public void destroy()
---------------------------
	This method is invoked only once when filter is taken out of the service.


2)FilterChain
==============
It is responsible to invoke the next filter or resource in the chain.

FilterChain contains only one method.

i)public void doFilter(HttpServletRequest req,HttpServletResponse res)
------------------------------------
	It passes the control to the next filter or resource.

	
3)FilterConfig
===============
For every filter our servlet container creates FilterConfig object.
It is one per filter.


Deployment Directory Structure 
-------------------------------
FilterApp
|
|---Java Resources
	|	
	|------src
		|
		|---com.ihub.www
			|
			|---MyFilter.java
			|---MyServlet.java
|---WebContent
	|
	|---index.html
	|---WEB-INF
		|
		|---web.xml 
Note:
----
In above application we need to add "servlet-api.jar" file in project build path.

index.html
----------
<center>
	<h1>
		<a href="test"> clickMe </a>
	</h1>
</center>

web.xml
--------
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" id="WebApp_ID" version="4.0">
 
  <display-name>FilterApp</display-name>
 
  <welcome-file-list>
  	<welcome-file>index.html</welcome-file>
  </welcome-file-list>
 
</web-app>


MyFilter.java
--------------
package com.ihub.www;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.Filter;
import javax.servlet.FilterChain;
import javax.servlet.FilterConfig;
import javax.servlet.ServletException;
import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;
import javax.servlet.annotation.WebFilter;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebFilter(urlPatterns = "/test", filterName = "MyFilter")
public class MyFilter implements Filter
{
		@Override
		public void init(FilterConfig config)throws ServletException
		{
			
		}
		
		@Override
		public void doFilter(ServletRequest req,ServletResponse res, FilterChain chain)throws ServletException,IOException
		{
			PrintWriter pw =res.getWriter();
			res.setContentType("text/html");
			
			pw.println("<center><h1>Filter Invoked Before</h1></center>");
			chain.doFilter(req, res);
			pw.println("<center><h1>Filter Invoked After</h1></center>");
			pw.close();
		}
		@Override
		public void destroy()
		{
			
		}	
}

MyServlet.java
--------------
package com.ihub.www;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet(urlPatterns = "/test",name = "MyServlet")
public class MyServlet extends HttpServlet
{
	protected void doGet(HttpServletRequest req,HttpServletResponse res)throws ServletException,IOException
	{
		PrintWriter pw =res.getWriter();
		res.setContentType("text/html");
		
		pw.println("<center><h1>Servlet Invoked </h1></center>");
	}
}

Request url
-----------
	http://localhost:2525/FilterApp/




Servlet Life Cycle Methods
==========================
Servlet contains three life cycle methods.

1) public void init(ServletConfig config)throws ServletException
----------------------------------------------------------
	It is used for instantiation event.
	This method will execute just before servlet object creation.
	

2) public void service(ServletRequest req,ServletResponse res)
			throws ServletException,IOException
-------------------------------------------------------------
	It is used for request arrival event.
	This method will execute when request goes to servlet program.

3) public void destroy() 
--------------------------
	It is used for destruction event.
	This method will execute just before servlet object destruction.

Diagram: servlet7.2


Deployment Directory Structure 
-----------------------------
LifeCycleApp
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
----
In above application we need to add "servlet-api.jar" file in project build path.

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
  
  <display-name>LifeCycleApp</display-name>
  
  <welcome-file-list>
  	<welcome-file>index.html</welcome-file>
  </welcome-file-list>
  
</web-app>


TestSrv.java
-------------
package com.ihub.www;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletConfig;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet(urlPatterns = "/test", name = "TestSrv")
public class TestSrv extends HttpServlet 
{
	@Override 
	public void init(ServletConfig config)throws ServletException
	{
		
	}
	
	@Override
	public void service(HttpServletRequest req,HttpServletResponse res)throws ServletException,IOException
	{
		PrintWriter pw =res.getWriter();
		res.setContentType("text/html");
		
		pw.println("<center><h1>Servlet Life Cycle Methods</h1></center>");
		pw.close();
	}
	
	@Override 
	public void destroy()
	{
		
	}
}

Request run
-----------
	http://localhost:2525/LifeCycleApp/
