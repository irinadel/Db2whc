---

copyright:
  years: 2014, 2019
lastupdated: "2018-11-21"

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

# 災害復旧 (DR)
{: #dr}

予想ダウン時間が 8 時間を超える大規模な障害が発生しているデータ・センターにお客様のデータウェアハウス・インスタンスがデプロイされている場合、災害復旧アクションを開始する前に、サービス・オペレーターがお客様のインスタンスを別のデータ・センターにフェイルオーバーすることの許可を求める通知がお客様に送信されます。
{: shortdesc}

DB2 バックアップが 7 日ごとに実行され、スナップショット・バックアップが毎日実行される Flex プランを除き、データベースの DB2 バックアップは毎日行われます。 毎日のバックアップは、IBM Cloud Object Storage サービスに保管され、そこから複数のアベイラビリティー・ゾーンに複製されます。 1 次データ・センターで問題が発生すると、サービス・オペレーターはお客様と協力して、2 次データ・センターにリカバリーされたデータベースを立ち上げます。

## **ブラジル: 補足ルール 14** (ブラジル連邦政府を対象としてプロビジョンされたシステムに適用)
{: #rule_14}

現在、補足規則 14 により、Db2 Warehouse on Cloud オファリングに対する災害復旧 (DR) オプションは、ブラジルにおいて連邦政府は利用できません。

