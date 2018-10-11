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

# Connecting overview
{: #overview}

You can connect command-line interfaces, IBM® or third-party applications and tools, or apps that you create to your {{site.data.keyword.dashdbshort_notm}} database. 
{: shortdesc}

## Prerequisites
{: #prereqs}

Before attempting to connect to your {{site.data.keyword.dashdbshort_notm}} database, verify that you have the necessary prerequisites. 

- Collect database details and credentials

   To connect to your database, you need database details (such as the host name), as well as credentials (such as a user ID and password.) You can collect this connection information from the {{site.data.keyword.dashdbshort_notm}} web console.

- Verify that a supported driver is installed

   - If your application or tool already contains the Db2 v11.1 IBM Data Server Driver Package, then your application or tool is able to connect to your {{site.data.keyword.dashdbshort_notm}} database using that driver.
   - Otherwise, install the Db2 driver package, which you can download from the {{site.data.keyword.dashdbshort_notm}} web console.

- Configure your environment

  - Add entries to the driver configuration file, `db2dsdriver.cfg`, for your database.

  - Secure Sockets Layer (SSL)

    You can choose to connect with or without SSL. Connection details, such as which port to use and the connection string, depend on whether or not you use SSL connections.

    To use SSL connections, you need a CA certificate:

    - If you use the latest {{site.data.keyword.dashdbshort_notm}} driver package, the certificate file is bundled with the package and will be used for connections.
    - If you use the IBM Data Server Driver Package, you can download the SSL certificate from the {{site.data.keyword.dashdbshort_notm}} web console.

- Confirm ports are available

   If your network is behind a firewall, confirm that communications are permitted on port number `50000` for standard protocols or port number `50001` for SSL connections.

<!-- Before you can connect to your {{site.data.keyword.dashdbshort_notm}} database, verify that you completed downloading and installing the necessary components on the prerequisites checklist: 

- [Prerequisites checklist](prereqs.html) -->

### Collecting connection information
{: #collect_info}

- [Database details and connection credentials](credentials.html)

### Downloading and installing driver package
{: #dl_install}

- [Download driver package](driver_pkg.html)
- [Installing on Linux or PowerLinux](install_linux.html)
- [Installing on Mac OS X](install_mac.html)
- [Installing on Windows](install_win.html)

### Configuring your environment
{: #cfg_env}

- [Configuring your environment](driver_pkg_cfg.html)
- [Secure Sockets Layer (SSL) support](ssl.html)

## Connecting programmatically
{: #conx_prgrm}

You can use common programming languages to create applications that connect to a {{site.data.keyword.dashdbshort_notm}} database.
{: shortdesc}

- [JDBC](jdbc.html)
- [Microsoft Windows ODBC or CLI](odbc_cli.html)
- [.NET](net_apps.html)
- [ODBC Data Source Administrator](odbc_data_source_admin.html)
- [PHP](php.html)
- [REST API](rest_api.html)

## Connecting apps and tools
{: #conx_apps_tools}

You can also connect external applications and tools to {{site.data.keyword.dashdbshort_notm}} and use them to further manage or analyze your data. For example:

- Connect your {{site.data.keyword.Bluemix_short}} applications that need an analytics database.
- [Aginity Workbench to migrate Netezza® data models and data to {{site.data.keyword.dashdbshort_notm}}](aginity_wb.html)
- [CLPPLUS](clpplus.html)
- [Cognos to run Business Intelligence reports against your data](cognos.html)
- [Data Studio](data_studio.html)
- [DataStage](datastage.html)
- [Data Server Manager](dsm.html)
- [Esri ArcGIS for Desktop to perform geospatial analytics and map publishing with your data](esri_arcgis.html)
- [InfoSphere Data Architect to design and deploy your database schema](ida.html)
- [InfoSphere Data Replication](idr.html)
- [Local R development environment](r_dev_env.html)
- [SAS](sas.html)
- [SPSS Statistics](spss_stats.html)
- Connect SQL-based tools to manipulate, analyze, or visualize your data:
  - [Excel](excel.html)
  - [Tableau](tableau.html)
- [Watson Studio (formerly IBM Data Science Experience)](watson_studio.html)

## Connecting to another Db2 database
{: #fed}

Db2 data virtualization (also known as federation) is supported by {{site.data.keyword.dashdbshort_notm}}. Data virtualization gives you single-query access to all of your data that is on multiple distributed databases anywhere in your organization. You can access data that is on any of your Db2 or Informix data sources, both in the cloud and on premises. 

This function is supported on all versions of {{site.data.keyword.dashdbshort_notm}}, except for the Entry plan. However, you can use the Entry plan as a target from which you can pull data.

[Data virtualization (federation)](../federation.html)

