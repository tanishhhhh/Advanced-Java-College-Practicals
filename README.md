# Advanced Java College Practicals 

#Jsp Program to show Date and Time 
 
```
<%@ page import="java.util.Date" %>

    
    
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
    
<meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
<title>Guru current Date</title>

</head>
<%
    Date date = new Date();
    %>

<body>
    
    <h1>Todays Date</h1>
    <p> Todays Date is: <%=date %></p>

</body>
</html>
```


#Servlet to show date and time 
```							       
   (Enter in try block only)
   java.util.Date date = new java.util.Date();
            out.println("<h2> Current Date and Time is : " + date.toString() + "</h2>");
```
                                                                            
									    									    
#Cookies
```

Index.html

<form action="servlet1" method="post">
Name:<input type="text" name="userName"/><br/>
<input type="submit" value="go"/>
</form>


import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;


public class FirstServlet extends HttpServlet {

  public void doPost(HttpServletRequest request, HttpServletResponse response){
	try{

	response.setContentType("text/html");
	PrintWriter out = response.getWriter();
		
	String n=request.getParameter("userName");
	out.print("Welcome "+n);

	Cookie ck=new Cookie("uname",n);//creating cookie object
       	response.addCookie(ck);//adding cookie in the response

	//creating submit button
	out.print("<form action='servlet2' method='post'>");
	out.print("<input type='submit' value='go'>");
	out.print("</form>");
		
	out.close();

        }catch(Exception e){System.out.println(e);}
  }
}



Servlet2.java

import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class SecondServlet extends HttpServlet {

public void doPost(HttpServletRequest request, HttpServletResponse response){
	try{

	response.setContentType("text/html");
	PrintWriter out = response.getWriter();
	
	Cookie ck[]=request.getCookies();
	out.print("Hello "+ck[0].getValue());

	out.close();

         }catch(Exception e){System.out.println(e);}
	}
	

}
```


#Jdbc Displayyy data
 ```
package javaapplication1;

import java.sql.*;

public class javaapplication1 {

    public static void main(String[] args) {
        try {
            Class.forName("com.mysql.jdbc.Driver");
            System.out.println("JavaApplication1.JavaApplication1.main()");
            System.out.println("connection");
            Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/sys", "root", "root");
            System.out.println("Driver");
            Statement stmt = con.createStatement();
            ResultSet rs = stmt.executeQuery("select * from login");

            while (rs.next()) {
                System.out.println(rs.getString(2) + " " + rs.getString(1));
                con.close();
            }
        } catch (ClassNotFoundException | SQLException e) {
            System.out.println(e);
        }
    }

    private static Statement createStatement() {
        throw new UnsupportedOperationException("Not SupportedYet");
    }
}
```




#Jdbc Insert dataaaa
```


import java.sql.*;

public class InsertTest {

    static final String DB_URL = "jdbc:mysql://localhost/sys";
    static final String USER = "root";
    static final String PASS = "root";

    public static void main(String[] args) {
        Connection conn = null;
        Statement stmt = null;
        try {
            Class.forName("com.mysql.jdbc.Driver");

            System.out.println("Connecting to database...");
            conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/sys", "root", "root");

            System.out.println("Inserting data into table...");
            stmt = conn.createStatement();
            String sql;
            sql = "insert into login(Name,Password) values ('Test1', 'Test2')";
            stmt.executeUpdate(sql);

            System.out.println("Data inserted successfully!");

        } catch (SQLException | ClassNotFoundException se) {
        } finally {
            try {
                if (stmt != null) {
                    stmt.close();
                }
            } catch (SQLException se2) {
            }
            try {
                if (conn != null) {
                    conn.close();
                }
            } catch (SQLException se) {
            }
        }
        System.out.println("Goodbye!");
    }
}
```
