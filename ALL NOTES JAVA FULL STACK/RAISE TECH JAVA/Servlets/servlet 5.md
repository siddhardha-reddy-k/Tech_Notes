Q) What is the difference between GET and POST Methodology?

GET					POST
-----					--------
It is a default methodology.		It is not a default methodology.

It sends the request fastly.		It is bit slow.

It carries limited amount of data.	It carries unlimited amount of data.

It is not good for secure data.		It is good for secure data.

It is not suitable for file uploading	It is suitable for file uploading and 
and encryption.				encryption.

To process GET methodology we will	To process POST methodology we will use  
use doGet(-,-) method.			doPost(-,-) method.


File Uploading 
==============
The process of capturing a file from client machine file system and storing in a server machine file system is called file uploading and reverse is called file downloading.

While dealing with matrimonial applications, job portal applications, profile management applications we need to upload and download a file.

There is no specific API in servlets to perform file uploading.

We need to use third party API called JAVAZOOM API.

JAVAZOOM API comes in zip format and once if we extracted we will get three jar files.

ex:
	uploadbean.jar (main jar file)
	struts.jar 
	cos.jar 

JAVAZOOM API : 
--------------
https://drive.google.com/file/d/1XXQqn3rQ_yWTr-i4DT0nl4_nCDE2ejWl/view?usp=drive_link

We can use file component in a form page as follow.
ex:
	File : <input type="file" name="f1"/>


Deployment Directory Structure 
-------------------------------
UploadApp
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
	|---form.html
	|---WEB-INF
		|
		|------web.xml
		|------lib
			|
			|---uploadbean.jar
			|---struts.jar
			|---cos.jar
Note:
-----
In above application we need to add "servlet-api.jar" and "uploadbean.jar" file in project build path.

form.html
---------
<form action="test" method="POST" enctype="multipart/form-data">
	
	File1: <input type="file" name="f1"/> <br>
	File2: <input type="file" name="f2"/> <br>
	
	<input type="submit" value="submit"/>
</form>

web.xml
-------
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" id="WebApp_ID" version="4.0">
  
  <display-name>UploadApp</display-name>

  <welcome-file-list>
  	<welcome-file>form.html</welcome-file>
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

import javazoom.upload.MultipartFormDataRequest;
import javazoom.upload.UploadBean;

@WebServlet(urlPatterns = "/test", name = "TestSrv")
public class TestSrv extends HttpServlet
{
	protected void doPost(HttpServletRequest req,HttpServletResponse res)throws ServletException,IOException
	{
		PrintWriter pw =res.getWriter();
		res.setContentType("text/html");
		
		//file uploading 
		try
		{
			UploadBean ub = new UploadBean();
			ub.setFolderstore("D:\\demo");
			ub.setOverwrite(false);
			
			MultipartFormDataRequest nreq = new MultipartFormDataRequest(req);
			ub.store(nreq);
			
			pw.println("<center><h1>Files are uploaded successfully</h1></center>");
			
		}
		catch(Exception e)
		{
			pw.println(e);
		}
		pw.close();
	}
}

Request url
----------
	http://localhost:2525/UploadApp/



ServletConfig object
====================
ServletConfig is an interface which is present in javax.servlet package.

ServletConfig object created by the web container for every servlets.

ServletConfig object is primarily used to pass or read initialization parameters (init parameters) from the deployment descriptor (web.xml) or from annotation to a specific servlet during its initialization phase. 

We can create ServletConfig object as follow.
ex:
	ServletConfig config = getServletConfig();

ServletConfig interface contains following methods.

1) public String getInitParameter(String name)
---------------------------------------
	It returns initialized parameter value based on parameter name.

2) public Enumeration getInitParameterNames()
---------------------------------------------
	It returns enumeration of initialized parameters.

3) public String getServletName() 
--------------------------------
	It returns servlet name.

4) public ServletContext getServletContext() 
-----------------------------------
	It returns ServletContext object


Deployment Directory Structure 
------------------------------
ConfigApp
|
|----Java Resources
	|
	|------src
		|
		|---com.ihub.www
			|
			|---TestSrv.java
|---WebContent
	|
	|----index.html
	|----WEB-INF
		|	
		|----web.xml 	
Note:
----
In above application we need to add "servlet-api.jar" file in project build path.

index.html
----------
<center>
	<h1>
		<a href="test"> clickMe  </a>
	</h1>
</center>

web.xml
--------
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" id="WebApp_ID" version="4.0">
  
  <display-name>ConfigApp</display-name>
  
  <welcome-file-list>
  	<welcome-file>index.html</welcome-file>
  </welcome-file-list>
  
</web-app>

TestSrv.java
-------------
package com.ihub.www;

import java.io.IOException;
import java.io.PrintWriter;
import java.util.Enumeration;

import javax.servlet.ServletConfig;
import javax.servlet.ServletContext;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebInitParam;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet(urlPatterns = "/test" , name = "TestSrv", initParams = {
		@WebInitParam(name = "driver",value = "oracle.jdbc.driver.OracleDriver"),
		@WebInitParam(name = "url", value="jdbc:oracle:thin:@localhost:1521:XE")
})
					
public class TestSrv extends HttpServlet
{
	protected void doGet(HttpServletRequest req,HttpServletResponse res)throws ServletException,IOException
	{
		PrintWriter pw =res.getWriter();
		res.setContentType("text/html");
		
		ServletConfig config = getServletConfig();
		pw.println(config.getInitParameter("driver")+"<br>");
		pw.println(config.getInitParameter("url")+"<br>");
		
		Enumeration<String> e = config.getInitParameterNames();
		while(e.hasMoreElements())
		{
			String s = e.nextElement();
			pw.println(s+"<br>");
		}
		pw.println(config.getServletName());
		
		//ServletContext context = config.getServletContext();
		
		pw.close();
	}
}

Request url 
-------------
	http://localhost:2525/ConfigApp/
