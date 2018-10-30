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

# Connecting Aginity Workbench

These instructions explain how to connect Aginity Workbench 4.3 to a {{site.data.keyword.dashdbshort_notm}} database. You can use Aginity Workbench to migrate IBM PureData for Analytics (Netezza) data models and data to {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

## Prerequisites

Before attempting to connect to your {{site.data.keyword.dashdbshort_notm}} database, verify that you have the necessary [prerequisites](connecting.html#prereqs).

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## Procedure

1. Download and install Aginity Workbench.

2. Determine your ODBC DSN from the connection information that you noted earlier.

3. Launch Aginity Workbench. If the database connection dialog box does not open automatically, open it by clicking **Connect** on the toolbar.

4. [Establish a database connection ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://www.aginity.com/documentation/WB/dashDB/Default.htm#Aginity_Topics/Aginity_Workbench/Database_Connection_Dialog_Box.htm){:new_window}. Use the host name, user ID, and password from the connection information that you noted earlier.


