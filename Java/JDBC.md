##JDBC

###JDBC Application Six Step
- 1.Import the packages: Requires that you include the packages containing the JDBC classes needed for database programming. Most often, using import java.sql.* will suffice.
- 2.Register the JDBC driver: Requires that you initialize a driver so you can open a communication channel with the database.
- 3.Open a connection: Requires using the DriverManager.getConnection() method to create a Connection object, which represents a physical connection with the database.
- 4.Execute a query: Requires using an object of type Statement for building and submitting an SQL statement to the database.
- 5.Extract data from result set: Requires that you use the appropriate ResultSet.getXXX() method to retrieve the data from the result set.
- 6.Clean up the environment: Requires explicitly closing all database resources versus relying on the JVM's garbage collection.

```java
//STEP 1. Import required packages
import java.sql.*;

public class JDBCPractice {
   // JDBC driver name and database URL
   static final String JDBC_DRIVER = "com.mysql.jdbc.Driver";
   static final String DB_URL = "jdbc:mysql://localhost/EMP";

   //  Database credentials
   static final String USER = "root";
   static final String PASS = "";

   public static void main(String[] args) {
	   Connection conn = null;
	   Statement stmt = null;
	   try{
	      //STEP 2: Register JDBC driver
	      ////forName(String name, boolean initialize, ClassLoader loader) method returns the Class object associated with the class or interface with the given string name, using the given class loader
	      Class.forName("com.mysql.jdbc.Driver");
	      //DriverManager.registerDriver(new com.mysql.jdbc.Driver());
	      //
	      //STEP 3: Open a connection
	      System.out.println("Connecting to database...");
	      conn = DriverManager.getConnection(DB_URL,USER,PASS);

	      //STEP 4: Execute a query
	      System.out.println("Creating statement...");
	      stmt = conn.createStatement();
	      String sql;
	      sql = "SELECT id, first, last, age FROM Employees";
	      ResultSet rs = stmt.executeQuery(sql);

	      //STEP 5: Extract data from result set
	      while(rs.next()){
	         //Retrieve by column name
	         int id  = rs.getInt("id");
	         int age = rs.getInt("age");
	         String first = rs.getString("first");
	         String last = rs.getString("last");

	         //Display values
	         System.out.print("ID: " + id);
	         System.out.print(", Age: " + age);
	         System.out.print(", First: " + first);
	         System.out.println(", Last: " + last);
	      }
	      //STEP 6: Clean-up environment
	      rs.close();
	      stmt.close();
	      conn.close();
	   }catch(SQLException se){
	      //Handle errors for JDBC
	      se.printStackTrace();
	   }catch(Exception e){
	      //Handle errors for Class.forName
	      e.printStackTrace();
	   }finally{
	      //finally block used to close resources
	      try{
	         if(stmt!=null)
	            stmt.close();
	      }catch(SQLException se2){
	      }// nothing we can do
	      try{
	         if(conn!=null)
	            conn.close();
	      }catch(SQLException se){
	         se.printStackTrace();
	      }//end finally try
	   }//end try
	   System.out.println("Goodbye!");
	}//end main
}//end FirstExample
```
