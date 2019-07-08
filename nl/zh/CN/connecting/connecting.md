---

copyright:
  years: 2014, 2019
lastupdated: "2019-04-01"

keywords:

subcollection: Db2whc

---

<!-- Attribute definitions --> 
{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}

# 连接概述
{: #connect_ov}

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

- [数据库详细信息和连接凭证](/docs/services/Db2whc/connecting?topic=Db2whc-db_details_cxn_creds#db_details_cxn_creds)

### 下载和安装驱动程序包
{: #dl_install}

- [下载驱动程序包](/docs/services/Db2whc/connecting?topic=Db2whc-dr_pkg#dr_pkg)
- [在 Linux 或 PowerLinux 上安装](/docs/services/Db2whc/connecting?topic=Db2whc-install_dr_pkg_linux#install_dr_pkg_linux)
- [在 Mac OS X 上安装](/docs/services/Db2whc/connecting?topic=Db2whc-install_dr_pkg_mac#install_dr_pkg_mac)
- [在 Windows 上安装](/docs/services/Db2whc/connecting?topic=Db2whc-install_dr_pkg_windows#install_dr_pkg_windows)

### 配置环境
{: #cfg_env}

- [配置环境](/docs/services/Db2whc/connecting?topic=Db2whc-cfg_loc_env#cfg_loc_env)
- [安全套接字层 (SSL) 支持](/docs/services/Db2whc/connecting?topic=Db2whc-ssl_support#ssl_support)

## 连接选项
{: #connect_opts}

{{site.data.keyword.dashdbshort_notm}} 根据您的应用程序连接需求提供了多个安全连接选项。  
{: shortdesc}

请参阅[连接选项](/docs/services/Db2whc/connecting?topic=Db2whc-connect_options#connect_options)。

## 以编程方式连接
{: #conx_prgrm}

您可以使用常用编程语言来创建连接到 {{site.data.keyword.dashdbshort_notm}} 数据库的应用程序。
{: shortdesc}

- [JDBC](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_jdbc#con_prog_jdbc)
- [Microsoft Windows ODBC 或 CLI](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_odbc_cli#con_prog_odbc_cli)
- [.NET](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_net#con_prog_net)
- [ODBC 数据源管理器](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_odbc_dsa#con_prog_odbc_dsa)
- [PHP](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_php#con_prog_php)
- [REST API](/docs/services/Db2whc/connecting?topic=Db2whc-con_rest_api#con_rest_api)
<!-- - [C++]() -->
<!-- - [Java]() -->
<!-- - [Node.js]() -->
<!-- - [Perl]() -->
<!-- - [Python]() -->

## 集成应用程序和工具
{: #conx_apps_tools}

您还可以将外部应用程序和工具连接到 {{site.data.keyword.dashdbshort_notm}}，以使用其进一步管理或分析数据。例如：

### 数据集成
{: #di}

- 连接需要分析数据库的 {{site.data.keyword.Bluemix_short}} 应用程序。
- [DataStage](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#datastage)
- [Informatica](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#informatica)
- [Lift](https://www.lift-cli.cloud.ibm.com/#docs){:external}
- [InfoSphere Data Replication](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#idr)
- [Segment](https://segment.com/docs/destinations/db2/){:external}
- [Data Studio](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#data_studio)
- [数据服务器管理器](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#dsm)
- [CLPPLUS](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#clpplus)
- [通过 Aginity Workbench 将 Netezza® 数据模型和数据迁移到 {{site.data.keyword.dashdbshort_notm}}](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#aginity_wb)
- [通过 InfoSphere Data Architect 设计和部署数据库模式](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#ida)

### 数据可视化/BI
{: #dvis_bi}

- [通过 Cognos Analytics 针对数据运行商业智能报告](/docs/services/Db2whc/connecting?topic=Db2whc-data_vis_bi#cognos)
- [Looker](https://docs.looker.com/setup-and-management/connecting-to-db){:external}
- [Tableau](/docs/services/Db2whc/connecting?topic=Db2whc-data_vis_bi#tableau)
- [Microsoft Excel](/docs/services/Db2whc/connecting?topic=Db2whc-data_vis_bi#excel)
- [通过 Esri ArcGIS for Desktop 对数据执行地理空间分析和地图发布](/docs/services/Db2whc/connecting?topic=Db2whc-data_vis_bi#esri_arcgis)

### Data Science
{: #dsci}

- [Watson Studio（原先的 IBM Data Science Experience）](/docs/services/Db2whc/connecting?topic=Db2whc-ds#watson_studio)
- [SPSS Statistics](/docs/services/Db2whc/connecting?topic=Db2whc-ds#spss_stats)
- [SAS](/docs/services/Db2whc/connecting?topic=Db2whc-ds#sas)
- [本地 R 开发环境](/docs/services/Db2whc/connecting?topic=Db2whc-ds#r_dev_env)

## 连接到另一个 Db2 数据库
{: #fed}

{{site.data.keyword.dashdbshort_notm}} 支持 Db2 数据虚拟化（也称为联合）。通过数据虚拟化，您能以单查询方式访问位于组织中任意位置的多个分布式数据库上的所有数据。您可以访问位于任何 Db2 或 Informix 数据源（包括云和内部部署）上的数据。
 

在其他所有版本的 {{site.data.keyword.dashdbshort_notm}} 都支持此功能，但入门套餐除外。但是，您可以使用入门套餐作为可从中拉取数据的目标。

- [数据虚拟化（联合）](/docs/services/Db2whc?topic=Db2whc-data_virt_fed#data_virt_fed)


