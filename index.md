---

copyright:
  years: 2014, 2018
lastupdated: "2018-10-24"

---

<!-- Attribute definitions --> 
{:javascript: #javascript .ph data-hd-programlang='javascript'}
{:java: #java .ph data-hd-programlang='java'}
{:ruby: #ruby .ph data-hd-programlang='ruby'}
{:php: #php .ph data-hd-programlang='php'}
{:python: #python .ph data-hd-programlang='python'}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}

# Getting started
{: #getting_started}

The {{site.data.keyword.dashdblong}} managed service is an SQL database provisioned for you in the cloud. You can use the Db2 warehouse just as you would use any database software, but without the overhead and expense of hardware setup or software installation and maintenance. 
{: shortdesc}

## Free trial
{: #freetrial}

You can try the {{site.data.keyword.dashdbshort_notm}} Entry plan with up to 1 GB of storage without charge. [Free trial ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/catalog/services/db2-warehouse){:new_window}

## Interfaces
{: #interfaces}

You can work with your warehouse database in the following ways:
{: shortdesc}

   * From the web console
   * REST API
   * Connect applications or your favorite tools from your local computer
   * Use {{site.data.keyword.dashdbshort_notm}} as a data source for your {{site.data.keyword.Bluemix_notm}} apps or services

### Web console
{: #web_console}

The web console provides a graphical interface for everything that you need to use your database, including: load facilities, an SQL editor, driver downloads, and more.
{: shortdesc}

![View of the web console dashboard page](images/console_v3.png)

<!-- Click the link to take a tour of the {{site.data.keyword.dashdbshort_notm}} for Analytics web console: [General tour ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://ibm.biz/dashdb-general-quick-tour){:new_window}. -->

You can access your web console in the following ways:
   * From your {{site.data.keyword.Bluemix_notm}} dashboard - You can open the web console from the Service Details page for your {{site.data.keyword.dashdbshort_notm}} service.
   * Direct URL - You can bookmark the URL of the web console for your {{site.data.keyword.dashdbshort_notm}} service.

### REST API
{: #api}

With {{site.data.keyword.dashdbshort_notm}} service plans, you can perform tasks related to file management and loading data by using the [{{site.data.keyword.dashdbshort_notm}} REST API ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://ibm.biz/db2whc_api){:new_window}.
{: shortdesc}

### Connect applications or your favorite tools from your local computer
{: #connect_apps}

Configure your local environment to connect to your {site.data.keyword.dashdbshort_notm}} database by completing the following steps:
{: shortdesc}

1. Download the [driver package](connecting/driver_pkg.html) from the {{site.data.keyword.dashdbshort_notm}} web console.
2. Install the driver package on the computer where your apps or tools are running:
   - [Installing on Linux or PowerLinux](connecting/install_linux.html)
   - [Installing on Mac OS X](connecting/install_mac.html)
   - [Installing on Windows](connecting/install_win.html)
3. [Configure the driver files](connecting/driver_pkg_cfg.html) for your {site.data.keyword.dashdbshort_notm}} database.

### Use Db2 Warehouse on Cloud as a data source for your {{site.data.keyword.Bluemix_notm}} apps or services
{: #data_src}

Apps hosted on {{site.data.keyword.Bluemix_notm}} can connect to your {{site.data.keyword.dashdbshort_notm}} database exactly the same way as your local applications connect to your {{site.data.keyword.dashdbshort_notm}} database.
{: shortdesc}

When your apps use the {{site.data.keyword.Bluemix_notm}} platform, you can take advantage of the `VCAP _SERVICES` environment variable to simplify the task of specifying database details and credentials:
1. On your {{site.data.keyword.Bluemix_notm}} dashboard, in the **Connections** tab of the Service Details page for your {{site.data.keyword.dashdbshort_notm}} service, click the **Create connection** button.
2. Select the {{site.data.keyword.Bluemix_notm}} app to use with your {{site.data.keyword.dashdbshort_notm}} database as a data source, and then click the **Connect** button.
3. Update your application code to retrieve database details and credentials from the `VCAP_SERVICES` environment variable:

    **Example without `VCAP_SERVICES`**

    ```php
    <?php
    $driver      = "DRIVER={IBM DB2 ODBC DRIVER};";

    $database    = "BLUDB";         # Get these database details from
    $hostname    = "<Host-name>";   # the Connection info page of the
    $port        = 50000;           # web console.
    $user        = "<User-ID >";    #
    $password    = "<Password>";    #
    $dsn         = "DATABASE=$database;" .
                   "HOSTNAME=$hostname;" .
                   "PORT=$port;" .
                   "PROTOCOL=TCPIP;" .
                   "UID=$user;" .
                   "PWD=$password;";

    $conn_string = $driver . $dsn;

    $conn        = db2_connect( $conn_string, "", "" );
    ?>
    ```

    **Example with `VCAP_SERVICES`**

    ```php
    <?php
    $driver      = "DRIVER={IBM DB2 ODBC DRIVER};";

    $vcap        = json_decode( getenv( "VCAP_SERVICES" ), true );
    $dsn         = $vcap[ "dashDB" ][0][ "credentials" ][ "dsn" ];

    $conn_string = $driver . $dsn;
                                   
    $conn        = db2_connect( $conn_string, "", "" );
    ?>
    ```

## Samples
{: #samples}

Here are links to samples demonstrating how to programmatically connect to your {{site.data.keyword.dashdbshort_notm}} database from applications in different languages:
{: shortdesc}

- [JDBC](connecting/jdbc.html)
- [Microsoft Windows ODBC or CLI](connecting/odbc_cli.html)
- [.NET](connecting/net_apps.html)
- [ODBC Data Source Administrator](connecting/odbc_data_source_admin.html)
- [PHP](connecting/php.html)
- [REST API](connecting/rest_api.html)

## Video: Introducing Db2 Warehouse on Cloud
{: #intro_vid}

Watch this video to see an introduction to {{site.data.keyword.dashdbshort_notm}}.

<iframe class="embed-responsive-item" id="youtubeplayer1" title="Introduction to {{site.data.keyword.dashdbshort_notm}}" type="text/html" width="640" height="390" src="//www.youtube.com/embed/0NO9OTFWzKs?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

## Video: Introducing the Flex Performance plan
{: #intro_vid_flex}

Watch this video to see an introduction to the {{site.data.keyword.dashdbshort_notm}} Flex Performance plan.

<iframe class="embed-responsive-item" id="youtubeplayer2" title="Creating a connection from Cognos Analytics" type="text/html" width="640" height="390" src="//www.youtube.com/embed/59PKSnzNQAg?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

## Video: Connecting an analytics application
{: #cognos_vid}

Watch this video to see how to create a connection from Cognos Analytics.

<iframe class="embed-responsive-item" id="youtubeplayer3" title="Creating a connection from Cognos Analytics" type="text/html" width="640" height="390" src="//www.youtube.com/embed/TRUEPVHGi0s?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

