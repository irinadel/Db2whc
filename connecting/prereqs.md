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

# Prerequisites

Before attempting to connect to your {{site.data.keyword.dashdbshort_notm}} database, verify that you have the necessary prerequisites. 
{: shortdesc}

## Procedure

1. Verify that a supported driver is installed

   - If your application or tool already contains the [Db2 v11.1 IBM Data Server Driver Package ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/docview.wss?uid=swg21385217){:new_window}, then your application or tool is able to connect to your {{site.data.keyword.dashdbshort_notm}} database using that driver.
   - Otherwise, install the [Db2 driver package](driver_pkg.html), which you can download from the web console.
2. Configure your environment

   - [Add entries to the driver configuration file, `db2dsdriver.cfg`, for your database](driver_pkg_cfg.html).

   - [Secure Sockets Layer (SSL)](ssl.html)

     You can choose to connect with or without SSL. Connection details, such as which port to use and the connection string, depend on whether or not you use SSL connections.

     To use SSL connections, you need a CA certificate:

      - If you use the latest {{site.data.keyword.dashdbshort_notm}} driver package, the certificate file is bundled with the package and will be used for connections.
      - If you use the IBM Data Server Driver Package, you can download the SSL certificate from the web console.
3. Confirm ports are available

   If your network is behind a firewall, confirm that communications are permitted on port number `50000` for standard protocols or port number `50001` for SSL connections.
4. Collect database details and credentials

   To connect to your database, you need database details (such as the host name), as well as credentials (such as a user ID and password.) You can collect this [connection information](credentials.html) from the web console.


