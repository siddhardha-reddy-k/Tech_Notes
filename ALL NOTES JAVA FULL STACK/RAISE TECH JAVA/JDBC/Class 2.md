To use any JDBC driver we need to register with DriverManager service.

Every JDBC application contains one built-in service called DriverManager service.

Class.forName()
===============
It is recommanded to use Class.forName() method to register JDBC driver with DriverManager service.

It takes loads driver class but it won't create object.

ex:
	Class.forName("driver-class-name");

Connection object
=================
Connection is an interface which is present in java.sql package.

It is an object of underlying supplied java class which implements java.sql.Connection interface.

To perform any operation in database we need to establish the connection. 

Once work with database is completed we need to use close the connection.

ex:
	Connection con;

DriverManager.getConnection()
=============================
DriverManager is a class which is present in java.sql package.

A getConnection() method is used interact with database software and gets one connection object represent connectivity between java application and database software.

ex:
	Connection con = DriverManager.getConnection("url","uname","pwd");

Statement object
================
Statement is an interface which is present in java.sql package.

It is a object of underlying supplied java class which implements java.sql.Statement interface.

It acts like a vehicle between java application and database software.

It is used to sends and executes SQL query in database software.

We can create Statement object as follow.

ex:
	Statement st = con.createStatement();



ResultSet object
================
Every ResultSet contains two positions.

1) BFR (Before First Record/Row)

2) ALR (After Last Record/Row)

By default record pointer points to BFR position.

Diagram: jdbc2.1

Every record ResultSet having 1 as base index and every column of record ResultSet having 1 as base index.

rs.next()
=========
It is used to move the record pointer from current position to next position. If next position is a record then it returns true. If next position is a ALR then it returns false.

To read the record ResultSet we need to use getXxx(-) method  with index number or by using column name.

Types of Queries in JDBC
=========================
According to JDBC point of view we have two types of queries.

1) Select Query
---------------
It gives bunch of records from database software.
ex:
	select * from student; 

JDBC Statement object gave executeQuery() method to execute select queries.
ex:
	ResultSet rs = st.executeQuery("select * from student");


2) Non-Select Query 
------------------
It gives numeric value representing number of records effected in a database table.
ex:
	insert into student values(104,'ramulu','pune');
	update student set sname='rani' where sno=104;
	delete from student where sno=104;

JDBC Statement object gave executeUpdate() method to execute non-select query. 
ex:
	int result = st.executeUpdate("delete from student");



Steps to develop JDBC application 
=================================
There are six steps to develop JDBC application.

1) Register JDBC driver with DriverManager service.

2) Establish the connection with database software.

3) Create Statement object.

4) Sends and executes SQL query in database software.

5) Gather the result from database software to process the result.

6) Close all JDBC connection objects.


Oracle Database 
===============
Download link : 
https://drive.google.com/file/d/0B9rC21sL6v0td1NDZXpkUy1oMm8/view?usp=drive_link&resourcekey=0-aKooR3NmAh_eLo_qGw_inA

username : system (default name)
password : admin 



Type4 JDBC Driver / Database properties 
=======================================
Driver 		: oracle.jdbc.driver.OracleDriver
		  -----------------  ------------
			pkg-name	Driver-class

						portno
						|
URL		: jdbc:oracle:thin@localhost:1521:XE
		  -----------------   |		   |	
			sub-protocol  hostname	  logical-database-name

USERNAME	: system 

PASSWORD	: admin 
