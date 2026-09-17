Implicit objects 
================
Object which can be used directly without any configuration is called implicit object.

Implicit objects created by the web container which is available for every JSP page.

JSP provides total 9 implicit objects.

ex:
	Object		Type
	------		-------
	out		JspWriter 
	request		HttpServletRequest 
	response	HttpServletResponse 
	config		ServletConfig
	application	ServletContext 
	session		HttpSession
	pageContext	PageContext
	page		Object  
	exception	Throwable 

response object
================
A response is a implicit object of type HttpServletResponse.

It is used to send response or errors to other resources.

Deployment Directory Structure 
------------------------------
JspApp13
|
|---Java Resources
|
|---WebContent
	|
	|---index.html 
	|---process.jsp
	|---WEB-INF
		|
		|---web.xml 
Note:
------
In above application we need to add "servlet-api.jar" file in project build path.
	
index.html
----------
<center>
	<h1>
		<a href="process.jsp"> Facebook </a>
	</h1>
</center>


process.jsp
----------
<%
	response.sendRedirect("http://www.facebook.com/login");
%>

web.xml
-------
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" id="WebApp_ID" version="4.0">
  
  <display-name>JspApp13</display-name>
  
  <welcome-file-list>
    <welcome-file>index.html</welcome-file>
   </welcome-file-list>
    
</web-app>

Request url
-----------
	http://localhost:2525/JspApp13/

config object
==============
A comfig is an implicit object of type ServletConfig.

It is used to read initialized parameters of perticular JSP page.

Deployment Directory Structure 
-------------------------------
JspApp14
|
|---Java Resources
|
|---WebContent
	|
	|---index.html
	|---process.jsp 
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

process.jsp
----------
<%
	String value = config.getInitParameter("driver");
	out.println(value);
%>

web.xml 
-------
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" id="WebApp_ID" version="4.0">
  
  <display-name>JspApp14</display-name>
  
  <servlet>
  	<servlet-name>ABC</servlet-name>
  	<jsp-file>/process.jsp</jsp-file>
  	<init-param>
  		<param-name>driver</param-name>
  		<param-value>oracle.jdbc.driver.OracleDriver</param-value>
  	</init-param>	
  </servlet>
  
  <servlet-mapping>
  	<servlet-name>ABC</servlet-name>
  	<url-pattern>/test</url-pattern>
  </servlet-mapping>
  
  
  <welcome-file-list>
    <welcome-file>index.html</welcome-file>
  </welcome-file-list>
  
</web-app>

Request url
-----------
	http://localhost:2525/JspApp14/




application object
==================
It is an implicit object of type ServletContext.

It is used to read configuration information from web.xml file which is global.

Deployment Directory Structure 
------------------------------
JspApp15
|
|---Java Resources
|
|---WebContent
	|
	|---index.html
	|---process.jsp 
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
		<a href="test"> clickMe </a>
	</h1>
</center>

process.jsp
-----------
<%
	String value = application.getInitParameter("driver");
	out.println(value);
%>

web.xml
--------
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" id="WebApp_ID" version="4.0">
  
  <display-name>JspApp15</display-name>
  
  <servlet>
  	<servlet-name>ABC</servlet-name>
  	<jsp-file>/process.jsp</jsp-file>
  </servlet>
  
  <servlet-mapping>
  	<servlet-name>ABC</servlet-name>
  	<url-pattern>/test</url-pattern>
  </servlet-mapping>
  
  <context-param>
  	<param-name>driver</param-name>
  	<param-value>oracle.jdbc.driver.OracleDriver</param-value>
  </context-param>
  
  
  <welcome-file-list>
    <welcome-file>index.html</welcome-file>
  </welcome-file-list>
  
</web-app>

Request url
-----------
	http://localhost:2525/JspApp15/





session	 object
===============
It is an implicit object of type HttpSession.

It is used to add,remove,set the attributes to/from session.

Deployment Directory Structure 
-------------------------------
JspApp16
|
|---Java Resources
|
|---WebContent
	|
	|---form.html
	|---first.jsp 
	|---second.jsp 
	|---WEB-INF
		|
		|---web.xml
Note:
------
In above application we need to add "servlet-api.jar" file in project build path.

form.html
---------
<form action="first.jsp">
	
	Name : <input type="text" name="t1"/> 
	
	<input type="submit" value="submit"/>
</form>

first.jsp
----------
<%
	String name = request.getParameter("t1");
	session.setAttribute("pname", name);
%>
<a href="second.jsp"> Next Page </a>


second.jsp
-----------
<%
	String name = (String)session.getAttribute("pname");
	out.println("Welcome :"+name);
%>

web.xml
--------
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" id="WebApp_ID" version="4.0">
  
  <display-name>JspApp16</display-name>
  
  <welcome-file-list>
    <welcome-file>form.html</welcome-file>
  </welcome-file-list>
  
</web-app>

Request url
---------
	http://localhost:2525/JspApp16/


pageContext object
===================
It is an implicit object of type PageContext.

It is used to add,remove or set the attributes to/from session along with following scopes.

We have four scopes in JSP.

1) page scope (default)

2) request scope 

3) session scope 

4) application scope 


Deployment Directory Structure 
-------------------------------
JspApp16
|
|---Java Resources
|
|---WebContent
	|
	|---form.html
	|---first.jsp 
	|---second.jsp 
	|---WEB-INF
		|
		|---web.xml
Note:
------
In above application we need to add "servlet-api.jar" file in project build path.

form.html
---------
<form action="first.jsp">
	
	Name : <input type="text" name="t1"/> 
	
	<input type="submit" value="submit"/>
</form>

first.jsp
----------
<%
	String name = request.getParameter("t1");
	pageContext.setAttribute("pname", name,pageContext.SESSION_SCOPE);
%>
<a href="second.jsp"> Next Page </a>


second.jsp
-----------
<%
	String name = (String)pageContext.getAttribute("pname",pageContext.SESSION_SCOPE);
	out.println("Hey! Welcome :"+name);
%>

web.xml
--------
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" id="WebApp_ID" version="4.0">
  
  <display-name>JspApp16</display-name>
  
  <welcome-file-list>
    <welcome-file>form.html</welcome-file>
  </welcome-file-list>
  
</web-app>

Request url
---------
	http://localhost:2525/JspApp16/


Junit 
=====
Junit is a unit testing framework.

Unit testing means checking a piece of code working as per requirement or not.

The latest version is Junit 5.

It is very important for TDD (Test Driven Development).

To perform unit testing we need to create test cases or test suit.


Project Structure 
-----------------
JunitProject 
|
|---src/main/java
|	|
	|---com.ihub.www
		|
		|---Demo.java

|---src/main/resources
|
|---src/test/java
	|
	|----com.ihub.www
		|
		|---DemoTest.java
|	
|---pom.xml 


Steps to perform unit testing
=============================
step1:
------
	Create a simple maven archetype project.

step2:
-------
	create a com.ihub.www package inside "src/main/java".

step3:
------
	Create a App.java file inside "com.ihub.www" package.

Demo.java
---------
package com.ihub.www;

public class Demo 
{
	public int sum(int a,int b)
	{
		return a+b;
	}
	
	public String concatinate(String str1,String str2)
	{
		return str1+str2;
	}
}


step4:
-----
	Create a Test file i.e DemoTest.java.
	ex:
		right click to App.java file --> new --> others -->
		Junit --> test case --> Next --> select the methods for 
		test cases --> finish.


step5:
-----
	Add unit testing logic inside DemoTest.java file.

AppTest.java
------------
package com.ihub.www;

import static org.junit.Assert.*;

import org.junit.After;
import org.junit.Before;
import org.junit.Test;

public class DemoTest {

	Demo d=null;
	
	@Before
	public void setUp() throws Exception {
		d=new Demo();
	}

	@After
	public void tearDown() throws Exception {
		
		
	}

	@Test
	public void testSum() {
		int result=d.sum(10,20);
		assertEquals(50, result);
	}

	@Test
	public void testConcatinate() {
		String result=d.concatinate("ihub", "talent");
		assertEquals("ihubtalent",result);
	}

}


step6:
-----
	Run the junit test cases.
	ex:
		Right click to AppTest.java file --> run as --> Junit test case.

Note:
-----
	Green color indicates unit test case is passed.
	Brown color indicates unit test case is failed.
