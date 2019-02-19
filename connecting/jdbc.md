---

copyright:
  years: 2014, 2019
lastupdated: "2018-09-25"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}

# Connecting programmatically with JDBC
{: #con_prog_jdbc}

Define a connection between a Java™ application and the {{site.data.keyword.dashdbshort_notm}} database.
{: shortdesc}

## Prerequisites

Before attempting to connect to your {{site.data.keyword.dashdbshort_notm}} database, verify that you have the necessary [prerequisites](/docs/services/Db2whc/connecting/connecting.html#prereqs).

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## Procedure

In each Java application, specify the user ID and password by including the **DriverManager.getConnection** method, and then include one of the following JDBC URL strings:

- For a connection with SSL:

  `jdbc:db2://<host_name>:50001/BLUDB:sslConnection=true;`

- For a connection without SSL:

  `jdbc:db2://<host_name>:50000/BLUDB`


