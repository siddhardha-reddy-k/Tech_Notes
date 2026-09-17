Include Directive Tag 
====================
The JSP include directive is a mechanism used to embed the content of one static resource (like an HTML file or another JSP page) directly into the current JSP page during the translation phase.

Deployment Directory Structure 
-------------------------------
JspApp8
|
|---Java Resources
|
|---WebContent
	|
	|---header.jsp 
	|---home.jsp 
	|---about.jsp
	|---service.jsp 
	|---WEB-INF
		|
		|---web.xml 
Note:
-----
In above application we need to add "servlet-api.jar" file in project build path.

header.jsp 
----------
<div style="background-color:#B53471; width:100%; height:50px">
		<a href="home.jsp" 
		style="color:#FFFFFF;text-decoration:none;margin:0px 100px; line-height:50px;"> 			Home 
		</a>

		<a href="about.jsp" 
		style="color:#FFFFFF;text-decoration:none;margin:0px 100px;line-height:50px;"> 			About 
		</a>
	
		<a href="service.jsp" 
		style="color:#FFFFFF;text-decoration:none;margin:0px 100px;line-height:50px;"> 			Service 
		</a>
</div>

home.jsp
--------

<%@include file="header.jsp" %>
<center>
	<h1>
		Home Page
	</h1>
</center>


about.jsp
---------

<%@include file="header.jsp" %>
<center>
	<h1>
		About Page
	</h1>
</center>

service.jsp
------------

<%@include file="header.jsp" %>
<center>
	<h1>
		Service Page
	</h1>
</center>

web.xml
-------
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" id="WebApp_ID" version="4.0">
  
  <display-name>JspApp8</display-name>
  
  <welcome-file-list>
  	<welcome-file>home.jsp</welcome-file>
  </welcome-file-list>

</web-app>

Request url
----------
	http://localhost:2525/JspApp8/home.jsp


Action Tags
============
Action tags are used to perform perticular task.

Action tags are used to control the flow of the pages.

Action tags are executed dynamically at runtime.

Action tags are divided into two types.

1) Standard Action Tags 

2) Custom Action Tags 


3) Standard Action Tags 
------------------------
We have following list of standard action tags.
ex:
	<jsp:include>
	<jsp:forward>
	<jsp:useBean>
	<jsp:setProperty>
	<jsp:getProperty> 
	and etc.

Action Forward Tag 
==================
In action forward, the output of source jsp program will be discarded and output of destination jsp program goes to browser window as dynamic response.

It internally uses servlet API functionality called rd.forward(req,res).

syntax:
-------
	<jsp:forward page="page_name/>


Deployment Directory Structure 
------------------------------
JspApp9
|
|---Java Resources
|
|---WebContent
	|
	|---A.jsp
	|---B.jsp
	|---WEB-INF
		|
		|---web.xml 
Note:
-----
In above application we need to add "servlet-api.jar" file in project build path.

A.jsp
-------
<b><i> Beginning of A.jsp file </i></b>
<br>
<jsp:forward page="B.jsp"/>
<br>
<b><i>Ending of A.jsp</i></b>

B.jsp
-----
<b><i> This is B.jsp file </i></b>

web.xml
-------
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" id="WebApp_ID" version="4.0">
  
  <display-name>JspApp9</display-name>
  
  <welcome-file-list>
    <welcome-file>A.jsp</welcome-file>
  </welcome-file-list>

</web-app>


Request url
----------
	http://localhost:2525/JspApp9/




Action include Tag 
==================
In action include, the output of source jsp program and destination jsp program combinely goes to browser window as dynamic response.

It internally uses servlet API functionality called rd.include(req,res). 

syntax:
-------
	<jsp:include page="page_name"/>


Deployment Directory Structure 
------------------------------
JspApp9
|
|---Java Resources
|
|---WebContent
	|
	|---A.jsp
	|---B.jsp
	|---WEB-INF
		|
		|---web.xml 
Note:
-----
In above application we need to add "servlet-api.jar" file in project build path.

A.jsp
-------
<b><i> Beginning of A.jsp file </i></b>
<br>
<jsp:include page="B.jsp"/>
<br>
<b><i>Ending of A.jsp</i></b>

B.jsp
-----
<b><i> This is B.jsp file </i></b>

web.xml
-------
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" id="WebApp_ID" version="4.0">
  
  <display-name>JspApp9</display-name>
  
  <welcome-file-list>
    <welcome-file>A.jsp</welcome-file>
  </welcome-file-list>

</web-app>


Request url
----------
	http://localhost:2525/JspApp9/





JSP to Java Bean Communication 
==============================
JSP to java bean communication is possible by using three tags as given below.

1) <jsp:useBean> tag 
-------------------
	It is used to create and locate bean class object.

2) <jsp:setProperty> tag 
-------------------------
	It is used to set the value to bean object and calls setter methods.

3) <jsp:getProperty> tag 
--------------------------
	It is used to get the value from bean object and calls getter methods.
Note:
-----
	All the above tags are independent tags.

Example1
--------

Deployment Directory Structure 
-----------------------------
JspApp10
|
|---Java Resources
	|
	|------src
		|
		|---com.ihub.www
			|
			|---CubeNumber.java
|---WebContent
	|
	|---process.jsp
	|---WEB-INF
		|
		|---web.xml 
Note:
-----
In above application we need to add "servlet-api.jar" file in project build path.

CubeNumber.java
-----------------
package com.ihub.www;

public class CubeNumber 
{
	public int cube(int n)
	{
		return n*n*n;
	}
}

process.jsp
------------
<jsp:useBean id="cn" class="com.ihub.www.CubeNumber" />

<center>
	<h1>
		<%= "Cube of a given number is ="+cn.cube(5) %>
	</h1>
</center>

web.xml
--------
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" id="WebApp_ID" version="4.0">
 
  <display-name>JspApp10</display-name>
 
  <welcome-file-list>
    <welcome-file>process.jsp</welcome-file>
  </welcome-file-list>

</web-app>

Request url
-----------
	http://localhost:2525/JspApp10/

Example2
---------

Deployment Directory Structure 
------------------------------
JspApp11
|
|---Java Resources
	|
	|------src
		|
		|---com.ihub.www
			|
			|---User.java
|---WebContent
	|
	|---form.html
	|---process.jsp
	|---WEB-INF
		|
		|---web.xml 
Note:
------
In above application we need to add "servlet-api.jar" file in project build path.

form.html
---------

<form action="process.jsp">

	<table align="center">
		<tr>
			<td>UserName:</td>
			<td><input type="text" name="username"/></td>
		</tr>
		<tr>
			<td>Password:</td>
			<td><input type="password" name="password"/></td>
		</tr>
		<tr>
			<td>Email:</td>
			<td><input type="text" name="email"/></td>
		</tr>
		<tr>
			<td><input type="reset" value="reset"/></td>
			<td><input type="submit" value="submit"/></td>
		</tr>
	</table>
	
</form>

User.java
--------
package com.ihub.www;

public class User 
{
	private String username;
	private String password;
	private String email;
	
	public String getUsername() {
		return username;
	}
	public void setUsername(String username) {
		this.username = username;
	}
	public String getPassword() {
		return password;
	}
	public void setPassword(String password) {
		this.password = password;
	}
	public String getEmail() {
		return email;
	}
	public void setEmail(String email) {
		this.email = email;
	}
}

process.jsp
-----------

<jsp:useBean id="u" class="com.ihub.www.User"/>

<jsp:setProperty property="*" name="u"/>


Records Are  <br>
<jsp:getProperty property="username" name="u"/> <br>
<jsp:getProperty property="password" name="u"/> <br>
<jsp:getProperty property="email" name="u"/> <br>


web.xml
----------
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" id="WebApp_ID" version="4.0">
  
  <display-name>JspApp11</display-name>
  
  <welcome-file-list>
    <welcome-file>form.html</welcome-file>
  </welcome-file-list>
  
</web-app>


Request url
----------
	http://localhost:2525/JspApp11/
