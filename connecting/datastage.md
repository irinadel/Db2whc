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

# Connecting DataStage

These instructions explain how to define a connection without SSL between IBM® InfoSphere® DataStage® version 9.1 and later and a {{site.data.keyword.dashdbshort_notm}} database by cataloging the database and defining a connection object, or how to create a connection with SSL by using a digital certificate that is issued by a third party.
{: shortdesc}

## Prerequisites

If you don’t already have a data server client installed, download and install the IBM Data Server Client Version 10.5 that is appropriate for your client machine’s operating system: [IBM Data Server Client ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/marketing/iwm/iwm/web/preLogin.do?source=swg-idsc97){:new_window}.

To make connections with the SSL protocol, download and install the 32-bit GSKit V8. Click the OS tab that is appropriate for your client machine’s operating system: [GSKit V8 - Install, Uninstall and Upgrade instructions ![External link icon](../../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/support/docview.wss?uid=swg21631462){:new_window}. For the following operating systems, ensure that you add the GSKit installation directory path to the OS-specific path environment variable:

- AIX®: **LIBPATH**
   - `/usr/opt/ibm/gsk8/lib`
- Linux: **LD_LIBRARY_PATH**
    - `/usr/local/ibm/gsk8/lib`
- UNIX: **LD_LIBRARY_PATH**
    - `/opt/ibm/gsk8/lib`
- Windows: **PATH**
    - `<installation_directory>\gsk8\bin`
    - `<installation_directory>\gsk8\lib`

Before attempting to connect to your {{site.data.keyword.dashdbshort_notm}} database, verify that you have the necessary [prerequisites](connecting.html#prereqs).

<!--Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## Procedure

- To create a connection with SSL, complete the following steps:

  1. Open a command line or terminal and make a new directory in the DataStage system to store the SSL certificate and key files.

     `# /home/db2inst2> mkdir SSL`

     `# /home/db2inst2> cd SSL`

  2. In the Db2 console, download the SSL certificate from the Connect your applications to the database page.

     a. From the main menu, click **Connect**.
     
     b. Click **Connection with SSL**, and then click the **SSL certificate (1 KB)** link.
     
     c. Save the `DigiCertGlobalRootCA.crt` certificate into the SSL directory that you made in step 1.
        
  3. Create a client keystore database in the DataStage system by using the **gsk8capicmd** utility. This utility is included in the DB2® server installation.

     `# /home/db2inst2/SSL> gsk8capicmd -keydb -create -db <keystore_db.kdb> -pw <ks_db_password> -stash`

     where `<keystore_db.kdb>` represents the client keystore database and `<ks_db_password>` represents the password for the client keystore database.
        
  4. Add the certificate to the client keystore database.

     `# /home/db2inst2/SSL> gsk8capicmd -cert -add -db <keystore_db.kdb> -pw <ks_db_password> -label BLUDB_SSL -file DigiCertGlobalRootCA.crt`

     where `<keystore_db.kdb>` represents the client keystore database and `<ks_db_password>` represents the password for the client keystore database.
    
  5. Configure the DB2 client on the DataStage server.
            
     a. Update the SSL configuration parameters in the database manager.

     `# /home/db2inst2> db2 update dbm cfg using SSL_CLNT_KEYDB /home/db2inst2/SSL/<keystore_db.kdb>`

     where `<keystore_db.kdb>` represents the client keystore database.

     `# /home/db2inst2> db2 update dbm cfg using SSL_CLNT_STASH /home/db2inst2/SSL/<keystore_db.sth>`

     where `<keystore_db.sth>` represents the client keystore database password stash.
            
     b. Catalog the target node with the SSL security option and then the BLUDB database at that target node.

     `# /home/db2inst2> db2 catalog tcpip node SSLCLOUD remote <IP_addr_of_BLUDB_database_server> server 50001 security SSL`

     where `<IP_addr_of_BLUDB_database_server>` represents the IP address of the BLUDB database server,

     `# /home/db2inst2> db2 catalog db BLUDB as BLUDB_S at node SSLCLOUD`

     `# /home/db2inst2> db2 terminate`

  6. Add read and execute permissions on the files in the SSL directory for everyone. The DataStage user who runs the jobs needs to access these files to make SSL connections to the Db2 database.

     `# /home/db2inst2/SSL> chmod 655 /home/db2inst2/SSL/*`

  7. Restart the DataStage server.

- To create a connection without SSL, catalog the target Db2 database on the IBM InfoSphere DataStage server by completing the following steps:

  1. Use a telnet client application such as PuTTY to connect to the DataStage server as the default instance owner (usually db2inst1).
  2. Create a catalog of the target Db2 database by using the following DB2 commands:

     `db2 catalog tcpip node nodename remote <IP_address_of_BLUDB_database_server> <port_number_of_BLUDB_database>`

     `db2 catalog db <BLUDB_db_name> at node <nodename>`

     `db2 connect to <BLUDB_db_name> user <BLUDB_db_user_name> using <BLUDB_db_password>`

     `db2 list tables`

     where `<IP_address_of_BLUDB_database_server>` represents the IP address of the BLUDB database server, `<port_number_of_BLUDB_database>` represents the port number of the BLUDB database, `<BLUDB_db_name>` represents the BLUDB database name, `<nodename>` represents the name of the node, `<BLUDB_db_user_name>` represents the BLUDB database user name, and `<BLUDB_db_password>` represents the BLUDB database password.

  3. Use the [connection information](credentials.html) that you collected beforehand to define a connection in the DataStage client. For details about defining a connection in DataStage, see the following DataStage documentation topic: [Creating a data connection object manually ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SSZJPZ_11.3.0/com.ibm.swg.im.iis.ds.design.doc/topics/t_ddesref_Creating_a_Data_Connection_Object_Manually.html){:new_window}. On the **Parameters** tab, you must select the **DB2 Connector** for the **Connect using Staging Type** field.
