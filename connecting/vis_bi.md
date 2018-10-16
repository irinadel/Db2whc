---

copyright:
  years: 2014, 2018
lastupdated: "2018-10-15"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Data visualization/BI
{: #overview}

You can also connect external applications and tools to {{site.data.keyword.dashdbshort_notm}} and use them to further manage or analyze your data. 
{: shortdesc}

## Cognos Analytics
{: #cognos}

You can run your IBM Cognos® reports against data in the cloud rather than the data in an on-premises database. After you load your data to a {{site.data.keyword.dashdbshort_notm}} database, you set up the JDBC driver, and then use the Cognos administration tools to create the database connection. <!--These instructions explain how to connect to the database from Cognos version 10.2.1.-->
{: shortdesc}

[Connecting Cognos Analytics ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/en/SSEP7J_11.0.0/com.ibm.swg.ba.cognos.ug_cra.doc/c_create_ds.html#create_ds){:new_window}

## Looker
{: #looker}

You can connect Looker to a {{site.data.keyword.dashdbshort_notm}} database. Looker is a business intelligence app and big data analytics platform with which you can explore, analyze, and share real-time business analytics.
{: shortdesc}

[Connecting Looker ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://docs.looker.com/setup-and-management/connecting-to-db){:new_window}

## Tableau
{: #tableau}

These instructions explain how to connect Tableau to a {{site.data.keyword.dashdbshort_notm}} database and apply to Tableau Desktop<!--version 8.x-->, but you can use similar steps for other Tableau tools.
{: shortdesc}

### Prerequisites

Before attempting to connect to your {{site.data.keyword.dashdbshort_notm}} database, verify that you have the necessary [prerequisites](connecting.html#prereqs).

### Procedure

1. In Tableau Desktop, open the window or page in your tool that is used to define a database connection.
2. From the start page, click **Connect to data**.
3. From the **Data Sources** list, select the data source or driver to use for your database connection. In the **On a server** section of the list, select **IBM Db2**.
4. From the **IBM DB2 Connection** window, enter the connection information by using the following table.

| Tableau field | Db2 connections information field |
|---------------|-----------------------------------|
| Step 1: Enter a server name | Host name |
| Step 2: Port | Port number |
| Step 3: Enter a database on the server | Database name |
| Username | User ID |
| Password | Password |
{: caption="Table 1. Fields in Tableau for connection information" caption-side="top"}

5. Click **Connect** to establish the connection. Tableau offers several options for connecting to your data. To make full use of your {{site.data.keyword.dashdbshort_notm}} database, choose the **Connect Live** option.

## Microsoft Excel
{: #excel}

These instructions explain how to connect Microsoft Excel <!--2010-->to a {{site.data.keyword.dashdbshort_notm}} database.
{: shortdesc}

### Prerequisites

Before attempting to connect to your {{site.data.keyword.dashdbshort_notm}} database, verify that you have the necessary [prerequisites](connecting.html#prereqs).

You must have the Db2 driver package or the IBM® Data Server Driver Package installed on your local computer. 

**Restriction**: Connections between Excel and {{site.data.keyword.dashdbshort_notm}} are supported on only the Windows operating system.

### Procedure

1. In the web console, go to the **Run SQL** page.
    
2. Type one or more SELECT statements in the editor text box.

3. Click one of the Run options.

4. Click **Excel ODC File**.

5. Download and open the `BLUExcel.odc` file in Excel. If a security notice is displayed, click **Enable**.

6. Click **Open** to connect to the {{site.data.keyword.dashdbshort_notm}} database. The **Connect To DB2 Database** dialog box opens.

7. Type the user ID and password that you use to log in to {{site.data.keyword.dashdbshort_notm}}. To obtain the user ID and password, click **Connect** in the web console or **Connect > Connection Information** in the web console.

8. Ensure that the connection mode is `Share`, and then click **OK**.

### Results

The query results are displayed in an Excel spreadsheet. These are the same results that are displayed in the Results viewer. Now you can generate charts and reports and analyze your data by using Excel. For more information about how to do this and how to run SQL queries on your data from the web console, see: 
- [Tutorial: Generating charts and reports by using Excel ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.analytics.doc/doc/explore_excel_reports.html){:new_window}
- [Analyzing with Excel ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.analytics.doc/doc/exploreexcel.html){:new_window}

## Esri ArcGIS for Desktop
{: #esri_arcgis}

You can connect Esri ArcGIS for Desktop <!--version 10.3.1 -->to a {{site.data.keyword.dashdbshort_notm}} database and then use it to analyze and visualize geospatial data.
{: shortdesc}

### Prerequisites

Before attempting to connect to your {{site.data.keyword.dashdbshort_notm}} database, verify that you have the necessary [prerequisites](connecting.html#prereqs).

You must have the Db2 driver package or the IBM® Data Server Driver Package installed on your computer.

### Procedure

1. Determine your ODBC DSN data from the [connection information](credentials.html) that you collected beforehand.

2. Create a new connection:
      
   a. In the ArcCatalog Catalog tree, open the Database Connections node and click **Add Database Connection**.
        
   b. In the Database Connections wizard:
   - Select **DB2** from the Database Platform drop-down list.
   - Enter the following string in the **Data source** field:
     ```
     HostName=<hostname>;Port=<port>;Database=<database>;
     CLIENTBUFFERSUNBOUNDLOBS=1;LOBCACHESIZE=50000000;
     FET_BUF_SIZE=256K  
     ```

     where `<hostname>`, `<port>`, and `<database>` are placeholders that represent the host name, port number, and database name that you noted earlier.
            
   - Select **Database authentication** as the authentication type.
            
   - Specify your user name and password (the user ID and password that you noted earlier) in the corresponding fields.
            
   - Press **OK**.
        
     ![Database Connections wizard](images/2_gs_conn.jpg)

### Results

The ArcCatalog component of Esri ArcGIS for Desktop is now connected to your {{site.data.keyword.dashdbshort_notm}} database. 


