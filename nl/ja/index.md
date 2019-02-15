---

copyright:
  years: 2014, 2019
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

# 概説
{: #getting_started}

{{site.data.keyword.dashdblong}} マネージド・サービスは、クラウド内でプロビジョンされた SQL データベースです。 任意のデータベース・ソフトウェアを使用するのと同じように Db2 ウェアハウスを使用できますが、ハードウェアのセットアップやソフトウェアのインストールおよび保守のためのオーバーヘッドもコストもかかりません。 
{: shortdesc}

## 無料トライアル
{: #freetrial}

ストレージが 1 GB までの {{site.data.keyword.dashdbshort_notm}} エントリー・プランを無料で試用できます。 [無料トライアル ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.bluemix.net/catalog/services/db2-warehouse){:new_window}

## インターフェース
{: #interfaces}

以下の方法で、ウェアハウス・データベースを使用した作業を行うことができます。
{: shortdesc}

   * Web コンソールから
   * REST API
   * ローカル・コンピューターからアプリケーションまたは任意のツールを接続する
   * {{site.data.keyword.Bluemix_notm}} アプリまたはサービス用のデータ・ソースとして {{site.data.keyword.dashdbshort_notm}} を使用する

### Web コンソール
{: #web_console}

Web コンソールは、ロード機能、SQL エディター、ドライバー・ダウンロードなど、データベースを使用するために必要なすべての操作を実行できるグラフィカル・インターフェースです。
{: shortdesc}

![Web コンソールのダッシュボード・ページの表示](images/console_v3.png)

<!-- Click the link to take a tour of the {{site.data.keyword.dashdbshort_notm}} for Analytics web console: [General tour ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://ibm.biz/dashdb-general-quick-tour){:new_window}. -->

以下の方法で、Web コンソールにアクセスできます。
   * {{site.data.keyword.Bluemix_notm}} ダッシュボードから - {{site.data.keyword.dashdbshort_notm}} サービスの「サービス詳細」ページから Web コンソールを開くことができます。
   * ダイレクト URL - {{site.data.keyword.dashdbshort_notm}} サービスの Web コンソールの URL をブックマークできます。

### REST API
{: #api}

{{site.data.keyword.dashdbshort_notm}} サービス・プランでは、ファイル管理およびデータのロードに関連するタスクを、[{{site.data.keyword.dashdbshort_notm}} REST API ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://ibm.biz/db2whc_api){:new_window} を使用して実行できます。
{: shortdesc}

### ローカル・コンピューターからアプリケーションまたは任意のツールを接続する
{: #connect_apps}

以下の手順を実行して、{{site.data.keyword.dashdbshort_notm}} データベースに接続するようにローカル環境を構成します。
{: shortdesc}

1. [ ドライバー・パッケージ](connecting/driver_pkg.html)を {{site.data.keyword.dashdbshort_notm}} Web コンソールからダウンロードします。
2. アプリまたはツールが実行されているコンピューターにドライバー・パッケージをインストールします。
   - [Linux または PowerLinux 上でのインストール](connecting/install_linux.html)
   - [Mac OS X 上でのインストール](connecting/install_mac.html)
   - [Windows 上でのインストール](connecting/install_win.html)
3. {site.data.keyword.dashdbshort_notm}} データベース用の[ドライバー・ファイルの構成](connecting/driver_pkg_cfg.html)。

### {{site.data.keyword.Bluemix_notm}} アプリまたはサービス用のデータ・ソースとして Db2 Warehouse on Cloud を使用する
{: #data_src}

{{site.data.keyword.Bluemix_notm}} でホストされているアプリは、ローカル・アプリケーションが {{site.data.keyword.dashdbshort_notm}} データベースに接続するのとまったく同じ方法で、{{site.data.keyword.dashdbshort_notm}} データベースに接続できます。
{: shortdesc}

アプリが {{site.data.keyword.Bluemix_notm}} プラットフォームを使用している場合、`VCAP _SERVICES` 環境変数を利用して、データベースの詳細および資格情報を指定する作業を単純化できます。
1. {{site.data.keyword.Bluemix_notm}} ダッシュボードで、{{site.data.keyword.dashdbshort_notm}} サービスの「サービス詳細」ページの**「接続」**タブで、**「接続の作成」**ボタンをクリックします。
2. {{site.data.keyword.dashdbshort_notm}} データベースをデータ・ソースとして使用する {{site.data.keyword.Bluemix_notm}} アプリを選択し、**「接続」**ボタンをクリックします。
3. データベースの詳細および資格情報を `VCAP_SERVICES` 環境変数から取り出すようにアプリケーション・コードを更新します。

    **`VCAP_SERVICES` を使用しない例**

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

    **`VCAP_SERVICES` を使用する例**

    ```php
    <?php
    $driver      = "DRIVER={IBM DB2 ODBC DRIVER};";

    $vcap        = json_decode( getenv( "VCAP_SERVICES" ), true );
    $dsn         = $vcap[ "dashDB" ][0][ "credentials" ][ "dsn" ];

    $conn_string = $driver . $dsn;
                                   
    $conn        = db2_connect( $conn_string, "", "" );
    ?>
    ```

## 例
{: #samples}

各種の言語で作成されたアプリケーションから {{site.data.keyword.dashdbshort_notm}} データベースへのプログラマチックな接続方法を示すサンプルへのリンクは次のとおりです。
{: shortdesc}

- [JDBC 
](connecting/jdbc.html)
- [Microsoft Windows ODBC または CLI](connecting/odbc_cli.html)
- [.NET](connecting/net_apps.html)
- [ODBC データ ソース アドミニストレータ](connecting/odbc_data_source_admin.html)
- [PHP](connecting/php.html)
- [REST API](connecting/rest_api.html)

## ビデオ: Introducing Db2 Warehouse on Cloud
{: #intro_vid}

{{site.data.keyword.dashdbshort_notm}} の概要を確認するには、このビデオを視聴してください。

<iframe class="embed-responsive-item" id="youtubeplayer1" title="Introduction to {{site.data.keyword.dashdbshort_notm}}" type="text/html" width="640" height="390" src="//www.youtube.com/embed/0NO9OTFWzKs?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

## ビデオ: Introducing the Flex Performance plan
{: #intro_vid_flex}

{{site.data.keyword.dashdbshort_notm}} Flex Performance plan の概要を確認するには、このビデオを視聴してください。

<iframe class="embed-responsive-item" id="youtubeplayer2" title="Creating a connection from Cognos Analytics" type="text/html" width="640" height="390" src="//www.youtube.com/embed/59PKSnzNQAg?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

## ビデオ: Connecting an analytics application
{: #cognos_vid}

Cognos Analytics からの接続の作成方法を確認するには、このビデオを視聴してください。

<iframe class="embed-responsive-item" id="youtubeplayer3" title="Creating a connection from Cognos Analytics" type="text/html" width="640" height="390" src="//www.youtube.com/embed/TRUEPVHGi0s?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

