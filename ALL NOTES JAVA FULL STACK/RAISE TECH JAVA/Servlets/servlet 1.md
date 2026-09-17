	Web Application 
===============
A web application is a software application which runs in a web server.

A web application is a interactive, data driven application which can be accessible by the browser over the network using HTTP protocol.

ex:
	https://www.flipkart.com 
	https://www.amazon.in 

A web application is a collection of web resource programs having the capability to generate web pages.

Diagram: servlet1.1

We have two types of web pages.

1) Static web pages / Passive web pages
----------------------------
A web page with fixed content is called static web page.
ex:
	facebook login page 
	Home page 
	About us page 
	contact us page 
	and etc.

2) Dynamic web pages / Active web pages 
--------------------------------------
A web page with dynamic content is called dynamic web page.
ex:
	Live cricket score page 
	stock market share value page 
	news page
	and etc 
	

We have two types of web resource programs.

1) Static web resource programs 
-------------------------------
A web resource program which is used to develop static web pages.
ex:
	HTML program 
	CSS program 
	Bootstrap program 
	angularjs program 
	reactjs program 
	and etc.

2) Dynamic web resource programs 
---------------------------------
A web resource program which is used to develop dynamic web pages.
ex:
	Servlet program 
	JSP program 
	and etc.

Based on the position and execution these web resource programs are classified into two types.

1) Client side web resource programs
-----------------------------------
A web resource program which executes at client side (Browser window) is called client side web resource program.

All static web resource programs are called client side web resource programs.
ex:
	HTML program 
	CSS program 
	Bootstrap program 
	Angularjs program 
	and etc.

2) Server side web resource programs
------------------------------------
A web resource program which executes at server side is called server side web resource program.

All dynamic web resource programs are called server side web resource programs.
ex:
	Servlets program 
	JSP program 
	and etc.

Note:
-----
The processing keeping the web application in a server is called deployment and reverse is called undeployment.

Web Application and Web Resource program Execution 
===================================================
Java application executes manually.

Web application and web resource program executed at the time when they have requested.

Diagram: servlet1.2

With respect to the diagram

1) Enduser gives the request to web resource program.

2) A web server traps that request and passes that request to appropriate web resource 
   program.

3) A web resource program executes the logic to process the request.

4) A web resource program communicates with database software if necessary.

5) A web resource program sends the result to web server.

6) A web server gives the output to browser window as dynamic response.


Web Server 
==========
A web server is a combination of software and hardware which is used to store , process and generate dynamic content such as web pages, images, audios, videos and etc.

It is a piece of software which is used to automate whole process of web application and web resource program execution.

ex:
	Tomcat, Resin and etc.


Responsibilities of web server
==============================
1) It takes contineous request.

2) It traps the request and forward to appropriate web resource program.

3) It provides environment to deploy and undeploy the web applications.

4) It allows to execute client side web resource programs at browser window.

5) It will add middleware services only to deployed web applications.

6) It takes the response and forward to browser window as dynamic response.

7) It is used to automate whole process of web application and web resource program 
   execution.

Note:
-----
	To execute java program we required JRE/JVM.
	To execute servlet program we required servlet container.
	To execute jsp program we required jsp container.


Web Container 
============
A web container is a software application which is used to manage whole process of web resource program i.e from birth to death.

Servlet container manage whole process of servlet program.

JSP container manage whole process of jsp program.

Some part of industry considers servlet container and JSP container are web containers.

Every server is designed to support servlet container and JSP container.


Tomcat 
======
Version			:	Tomcat 9 

Vendor			:	Apache Software Foundation (ASF)

Website			:	https://tomcat.apache.org

Port No			:	8080

Servlet container 	:	Catalina 

JSP container		:	Jasper 

Download link		:

https://drive.google.com/file/d/1u547booDvVY630rN4drEQ8c8lU0In7T6/view?usp=drive_link



Tomcat Software Installation 
============================
Double click to Tomcat software --> Yes --> Next --> I Agree --> select Full -->
Next --> adminstrator login : username : admin 
			      password : admin   ---> Next ---> Next --> Install.


Steps to setup Tomcat to manual mode 
====================================
services ---> Apache Tomcat --> click to stop link --> double click to apache tomcat --> startup type : manual --> Apply --> ok.
