JSP Tags/Elements 
=================
We have three tags in JSP.

1) Scripting tags 
-----------------
	It is classified into three types.
	
	i) Scriptlet tag 
		ex:
			<% code here %>

	ii) Expression tag 
		ex:
			<%= code here %>

	iii) Declaration tag 
		ex:
			<%! code here %>

2) Directive tags 
------------------
	It is classified into two types.
	
	i) Page directive tag 
		ex:
			<%@page attribute=value %>

	ii) Include directive tag 
		ex:
			<%@include attribute=value %>

3) Action tags 
--------------
	We have following list of action tags.
	ex:
		<jsp:include>
		<jsp:forward>
		<jsp:useBean>
		<jsp:setProperty>
		<jsp:getProperty>
		and etc.

Comments in JSP
-------------
	<%-- comment  --%> 

	
Scriptlet tag
==============
It is used to declare java code.

syntax:
-------
	<% code here %> 

Deployment Directory Structure 
------------------------------
JspApp2
|
|---Java Resources
|
|---WebContent
	|
	|---form.html
	|---process.jsp
	|---WEB-INF
		|
		|---web.xml 
Note:
----
In above application we need to add "servlet-api.jar" file in project build path.


form.html
---------
<form action="process.jsp">
	
	Name: <input type="text" name="t1"/> 
	
	<input type="submit" value="submit"/>
	
</form>


web.xml
-------
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" id="WebApp_ID" version="4.0">
 
  <display-name>JspApp2</display-name>
 
  <welcome-file-list>
  	<welcome-file>form.html</welcome-file>
  </welcome-file-list>
  
</web-app>


process.jsp
-----------
<center>
	<h1>
		<%
			String name = request.getParameter("t1");
			out.println("Welcome :"+name);
		%>
	</h1>
</center>

Request url
-----------
	http://localhost:2525/JspApp2/



Expression tag
===============
The code which is written in expression tag will return to the output stream of a response. It means we don't need to use out.println() method to print the data.

syntax:
-------
	<%=  code here %> 

Note:
-----
	Expression tag does not allow semicolon.


Deployment Directory Structure 
------------------------------
JspApp3
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
---------
<center>
	<h1>
		<a href="process.jsp"> getMsg </a>
	</h1>
</center>

web.xml
-------
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" id="WebApp_ID" version="4.0">
  
  <display-name>JspApp3</display-name>
  
  <welcome-file-list>
  	<welcome-file>index.html</welcome-file>
  </welcome-file-list>
  
</web-app>

process.jsp
-----------
<%
	java.util.Calendar c = java.util.Calendar.getInstance();
	int h = c.get(java.util.Calendar.HOUR_OF_DAY);
	if(h<12)
	{
%>
		<center>
			<h1>
			<%= "Good Morning" %>
			</h1>
		</center>
<% 
	}
	else if(h<16)
	{
%>
		<center>
			<h1>
			<%= "Good Afternoon" %>
			</h1>
		</center>
<% 
	}
	else if(h<20)
	{
%>
		<center>
			<h1>
			<%= "Good Evening" %>
			</h1>
		</center>
<% 	
	}
	else
	{
%>
		<center>
			<h1>
			<%= "Good Night" %>
			</h1>
		</center>
<% 	
	}
%>	

Request url
----------
	http://localhost:2525/JspApp3/


Declaration tag
===============
It is used to declare fields and methods.

syntax:
-------
	<%!  code here  %>

Deployment Directory Structure 
------------------------------
JspApp4
|
|---Java Resources
|
|---WebContent
	|
	|---process.jsp
	|---WEB-INF
		|
		|---web.xml 
Note:
-----
In above application we need to add "servlet-api.jar" file in project build path.

process.jsp
------------

<%!
	int i = 100;

	int cube(int n)
	{
		return n*n*n;
	}
%>
<center>
	<h1>
		<%= "The value is ="+i %>  
		<br>
		<%= "Cube of a given number is ="+cube(5) %>
	</h1>
</center>

web.xml
--------
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" id="WebApp_ID" version="4.0">
  
  <display-name>JspApp4</display-name>
  
  <welcome-file-list>
    <welcome-file>process.jsp</welcome-file>
  </welcome-file-list>

</web-app>

Request url
-----------
	http://localhost:2525/JspApp4/







Exception Handling in JSP 
=========================
Runtime errors are called exceptions.

Exceptions may raise any time in our application so handling exceptions always safer side for the developer/programmer.

There are two ways to handle the exceptions in JSP.

1) Using errorPage and isErrorPage attribute of page directive tag 

2) Using <error-page> element in web.xml file 

3) Using errorPage and isErrorPage attribute of page directive tag 
-------------------------------------------------------------------

Deployment Directory Structure 
-----------------------------
JspApp5
|
|---Java Resources
|
|---WebContent
	|
	|---form.html
	|---process.jsp
	|---error.jsp 
	|---WEB-INF
		|
		|--web.xml 
Note:
-----
In above application we need to add "servlet-api.jar" file in project build path.

form.html
----------

<form action="process.jsp">
	
	No1: <input type="text" name="t1"/> <br>
	
	No2: <input type="text" name="t2"/> <br>
	
	<input type="submit" value="divide"/>
	
</form>

web.xml
--------
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" id="WebApp_ID" version="4.0">
  <display-name>JspApp5</display-name>
  <welcome-file-list>
  	<welcome-file>form.html</welcome-file>
  </welcome-file-list>
</web-app>


process.jsp
-----------

<%@page errorPage="error.jsp" %>
<%
	String sno1 = request.getParameter("t1");
	String sno2 = request.getParameter("t2");
	
	int a = Integer.parseInt(sno1);
	int b = Integer.parseInt(sno2);
	
	int c = a/b;
%>
<center>
	<h1>
		<%= "Division of two numbers is ="+c %>
	</h1>
</center>


error.jsp
---------

<%@page isErrorPage="true" %>
<b>
	<i>
		Sorry!! Exception occurred
	</i>
</b>
<%= exception %>

Request url
----------
	http://localhost:2525/JspApp5/
