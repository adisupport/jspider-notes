JDBC stands for Java Database Connectivity. JDBC is Interface to connect and execute the query with the database.
This Interfaces are implemented by database vendor, this class is called **Driver Class**.

### Connection Interface
``` Java JDBC Interfaces

public interface Connection{
	
	//creates a statement object that can be used to execute SQL queries.
	Statement createStatement();
	
	//Creates a Statement object that will 
	//generate ResultSet objects with the given type and concurrency.
	Statement createStatement(int resultSetType,int resultSetConcurrency)
	
	//is used to set the commit status. By default, it is true.
	void setAutoCommit(boolean status);

	//saves the changes made since the previous commit/rollback
	// is permanent.
	void commit();

	//Drops all changes made since the previous commit/rollback.
	void rollback();

	// closes the connection and Releases a JDBC resources immediately.
	close();
}
```
> [!tip] To Get Connection Object
Connection con = Driver.getConnetion(URL,username,password);
### Statement Interface

``` Java
public interface Statement{
	// execute SELECT Query
	ResultSet excuteQuery(`SQL Command`)
	
	// execute Schema Query like drop,create,insert,delete,Alter Table
	int excuteUpdate(`SQL Command`) 
	
	//is used to execute queries that may return multiple results
	public boolean execute(String sql)


	// is used to execute batch of commands.
	public int[] executeBatch()
}

```
> [!tip] To Get Statement Object
> Statement statement = con.createStatement();

### ResultSet Interface

>[!tip] What kind of APIs in ResultSet Interface
> JDBC return ResultSet object after completing Statement execution.
> ResultSet interface has **row Iterator** and **Getter** Methods

``` Java
public interface ResultSet{
	// move cursor to next row
	public boolean next();
	
	// move cursor to previous row
	public boolean previous();
	
	// move to first row
	public boolean first();
	
	// move to last row
	public boolean last();
	//move cusror to specific row number
	public boolean absoulte(int row);

	// is used to move the cursor to the relative row number in the 
	//ResultSet object, it may be positive or negative.
	//relative to **current** cusror Position
	public boolean relative(int row);
	
	// Retrive Data From Coloumn
	public int getInt(int coloumnIndex);
	public int getInt(String ColumnName);
	public String getString(String ColumnName);
	public String getString(int ColumnIndex);
}

```

## 5 Step To Run SQL Query On Database Using JDBC.


Step 1: Register Driver Class

``` Java
// Load driver class
String driverClassName = "sun.jdbc.odbc.JdbcOdbcDriver";
Class.forName(driverClassName);
```
`Class.forName can throw Exception ClassNotFoundException`
`Its Better to user *throws* Keyword in methods`

> [!note] Driver Class
> Driver class has the implementation of JDBC interface which we used to work with database.
> Every database vendor provides driver class.
> **How to get Driver Class**: use maven repository Search  like `Postgres JDBC Driver` and add into pom.xml file, that's it.

Step 2: Create Connection 
``` Java
// Obtain a connection
String url = "jdbc:odbc:XE";
String username = "scott";
String password = "tiger";
Connection con = DriverManager.getConnection( url, username,password);
```

Step 3: Obtain a statement object (DB CURSOR)
``` Java
// Obtain a statement
Statement st = con.createStatement();
```

Step 4: Execute SQL Command
``` Java
String query = "insert into students values(109, 'bhatt')";
int count = st.executeUpdate(query);
System.out.println("number of rows affected by this query= "+ count);
```

Step 5: Close Connection.
``` Java
con.close();
```


# Complete Code
```Java
//Java program to implement a simple JDBC application
package com.vinayak.jdbc;

import java.sql.*;

public class JDBCDemo {

	public static void main(String args[])
		throws SQLException, ClassNotFoundException
	{
		String driverClassName = "sun.jdbc.odbc.JdbcOdbcDriver";
		// Load driver class
		Class.forName(driverClassName);

		// Obtain a connection
		String url = "jdbc:odbc:XE";
		String username = "scott";
		String password = "tiger";
		Connection con = DriverManager.getConnection(
			url, username, password);

		// Obtain a statement
		Statement st = con.createStatement();

		// Execute the query
		String query = "insert into students values(109, 'bhatt')";
		int count = st.executeUpdate(query);
		System.out.println(
			"number of rows affected by this query= "
			+ count);

		// Closing the connection as per the
		// requirement with connection is completed
		con.close();
	}
} // class


```