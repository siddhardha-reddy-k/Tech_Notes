If jdbc Statement object is created without TYPE,MODE value then ResultSet object is called Non-Scrollable ResultSet object.

ex:
	Statement st = con.createStatement();
	ResultSet rs = st.executeQuery("select * from student");

If JDBC Statement object is created with TYPE,MODE value then ResultSet object is called Scrollable ResultSet object.

ex:
	Statement st = con.createStatement(TYPE_VALUE,MODE_VALUE);
	ResultSet rs = st.executeQuery("select * from student");


We have following list of TYPE values.
ex:
	ResultSet.TYPE_SCROLL_SENSITIVE
	ResultSet.TYPE_SCROLL_INSENSITIVE

We have following list of MODE values.
ex:
	ResultSet.CONCUR_READ_ONLY
	ResultSet.CONCUR_UPDATABALE 

ex:
---
package com.ihub.www;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;

public class ScrollableResultSetApp 
{
	public static void main(String[] args)throws Exception  
	{
		Class.forName("oracle.jdbc.driver.OracleDriver");
		Connection con = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE","system","admin");
		Statement st = con.createStatement(ResultSet.TYPE_SCROLL_SENSITIVE,ResultSet.CONCUR_READ_ONLY);
		String qry = "select * from student";
		ResultSet rs = st.executeQuery(qry);
		
		//top to bottom 
		while(rs.next())
		{
			System.out.println(rs.getRow()+" "+rs.getInt(1)+" "+rs.getString(2)+" "+rs.getString(3));
		}
		
		//bottom to top 
		rs.afterLast();
		while(rs.previous())
		{
			System.out.println(rs.getRow()+" "+rs.getInt(1)+" "+rs.getString(2)+" "+rs.getString(3));
		}
		
		rs.first();
		System.out.println(rs.getRow()+" "+rs.getInt(1)+" "+rs.getString(2)+" "+rs.getString(3));
		
		rs.last();
		System.out.println(rs.getRow()+" "+rs.getInt(1)+" "+rs.getString(2)+" "+rs.getString(3));
		
		rs.relative(-1);
		System.out.println(rs.getRow()+" "+rs.getInt(1)+" "+rs.getString(2)+" "+rs.getString(3));
		
		
		rs.close();
		st.close();
		con.close();
	}
}


Steps to interact with MySQL Database
=====================================
step1:
------
	Download and Install MySQL database.
	ex:
		https://dev.mysql.com/downloads/installer/

step2:
------
	Copy the mysql server bin directory and paste in environmental variables.
		 	
	ex:
		user variables : 
		----------------
		variable name : Path 
		variable value : C:\Program Files\MySQL\MySQL Server 8.0\bin;	

step3:
------
	Connect to mysql database.
			
		cmd> mysql -u root -p (press enter btn)
			password : root 
	
	ex:
		username : root (default)
		password : root 

step4:
------
	Create a schema and use that schema.	
	ex:
		create schema batch56;
		
		show databases;
		
		use  batch56;

step5:
------
	Create a student table with records.
	ex:
		create table student(sno int(3),sname varchar(10),sadd varchar(12));

		insert into student values(101,'venkat','hyd');
		insert into student values(102,'charan','delhi');
		insert into student values(103,'thimmappa','vizag');
		commit;		
		select * from student;

step6:
------
	Launch Eclipse IDE by choosing workspace location.

step7:
------
	Create a java project i.e MySQLProj.
	

step8:
------
	Add "mysql-connector-j.jar" file in project build path.

	ex:
		https://repo1.maven.org/maven2/com/mysql/mysql-connector-j/8.0.31/

step9:
------
	Create a "com.ihub.www" package inside "src" folder.

step10:
------
	Create a SelectApp.java file inside "com.ihub.www" package.

SelectApp.java
--------------
package com.ihub.www;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;

public class SelectApp 
{
	public static void main(String[] args) 
	{
		final String DRIVER="com.mysql.cj.jdbc.Driver";
		final String URL="jdbc:mysql://localhost:3306/batch53";
		final String USERNAME="root";
		final String PASSWORD="root";
		final String QUERY="select * from student";
		
		Connection con = null;
		PreparedStatement ps = null;
		ResultSet rs = null;
		try
		{
			Class.forName(DRIVER);
			con = DriverManager.getConnection(URL,USERNAME,PASSWORD);
			ps = con.prepareStatement(QUERY);
			rs = ps.executeQuery();
			while(rs.next())
			{
				System.out.println(rs.getRow()+" "+rs.getInt(1)+" "+rs.getString(2)+" "+rs.getString(3));
			}
			rs.close();
			ps.close();
			con.close();
		}
		catch(Exception e)
		{
			e.printStackTrace();
		}
	}
}

step11:
------
	Run SelectApp.java file.




JDBC Application to interact with MongoDB Database
====================================================

step1:
-----
	Download and install MongoDB Community Server.
	ex:
		https://www.mongodb.com/try/download/community

step2:
-----
	Downoad and install MongoDB Shell.
	ex:
		https://www.mongodb.com/try/download/shell

step3:
------
	Extract Mongodb shell inside "MongoDB" folder.
	ex:
		C:\Program Files\MongoDB

step4:
------
	Copy "bin" directory of mongoshell.
	ex:
		C:\Program Files\MongoDB\mongosh-2.3.0-win32-x64\bin

step5:
-----
	Paste "bin" directory in environmental variables.
	ex:
		right click to This PC --> properties --> Advanced System Settings -->
		Environmental variables -->  System variables --> click to path --> click to edit 
		button --> New --> paste (C:\Program Files\MongoDB\mongosh-2.3.0-win32-x64\bin) -->ok
		--->ok  --->ok.

step6:
-----
	Launch Eclipse IDE by choosing workspace location.

step7:
-----
	Create java project i.e MongoDBProj inside eclipse IDE.

	ex:
		File --> New --> Java project --> Name : MongoDBProj --> Next --> Finish.

step8:
-----
	Download and add mongodb jar file in project build path.
	ex:
		jar file link : 
		https://repo1.maven.org/maven2/org/mongodb/mongo-java-driver/3.11.2/


	right click to MongoDBProj --> Buildpath --> configure build path --> libraries -->
	click to classpath --> add external jars --> select mongo-java-driver.jar file --> 
	Open --> Apply and close.

step9:
------
	Create a "com.ihub.www" package inside "src" folder.

step10:
------
	Create a InsertApp.java file inside "com.ihub.www" package.

SelectApp.java
--------------
package com.ihub.www;

import org.bson.Document;

import com.mongodb.client.MongoClient;
import com.mongodb.client.MongoClients;
import com.mongodb.client.MongoCollection;
import com.mongodb.client.MongoDatabase;

public class InsertApp 
{
	public static void main(String[] args) 
	{
		try(MongoClient mongoClient=MongoClients.create("mongodb://localhost:27017");)
		{
			MongoDatabase mongoDatabase=mongoClient.getDatabase("myDatabase");
			
			MongoCollection<Document> mongoCollection=mongoDatabase.getCollection("myCollection");
			
			Document doc=new Document("id", 101)
							.append("name","Alan")
							.append("add","Hyd");
			
			mongoCollection.insertOne(doc);
			
			System.out.println("Record Inserted in MongoDB");
			
		}
		catch(Exception e)
		{
			e.printStackTrace();
		}
	}
}

step11:
-------
	Run the jdbc application.


MongoDB Commands
=================

show dbs;

use  myDatabase;

show collections; 

db.myCollection.find();

db.myCollection.drop();

db.dropDatabase();  or db.myDatabase.drop();




SelectApp.java
-------------
package com.ihub.www;

import org.bson.Document;

import com.mongodb.client.MongoClient;
import com.mongodb.client.MongoClients;
import com.mongodb.client.MongoCollection;
import com.mongodb.client.MongoDatabase;

public class InsertApp 
{
	public static void main(String[] args) 
	{
		try(MongoClient mongoClient=MongoClients.create("mongodb://localhost:27017");)
		{
			MongoDatabase mongoDatabase=mongoClient.getDatabase("myDatabase");
			
			MongoCollection mongoCollection=mongoDatabase.getCollection("myCollection");
			
			Document doc=(Document) mongoCollection.find(new Document("id",101)).first();
			
			System.out.println(doc);
		}
		catch(Exception e)
		{
			e.printStackTrace();
		}
	}
}
