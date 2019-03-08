---

copyright:
  years: 2014, 2019
lastupdated: "2018-10-15"

keywords:

subcollection: Db2whc

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

# 連接概觀
{: #connect_ov}

您可以將指令行、IBM® 或協力廠商應用程式及工具，或是您建立的應用程式，連接到您的 {{site.data.keyword.dashdbshort_notm}} 資料庫。
{: shortdesc}

## 必要條件
{: #prereqs}

在嘗試連接至您的 {{site.data.keyword.dashdbshort_notm}} 資料庫之前，請驗證您是否具有必要的必備項目。 

- 收集資料庫詳細資料及認證

   若要連接至您的資料庫，您需要資料庫詳細資料（例如主機名稱）以及認證（例如使用者 ID 及密碼）。您可以從 {{site.data.keyword.dashdbshort_notm}} Web 主控台中收集此連線資訊。

- 驗證是否已安裝支援的驅動程式

   - 如果您的應用程式或工具已包含 Db2 11.1 版 IBM Data Server Driver Package，則您的應用程式或工具就能夠使用該驅動程式連接至您的 {{site.data.keyword.dashdbshort_notm}} 資料庫。
   - 否則，請安裝 Db2 驅動程式套件，您可以從 {{site.data.keyword.dashdbshort_notm}} Web 主控台下載該套件。

- 配置環境

  - 將項目新增至資料庫的驅動程式配置檔 `db2dsdriver.cfg`。
  - Secure Sockets Layer (SSL)

    您可以選擇使用或不使用 SSL 進行連線。連線詳細資料（例如要使用的埠及連線字串）取決於是否使用 SSL 連線。

    若要使用 SSL 連線，您需要 CA 憑證：
    - 如果您使用最新的 {{site.data.keyword.dashdbshort_notm}} 驅動程式套件，則憑證檔會與此套件組合在一起，且將用於連線。
    - 如果您使用 IBM Data Server Driver Package，則可以從 {{site.data.keyword.dashdbshort_notm}} Web 主控台下載 SSL 憑證。

- 確認埠可用

   如果您的網路受防火牆保護，請確認允許在埠號 `50000` 上進行標準通訊協定的通訊，或在埠號 `50001` 上進行 SSL 連線的通訊。

<!-- Before you can connect to your {{site.data.keyword.dashdbshort_notm}} database, verify that you completed downloading and installing the necessary components on the prerequisites checklist: 

- [Prerequisites checklist](prereqs.html) -->

### 收集連線資訊
{: #collect_info}

- [資料庫詳細資料及連線認證](/docs/services/Db2whc/connecting/credentials.html)

### 下載並安裝驅動程式套件
{: #dl_install}

- [下載驅動程式套件](/docs/services/Db2whc/connecting/driver_pkg.html)
- [在 Linux 或 PowerLinux 上安裝](/docs/services/Db2whc/connecting/install_linux.html)
- [在 Mac OS X 上安裝](/docs/services/Db2whc/connecting/install_mac.html)
- [在 Windows 上安裝](/docs/services/Db2whc/connecting/install_win.html)

### 配置環境
{: #cfg_env}

- [配置環境](/docs/services/Db2whc/connecting/driver_pkg_cfg.html)
- [Secure Sockets Layer (SSL) 支援](/docs/services/Db2whc/connecting/ssl.html)

## 以程式設計方式連接
{: #conx_prgrm}

您可以使用一般程式設計語言來建立連接 {{site.data.keyword.dashdbshort_notm}} 資料庫的應用程式。
{: shortdesc}

- [JDBC](/docs/services/Db2whc/connecting/jdbc.html)
- [Microsoft Windows ODBC 或 CLI](odbc_cli.html)
- [.NET](/docs/services/Db2whc/connecting/net_apps.html)
- [ODBC 資料來源管理員](/docs/services/Db2whc/connecting/odbc_data_source_admin.html)
- [PHP](/docs/services/Db2whc/connecting/php.html)
- [REST API](/docs/services/Db2whc/connecting/rest_api.html)
<!-- - [C++]() -->
<!-- - [Java]() -->
<!-- - [Node.js]() -->
<!-- - [Perl]() -->
<!-- - [Python]() -->

## 整合應用程式及工具
{: #conx_apps_tools}

您也可以將外部應用程式和工具連接到 {{site.data.keyword.dashdbshort_notm}}，並使用它們進一步管理或分析您的資料。例如：

### 資料整合
{: #di}

- 連接需要分析資料庫的 {{site.data.keyword.Bluemix_short}} 應用程式。
- [DataStage](/docs/services/Db2whc/connecting/data.html#datastage)
- [Informatica](/docs/services/Db2whc/connecting/data.html#informatica)
- [Lift ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](https://lift.ng.bluemix.net/#docs){:new_window}
- [InfoSphere Data Replication](/docs/services/Db2whc/connecting/data.html#idr)
- [Segment ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](https://segment.com/docs/destinations/db2/){:new_window}
- [Data Studio](/docs/services/Db2whc/connecting/data.html#data_studio)
- [Data Server Manager](/docs/services/Db2whc/connecting/data.html#dsm)
- [CLPPLUS](/docs/services/Db2whc/connecting/data.html#clpplus)
- [Aginity Workbench，用來將 Netezza® 資料模型及資料移轉至 {{site.data.keyword.dashdbshort_notm}}](/docs/services/Db2whc/connecting/data.html#aginity_wb)
- [InfoSphere Data Architect，用來設計及部署資料庫綱目](/docs/services/Db2whc/connecting/data.html#ida)

### 資料視覺化/BI
{: #dvis_bi}

- [Cognos Analytics，用來針對您的資料執行「商業智慧」報告](/docs/services/Db2whc/connecting/vis_bi.html#cognos)
- [Looker ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](https://docs.looker.com/setup-and-management/connecting-to-db){:new_window}
- [Tableau](/docs/services/Db2whc/connecting/vis_bi.html#tableau)
- [Microsoft Excel](/docs/services/Db2whc/connecting/vis_bi.html#excel)
- [Esri ArcGIS for Desktop，用來使用您的資料執行地理空間分析和地圖發佈](/docs/services/Db2whc/connecting/vis_bi.html#esri_arcgis)

### 資料科學
{: #dsci}

- [Watson Studio（先前稱為 IBM Data Science Experience）](/docs/services/Db2whc/connecting/data_sci.html#watson_studio)
- [SPSS Statistics](/docs/services/Db2whc/connecting/data_sci.html#spss_stats)
- [SAS](/docs/services/Db2whc/connecting/data_sci.html#sas)
- [Local R 開發環境](/docs/services/Db2whc/connecting/data_sci.html#r_dev_env)

## 連接至另一個 Db2 資料庫
{: #fed}

{{site.data.keyword.dashdbshort_notm}} 支援 Db2 資料虛擬化（也稱為聯合）。資料虛擬化讓您能對位於組織各地多個分散式庫料庫上的所有資料，進行單一查詢的存取。您可以存取位於任何 Db2 或 Informix 資料來源的資料，不論是在雲端或內部部署皆可。
 

這項功能在所有版本的 {{site.data.keyword.dashdbshort_notm}} 上皆受支援，但入門方案例外。不過，您可以使用入門方案作為從中取回資料的目標。

- [資料虛擬化（聯合）](/docs/services/Db2whc/federation.html)


