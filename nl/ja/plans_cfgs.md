---

copyright:
  years: 2014, 2018
lastupdated: "2018-10-24"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# プランおよび構成
{: #plans_cfgs}

お客様の用途に合わせて構成および最適化されている {{site.data.keyword.dashdbshort_notm}} プランを選択できます。
{: shortdesc}

   * 試行用のエントリー・プラン。 最大 1 GB までのストレージを使用できる無料トライアルです。
   * Flex プラン。ストレージとコンピュートのリソースを個別に拡張可能
   * SMP プラン。実動用のさまざまなサイズを選択可能。単一ノードおよび単一インスタンスで構成される小規模、中規模、および大規模のプラン
   * MPP 複数ノード・クラスター構成。並列処理およびハイパフォーマンス用
   * 高可用性向けに構成されたプラン
   * Oracle 互換性

[{{site.data.keyword.Bluemix}} カタログ](https://console.bluemix.net/catalog/services/db2-warehouse){:new_window}で、使用可能なすべての {{site.data.keyword.dashdbshort_notm}} プランを確認してください。
<!--   * Plans configured for data warehouse and online analytical processing (OLAP) workloads: [{{site.data.keyword.dashdbshort_notm}}](https://console.bluemix.net/catalog/services/db2-warehouse){:new_window} -->
<!--   * Plans configured for high-speed, transactional processing (OLTP): [{{site.data.keyword.dashdbshort_notm}} for Transactions](https://console.ng.bluemix.net/catalog/services/dashdb-for-transactions-sql-database){:new_window} -->

{{site.data.keyword.dashdbshort_notm}} Flex Performance plan の概要を確認するには、このビデオを視聴してください。

<iframe class="embed-responsive-item" id="youtubeplayer" title="Creating a connection from Cognos Analytics" type="text/html" width="640" height="390" src="//www.youtube.com/embed/59PKSnzNQAg?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

{{site.data.keyword.dashdbshort_notm}} サービスを、{{site.data.keyword.Bluemix}} のネットワーク分離環境にデプロイするように要求することができます。 [{{site.data.keyword.IBM_notm}} 営業担当員 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/connect/ibm/us/en/?lnk=fcw){:new_window} にお問い合わせください。

必要な構成がカタログにない場合は、[{{site.data.keyword.IBM_notm}} 営業担当員に連絡して ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/connect/ibm/us/en/?lnk=fcw){:new_window}、他のオプションについて相談してください。

## データ・センターでのプランの可用性
{: #availability}

以下の表は、地理的地域にあるデータ・センター別のさまざまな Db2 Warehouse on Cloud プランの可用性に関する情報を提供します。

| Db2 Warehouse on Cloud プラン |アジア太平洋地域| ヨーロッパ | 北米/中米 | 南米 |
|------------------------------|--------------|-----------|-----------------------    |---------------|
| Flex                         | *NA          | フランクフルト |ワシントン D.C.(米国東部) | *NA           |
|                              |              |           | ダラス (米国南部)         |               |  
|      |||||
| SMP                          | 香港    | アムステルダム |ワシントン D.C.(米国東部) | サンパウロ |
|                              | ソウル | フランクフルト | ダラス (米国南部)         |               | 
|                              |シンガポール| ロンドン |モントリオール                |               | 
|                              |シドニー | ミラノ | ケレタロ                 |               | 
|                              | 東京 | オスロ | トロント |               | 
|                              |              | パリ |                           |               |
|      |||||
| MPP                          | 香港    | アムステルダム |ワシントン D.C.(米国東部) | サンパウロ |
|                              | ソウル | フランクフルト | ダラス (米国南部)         |               | 
|                              |シンガポール| ロンドン |モントリオール                |               | 
|                              |シドニー | ミラノ | ケレタロ                 |               | 
|                              | 東京 | オスロ | トロント |               | 
|                              |              | パリ |                           |               |
{: caption="表 1. Db2 Warehouse on Cloud サービス・プランをサポートしているデータ・センター" caption-side="top"}

*NA = 現在、利用不可



