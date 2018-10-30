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

# Connecting Data Server Manager

A connection between your IBM® Data Server Manager and your {{site.data.keyword.dashdbshort_notm}} database enables you to monitor and manage the database from the Data Server Manager web console. 
{: shortdesc}

## Prerequisites

Before attempting to connect to your {{site.data.keyword.dashdbshort_notm}} database, verify that you have the necessary [prerequisites](connecting.html#prereqs).

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## Procedure

The connection procedure was tested on Data Server Manager version 1.1. The same procedure applies to all of the other versions of the Data Server Manager software.

To create a connection, complete the following steps:

1. Log in to your Data Server Manager web console.
    
2. In the Data Server Manager web console, go to **Set Up > Database Connections**.
    
3. Click the ![+ sign inside a circle](images/icon_R_plus.gif) icon to add a database connection. On the **Add Database Connection** page under the **Database Connection** tab, enter the required information in the following fields:

   - *Database connection name*: The name must be unique to Data Server Manager
   - *Data server type*: From the drop-down menu, select **DB2 for Linux, UNIX, and Windows**
   - *Database name*: `BLUDB`
   - *Host name*: Enter the {{site.data.keyword.dashdbshort_notm}} host name 
   - *Port number*: For a connection without SSL, enter `50000`. For a connection with SSL, enter `50001`. 
   - *JDBC security*: From the drop-down menu, select **Clear text password**
   - *User ID*: Your {{site.data.keyword.dashdbshort_notm}} user ID 
   - *Password*: Your {{site.data.keyword.dashdbshort_notm}} password 

4. For a connection with SSL, select the **Advanced JDBC Properties** tab. Enter the required information in the following fields:

   - *Property*: `sslConnection`
   - *Value*: `true`

    Click the **Add** button. Select the **Database Connection** tab.
    
5. Test the connection by clicking the **Test Connection** button. If the connection is successful, click **OK**.

