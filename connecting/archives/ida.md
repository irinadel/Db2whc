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

# Connecting InfoSphere Data Architect

These instructions explain how to create a connection from InfoSphere® Data Architect version 9.1.x to a {{site.data.keyword.dashdbshort_notm}} database.
{: shortdesc}

## Prerequisites

Before attempting to connect to your {{site.data.keyword.dashdbshort_notm}} database, verify that you have the necessary [prerequisites](connecting.html#prereqs).

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## Procedure

1. In the Data Source Explorer view of InfoSphere Data Architect, right-click **Database Connections**, then select **New**.
    
2. On the **Local** tab, select **DB2 for Linux, UNIX, and Windows** as the database manager.
    
3. On the **General** tab, enter the following values:

   - *Database*: `BLUDB`
   - *Host*: The host name that you collected beforehand.
   - *Port*: For a connection without SSL, enter `50000`. For a connection with SSL, enter `50001`. 
   - *User name*: The user ID that you collected beforehand.
   - *Password*: The password that you collected beforehand.

4. For an SSL connection, click the **Optional** tab. Enter an `sslConnection` property and specify a value of `true`. Click **Add**.
    
5. [*Optional*]: Click **Test Connection** to verify that the connection succeeded.

