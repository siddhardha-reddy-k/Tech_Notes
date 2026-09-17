JDBC
=====
As if now it is known as trademark.

But earlier it is known as Java Database Connectivity.

RAM is a temperory storage device or medium. 

During the program execution our data will store in a RAM.

Once the program execution is completed we will loss the data.

To overcome this limitation we are making our application writing the data into file or database software.

Files and database software's act like a permanent storage device or medium.

Persistence 
===========
The process of storing and managing the data for a long period of time is called persistence.


Important Terminologies 
=======================

1) Persistence store 
--------------------
It is  a place where we can store and manage the data for a long period of time.
ex:
	File's
	Database Software's.

2) Persistence data 
---------------------
A data of a persistence store is called persistence data.
ex:
	Records 
	Tables 

3) Persistence operations 
-------------------------
Create, Update, Delete, Insert , Select and etc are called persistence operations.
In realtime this operation is also known as CURD operation, CRUD operation or SCUD operation.
ex:
	C - create 		S - select 
	U - update 		C - create 
	R - read 		U - update 
	D - delete 		D - delete 

4) Persistence logic 
---------------------
A logic which is capable to perform persistence operations is called persistence logic.
ex:
	IOStream 
	JDBC Code 
	Hibernate Code 
	and etc.

5) Persistence technology 
-------------------------
A technology which is used to develop persistence logics is called persistence technology.
ex:
	JDBC 
	Hibernate 
	Ibatis 
	and etc.


Q) What is JDBC?

JDBC is a persistence technology which is used to develop persistence logics having the capability to perform persistence operations on persistence data of a persistence store.


Limitations with file as a persistence store 
============================================
> We can store limited amount of data.

> There is no security.

> Fetching the data with multiple conditions is not possible.

> It does not allow us to apply constraints.
  (Not Null, UNIQUE, Primary Key, Foreign Key and CHECK)

> It does not show an application with relationship.

> Updation and deletion of data can't be done directly.

> Merging and comparision of data can't be don easily.

Advantages of database as a persistence store 
============================================
> We can store unlimited amount of data.

> There is a security.

> Fetching the data with multiple conditions is possible.

> It allows us to apply constriants.

> It shows an application with relationships.

> Updation and deletion of data can be done directly.

> Merging and comparision of data can be done easily.

Note:
-----
		
			IOStream 
	JavaApp	-------------------------------- File 
		Serialization / Deserialization 


			JDBC Code 
	JavaApp -------------------------------- Database 

Every JDBC application is a two-tier application.

Java with JDBC code acts like a frontend/tier1/layer1 and databse software acts like a backend/tier2/layer2.

The one which is visible to the enduser to use the system is called frontend.

The one which is not visible to the enduser but it performs operations based on the instructions given by frontend is called backend.

Enduser is a non-technical person. He can't prepare and execute SQL query in database software. So he depend upon frontend developers having the capability to do that work for them.

Diagram: jdbc1.1


JDBC Driver 
===========
It acts like a bridge between java application and database software.
It is used to convert java instructions to database instructions and vice versa.
Diagram: jdbc1.2


ODBC Driver 
===========
VBScript, Perl, D2K uses ODBC driver to locate and interact with database software.

Diagram: jdbc1.3

ODBC driver is developed in c language by taking the support of pointers. Java does not support pointers.To overcome this limitation Sun Micro System introduced JDBC drivers exclusively.


Q) How many drivers are there in JDBC?

We have four types of JDBC drivers.

1) Type1 JDBC Driver / JDBC-ODBC Bridge Driver

2) Type2 JDBC Driver / Native API Driver 

3) Type3 JDBC Driver / Net Protocol Driver

4) Type4 JDBC Driver / Native Protocol Driver 


Q) What is JDBC?

A JDBC a open technology given by Sun Micro System having set of rules and guidelines to develop JDBC drivers to interact with multiple database softwares.
