---

copyright:
  years: 2014, 2018
lastupdated: "2018-02-27"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Db2 Warehouse on Cloud の概要
{: #overview}

{{site.data.keyword.dashdblong}} サービス・プランでは、 データウェアハウスを使用して、特殊なタイプを含むリレーショナル・データを保管します。 組み込み分析を使用するか、お客様独自のアプリケーションを接続して、お客様独自のデータまたは他のクラウド・サービスからロードしたデータを分析します。 分析ワークロードに対して、縦欄の表で高性能のメモリー内データベース・テクノロジーを活用できます。 {{site.data.keyword.dashdbshort_notm}} Web コンソールは、
共通データ管理タスク (データのロードなど) および分析タスク (照会や R スクリプトの実行など) を処理します。
{: shortdesc}

また、外部アプリケーションやツールを {{site.data.keyword.dashdbshort_notm}} に接続して利用し、
データをさらに管理または分析することも可能です。 例えば、以下を行えます。
* {{site.data.keyword.IBM_notm}} InfoSphere® Data Architect を接続して、データベース・スキーマを設計およびデプロイします。
* {{site.data.keyword.IBM_notm}} Cognos® サーバーを接続して、データに対して Cognos レポートを実行します。
* SQL ベースのツール (Tableau、Microstrategy、Microsoft Excel など) を接続して、データを操作または分析します。
* 分析データベースを必要とする {{site.data.keyword.Bluemix_short}} アプリケーションを接続します。
* Aginity Workbench を接続して、Netezza® データ・モデルおよびデータを {{site.data.keyword.dashdbshort_notm}} にマイグレーションします。

## Db2 Warehouse on Cloud マネージド・サービス
{: #managed_service}

{{site.data.keyword.dashdbshort_notm}} の完全マネージド・サービスは、すべてのソフトウェア・アップグレード、オペレーティング・システム更新、およびハードウェア保守を処理します。 このサービスには、データベースおよびインフラストラクチャーの 24 時間 365 日ヘルス・モニターが含まれています。 ハードウェアまたはソフトウェアの障害が発生した場合は、このサービスが自動的に再始動されます。
{: shortdesc}

## プランおよび構成
{: #plans_cfgs}

お客様の用途に合わせて構成および最適化されている {{site.data.keyword.dashdbshort_notm}} プランを選択できます。
{: shortdesc}

* 試行用のエントリー・プラン
* Flex Performance プラン。ストレージとコンピュートのリソースを個別に拡張可能
* 実動用の小規模プラン、中規模プラン、および大規模プラン
* 並列処理用の MPP 構成
* 高可用性のために構成されたプラン、または、Oracle 互換性のために構成されたプラン
* その他 ...

{{site.data.keyword.Bluemix}} カタログで、使用可能なプランを確認してください。
* データウェアハウスおよび分析 (OLAP) ワークロード用に構成されたプラン: [{{site.data.keyword.dashdbshort_notm}}](https://console.bluemix.net/catalog/services/db2-warehouse){:new_window}

必要な構成がカタログにない場合は、[{{site.data.keyword.IBM_notm}} 営業担当員に連絡して ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/connect/ibm/us/en/?lnk=fcw){:new_window}、他のオプションについて相談してください。

## Db2 Warehouse on Cloud のプロビジョニング
{: #whse_provision}

{{site.data.keyword.dashdbshort_notm}} データベースを {{site.data.keyword.BluSoftlayer_full}} 上で AWS 用にプロビジョンできます。
{: shortdesc}

データウェアハウスを AWS 用にプロビジョンする場合は、**MPP Small for AWS** プランを選択してください。
