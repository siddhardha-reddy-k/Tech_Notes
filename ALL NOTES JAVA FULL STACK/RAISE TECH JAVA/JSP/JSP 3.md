2) Using <error-page> element in web.xml file 
=============================================
This approach is recommanded to use because we don't need to define errorPage attribute in each jsp page. Defining single entry of <error-page> element in web.xml file will handle all types of exceptions.


Deployment Directory structure 
------------------------------
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
		|---web.xml 
Note:
----
In above application we need to add "servlet-api.jar" file in project build path.

form.html
--------

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
  
  <error-page>
  	<exception-type>java.lang.Exception</exception-type>
  	<location>/error.jsp</location>
  </error-page>
  
  <welcome-file-list>
  	<welcome-file>form.html</welcome-file>
  </welcome-file-list>
</web-app>

process.jsp
-----------

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
----------
<%@page isErrorPage="true" %>
<b>
	<i style="color:red">
		Sorry!! Exception occurred
	</i>
</b>
<br>
<%= exception %>

web.xml
--------
	http://localhost:2525/JspApp5/

Jsp to Database Communication 
=============================

Deployment Directory Structure 
------------------------------
JspApp6
|
|---Java Resources
|
|---WebContent
	|
	|---form.html
	|---process.jsp 	
	|---WEB-INF
		|
		|-------web.xml 
		|-------lib
			|
			|---ojdbc14.jar
Note:
----
In above application we need to add "servlet-api.jar" and "ojdbc14.jar" file in project build path.

form.html
---------
<form action="process.jsp">

	No : <input type="text" name="t1"/> <br>
	
	Name : <input type="text" name="t2"/> <br>
	
	Address : <input type="text" name="t3"/> <br>
	
	<input type="submit" value="submit"/>

</form>

process.jsp
-----------
<%@page import="java.sql.*" %>
<%
	String sno = request.getParameter("t1");
	int no = Integer.parseInt(sno);
	String name = request.getParameter("t2");
	String add = request.getParameter("t3");
	
	Connection con = null;
	PreparedStatement ps = null;
	int result = 0;
	String qry = null;
	try
	{
		Class.forName("oracle.jdbc.driver.OracleDriver");
		con = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE","system","admin");
		qry = "insert into student values(?,?,?)";
		ps = con.prepareStatement(qry);
		//set the values 
		ps.setInt(1,no);
		ps.setString(2,name);
		ps.setString(3,add);
		//execute 
		result = ps.executeUpdate();
		if(result==0)
			out.println("No Record Inserted");
		else
			out.println("Record Inserted");
		
		ps.close();
		con.close();
	}
	catch(Exception e)
	{
		out.println(e);
	}
%>

web.xml
-------
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" id="WebApp_ID" version="4.0">

  <display-name>JspApp6</display-name>
  
  <welcome-file-list>
    <welcome-file>form.html</welcome-file>
  </welcome-file-list>

</web-app>

Request url 
-----------
	http://localhost:2525/JspApp6/


JSP application to read the data from database 
==============================================

Deployment Directory Structure 
------------------------------
JspApp7
|
|---Java Resources
|
|---WebContent 
	|
	|---process.jsp 
	|---WEB-INF
		|
		|------web.xml 
		|------lib
			|
			|---ojdbc14.jar	
Note:
-----
In above application we need to add "servlet-api.jar" and "ojdbc14.jar" file in project build path.

process.jsp
-----------
<%@page import="java.sql.*" %>

<center>
	<h2> 
		<a href="process.jsp?flag=true"> Fetch Data </a>
	</h2>
</center>
<hr/>

<%
	if("true".equals(request.getParameter("flag")))
	{
%>
	<table border="1" width="100%">
		<tr>
			<th>No</th>
			<th>Name</th>
			<th>Address</th>
		</tr>
		
<%
		Connection con = null;
		PreparedStatement ps = null;
		ResultSet rs = null;
		String qry = null;
		try
		{
			Class.forName("oracle.jdbc.driver.OracleDriver");
			con = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE","system","admin");
			qry = "select * from student";
			ps = con.prepareStatement(qry);
			rs = ps.executeQuery();
			while(rs.next())
			{
%>
				<tr>
					<td> <%= rs.getInt(1) %></td>
					<td> <%= rs.getString(2)  %></td>
					<td> <%= rs.getString(3)  %></td>
				</tr>
<% 
			}
		}
		catch(Exception e)
		{
			out.println(e);		
		}
%>
		
		
	</table>
<%		
	}
%>

web.xml
--------
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" id="WebApp_ID" version="4.0">
  
  <display-name>JspApp7</display-name>
  
  <welcome-file-list>
    <welcome-file>process.jsp</welcome-file>
  </welcome-file-list>

</web-app>

Request url
---------
	http://localhost:2525/JspApp7/
