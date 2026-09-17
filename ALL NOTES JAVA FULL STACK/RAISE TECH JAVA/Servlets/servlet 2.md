Servlets 
========
It is a dynamic web resource program which is used to enhance the functionality of web server, proxy server or IDE's server.

or 

It is a server side web resource prgoram which is used to generate dynamic web pages. 

or 

A servlet is a single instance multithread java based web resource program which is used to develop web applications. 

Diagram: servlet2.1

First web application development having servlet program as web resource program
================================================================================
Diagram: servlet2.2

Deployment Directory Structure 
------------------------------
DateApp
|
|---Java Resources
	|
	|------src
		|
		|---com.ihub.www
			|
			|---DateSrv.java
|---WebContent
	|
	|---WEB-INF
		|
		|---web.xml 
Note:
------
In above application we need to add "servlet-api.jar" file in project build path.

step1:
-------
	Launch eclipse IDE by choosing workspace location.

step2:
------
	Create a dynamic web project i.e DateApp.
	ex:
		File --> New --> Dynamic web project --> 
		Project Name : DateApp 
		Dynamic web module version : 4.0  --> Next 
		---> Next -->click to Generate web.xml file --> Finish. 
step3:
------
	Add "servlet-api.jar" file in project build path.
	ex:
		Right click to DateApp project --> build path --> 
		Configuer build path --> libraries --> add external jars 
		--> select servlet-api.jar file --> open --> apply and close.

step4:
-------
	Create a "com.ihub.www" package inside "Java Resources/src" folder.

step5:
------
	Create a DateSrv.java file inside "com.ihub.www" package.

DateSrv.java
-------------
package com.ihub.www;

import java.io.IOException;
import java.io.PrintWriter;
import java.util.Date;

import javax.servlet.GenericServlet;
import javax.servlet.ServletException;
import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;

public class DateSrv extends GenericServlet
{
	public void service(ServletRequest req,ServletResponse res)throws ServletException,IOException
	{
		PrintWriter pw = res.getWriter();
		res.setContentType("text/html");
		
		Date d = new Date();
	pw.println("<center><h1>Current Date and Time <br> "+d+"</h1></center>");
		
		pw.close();
	}
}

step6:
-----
	Configure servlet program in web.xml file.

web.xml 
-------
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" id="WebApp_ID" version="4.0">
  <display-name>DateApp</display-name>
  
  <servlet>
  	<servlet-name>DateSrv</servlet-name>
  	<servlet-class>com.ihub.www.DateSrv</servlet-class>
  </servlet>
  
  <servlet-mapping>
  	<servlet-name>DateSrv</servlet-name>
  	<url-pattern>/test</url-pattern>
  </servlet-mapping>
  
</web-app>


step7:
-----
	Add Tomcat 9.x server to Eclipse ide.
	ex:
		window --> preferences --> server --> Runtime Environment 			--> click to add button --> select Apache Tomcat 9 -->
		select tomcat installation directory --> Finish --> apply & close.

step8:
------
	Run dynamic web project.
	ex:
		right click to DateApp project --> run as --> Run on server 
		--> select Apache tomcat 9 --> Next --> Finish.

step9:
------	
	Test the application by using below request url.
	ex:
		http://localhost:2525/DateApp/test

Note:
-----
	If any error is there in web.xml file then we will get 404 Error.
	If any error is there in servlets then we will get 500 Error.


Types of URL Patterns 
=====================
Each servlet program recognize with the help of url pattern.

URL pattern hide technology name or class name from outsider for security reason.

Our client, web server and other web resource programs recognize each servlet program by using url pattern.

We have three types of url patterns.

1) Exact match url pattern 

2) Directory match url pattern 

3) Extension match url pattern 

Every server is designed to support above three url patterns.

1) Exact match url pattern
---------------------------
It starts with '/' symbol having some name.
ex:
	web.xml 
	-------
		<url-pattern>/test</url-pattern>

	request url
	-----------
		http://localhost:2525/DateApp/test    // valid 
		http://localhost:2525/DateApp/best    // invalid 		
		http://localhost:2525/DateApp/x/test  // invalid 

2) Directory match url pattern 
------------------------------
It starts with '/' symbol and ends with '*' symbol.

ex:
	web.xml 
	-------
		<url-pattern>/x/y/*</url-pattern>

	Request url
	-----------
		http://localhost:2525/DateApp/x/y/z  		//valid
		http://localhost:2525/DateApp/x/y/z/test  	//valid 
		http://localhost:2525/DateApp/y/x/z		//invalid 


3) Extension match url pattern 
------------------------------
It starts with '*' symbol having some extension.
ex:
	web.xml 
	-------
		<url-pattern>*.do</url-pattern>

	Request url
	-----------
		http://localhost:2525/DateApp/test     //invalid 
		http://localhost:2525/DateApp/test.do  //valid 
		http://localhost:2525/DateApp/x/y/z.do //valid 
