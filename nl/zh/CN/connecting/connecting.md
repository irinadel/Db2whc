---

copyright:
  years: 2014, 2019
lastupdated: "2018-10-15"

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

# 连接概述
{: #connect}

您可以将命令行界面、IBM® 或第三方应用程序和工具或者自己创建的应用程序连接到 {{site.data.keyword.dashdbshort_notm}} 数据库。
{: shortdesc}

## 先决条件
{: #prereqs}

在尝试连接到 {{site.data.keyword.dashdbshort_notm}} 数据库之前，请验证您是否具有必需的先决条件。 

- 收集数据库详细信息和凭证

   要连接到数据库，您需要数据库详细信息（例如，主机名）以及凭证（例如，用户标识和密码）。您可以通过 {{site.data.keyword.dashdbshort_notm}} Web 控制台来收集这些连接信息。

- 确认是否已安装支持的驱动程序

   - 如果应用程序或工具已包含 Db2 V11.1 IBM Data Server Driver Package，那么应用程序或工具可以使用该驱动程序来连接到 {{site.data.keyword.dashdbshort_notm}} 数据库。
   - 否则，请安装 Db2 驱动程序包，您可以通过 {{site.data.keyword.dashdbshort_notm}} Web 控制台来下载该包。

- 配置环境

  - 在驱动程序配置文件 `db2dsdriver.cfg` 中，添加数据库的相应条目。
  - 安全套接字层 (SSL)

    您可以选择是使用还是不使用 SSL 进行连接。连接详细信息（例如，要使用的端口以及连接字符串）取决于您是否使用 SSL 连接。

    要使用 SSL 连接，您需要 CA 证书：
    - 如果使用的是最新的 {{site.data.keyword.dashdbshort_notm}} 驱动程序包，那么证书文件已与该包捆绑在一起，并将用于连接。
    - 如果使用的是 IBM Data Server Driver Package，那么可以通过 {{site.data.keyword.dashdbshort_notm}} Web 控制台来下载 SSL 证书。

- 确认端口是否可用

   如果您的网络受防火墙保护，请确认是否允许在端口号 `50000`（对于标准协议）和端口号 `50001`（对于 SSL 连接）上进行通信。

<!-- Before you can connect to your {{site.data.keyword.dashdbshort_notm}} database, verify that you completed downloading and installing the necessary components on the prerequisites checklist: 

- [Prerequisites checklist](prereqs.html) -->

### 收集连接信息
{: #collect_info}

- [数据库详细信息和连接凭证](credentials.html)

### 下载和安装驱动程序包
{: #dl_install}

- [下载驱动程序包](driver_pkg.html)
- [在 Linux 或 PowerLinux 上安装](install_linux.html)
- [在 Mac OS X 上安装](install_mac.html)
- [在 Windows 上安装](install_win.html)

### 配置环境
{: #cfg_env}

- [配置环境](driver_pkg_cfg.html)
- [安全套接字层 (SSL) 支持](ssl.html)

## 以编程方式连接
{: #conx_prgrm}

您可以使用常用编程语言来创建连接到 {{site.data.keyword.dashdbshort_notm}} 数据库的应用程序。
{: shortdesc}

- [JDBC](jdbc.html)
- [Microsoft Windows ODBC 或 CLI](odbc_cli.html)
- [.NET](net_apps.html)
- [ODBC 数据源管理器](odbc_data_source_admin.html)
- [PHP](php.html)
- [REST API](rest_api.html)
<!-- - [C++]() -->
<!-- - [Java]() -->
<!-- - [Node.js]() -->
<!-- - [Perl]() -->
<!-- - [Python]() -->

## 集成应用程序和工具
{: #conx_apps_tools}

您还可以将外部应用程序和工具连接到 {{site.data.keyword.dashdbshort_notm}}，以使用其进一步管理或分析数据。例如：

### 数据集成
- 连接需要分析数据库的 {{site.data.keyword.Bluemix_short}} 应用程序。
- [DataStage](data.html#datastage)
- [Informatica](data.html#informatica)
- [Lift ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://lift.ng.bluemix.net/#docs){:new_window}
- [InfoSphere Data Replication](data.html#idr)
- [Segment ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://segment.com/docs/destinations/db2/){:new_window}
- [Data Studio](data.html#data_studio)
- [数据服务器管理器](data.html#dsm)
- [CLPPLUS](data.html#clpplus)
- [通过 Aginity Workbench 将 Netezza® 数据模型和数据迁移到 {{site.data.keyword.dashdbshort_notm}}](data.html#aginity_wb)
- [通过 InfoSphere Data Architect 设计和部署数据库模式](data.html#ida)

### 数据可视化/BI
- [通过 Cognos Analytics 针对数据运行商业智能报告](vis_bi.html#cognos)
- [Looker ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://docs.looker.com/setup-and-management/connecting-to-db){:new_window}
- [Tableau](vis_bi.html#tableau)
- [Microsoft Excel](vis_bi.html#excel)
- [通过 Esri ArcGIS for Desktop 对数据执行地理空间分析和地图发布](vis_bi.html#esri_arcgis)

### Data Science
- [Watson Studio（原先的 IBM Data Science Experience）](data_sci.html#watson_studio)
- [SPSS Statistics](data_sci.html#spss_stats)
- [SAS](data_sci.html#sas)
- [本地 R 开发环境](data_sci.html#r_dev_env)

## 连接到另一个 Db2 数据库
{: #fed}

{{site.data.keyword.dashdbshort_notm}} 支持 Db2 数据虚拟化（也称为联合）。通过数据虚拟化，您能以单查询方式访问位于组织中任意位置的多个分布式数据库上的所有数据。您可以访问位于任何 Db2 或 Informix 数据源（包括云和内部部署）上的数据。
 

在其他所有版本的 {{site.data.keyword.dashdbshort_notm}} 都支持此功能，但入门套餐除外。但是，您可以使用入门套餐作为可从中拉取数据的目标。

- [数据虚拟化（联合）](../federation.html)


