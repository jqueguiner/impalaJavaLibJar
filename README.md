impalaJavaLibJar
================

jar file for Java connection to Impala no Maven needed

## Included JAR

the source contains the following packages needed to connect Java Web App to Impala Client:

* commons-logging-1.1.3.jar
* hadoop-common.jar
* hive-common.jar
* hive-jdbc.jar
* hive-metastore.jar
* hive-service.jar
* libfb303-0.9.0.jar
* libthrift-0.9.2.cloudera.2.jar
* log4j-1.2.16.jar
* slf4j-api-1.7.5.jar
* httpcore-4.1.3.jar
* httpclient-4.2.5.jar
* log4j.properties

## Original Instruction on Impala

Original Instructions can be found here:
http://www.cloudera.com/content/cloudera-content/cloudera-docs/Impala/latest/Installing-and-Using-Impala/ciiu_impala_jdbc.html

## Usage in Eclipse
Include the ImpalaConnection JAR file provide in eclipse by following this tutorial:
http://www.wikihow.com/Add-JARs-to-Project-Build-Paths-in-Eclipse-%28Java%29

## Example of Java Class
Example from the very nice github https://github.com/onefoursix/Cloudera-Impala-JDBC-Example

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class test {
	// here is an example query based on one of the Hue sample tables
	//keep the limit 10 for testing
	private static final String SQL_STATEMENT = "SELECT * FROM yourtable limit 10";
	// set the impalad host 127.0.0.1 for localhost
	private static final String IMPALAD_HOST = "127.0.0.1";
	// port 21050 is the default impalad JDBC port
	private static final String IMPALAD_JDBC_PORT = "21050";
	private static final String CONNECTION_URL = "jdbc:hive2://" + IMPALAD_HOST + ':' + IMPALAD_JDBC_PORT + "/;auth=noSasl";
	private static final String JDBC_DRIVER_NAME = "org.apache.hive.jdbc.HiveDriver";
	
	public static void main(String[] args) {
		
		System.out.println("\n=============================================");
		System.out.println("Cloudera Impala JDBC Example");
		System.out.println("Using Connection URL: " + CONNECTION_URL);
		System.out.println("Running Query: " + SQL_STATEMENT);
		Connection con = null;
		
		try {
			Class.forName(JDBC_DRIVER_NAME);
			con = DriverManager.getConnection(CONNECTION_URL);
			Statement stmt = con.createStatement();
			ResultSet rs = stmt.executeQuery(SQL_STATEMENT);
			System.out.println("\n== Begin Query Results ======================");
			// print the results to the console
			while (rs.next()) {
				// the example query returns one String column
				System.out.println(rs.getString(1));
			}
			System.out.println("== End Query Results =======================\n\n");
		} catch (SQLException e) {
			e.printStackTrace();
		} catch (Exception e) {
			e.printStackTrace();
		} finally {
			try {
				con.close();
			} catch (Exception e) {
				// swallow
			}
		}
	}
}
```
