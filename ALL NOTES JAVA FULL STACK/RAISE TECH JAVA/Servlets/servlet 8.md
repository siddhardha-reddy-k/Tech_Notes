Q) How to enable load-on-startup and what happens if enable load-on-startup?

We can enable load-on-startup as follow.

ex:
	@WebServlet(urlPatterns = "/test", name = "TestSrv",loadOnStartup = 1)
	class  TestSrv extends HttpServlet 
	{
		-
		-
	}

If we enable load-on-startup then servlet container creates servlet object during the server startup or during the deployment of web application.

It means servlet container creates servlet object before we give the request.

Stateless behaviour of web application 
======================================
Diagram : servlet8.1

Above diagram demonstrate stateless behaviour of web application.

By default every servlet application is a stateless web application.

In stateless web application, we can't access previous request data while processing the current request during a session.

To overcome this limitation we need to use Session Tracking.

Deployment Directory Structure 
------------------------------
StatelessApp
|
|---Java Resources
	|
	|------src
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
-----
In above application we need to add "servlet-api.jar" file in project build path.

form.html
---------
<form action="test1">
	
	Name: <input type="text" name="t1"/> <br>
	
	Father Name : <input type="text" name="t2"/> <br>
	
	Maritial Status : 
	<input type="checkbox" name="t3" value="married"/> MARRIED
	<input type="checkbox" name="t3" value="single"/> SINGLE 
	<br>
	
	<input type="submit" value="submit"/>
	
</form>

web.xml
--------
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" id="WebApp_ID" version="4.0">
  
  <display-name>StatelessApp</display-name>
  
  <welcome-file-list>
  	<welcome-file>form.html</welcome-file>
  </welcome-file-list>
  
</web-app>

TestSrv1.java
-------------
package com.ihub.www;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet(urlPatterns = "/test1",name="TestSrv1",loadOnStartup = 1)
public class TestSrv1 extends HttpServlet
{
	protected void doGet(HttpServletRequest req,HttpServletResponse res)throws ServletException,IOException
	{
		PrintWriter pw =res.getWriter();
		res.setContentType("text/html");
		
		//reading form data 
		String name = req.getParameter("t1");
		String fname = req.getParameter("t2");
		String ms = req.getParameter("t3");
		
		if(ms.equals("married"))
		{
			pw.println("<form action='test2'>");
			pw.println("Spouse Name : <input type='text' name='f2t1'/> <br> ");
			pw.println("No of child : <input type='text' name='f2t2'/> <br> ");
			pw.println("<input type='submit' value='submit'/>");
			pw.println("</form>");
		}
		else
		{
			pw.println("<form action='test2'>");
			pw.println("When will u marry : <input type='text' name='f2t1'/> <br> ");
			pw.println("Why will u marry : <input type='text' name='f2t2'/> <br> ");
			pw.println("<input type='submit' value='submit'/>");
			pw.println("</form>");
		}
		pw.close();
	}
}

TestSrv2.java
--------------
package com.ihub.www;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet(urlPatterns = "/test2",name="TestSrv2",loadOnStartup = 2)
public class TestSrv2 extends HttpServlet
{
	protected void doGet(HttpServletRequest req,HttpServletResponse res)throws ServletException,IOException
	{
		PrintWriter pw =res.getWriter();
		res.setContentType("text/html");
		
		//reading form 1 data 
		String name = req.getParameter("t1");
		String fname = req.getParameter("t2");
		String ms = req.getParameter("t3");
		
		//reading form 2 data 
		String val1 = req.getParameter("f2t1");
		String val2 = req.getParameter("f2t2");
		
		pw.println("Form 1 Data :"+name+" "+fname+" "+ms+"<br>");
		pw.println("Form 2 Data :"+val1+" "+val2+"<br>");
		pw.close();
	}
}

Request url
----------
	http://localhost:2525/StatelessApp/


Session
========
A process of continue and related operations performed on a web application with multiple request and response is called session.

ex:
	Signin to gmail and signout from gmail is one session. 
	staring of java class and ending of java class is one session.

In stateless web application ,no web resource program can access previous request data while processing the current request during a session.

To overcome this limitation we need to use session tracking.


Session Tracking / Session Management 
=====================================
Session tracking makes our web application as statefull web application even though our HTTP protocol is stateless.

In stateless web application, no web resource program can access previous request data while processing the current request during a session.

In statefull web application , web resource programs can access previous request data while processing the current request during a session.

There are four techniques to perform session tracking.

1) Using hidden box fields

2) Using HttpCookies 

3) Using HttpSession with Cookies

4) URL Rewriting 

HttpSession
=============
HttpSession is an interface which is present in javax.servlet package.

In HttpSession for request a unique session id will be generated by web container to identify a user is a new user or existing user.

Diagram: servlet8.2

We can create HttpSession object as follow.
ex:
	HttpSession session = req.getSession(true);

The main objective of HttpSession object are 

1) To bind the objects.

2) To manipulate the data which is present in HttpSession.



Deployment Directory Structure 
------------------------------
SessionApp
|
|---Java Resources
	|
	|------src
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
-----
In above application we need to add "servlet-api.jar" file in project build path.


form.html
--------
<form action="test1">
	
	Name: <input type="text" name="t1"/> <br>
	
	Father Name : <input type="text" name="t2"/> <br>
	
	Maritial Status : 
	<input type="checkbox" name="t3" value="married"/> MARRIED
	<input type="checkbox" name="t3" value="single"/> SINGLE 
	<br>
	
	<input type="submit" value="submit"/>
	
</form>

web.xml
--------
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" id="WebApp_ID" version="4.0">
  
  <display-name>StatelessApp</display-name>
  
  <welcome-file-list>
  	<welcome-file>form.html</welcome-file>
  </welcome-file-list>
  
</web-app>


TestSrv1.java
-------------
package com.ihub.www;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;

@WebServlet(urlPatterns = "/test1",name="TestSrv1",loadOnStartup = 1)
public class TestSrv1 extends HttpServlet
{
	protected void doGet(HttpServletRequest req,HttpServletResponse res)throws ServletException,IOException
	{
		PrintWriter pw =res.getWriter();
		res.setContentType("text/html");
		
		//reading form data 
		String name = req.getParameter("t1");
		String fname = req.getParameter("t2");
		String ms = req.getParameter("t3");
		
		//add form 1 data to HttpSession object
		HttpSession session = req.getSession(true);
		session.setAttribute("pname", name);
		session.setAttribute("pfname", fname);
		session.setAttribute("pms", ms);
		
		if(ms.equals("married"))
		{
			pw.println("<form action='test2'>");
			pw.println("Spouse Name : <input type='text' name='f2t1'/> <br> ");
			pw.println("No of child : <input type='text' name='f2t2'/> <br> ");
			pw.println("<input type='submit' value='submit'/>");
			pw.println("</form>");
		}
		else
		{
			pw.println("<form action='test2'>");
			pw.println("When will u marry : <input type='text' name='f2t1'/> <br> ");
			pw.println("Why will u marry : <input type='text' name='f2t2'/> <br> ");
			pw.println("<input type='submit' value='submit'/>");
			pw.println("</form>");
		}
		pw.close();
	}
}


TestSrv2.java
--------------
package com.ihub.www;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;

@WebServlet(urlPatterns = "/test2",name="TestSrv2",loadOnStartup = 2)
public class TestSrv2 extends HttpServlet
{
	protected void doGet(HttpServletRequest req,HttpServletResponse res)throws ServletException,IOException
	{
		PrintWriter pw =res.getWriter();
		res.setContentType("text/html");
		
		//reading form 1 data from HttpSession
		HttpSession session = req.getSession(false);
		String name = (String)session.getAttribute("pname");
		String fname = (String)session.getAttribute("pfname");
		String ms = (String)session.getAttribute("pms");
		
		//reading form 2 data 
		String val1 = req.getParameter("f2t1");
		String val2 = req.getParameter("f2t2");
		
		pw.println("Form 1 Data :"+name+" "+fname+" "+ms+"<br>");
		pw.println("Form 2 Data :"+val1+" "+val2+"<br>");
		pw.close();
	}
}

Request url 
-----------
	http://localhost:2525/StatelessApp/
