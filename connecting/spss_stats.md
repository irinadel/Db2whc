---

copyright:
  years: 2014, 2018
lastupdated: "2018-09-25"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Connecting SPSS Statistics

These instructions explain how to create a connection from IBM® SPSS® Statistics to a {{site.data.keyword.dashdbshort_notm}} database.
{: shortdesc}

## Prerequisites

Before attempting to connect to your {{site.data.keyword.dashdbshort_notm}} database, verify that you have the necessary [prerequisites](connecting.html#prereqs).

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## Procedure

1. In SPSS Statistics, click **File > Open Database > New Query**.
    
2. In the Database Wizard, click **Add ODBC data source**.
    
3. Use the ODBC Data Source Administrator window to add an ODBC data source name (DSN) for the {{site.data.keyword.dashdbshort_notm}} database:
        
   a. On the **User DSN** tab, click **Add**.

   b. On the Create New Data Source window, select the driver that is named **IBM DB2 ODBC DRIVER** and click **Finish**.

   Be sure that the driver that you select is not a driver with a similar name such as `IBM DB2® ODBC DRIVER - DB2COPY`. If the driver does not appear in the list, exit SPSS Statistics, then download and install the driver. See [Db2 driver package](driver_pkg.html).
        
   c. In the ODBC IBM Driver - Add window, enter a data source name (usually the name of the database you are connecting to), and click **Add**.
        
   d. From the CLI/ODBC Settings window, on the **Data Source** tab, enter the user ID and password from the [connection information](credentials.html) that you collected beforehand.
        
   e. On the Advanced Settings page, for each of the following parameters, click **Add** to open the Add CLI Parameter window to begin the step, and click **OK** to return to the Advanced Settings page:
            
   - Select the `Database` parameter, then click **OK** to open the CLI/ODBC Settings window. In the **Pending Value** field, enter the database name from the connection information that you collected beforehand.

   - Select the `Hostname` parameter, then click **OK** to open the CLI/ODBC Settings window. In the **Pending Value** field, enter the host name from the connection information that you collected beforehand.

   - Select the `Port` parameter, then click **OK** to open the CLI/ODBC Settings window. In the **Pending Value** field, enter the port number from the connection information that you collected beforehand.
            
   - Select the `Protocol` parameter, then click **OK** to open the CLI/ODBC Settings window. Select **TCP/IP**.
        
   f. Click **OK** to return to the ODBC Data Source Administrator window.
        
   g. On the **User DSN** tab, select the data source name, then click **Configure**.
        
   h. On the CLI/ODBC Settings window, click **Connect** to test the connection.
            
   - If the connection is successful, click **OK** to return to the ODBC Data Source Administrator window, and then click **OK** to exit the window.
            
   - If the connection is not successful, note and correct any errors before you test the connection again.
