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

# Connecting Tableau

These instructions explain how to connect Tableau to a {{site.data.keyword.dashdbshort_notm}} database and apply to Tableau Desktop version 8.x, but you can use similar steps for other Tableau tools.
{: shortdesc}

## Prerequisites

Before attempting to connect to your {{site.data.keyword.dashdbshort_notm}} database, verify that you have the necessary [prerequisites](connecting.html#prereqs).

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## Procedure

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

