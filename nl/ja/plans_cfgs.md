---

copyright:
  years: 2014, 2019
lastupdated: "2019-06-05"

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

# プランおよび構成
{: #plans_cfgs}

お客様の用途に合わせて構成および最適化されている {{site.data.keyword.dashdbshort_notm}} プランを選択できます。
{: shortdesc}

   * 試行用のエントリー・プラン。 最大 1 GB までのストレージを使用できる無料トライアルです。 [エントリー・プランの制約事項](#ep_restrictions)を参照してください。
   * Flex プラン。ストレージとコンピュートのリソースを個別に拡張可能
   * SMP プラン。実動用のさまざまなサイズを選択可能。単一ノードおよび単一インスタンスで構成される小規模、中規模、および大規模のプラン
   * MPP 複数ノード・クラスター構成。並列処理およびハイパフォーマンス用
   * 高可用性向けに構成されたプラン
   * Oracle 互換性

[{{site.data.keyword.Bluemix}} カタログ](https://cloud.ibm.com/catalog/services/db2-warehouse){:external}で、使用可能なすべての {{site.data.keyword.dashdbshort_notm}} プランを確認してください。
<!--   * Plans configured for data warehouse and online analytical processing (OLAP) workloads: [{{site.data.keyword.dashdbshort_notm}}](https://console.bluemix.net/catalog/services/db2-warehouse){:external} -->
<!--   * Plans configured for high-speed, transactional processing (OLTP): [{{site.data.keyword.dashdbshort_notm}} for Transactions](https://console.ng.bluemix.net/catalog/services/dashdb-for-transactions-sql-database){:external} -->

{{site.data.keyword.dashdbshort_notm}} Flex Performance plan の概要を確認するには、このビデオを視聴してください。

<iframe class="embed-responsive-item" id="youtubeplayer" title="Creating a connection from Cognos Analytics" type="text/html" width="640" height="390" src="//www.youtube.com/embed/59PKSnzNQAg?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

{{site.data.keyword.dashdbshort_notm}} サービスを、{{site.data.keyword.Bluemix}} のネットワーク分離環境にデプロイするように要求することができます。 [{{site.data.keyword.IBM_notm}} 営業担当員](https://www.ibm.com/connect/ibm/us/en/?lnk=fcw){:external}にお問い合わせください。

必要な構成がカタログにない場合は、[{{site.data.keyword.IBM_notm}} 営業担当員](https://www.ibm.com/connect/ibm/us/en/?lnk=fcw){:external}に連絡して他のオプションについて相談してください。

## IBM Cloud データ・センターでのプランの可用性
{: #availability}

以下の表は、地理的地域にある IBM Cloud データ・センター別のさまざまな {{site.data.keyword.dashdbshort_notm}} プランの可用性に関する情報を提供します。

| {{site.data.keyword.dashdbshort_notm}} プラン | アジア太平洋地域 | ヨーロッパ    | 北米/中米     | 南米 |
|------------------------------|--------------|-----------|---------------------------|---------------|
| Flex / Flex Performance      | 東京        | フランクフルト | ワシントン D.C. (米国東部) | *NA           |
|                              |              |           | ダラス (米国南部)         |               |  
|      |||||
| Flex One                     | *NA          | *NA       | ダラス (米国南部)         | *NA           |
|      |||||
| SMP                          | 香港    | アムステルダム | ワシントン D.C. (米国東部) | サンパウロ     |
|                              | ソウル        | フランクフルト | ダラス (米国南部)         |               | 
|                              | シンガポール    | ロンドン    | モントリオール                  |               | 
|                              | シドニー       | ミラノ     | ケレタロ                 |               | 
|                              | 東京        | オスロ      | トロント                   |               | 
|                              |              | パリ     |                           |               |
|      |||||
| MPP                          | 香港    | アムステルダム | ワシントン D.C. (米国東部) | サンパウロ     |
|                              | ソウル        | フランクフルト | ダラス (米国南部)         |               | 
|                              | シンガポール    | ロンドン    | モントリオール                  |               | 
|                              | シドニー       | ミラノ     | ケレタロ                 |               | 
|                              | 東京        | オスロ      | トロント                   |               | 
|                              |              | パリ     |                           |               |
{: caption="表 1. Db2 Warehouse on Cloud サービス・プランをサポートしている IBM Cloud データ・センター" caption-side="top"}

*NA = 現在、利用不可

## Amazon Web Services データ・センターでのプランの可用性
{: #availability_aws}

以下の表は、地理的地域にある Amazon Web Services データ・センター別のさまざまな {{site.data.keyword.dashdbshort_notm}} プランの可用性に関する情報を提供します。

| {{site.data.keyword.dashdbshort_notm}} プラン | アジア太平洋地域 | ヨーロッパ    | 北米/中米     | 南米 |
|------------------------------|--------------|-----------|---------------------------|---------------|
| Flex                         | シドニー       | フランクフルト | 北バージニア | *NA           |
|                              | シンガポール    | ロンドン    |             |               |  
|      |||||
| Flex Performance             | シドニー       | フランクフルト | 北バージニア | *NA           |
|                              | シンガポール    | ロンドン    |             |               | 
{: caption="表 2. Db2 Warehouse on Cloud サービス・プランをサポートしている Amazon Web Services データ・センター" caption-side="top"}

*NA = 現在、利用不可


## エントリー・プランの制約事項
{: #ep_restrictions}

基幹業務のワークロードまたはパフォーマンスの影響を受けやすいワークロードには、エントリー・サービス・プランではなく、エンタープライズ・レベルのサービス・プランを使用することを強くお勧めします。 
{: important}

次の表に、{{site.data.keyword.dashdbshort_notm}} エントリー・プランの制約事項を示します。

| カテゴリー | 項目 | 制約事項 | 
|----------|------|-------------|
| リソース | ストレージ | 1 ユーザーにつき 20 GB のストレージ。 このプランは、使用されているストレージが 1 GB 未満の場合にのみ無料です。 |
|  | 接続 | 1 ユーザーにつき 50 の接続。 この制限は、インスタンスのシステムの整合性を維持するために動的に調整される場合があります。 |
|  | パフォーマンス | マルチテナント・システム上の他のユーザーが実行するワークロードによって、パフォーマンスが変動する可能性があります。 |
|  |  |
| フィーチャーおよび機能 | フェデレーション | サポートされていません |
|  | Oracle 互換性 | サポートされていません |
|  | ユーザー定義拡張機能 (UDF) | サポートされていません |
|  | ユーザー管理 | ユーザーに管理権限が与えられていません |
|  | 行および列のアクセス制御 (RCAC) | サポートされていません |
|  | データのロードに使用するための IBM InfoSphere Data Replication | サポートされていません |
|  |  |
| ネットワーキング環境 | IBM Cloud Integrated Analytics | サポートされていません |
|  | IBM Cloud Dedicated | サポートされていません |
|  |  |
| セキュリティー・コンプライアンス | Health Information Portability and Accountability Act of 1996 (HIPAA) | サポートされていません。 サービス記述書を参照してください。 |
|  | EU 一般データ保護規則 (GDPR) | 特定の制限は適用されません |
|  |  |
| アカウント管理 | 再活動化 | 再活動化の要件はありません |
{: caption="表 3. {{site.data.keyword.dashdbshort_notm}} エントリー・プランの制約事項" caption-side="top"}
