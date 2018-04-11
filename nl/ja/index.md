---

copyright:
  years: 2014, 2018
lastupdated: "2018-03-15"

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
{:pre: .pre}

# 概説
{: #getting_started}

{{site.data.keyword.dashdblong}} マネージド・サービスは、クラウド内でプロビジョンされた SQL データベースです。 任意のデータベース・ソフトウェアを使用するのと同じように Db2 ウェアハウスを使用できますが、ハードウェアのセットアップやソフトウェアのインストールおよび保守のためのオーバーヘッドもコストもかかりません。 
{: shortdesc}

## 無料トライアル
{: #freetrial}

ストレージが 1 GB までの {{site.data.keyword.dashdbshort_notm}} エントリー・プランを無料で試用できます。 [無料トライアル ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.bluemix.net/catalog/services/dashdb){:new_window}

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

以下の方法で、Web コンソールにアクセスできます。
* {{site.data.keyword.Bluemix_notm}} ダッシュボードから - {{site.data.keyword.dashdbshort_notm}} サービスの「サービス詳細」ページから Web コンソールを開くことができます。
* ダイレクト URL - {{site.data.keyword.dashdbshort_notm}} サービスの Web コンソールの URL をブックマークできます。

### REST API
{: #api}

{{site.data.keyword.dashdbshort_notm}} サービス・プランでは、ファイル管理、データのロード、および R スクリプトの実行に関連するタスクを、[{{site.data.keyword.dashdbshort_notm}} REST API ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://ibm.biz/db2whc_api){:new_window} を使用して実行できます。
{: shortdesc}

### ローカル・コンピューターからアプリケーションまたは任意のツールを接続する
{: #connect_apps}

以下の手順を実行して、Db2 ウェアハウス・データベースに接続するようにローカル環境を構成します。
{: shortdesc}

1. Db2 Warehouse on Cloud Web コンソールから、[ドライバー・パッケージ ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_driver_package.html){:new_window} をダウンロードします。
2. アプリまたはツールが実行されているコンピューターで [ドライバー・パッケージのインストール![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_driver_package_install.html){:new_window} を行います。
3. Db2 ウェアハウス・データベース用に[ドライバー・ファイルの構成 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/support/knowledgecenter/en/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_driver_package_config.html){:new_window} を行います。

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

各種の言語で作成されたアプリケーションから {{site.data.keyword.dashdbshort_notm}} データベースに接続する方法を示すサンプルへのリンクは次のとおりです。
{: shortdesc}

* [.NET ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting__net_applications.html){:new_window}
* [JDBC ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_jdbc_applications.html){:new_window}
* [PHP ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_php.html){:new_window}
* [GitHub にある {{site.data.keyword.dashdbshort_notm}} サンプル ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/IBM-Bluemix/dashdb-nodejs-helloworld){:new_window}


