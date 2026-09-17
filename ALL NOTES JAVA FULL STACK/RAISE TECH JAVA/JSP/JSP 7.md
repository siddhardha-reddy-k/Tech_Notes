Maven 
=====
Maven is a project building management tool.

It is used to simplify the project development process.

It contains pom.xml file.

POM stands for Project Object Model.

A pom.xml file contains dependencies, goals , packages and etc.


Steps to develop Maven project 
==============================
step1:
------
	Create a maven project for web application.
	ex:
		File --> new --> Maven project --> Next --> 
		Groupid : org.apache.maven.archetype
		Artifact id : maven.archetype.webapp
		version : 1.0  --> Next --> 
		Group Id : com.ihub.www
		Artificat Id: MavenProj
		version : keep same 
		package : com.ihub.www  ---> Finish. 

step2:
------
	Add "servlet-api.jar" dependency inside pom.xml file.
	ex:
		<dependency>
    			<groupId>javax.servlet</groupId>
    			<artifactId>javax.servlet-api</artifactId>
    			<version>4.0.1</version>
    			<scope>provided</scope>
		</dependency>
step3:
------
	Goto index.jsp inside "src/main/webapp" folder.

index.jsp
----------
<center>
	<h1>
		<a href="test"> clickMe </a>
	</h1>
</center>
	
step4:
-------	
	Goto web.xml file inside "src/main/webapp/WEB-INF" folder.

web.xml
--------
<!DOCTYPE web-app PUBLIC
 "-//Sun Microsystems, Inc.//DTD Web Application 2.3//EN"
 "http://java.sun.com/dtd/web-app_2_3.dtd" >

<web-app>

  <display-name>Archetype Created Web Application</display-name>
  
  <welcome-file-list>
  	<welcome-file>index.jsp</welcome-file>
  </welcome-file-list>
  
</web-app>

	
step5:
------
	Create "java" folder inside "src/main" folder.

step6:
------
	Create a "com.ihub.www" package inside "src/main/java" folder.

step7:
------
	Create a "TestSrv.java" file inside "com.ihub.www" package.

TestSrv.java
-----------
package com.ihub.www;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet(urlPatterns = "/test")
public class TestSrv extends HttpServlet 
{
	protected void doGet(HttpServletRequest req,HttpServletResponse res)throws ServletException,IOException
	{
		PrintWriter pw =res.getWriter();
		res.setContentType("text/html");
		
		pw.println("<center><h1>Welcome to Maven project </h1></center>");
		
		pw.close();
	}
}

step8:
------
	Run maven project.
	ex:
		right click to MavenProj --> run as --> run on server.



Q) What is the difference between GIT and GITHUB ?

GIT					GITHUB 
-------------				------------
It is a distributed version control	It is a hosting server for GIT.
system which is used to track the 
changes in each file of a project.

It is locally installed in a computer.	It is hosted on web.

It is a software.			It is a service.

It contains local repository.		It contains remote repository.

It is command based.			It is GUI.

GIT Stages
==========
There are three git stages.

1) Working Directory 

2) Staging area 

3) Repository 

Diagram: jsp7.1


Steps to push the code in GITHUB 
================================
step1:
-----
	Create a account in github.
	ex:
		https://github.com/
		
step2:
-----
	Login to GITHUB account.
	ex:
		username : NiyazulHasan
		password : ********

step3:
-----
	Create a remote repository.
	ex:
		https://github.com/NiyazulHasan/QT-JAVA-056

step4:
------
	Download and install GIT software.
	ex:
		https://git-scm.com/install/

step5:
------
	Create a "myfolder" on desktop.	

step6:
------
	Open git bash from "myfolder" location. 

step7:
------
	Initialized git empty repository.
	ex:	
		git init 

step8:
-----
	Change master branch to main branch.
	ex:
		git branch --move master main 

step9:
------
	Add the files to working directory.
	
step10:
-------
	Check git status.
	ex:
		git status 

step11:
---------
	Add the files to staging area.
	ex:
		git add . 
step12:
--------
	Commit the changes.
	ex:
		git commit -m "core java notes"

step13:
-------
	Add remote origin.
	ex:
		git remote add origin https://github.com/NiyazulHasan/QT-JAVA-056

step14:
------
	Push the code to remote repository.
	ex:
		git push -f origin main 

step15:
------
	Referesh the GITHUB page.
	ex:
		https://github.com/NiyazulHasan/QT-JAVA-056


Steps to pull the code from GITHUB 
===================================
step1:
------
	Create a "demo" folder on desktop.

step2:
-----
	Open the git bash from "demo" folder.

step3:
------
	Initialized the git empty repository.
	ex:
		git init

step4:
------
	Pull the code.
	ex:
		git pull https://github.com/NiyazulHasan/QT-JAVA-056

