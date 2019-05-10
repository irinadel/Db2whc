---

copyright:
  years: 2014, 2019
lastupdated: "2019-04-16"

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

<!-- If your data warehouse instance is deployed in a data center that suffers a significant data center outage with an expected downtime of more than 8 hours, you will be sent a request to allow service operators to fail over your instance to another data center before disaster recovery actions can begin.
{: shortdesc}

A Db2 backup of your database is done every day, except for the Flex plan where a Db2 backup is done every 7 days and a snapshot backup is done daily. Daily backups are stored in the IBM Cloud Object Storage service from which it is replicated to multiple availability zones. If something should happen to your primary data center, our service operators will work with you to stand up your recovered database in a secondary data center. -->

災害復旧方針は、プランのタイプおよび現在実行されているデータウェアハウスの世代によって異なります。
{: shortdesc}

第 1 世代の SMP のスモール・プラン、ミディアム・プラン、ラージ・プランおよび MPP スモール・プランの場合は、バックアップが 1 日に 1 回実行され、{{site.data.keyword.Bluemix_notm}} Object Storage サービスにデプロイされます。 バックアップはそこから複数のアベイラビリティー・ゾーンに複製されます。 1 次データ・センターで災害イベントが発生すると、サービス・オペレーターはお客様と協力して、別のデータ・センターで新しいデータウェアハウスを稼働させます。 {{site.data.keyword.Bluemix_notm}} Object Storage サービスにある日次バックアップが使用されます。

{{site.data.keyword.Bluemix_notm}} 上の第 2 世代の Flex プランの場合は、バックアップが 1 週間に 1 回実行され、{{site.data.keyword.Bluemix_notm}} Object Storage サービスにデプロイされます。 バックアップはそこから複数のアベイラビリティー・ゾーンに複製されます。 1 次データ・センターで災害イベントが発生すると、サービス・オペレーターはお客様と協力して、別のデータ・センターで新しいデータウェアハウスを稼働させます。 {{site.data.keyword.Bluemix_notm}} Object Storage サービスにある週次バックアップが使用されます。

Amazon Web Services 上の第 2 世代の Flex プランの場合は、日次セルフサービス・バックアップが AWS S3 に自動的にオフロードされます。 S3 内にあるとき、バックアップは複数の地域に複製されます。 災害イベントが発生すると、最新のバックアップが使用されて、2 次データ・センターにクラスターがリストアされます。

## **ブラジル: 補足ルール 14** (ブラジル連邦政府を対象としてプロビジョンされたシステムに適用)
{: #rule_14}

現時点では、補足ルール 14 により、ブラジル連邦政府用に {{site.data.keyword.dashdbshort_notm}} オファリングの災害復旧 (DR) オプションを使用することはできません。

