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

# Connecting Excel

These instructions explain how to connect Microsoft Excel 2010 to a {{site.data.keyword.dashdbshort_notm}} database.
{: shortdesc}

## Prerequisites

Before attempting to connect to your {{site.data.keyword.dashdbshort_notm}} database, verify that you have the necessary [prerequisites](connecting.html#prereqs).

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

You must have the Db2 driver package or the IBM® Data Server Driver Package installed on your local computer. 

**Restriction**: Connections between Excel and {{site.data.keyword.dashdbshort_notm}} are supported on only the Windows operating system.

## Procedure

1. In the web console, go to the **Run SQL** page.
    
2. Type one or more SELECT statements in the editor text box.

3. Click one of the Run options.

4. Click **Excel ODC File**.

5. Download and open the `BLUExcel.odc` file in Excel. If a security notice is displayed, click **Enable**.

6. Click **Open** to connect to the {{site.data.keyword.dashdbshort_notm}} database. The **Connect To DB2 Database** dialog box opens.

7. Type the user ID and password that you use to log in to {{site.data.keyword.dashdbshort_notm}}. To obtain the user ID and password, click **Connect** in the web console or **Connect > Connection Information** in the web console.

8. Ensure that the connection mode is `Share`, and then click **OK**.

## Results

The query results are displayed in an Excel spreadsheet. These are the same results that are displayed in the Results viewer. Now you can generate charts and reports and analyze your data by using Excel. For more information about how to do this and how to run SQL queries on your data from the web console, see [Tutorial: Generating charts and reports by using Excel ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.analytics.doc/doc/explore_excel_reports.html){:new_window} and [Analyzing with Excel ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.analytics.doc/doc/exploreexcel.html){:new_window}. 