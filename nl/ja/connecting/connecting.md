---

copyright:
  years: 2014, 2018
lastupdated: "2018-10-15"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 接続の概要
{: #overview}

コマンド行インターフェース、IBM® またはサード・パーティーのアプリケーションやツール、作成したアプリケーションを {{site.data.keyword.dashdbshort_notm}} データベースに接続できます。 
{: shortdesc}

## 前提条件
{: #prereqs}

{{site.data.keyword.dashdbshort_notm}} データベースへの接続を試行する前に、必要な前提条件を満たしていることを確認します。 

- 以下のようにデータベースの詳細と資格情報を収集します。

   データベースに接続するには、データベースの詳細 (ホスト名など) と、資格情報 (ユーザー ID とパスワードなど) が必要です。 この接続情報は、{{site.data.keyword.dashdbshort_notm}} Web コンソールから収集できます。

- 以下のように、サポートされているドライバーがインストール済みであることを確認します。

   - アプリケーションかツールに既に Db2 v11.1 IBM Data Server Driver Package が含まれている場合は、アプリケーションまたはツールは、そのドライバーを使用して {{site.data.keyword.dashdbshort_notm}} データベースに接続できます。
   - 含まれていない場合は、Db2 ドライバー・パッケージをインストールします。このパッケージは、{{site.data.keyword.dashdbshort_notm}} Web コンソールからダウンロードできます。

- 環境の構成

  - ドライバー構成ファイル `db2dsdriver.cfg` に、データベースに関する項目を追加します。
  - Secure Sockets Layer (SSL)

    接続に SSL を使用するか使用しないかを選択できます。 使用するポートや接続ストリングなどの接続の詳細は、SSL 接続を使用するかどうかに応じて異なります。

    SSL 接続を使用するには、CA 証明書が必要です。
    - 最新の {{site.data.keyword.dashdbshort_notm}} ドライバー・パッケージを使用している場合は、証明書ファイルがパッケージに組み込まれており、このファイルが接続に使用されます。
    - IBM Data Server Driver Package を使用する場合は、{{site.data.keyword.dashdbshort_notm}} Web コンソールから SSL 証明書をダウンロードできます。

- ポートが使用可能であることを確認します。

   ネットワークがファイアウォールの背後にある場合、標準プロトコルにはポート番号 `50000`、SSL 接続にはポート番号 `50001` で通信が許可されていることを確認します。

<!-- Before you can connect to your {{site.data.keyword.dashdbshort_notm}} database, verify that you completed downloading and installing the necessary components on the prerequisites checklist: 

- [Prerequisites checklist](prereqs.html) -->

### 接続情報の収集
{: #collect_info}

- [データベースの詳細と接続資格情報](credentials.html)

### ドライバー・パッケージのダウンロードおよびインストール
{: #dl_install}

- [ドライバー・パッケージのダウンロード](driver_pkg.html)
- [Linux または PowerLinux 上でのインストール](install_linux.html)
- [Mac OS X 上でのインストール](install_mac.html)
- [Windows 上でのインストール](install_win.html)

### 環境の構成
{: #cfg_env}

- [環境の構成](driver_pkg_cfg.html)
- [Secure Sockets Layer (SSL) サポート](ssl.html)

## プログラムによる接続
{: #conx_prgrm}

共通プログラミング言語を使用して、{{site.data.keyword.dashdbshort_notm}} データベースに接続するアプリケーションを作成できます。
{: shortdesc}

- [JDBC 
](jdbc.html)
- [Microsoft Windows ODBC または CLI](odbc_cli.html)
- [.NET](net_apps.html)
- [ODBC データ ソース アドミニストレータ](odbc_data_source_admin.html)
- [PHP](php.html)
- [REST API](rest_api.html)
<!-- - [C++]() -->
<!-- - [Java]() -->
<!-- - [Node.js]() -->
<!-- - [Perl]() -->
<!-- - [Python]() -->

## アプリケーションとツールの統合
{: #conx_apps_tools}

また、外部アプリケーションやツールを {{site.data.keyword.dashdbshort_notm}} に接続して利用し、
データをさらに管理または分析することも可能です。 例えば、以下を行えます。

### データ統合
- 分析データベースを必要とする {{site.data.keyword.Bluemix_short}} アプリケーションを接続します。
- [DataStage](data.html#datastage)
- [Informatica](data.html#informatica)
- [Lift ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://lift.ng.bluemix.net/#docs){:new_window}
- [InfoSphere Data Replication](data.html#idr)
- [Segment ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://segment.com/docs/destinations/db2/){:new_window}
- [Data Studio](data.html#data_studio)
- [Data Server Manager](data.html#dsm)
- [CLPPLUS](data.html#clpplus)
- [Aginity Workbench を接続して、Netezza® データ・モデルおよびデータを {{site.data.keyword.dashdbshort_notm}}](data.html#aginity_wb) にマイグレーションします
- [InfoSphere Data Architect を接続して、データベース・スキーマを設計およびデプロイします](data.html#ida)

### データ可視化/BI
- [Cognos Analytics を接続して、データに対してビジネス・インテリジェンス・レポートを実行します](vis_bi.html#cognos)
- [Looker ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.looker.com/setup-and-management/connecting-to-db){:new_window}
- [Tableau](vis_bi.html#tableau)
- [Microsoft Excel](vis_bi.html#excel)
- [Esri ArcGIS for Desktop を接続して、ご使用のデータで地理情報分析やマップ・パブリッシュを実行します](vis_bi.html#esri_arcgis)

### Data Science
- [Watson Studio (以前の IBM Data Science Experience)](data_sci.html#watson_studio)
- [SPSS Statistics](data_sci.html#spss_stats)
- [SAS](data_sci.html#sas)
- [ローカル R 開発環境](data_sci.html#r_dev_env)

## 他の DB2 データベースへの接続
{: #fed}

DB2 データ仮想化 (フェデレーションとも呼ばれる) は、{{site.data.keyword.dashdbshort_notm}} によってサポートされます。 データ仮想化によって、組織内の任意の場所にある複数の分散データベース上にあるすべてのデータに対して単一照会アクセスが可能になります。 クラウドとオンプレミスの両方の DB2 または Informix のデータ・ソースにあるデータにアクセスできます。 

このファンクションは、エントリー・プランを除き、{{site.data.keyword.dashdbshort_notm}} のすべてのバージョンでサポートされています。 ただし、データをプルできるターゲットとしてエントリー・プランを使用できます。

- [データ仮想化 (フェデレーション)](../federation.html)


