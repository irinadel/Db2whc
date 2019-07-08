---

copyright:
  years: 2014, 2019
lastupdated: "2019-05-21"

keywords:

subcollection: Db2whc

---

<!-- Attribute definitions --> 
{:javascript: #javascript .ph data-hd-programlang='javascript'}
{:java: #java .ph data-hd-programlang='java'}
{:ruby: #ruby .ph data-hd-programlang='ruby'}
{:php: #php .ph data-hd-programlang='php'}
{:python: #python .ph data-hd-programlang='python'}
{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}

# 入門指導教學
{: #getting-started}

{{site.data.keyword.dashdblong}} 受管理服務是在雲端中為您所佈建的 SQL Database。您就像使用任何資料庫軟體一般的使用 Db2 倉儲，但沒有硬體設置或軟體安裝及維護的額外負荷與費用。
{: shortdesc}

<!-- New tutorial submitted by Olaf Depper of DTE on 5-May-2019. Working on edits of Word doc. -->
<!--To get started on accessing and working with {{site.data.keyword.dashdbshort_notm}}, go through the [Getting started tutorial](https://cloudcontent.mybluemix.net/cloud/garage/dte/tutorial/test-db2-warehouse-cloud-post-sales){:external}. -->

## 免費試用
{: #freetrial}

您可以嘗試 {{site.data.keyword.dashdbshort_notm}} 入門方案，免費使用高達 1 GB 的儲存空間。[免費試用](https://cloud.ibm.com/catalog/services/db2-warehouse){:external}

## 介面
{: #interfaces}

您可以透過下列方式來使用倉儲資料庫：
{: shortdesc}

   * 從 Web 主控台
   * REST API
   * 連接本端電腦的應用程式或您最愛的工具
   * 將 {{site.data.keyword.dashdbshort_notm}} 用作 {{site.data.keyword.Bluemix_notm}} 應用程式或服務的資料來源

### Web 主控台
{: #web_console}

Web 主控台為您使用資料庫所需的所有項目提供一個圖形介面，包括：負載機能、SQL 編輯器、驅動程式下載等等。
{: shortdesc}

![Web 主控台儀表板頁面的視圖](images/uc.png "Web 主控台開啟至儀表板頁面"){: caption="圖 1. Web 主控台儀表板頁面的視圖" caption-side="bottom"}

<!-- Click the link to take a tour of the {{site.data.keyword.dashdbshort_notm}} for Analytics web console: [General tour](http://ibm.biz/dashdb-general-quick-tour){:external}. -->

您可以透過下列方式來存取 Web 主控台：
   * 從 {{site.data.keyword.Bluemix_notm}} 儀表板 - 您可以從 {{site.data.keyword.dashdbshort_notm}} 服務的「服務詳細資料」頁面中開啟 Web 主控台。
   * 直接 URL - 您可以對 {{site.data.keyword.dashdbshort_notm}} 服務的 Web 主控台的 URL 加上書籤。

### REST API
{: #api}

使用 {{site.data.keyword.dashdbshort_notm}} 服務方案，您可以透過使用 [{{site.data.keyword.dashdbshort_notm}} REST API](http://ibm.biz/db2whc_api){:external} 執行與檔案管理及載入資料相關的作業。
{: shortdesc}

### 連接本端電腦的應用程式或您最愛的工具
{: #connect_apps}

請完成下列步驟，配置本端環境以連接至 {{site.data.keyword.dashdbshort_notm}} 資料庫：
{: shortdesc}

1. 從 {{site.data.keyword.dashdbshort_notm}} Web 主控台下載[驅動程式套件](/docs/services/Db2whc/connecting?topic=Db2whc-dr_pkg#dr_pkg)。
2. 在您的應用程式或工具執行所在的電腦上，安裝驅動程式套件。
   - [在 Linux 或 PowerLinux 上安裝](/docs/services/Db2whc/connecting?topic=Db2whc-install_dr_pkg_linux#install_dr_pkg_linux)
   - [在 Mac OS X 上安裝](/docs/services/Db2whc/connecting?topic=Db2whc-install_dr_pkg_mac#install_dr_pkg_mac)
   - [在 Windows 上安裝](/docs/services/Db2whc/connecting?topic=Db2whc-install_dr_pkg_windows#install_dr_pkg_windows)
3. 針對 {{site.data.keyword.dashdbshort_notm}} 資料庫[配置驅動程式檔案](/docs/services/Db2whc/connecting?topic=Db2whc-cfg_loc_env#cfg_loc_env)。

### 將 Db2 Warehouse on Cloud 用作 {{site.data.keyword.Bluemix_notm}} 應用程式或服務的資料來源
{: #data_src}

將 {{site.data.keyword.Bluemix_notm}} 上管理的應用程式連接至 {{site.data.keyword.dashdbshort_notm}} 資料庫的方式，與將您的本端應用程式連接至 {{site.data.keyword.dashdbshort_notm}} 資料庫的方式相同。
{: shortdesc}

當您的應用程式使用 {{site.data.keyword.Bluemix_notm}} 平台時，您可以充分運用 `VCAP _SERVICES` 環境變數，以簡化指定資料庫詳細資料及認證的作業。
1. 在 {{site.data.keyword.Bluemix_notm}} 儀表板上，於 {{site.data.keyword.dashdbshort_notm}} 服務的「服務詳細資料」頁面的**連線**標籤中，按一下**建立連線**按鈕。
2. 選取要與 {{site.data.keyword.dashdbshort_notm}} 資料庫搭配使用作為資料來源的 {{site.data.keyword.cloud_notm}} 應用程式，然後按一下**連接**按鈕。
3. 更新應用程式碼，擷取 `VCAP_SERVICES` 環境變數中的資料庫詳細資料及認證：

    **不含 `VCAP_SERVICES` 的範例**

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

    **含有 `VCAP_SERVICES` 的範例**

    ```php
    <?php
    $driver      = "DRIVER={IBM DB2 ODBC DRIVER};";

    $vcap        = json_decode( getenv( "VCAP_SERVICES" ), true );
    $dsn         = $vcap[ "dashDB" ][0][ "credentials" ][ "dsn" ];

    $conn_string = $driver . $dsn;
                                   
    $conn        = db2_connect( $conn_string, "", "" );
    ?>
    ```

## 範例
{: #samples}

以下鏈結範例示範如何從不同語言的應用程式以程式設計方式連接至 {{site.data.keyword.dashdbshort_notm}} 資料庫：
{: shortdesc}

- [JDBC](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_jdbc#con_prog_jdbc)
- [Microsoft Windows ODBC 或 CLI](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_odbc_cli#con_prog_odbc_cli)
- [.NET](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_net#con_prog_net)
- [ODBC 資料來源管理員](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_odbc_dsa#con_prog_odbc_dsa)
- [PHP](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_php#con_prog_php)
- [REST API](/docs/services/Db2whc/connecting?topic=Db2whc-con_rest_api#con_rest_api)

## 視訊：簡介 Db2 Warehouse on Cloud
{: #intro_vid}

觀看此視訊，以查看 {{site.data.keyword.dashdbshort_notm}} 的簡介。

<iframe class="embed-responsive-item" id="youtubeplayer1" title="簡介 {{site.data.keyword.dashdbshort_notm}}" type="text/html" width="640" height="390" src="//www.youtube.com/embed/0NO9OTFWzKs?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

## 視訊：簡介彈性效能方案
{: #intro_vid_flex}

觀看此視訊，以查看「{{site.data.keyword.dashdbshort_notm}} 彈性效能」方案的簡介。

<iframe class="embed-responsive-item" id="youtubeplayer2" title="從 Cognos Analytics 建立連線" type="text/html" width="640" height="390" src="//www.youtube.com/embed/59PKSnzNQAg?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

## 視訊：連接分析應用程式
{: #cognos_vid}

觀看此視訊，以查看如何從 Cognos Analytics 建立連線。

<iframe class="embed-responsive-item" id="youtubeplayer3" title="從 Cognos Analytics 建立連線" type="text/html" width="640" height="390" src="//www.youtube.com/embed/TRUEPVHGi0s?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

