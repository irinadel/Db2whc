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

# Connecting an R development environment

Instead of using the RStudio® environment that is integrated within IBM Watson Studio, you might prefer to use your own, locally-installed R development environment. For example, you might have your own RStudio installation, or you might prefer to use some other development tool such as Rcmdr or Rattle. These instructions explain how to connect an R development environment to a {{site.data.keyword.dashdbshort_notm}} database.
{: shortdesc}

## Prerequisites

Before attempting to connect to your {{site.data.keyword.dashdbshort_notm}} database, verify that you have the necessary [prerequisites](connecting.html#prereqs).

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## Procedure

1. In your local R environment, install the `ibmdbR` package by entering the following command:

   `install.packages("ibmdbR")`

   Your local R environment accesses the Comprehensive R Archive Network (CRAN) and automatically downloads and installs the `ibmdbR` package and any prerequisite packages that are not already installed.
    
2. Create an ODBC driver connection between your R development environment and your {{site.data.keyword.dashdbshort_notm}} database:
        
   a. [Set up your database as an ODBC data source ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_cli_and_odbc_applications.html){:new_window}.
        
   b. Open your locally installed R development environment.
        
   c. At the R prompt, enter the following statements to create the connection. Replace the placeholders with the [connection information](credentials.html) that you collected beforehand.

   - If your locally installed R development environment runs in the {{site.data.keyword.dashdbshort_notm}} database:

     ```
     library(ibmdbR)
     host.name <- "placeholderForYourHostName"
     port <-"placeholderForPortNumber" # 50000 if not using SSL or 50001 if using SSL
     user.name <-"placeholderForYourUserName"
     pwd <- "placeholderForYourPassword"
     con.text <- paste("placeholderForYourDSNName;DRIVER=BLUDB",
                       ";Database=BLUDB",
                       ";Hostname=",host.name,
                       ";Port=",port,
                       ";PROTOCOL=TCPIP",
                       ";UID=", user.name,
                       ";PWD=",pwd,sep="")
     # Connect to using a odbc Driver Connection string to a remote database
     con <- idaConnect(con.text)
     ```

   - If your locally installed R development environment does not run in the {{site.data.keyword.dashdbshort_notm}} database:

     ```
     library(ibmdbR)
     driver.name <- "{placeholderForYourDriverName}"
     db.name <- "placeholderForYourDatabaseName"
     host.name <- "placeholderForYourHostName"
     port <-"placeholderForYourPort"
     user.name <-"placeholderForYourUserName"
     pwd <- "placeholderForYourPassword"
     con.text <- paste("placeholderForYourDSNName;DRIVER=",driver.name,
                       ";Database=",db.name,
                       ";Hostname=",host.name,
                       ";Port=",port,
                       ";PROTOCOL=TCPIP",
                       ";UID=", user.name,
                       ";PWD=",pwd,sep="")
     # Connect to using a odbc Driver Connection string to a remote database
     con <- idaConnect(con.text)
     ```

     **Note**: The statement that is used to create the connection object uses the `idaConnect()` method, not the `odbcConnect()` or `odbcDriverConnect()` methods.
        
   d. Initialize the analytics package by issuing the following R command:

   `idaInit(con)`

   e. To test whether the connection is working, issue the following R command:

   `idaShowTables()`

   The console displays a list of all of the tables and views in the current schema.
