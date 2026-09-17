Batch Processing 
================
Batch processing is used to declare multiple queries to a batch and makes a single call to database software.

To add the queries to batch we need to use addBatch() method of Statement object.
ex:
	st.addBatch(query);

To execute the batch we need to use executeBatch() method of Statement object.
ex:
	int[] result = st.executeBatch();

ex:
---
package com.ihub.www;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.Statement;

public class BatchProcessingApp 
{
	public static void main(String[] args)throws Exception 
	{
		Class.forName("oracle.jdbc.driver.OracleDriver");
		Connection con = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE","system","admin");
		Statement st = con.createStatement();
		
		//declare the queries 
		String qry1 = "insert into student values(105,'sai','hyd')";
		String qry2 = "update student set sname='rani' where sname='raja'";
		String qry3 = "delete from student where sno=104"; 
		
		//add the queries to batch 
		st.addBatch(qry1);
		st.addBatch(qry2);
		st.addBatch(qry3);
		
		//execute the batch 
		int[] result = st.executeBatch();
		
		int sum = 0;
		for(int i : result)
		{
			sum += i;
		}
		System.out.println("Number of Records effected are :"+sum);
		
		st.close();
		con.close();
	}
}



Transaction Management 
======================
Transaction means single unit of work.

In transaction management we commit if transaction done successfully.

In transaction management we rollback if transaction failed.

Diagram: jdbc9.1

SBI table 
=========
drop table sbi;
create table sbi(accno number(6),accholder varchar2(10),accbal number(8));
insert into sbi values(100001,'saichand',80000);
insert into sbi values(200002,'kiran',90000);
commit;

KOTAK table 
===========
drop table kotak;
create table kotak(accno number(6),accholder varchar2(10),accbal number(8));
insert into kotak values(111111,'revanth',5000);
insert into kotak values(222222,'sudharshan',6000);
commit;


package com.ihub.www;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.Statement;
import java.util.Scanner;

public class TXNManagementApp 
{
	public static void main(String[] args)throws Exception  
	{
		Scanner sc = new Scanner(System.in);
		
		System.out.println("Enter the source account number :");
		int sno = sc.nextInt();
		
		System.out.println("Enter the destination account number :");
		int dno = sc.nextInt();
		
		System.out.println("Enter the amount to transfer :");
		int amount = sc.nextInt();
		
		Class.forName("oracle.jdbc.driver.OracleDriver");
		Connection con = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE","system","admin");
		
		//set auto commit false
		con.setAutoCommit(false);
		
		Statement st = con.createStatement();
		
		String qry1 = "update sbi set accbal = accbal -"+amount+" where accno="+sno;
		String qry2 = "update kotak set accbal = accbal +"+amount+" where accno="+dno;
		
		//add the queries to batch 
		st.addBatch(qry1);
		st.addBatch(qry2);
		
		//execute the batch 
		int[] result = st.executeBatch();
		
		boolean flag=true;
		for(int i : result)
		{
			if(i==0) 
			{
				flag=false;
				break;
			}
		}
		if(flag==true)
		{
			System.out.println("Transaction Done Successfully");
			con.commit();
		}
		else
		{
			System.out.println("Transaction Failed ");
			con.rollback();
		}
		
		st.close();
		con.close();
	}
}

Types of ResultSet object
=========================
We have two types of ResultSet objects.

1) Non-Scrollable ResultSet object

2) Scrollable ResultSet object 

Diagram: jdbc9.2

1) Non-Scrollable ResultSet object
----------------------------------
If a ResultSet object which allows us to read the records sequentially, uni-directionally is called non-scrollable ResultSet object.

By default every ResultSet object is a non-scrollable ResultSet object.

2) Scrollable ResultSet object 
--------------------------------
If a ResultSet object which allows us to read the records non-sequentially, randomly, bi-directionaly is called scrollable ResultSet object.
