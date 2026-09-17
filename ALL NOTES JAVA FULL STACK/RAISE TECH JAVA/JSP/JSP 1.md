JSP
====
JSP stands for Java Server Pages.

JSP is a server side web resource program which is used to develop web applications.


Q) Difference between Servlets and JSP ?

Servlets					JSP 
---------					--------
To work with servlets strong java 		To work with JSP strong java 
knowledge is required.				knowledge is not required.

It is not suitable for non-java 		It is suitable for java and non-java 
programmers.					programmers.

It does not support tags.			It supports tags.

It is faster.					It is bit slow.

It accept all protocol request.			It accept only HTTP request.

It supports annotations.			It does not support annotations.

It does not give implicit objects.		It gives 9 implicit objects.

Configuration of servlet program in web.xml 	Configuration of jsp program in web.xml 
file is mandatory.				file is optional.

Handling exceptions are mandatory.		Handling exceptions are optional.

We can't maintain HTML code and Java code 	We can maintain HTML code and java code 
seperately.					seperately.


First Web Application development having JSP program as web resource program 
============================================================================

Deployment Directory Structure 
-----------------------------
JspApp1
|
|----Java Resources
|
|----WebContent
	|
	|----ABC.jsp 
	|----WEB-INF
		|
		|---web.xml 
Note:
-----
In above application we need to add "servlet-api.jar" file in project build path.


ABC.jsp 
-------
<center>
	<h1>
	<%
		java.util.Date d = new java.util.Date();
		out.println(d);
	%>
	</h1>
</center>

web.xml
-------
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" id="WebApp_ID" version="4.0">
  
  <display-name>JspApp1</display-name>
  
  <welcome-file-list>
  	<welcome-file>ABC.jsp</welcome-file>
  </welcome-file-list>
  
</web-app>

Request url
----------
	http://localhost:2525/JspApp1/




Configuration of JSP program in web.xml file
=============================================


Deployment Directory Structure 
-----------------------------
JspApp1
|
|----Java Resources
|
|----WebContent
	|
	|----ABC.jsp 
	|----WEB-INF
		|
		|---web.xml 
Note:
-----
In above application we need to add "servlet-api.jar" file in project build path.

ABC.jsp
---------
<center>
	<h1>
	<%
		java.util.Date d = new java.util.Date();
		out.println(d);
	%>
	</h1>
</center>

web.xml 
--------
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" id="WebApp_ID" version="4.0">
  
  <display-name>JspApp1</display-name>
  
  <servlet>
  	<servlet-name>ABC</servlet-name>
  	<jsp-file>/ABC.jsp</jsp-file>
  </servlet>
  
  <servlet-mapping>
  	<servlet-name>ABC</servlet-name>
  	<url-pattern>/test</url-pattern>
  </servlet-mapping>
  
</web-app>

Request url
-----------
	http://localhost:2525/JspApp1/ABC.jsp 
	http://localhost:2525/JspApp1/test


How can we access our web application accessible by using URL Pattern 
=====================================================================
To access our web application accessible by using url pattern but not with file name so we need to keep ABC.jsp file inside "WEB-INF" folder.

Deployment Directory Structure 
-----------------------------
JspApp1
|
|----Java Resources
|
|----WebContent
	| 
	|----WEB-INF
		|
		|---ABC.jsp
		|---web.xml 
Note:
-----
In above application we need to add "servlet-api.jar" file in project build path.

ABC.jsp
--------
<center>
	<h1>
	<%
		java.util.Date d = new java.util.Date();
		out.println(d);
	%>
	</h1>
</center>

web.xml
------
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" id="WebApp_ID" version="4.0">
  
  <display-name>JspApp1</display-name>
  
  <servlet>
  	<servlet-name>ABC</servlet-name>
  	<jsp-file>/WEB-INF/ABC.jsp</jsp-file>
  </servlet>
  
  <servlet-mapping>
  	<servlet-name>ABC</servlet-name>
  	<url-pattern>/test</url-pattern>
  </servlet-mapping>
  
</web-app>


Request url
-----------
	http://localhost:2525/JspApp1/ABC.jsp  //invalid 
	http://localhost:2525/JspApp1/test

Note:
-----
Servlet container executes servlet program directly.

JSP container can't execute jsp program directly. It takes the support of servlet container to execute JSP program. Hence for every JSP program JES (Java Equivalent Servlet) class will be created.



JSP Life Cycle Methods 
======================
We have three life cycle methods in JSP.

1) _jspInit() 
-------------
	It is used for instantiation event.
	This method will execute just before JES class object creation.

2) _jspService()
-------------------
	It is used for request arrival event.
	This method will execute when request goes to jsp program.

3) _jspDestroy() 
----------------
	It is used for destruction event.
	This method will execute just before JES class object destruction.


Phases in JSP 
=============
We have two phases in JSP.

1) Translation phase 

2) Request processing phase 

3) Translation phase 
--------------------
In translation phase, our JSP program converts to JES class.

2) Request Processing phase 
--------------------------
In request processing phase, our JES class will be executed and result sends to browser 
window as dynamic response.

Diagram: jsp1.1



How to enable load-on-startup and what happens if we enable load-on-startup 
============================================================================
We can enable <load-on-startup> inside web.xml file.

web.xml
-------
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" id="WebApp_ID" version="4.0">
  
  <display-name>JspApp1</display-name>
  
  <servlet>
  	<servlet-name>ABC</servlet-name>
  	<jsp-file>/WEB-INF/ABC.jsp</jsp-file>
	<load-on-startup>1</load-on-startup>
  </servlet>
  
  <servlet-mapping>
  	<servlet-name>ABC</servlet-name>
  	<url-pattern>/test</url-pattern>
  </servlet-mapping>
  
</web-app>
	
If we enable load-on-startup then translation phase will be done during the server startup or during the deployment of web application.

It means our JES class object will be created before we give the request.