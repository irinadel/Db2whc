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

# Connecting CLPPlus

Command line processor plus (CLPPlus) is included in the Db2 driver package. CLPPlus provides a command-line interface that you can use to connect to a {{site.data.keyword.dashdbshort_notm}} database. You can use CLPPlus to define, edit, and run statements, scripts, and commands.
{: shortdesc}

## Prerequisites

Before attempting to connect to your {{site.data.keyword.dashdbshort_notm}} database, verify that you have the necessary [prerequisites](connecting.html#prereqs).

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

To use CLPPlus, ensure that a software development kit (SDK) or a Java runtime environment (JRE) for Java Version 1.5.0 or later is installed on your computer and that environment variables are set as follows:

- The `JAVA_HOME` environment variable is set to the Java installation directory on your computer.
- The `PATH` environment variable setting includes the `bin` subdirectory of the Java installation directory on your computer.

## Procedure

1. In a command shell on Linux operating systems, at the Windows command prompt, or in the DB2 command window on Windows operating systems, run the following commands:

   These commands create new entries in the driver configuration file (`db2dsdriver.cfg`) on your computer and set the connection attributes. You need to do this step only one time.

   - For a connection with SSL:

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50001 -parameter "SecurityTransportMode=SSL"`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50001`  

     where:
     
     - `<hostname>` is the host name of the server.
     - `<alias>` is an alias that you choose.

   - For a connection without SSL:

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50000`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50000`

2. To start CLPPlus with a connection to a {{site.data.keyword.dashdbshort_notm}} database that uses the entries in the `db2dsdriver.cfg` file, run the following command:

   - Windows environments: 

     `clpplus <userid>@<alias>`

   - Linux environments:

     `clpplus -nw <userid>@<alias>`

     where:
     
     - `<userid>` is the user ID from the connect credentials you collected beforehand.
     - `<alias>` is the alias that you created with the **db2cli writecfg** command.

   Running this command opens a CLPPlus window.

3. In the CLPPlus window, enter your password. The database information is displayed, followed by an SQL prompt. Sample output follows:

```
   Hostname = 192.0.2.0
   Database server = DB2/LINUXX8664  SQL10054
   SQL authorization ID = smith
   Local database alias = BLUDB
   Port = 50001
   
   SQL>
```

## Results

You can now enter CLPPlus commands or SELECT statements and run scripts to work with the data in the database.

## Examples

The following examples use a short script that retrieves rows from the sample table `GOSALES.BRANCH`. The script file is named `cities.sql` and is on the local Windows computer in the `C:\temp directory`. The `cities.sql` file contains the following text:

```
SET ECHO ON
SELECT branch_code, city from GOSALES.BRANCH;
```

### Example 1 

To run the script interactively:

1. Start CLPPlus with your user ID and the alias that you created in the `db2dsdriver.cfg` file by running the following command:

   `clpplus <user_id>@<alias>`
2. Enter your password.
3. At the SQL prompt, enter the following text:

   `start C:\temp\cities.sql`

### Example 2

Start CLPPlus with your user ID and the alias that you created in the `db2dsdriver.cfg` file and run the script in one step:

`clpplus <user_id>/<password>@<alias> @C:\temp\cities.sql`

Sample output from the `cities.sql` script follows:

```
BRANCH_CODE CITY
----------- --------------------------------------------------
          6 Paris
          7 Milano
          9 Amsterdam
         13 Hamburg
         14 München
         15 Kista
         17 Calgary
         18 Toronto
         19 Boston
         20 Seattle
         21 Los Angeles
         22 Miami
         23 Lyon
         24 Distrito Federal
         25 Tokyo
         26 Osaka City
         28 Melbourne
         29 Bilbao
         30 Sao Paulo
         31 Kuopio
         32 Seoul
         33 Singapore

BRANCH_CODE CITY
----------- --------------------------------------------------
         34 Shanghai
         35 London
         36 Birmingham
         37 Zürich
         38 Heverlee
         39 Wien
         40 Geneve

29 rows were retrieved.
```

