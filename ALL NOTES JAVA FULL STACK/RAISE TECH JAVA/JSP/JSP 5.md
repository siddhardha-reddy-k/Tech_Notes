Custom Tags in JSP 
==================
Tags which are created by the user based on the application requirements are called custom tags.
ex:
	<ihub:student />
	<qt:trainer />
	and etc.

To create custom tags in JSP we need to use taglib directive tag.
ex:
	<%@taglib uri="tagLibraryURI" prefix="tagPrefix" %>

We can configure tag information inside TLD file.
TLD stands for Tag Library Descriptor.

Deployment Directory Structure 
==============================
JspApp12
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
		|---mytags.tld
Note:
----
In above application we need to add "servlet-api.jar" and "jsp-api.jar" file in project build path.

process.jsp
-----------
<%@taglib uri="/WEB-INF/mytags.tld" prefix="qt" %>

<center>
	<h1>
		Cube of a number = <qt:cube number="5" />
	</h1>
</center>

web.xml
-------
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" id="WebApp_ID" version="4.0">
  
  <display-name>JspApp12</display-name>
  
  <welcome-file-list>
    <welcome-file>process.jsp</welcome-file>
  </welcome-file-list>
  
</web-app>

mytags.tld
-----------
<?xml version="1.0" encoding="ISO-8859-1" ?>  
<!DOCTYPE taglib  
        PUBLIC "-//Sun Microsystems, Inc.//DTD JSP Tag Library 1.2//EN"  
    "http://java.sun.com/j2ee/dtd/web-jsptaglibrary_1_2.dtd">  
  
<taglib>  
  <tlib-version>1.0</tlib-version>  
  <jsp-version>1.2</jsp-version>  
  <short-name>simple</short-name>  
  <uri>http://tomcat.apache.org/example-taglib</uri>
  
  <tag>
  		<name>cube</name>
  		<tag-class>com.ihub.www.CubeNumber</tag-class>
  		<attribute>
  			<name>number</name>
  			<required>true</required>
  		</attribute>
  </tag> 
  
</taglib>

CubeNumber.java
---------------
package com.ihub.www;

import javax.servlet.jsp.JspException;
import javax.servlet.jsp.JspWriter;
import javax.servlet.jsp.tagext.TagSupport;

public class CubeNumber extends TagSupport
{
	private int number;
	
	//setter method 
	public void setNumber(int number)
	{
		this.number=number;
	}
	
	public int doStartTag()throws JspException
	{
		
		JspWriter out = pageContext.getOut();
		try
		{
			out.print(number*number*number);
		}
		catch(Exception e)
		{
			e.printStackTrace();
		}
		return SKIP_BODY;
	}
}

Request url
-----------
	http://localhost:2525/JspApp12/


MVC in JSP 
===========
MVC stands for Model View Controller.

MVC is a design pattern which seperates business logic, persistence logic and data.

Controller acts like a interface between Model and View.

Controller intercepts all incoming requests.

Model contains business logic and some times it contains data.

View represent UI i.e presentation logic.

Diagram: jsp5.1

Deployment Directory Structure 
------------------------------
MVCApp
|
|---Java Resources
	|
	|------src
		|
		|---com.ihub.www
			|
			|---LoginBean.java		
			|---LoginSrv.java
|---WebContent
	|
	|---form.html
	|---view.jsp
	|---error.jsp
	|---WEB-INF
		|
		|---web.xml 	
form.html
----------

<form action="test">
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
			<td><input type="reset" value="reset"/></td>
			<td><input type="submit" value="submit"/></td>
		</tr>
	</table>
</form>

web.xml
-------
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" id="WebApp_ID" version="4.0">
  
  <display-name>MVCApp</display-name>
  
  <welcome-file-list>
    <welcome-file>form.html</welcome-file>
  </welcome-file-list>

</web-app>


LoginBean.java
-------------
package com.ihub.www;

public class LoginBean 
{
	private String username;
	private String password;
	
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
}

LoginSrv.java
---------------
package com.ihub.www;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.RequestDispatcher;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet(urlPatterns = "/test", name = "LoginSrv")
public class LoginSrv extends HttpServlet 
{
	protected void doGet(HttpServletRequest req,HttpServletResponse res)throws ServletException,IOException
	{
		PrintWriter pw =res.getWriter();
		res.setContentType("text/html");
		
		//reading form data 
		String name = req.getParameter("username");
		String pass = req.getParameter("password");
		
		//add the data to bean object
		LoginBean lb = new LoginBean();
		lb.setUsername(name);
		lb.setPassword(pass);
		
		//add bean object to request parameter
		req.setAttribute("bean", lb);
		
		if(pass.equals("admin"))
		{
			RequestDispatcher rd = req.getRequestDispatcher("view.jsp");
			rd.forward(req, res);
		}
		else
		{
			RequestDispatcher rd = req.getRequestDispatcher("error.jsp");
			rd.forward(req, res);
		}
		
		pw.close();
	}
}


view.jsp
----------
<%@page import="com.ihub.www.LoginBean" %>

<%
	LoginBean lb = (LoginBean)request.getAttribute("bean");
%>

<%= lb.getUsername() %> <br>
<%= lb.getPassword() %> <br>

error.jsp
----------
<center>
	<b style="color:red">
		Incorrect username or password
	</b>
</center>

<%@include file="form.html" %>


Request url
-----------
	http://localhost:2525/MVCApp/

How to deploy web application in Tomcat server 
==============================================
step1:
------
	Create a dynamic web project i.e MVCApp.
step2:
------
	Convert the project to war file.
step3:
------
	Launch Tomcat server from "bin" directory. 
step4:
------
	Goto Tomcat console page.
	ex:
		http://localhost:2525
step5:
------
	Goto Manager App and pass credentials.
	ex:		
		username : admin 
		password : admin 

step6:
------
	Select the war file to deploy.
