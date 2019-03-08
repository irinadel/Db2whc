---

copyright:
  years: 2014, 2019
lastupdated: "2018-10-24"

keywords:

subcollection: Db2whc

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

# 入门
{: #getting_started}

{{site.data.keyword.dashdblong}} 受管服务是在云中为您供应的 SQL 数据库。您可以使用 Db2 Warehouse 就像使用任何数据库软件一样，但是却没有硬件设置或软件安装和维护所产生的开销和费用。
{: shortdesc}

## 免费试用
{: #freetrial}

您可以试用 {{site.data.keyword.dashdbshort_notm}} 入门级套餐，可免费使用多达 1 GB 存储。[免费试用 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.bluemix.net/catalog/services/db2-warehouse){:new_window}

## 界面
{: #interfaces}

您可以通过以下方法来使用仓库数据库：
{: shortdesc}

   * 从 Web 控制台
   * REST API
   * 从本地计算机连接应用程序或喜爱的工具
   * 使用 {{site.data.keyword.dashdbshort_notm}} 作为 {{site.data.keyword.Bluemix_notm}} 应用程序或服务的数据源

### Web 控制台
{: #web_console}

Web 控制台为您需要使用数据库的所有项目提供图形界面，包括：装入功能、SQL 编辑器、驱动程序下载等。
{: shortdesc}

![Web 控制台仪表板页面的视图](images/console_v3.png)

<!-- Click the link to take a tour of the {{site.data.keyword.dashdbshort_notm}} for Analytics web console: [General tour ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://ibm.biz/dashdb-general-quick-tour){:new_window}. -->

您可以通过以下方法来访问 Web 控制台：
   * 从 {{site.data.keyword.Bluemix_notm}} 仪表板 - 您可以从 {{site.data.keyword.dashdbshort_notm}} 服务的“服务详细信息”页面打开 Web 控制台。
   * 直接 URL - 您可以针对 {{site.data.keyword.dashdbshort_notm}} 服务为 Web 控制台的 URL 设置书签。

### REST API
{: #api}

使用 {{site.data.keyword.dashdbshort_notm}} 服务套餐，您可以利用 [{{site.data.keyword.dashdbshort_notm}} REST API ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://ibm.biz/db2whc_api){:new_window}，执行与文件管理和装入数据相关的任务。
{: shortdesc}

### 从本地计算机连接应用程序或喜爱的工具
{: #connect_apps}

通过完成以下步骤，配置本地环境以连接到 {{site.data.keyword.dashdbshort_notm}} 数据库：
{: shortdesc}

1. 通过 {{site.data.keyword.dashdbshort_notm}} Web 控制台下载[驱动程序包](/docs/services/Db2whc/connecting/driver_pkg.html)。
2. 在运行应用程序或工具的计算机上安装驱动程序包：
   - [在 Linux 或 PowerLinux 上安装](/docs/services/Db2whc/connecting/install_linux.html)
   - [在 Mac OS X 上安装](/docs/services/Db2whc/connecting/install_mac.html)
   - [在 Windows 上安装](/docs/services/Db2whc/connecting/install_win.html)
3. 为 {site.data.keyword.dashdbshort_notm}} 数据库[配置驱动程序文件](/docs/services/Db2whc/connecting/driver_pkg_cfg.html)。

### 使用 Db2 Warehouse on Cloud 作为 {{site.data.keyword.Bluemix_notm}} 应用程序或服务的数据源
{: #data_src}

在 {{site.data.keyword.Bluemix_notm}} 上托管的应用程序可以使用与本地应用程序连接到 {{site.data.keyword.dashdbshort_notm}} 数据库完全相同的方法，连接到 {{site.data.keyword.dashdbshort_notm}} 数据库。
{: shortdesc}

当应用程序使用 {{site.data.keyword.Bluemix_notm}} 平台时，您可以利用 `VCAP _SERVICES` 环境变量来简化指定数据库详细信息和凭证的任务：
1. 在 {{site.data.keyword.Bluemix_notm}} 仪表板上，在 {{site.data.keyword.dashdbshort_notm}} 服务的“服务详细信息”页面的**连接**选项卡上，单击**创建连接**按钮。
2. 选择 {{site.data.keyword.Bluemix_notm}} 应用程序以使用 {{site.data.keyword.dashdbshort_notm}} 数据库作为数据源，然后单击**连接**按钮。
3. 更新应用程序代码以从 `VCAP_SERVICES` 环境变量检索数据库详细信息和凭证：

    **没有 `VCAP_SERVICES` 的示例**

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

    **具有 `VCAP_SERVICES` 的示例**

    ```php
    <?php
    $driver      = "DRIVER={IBM DB2 ODBC DRIVER};";

    

    $vcap        = json_decode( getenv( "VCAP_SERVICES" ), true );
    $dsn         = $vcap[ "dashDB" ][0][ "credentials" ][ "dsn" ];

    $conn_string = $driver . $dsn;
                                   
    
                                   
    $conn        = db2_connect( $conn_string, "", "" );
    ?>
    ```

## 样本
{: #samples}

下面是一些样本的链接，这些样本演示了在不同的语言中，如何以编程方式从应用程序连接到 {{site.data.keyword.dashdbshort_notm}} 数据库：
{: shortdesc}

- [JDBC](/docs/services/Db2whc/connecting/jdbc.html)
- [Microsoft Windows ODBC 或 CLI](/docs/services/Db2whc/connecting/odbc_cli.html)
- [.NET](/docs/services/Db2whc/connecting/net_apps.html)
- [ODBC 数据源管理器](/docs/services/Db2whc/connecting/odbc_data_source_admin.html)
- [PHP](/docs/services/Db2whc/connecting/php.html)
- [REST API](/docs/services/Db2whc/connecting/rest_api.html)

## 视频：Db2 Warehouse on Cloud 简介
{: #intro_vid}

观看以下视频以了解 {{site.data.keyword.dashdbshort_notm}} 简介。

<iframe class="embed-responsive-item" id="youtubeplayer1" title="{{site.data.keyword.dashdbshort_notm}} 简介" type="text/html" width="640" height="390" src="//www.youtube.com/embed/0NO9OTFWzKs?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

## 视频：Flex Performance 套餐简介
{: #intro_vid_flex}

观看以下视频以了解 {{site.data.keyword.dashdbshort_notm}} Flex Performance 套餐简介。

<iframe class="embed-responsive-item" id="youtubeplayer2" title="通过 Cognos Analytics 创建连接" type="text/html" width="640" height="390" src="//www.youtube.com/embed/59PKSnzNQAg?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

## 视频：连接分析应用程序
{: #cognos_vid}

观看以下视频以了解如何通过 Cognos Analytics 创建连接。

<iframe class="embed-responsive-item" id="youtubeplayer3" title="通过 Cognos Analytics 创建连接" type="text/html" width="640" height="390" src="//www.youtube.com/embed/TRUEPVHGi0s?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

