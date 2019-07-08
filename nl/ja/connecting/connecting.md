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

# 接続の概要
{: #connect_ov}

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

- [データベースの詳細と接続資格情報](/docs/services/Db2whc/connecting?topic=Db2whc-db_details_cxn_creds#db_details_cxn_creds)

### ドライバー・パッケージのダウンロードおよびインストール
{: #dl_install}

- [ドライバー・パッケージのダウンロード](/docs/services/Db2whc/connecting?topic=Db2whc-dr_pkg#dr_pkg)
- [Linux または PowerLinux 上でのインストール](/docs/services/Db2whc/connecting?topic=Db2whc-install_dr_pkg_linux#install_dr_pkg_linux)
- [Mac OS X 上でのインストール](/docs/services/Db2whc/connecting?topic=Db2whc-install_dr_pkg_mac#install_dr_pkg_mac)
- [Windows 上でのインストール](/docs/services/Db2whc/connecting?topic=Db2whc-install_dr_pkg_windows#install_dr_pkg_windows)

### 環境の構成
{: #cfg_env}

- [環境の構成](/docs/services/Db2whc/connecting?topic=Db2whc-cfg_loc_env#cfg_loc_env)
- [Secure Sockets Layer (SSL) サポート](/docs/services/Db2whc/connecting?topic=Db2whc-ssl_support#ssl_support)

## 接続オプション
{: #connect_opts}

アプリケーションの接続要件に応じて、{{site.data.keyword.dashdbshort_notm}} は複数のセキュア接続オプションを提供しています。  
{: shortdesc}

[接続オプション](/docs/services/Db2whc/connecting?topic=Db2whc-connect_options#connect_options)を参照してください。

## プログラムによる接続
{: #conx_prgrm}

共通プログラミング言語を使用して、{{site.data.keyword.dashdbshort_notm}} データベースに接続するアプリケーションを作成できます。
{: shortdesc}

- [JDBC](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_jdbc#con_prog_jdbc)
- [Microsoft Windows ODBC または CLI](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_odbc_cli#con_prog_odbc_cli)
- [.NET](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_net#con_prog_net)
- [ODBC データ ソース アドミニストレータ](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_odbc_dsa#con_prog_odbc_dsa)
- [PHP](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_php#con_prog_php)
- [REST API](/docs/services/Db2whc/connecting?topic=Db2whc-con_rest_api#con_rest_api)
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
{: #di}

- 分析データベースを必要とする {{site.data.keyword.Bluemix_short}} アプリケーションを接続します。
- [DataStage](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#datastage)
- [Informatica](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#informatica)
- [Lift](https://www.lift-cli.cloud.ibm.com/#docs){:external}
- [InfoSphere Data Replication](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#idr)
- [Segment](https://segment.com/docs/destinations/db2/){:external}
- [Data Studio](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#data_studio)
- [Data Server Manager](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#dsm)
- [CLPPLUS](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#clpplus)
- [Aginity Workbench を接続して、Netezza® データ・モデルおよびデータを {{site.data.keyword.dashdbshort_notm}}](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#aginity_wb) にマイグレーションします
- [InfoSphere Data Architect を接続して、データベース・スキーマを設計およびデプロイします](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#ida)

### データ可視化/BI
{: #dvis_bi}

- [Cognos Analytics を接続して、データに対してビジネス・インテリジェンス・レポートを実行します](/docs/services/Db2whc/connecting?topic=Db2whc-data_vis_bi#cognos)
- [Looker](https://docs.looker.com/setup-and-management/connecting-to-db){:external}
- [Tableau](/docs/services/Db2whc/connecting?topic=Db2whc-data_vis_bi#tableau)
- [Microsoft Excel](/docs/services/Db2whc/connecting?topic=Db2whc-data_vis_bi#excel)
- [Esri ArcGIS for Desktop を接続して、ご使用のデータで地理情報分析やマップ・パブリッシュを実行します](/docs/services/Db2whc/connecting?topic=Db2whc-data_vis_bi#esri_arcgis)

### Data Science
{: #dsci}

- [Watson Studio (以前の IBM Data Science Experience)](/docs/services/Db2whc/connecting?topic=Db2whc-ds#watson_studio)
- [SPSS Statistics](/docs/services/Db2whc/connecting?topic=Db2whc-ds#spss_stats)
- [SAS](/docs/services/Db2whc/connecting?topic=Db2whc-ds#sas)
- [ローカル R 開発環境](/docs/services/Db2whc/connecting?topic=Db2whc-ds#r_dev_env)

## 他の Db2 データベースへの接続
{: #fed}

Db2 データ仮想化 (フェデレーションとも呼ばれる) は、{{site.data.keyword.dashdbshort_notm}} によってサポートされます。 データ仮想化によって、組織内の任意の場所にある複数の分散データベース上にあるすべてのデータに対して単一照会アクセスが可能になります。 クラウドとオンプレミスの両方の Db2 または Informix のデータ・ソースにあるデータにアクセスできます。 

このファンクションは、エントリー・プランを除き、{{site.data.keyword.dashdbshort_notm}} のすべてのバージョンでサポートされています。 ただし、データをプルできるターゲットとしてエントリー・プランを使用できます。

- [データ仮想化 (フェデレーション)](/docs/services/Db2whc?topic=Db2whc-data_virt_fed#data_virt_fed)


