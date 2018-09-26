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

# Connecting Data Studio

These instructions explain how to create a connection from IBM® Data Studio version 4.1.x to a {{site.data.keyword.dashdbshort_notm}} database.
{: shortdesc}

## Prerequisites

Before attempting to connect to your {{site.data.keyword.dashdbshort_notm}} database, verify that you have the necessary [prerequisites](connecting.html#prereqs).

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## Procedure

1. In Data Studio, click **All Databases > New Connection to a database**.

2. On the **Local** tab, select **DB2 for Linux, UNIX, and Windows** as the database manager.
    
3. On the **General** tab, enter the following values:
   - *Database*: `BLUDB`
   - *Host*: The host name.
   - *Port*: For a connection without SSL, enter `50000`. For a connection with SSL, enter `50001`. 
   - *User name*: The user name that you use to log in.
   - *Password*: The password that you use to log in.

4. For an SSL connection, click the **Optional** tab, and then click **Add**. For the `sslConnection` property, specify `true`.

5. [*Optional*]: Click **Test Connection** to verify that the connection succeeded.
