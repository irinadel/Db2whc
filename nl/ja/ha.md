---

copyright:
  years: 2014, 2019
lastupdated: "2018-04-30"

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

# 高可用性 (HA) 
{: #ha}

データベース・ソリューションの成果を測る基準は、その可用性にあります。 {{site.data.keyword.dashdblong}} には、お客様のワークロードの継続性を維持するための高可用性プランがあります。
{: shortdesc}

## MPP プラン
{: #ha_mpp}

{{site.data.keyword.dashdbshort_notm}} MPP プラン・クラスターは、高可用性でプロビジョンされます。  

MPP プランのためにノードがダウンすると、HA コンポーネントは残りの正常なノードでデータベース・パーティションを再起動します。 このフェーズでは、短いダウン時間が発生します。 

ノードをクラスターに追加し直した後、フル・キャパシティーで実行するために、データベース・エンジンを再起動する必要があります。 

## Flex Performance プラン
{: #ha_flex}

予期しないノード障害が発生した場合、Flex Performance MPP クラスターは、IBM コンテナー・サービス (Kubernetes に基づく) の使用により、短いダウン時間の後、フル・キャパシティーに戻されます。 障害が発生したノード・エンティティーを移動するために、プールからのノードが使用されます。 

### コンピュート HA
{: #compute_ha}

ノード障害はコンテナー・サービスによってすぐに検出されます。 障害が発生したノードで実行されていたコンテナーとポッドは、ノードのプールからの新しいノードに、スケジュールされます。 システムは、短いダウン時間の後に 100 % の正常な動作に戻ります。

### ストレージ HA
{: #storage_ha}

ユーザーのストレージは、デュアル・パリティーの RAID6 実装で構成されており、同じ RAID グループ内の二重ディスク障害に対する保護を提供して、システムのハイパフォーマンスで可用性の高いストレージを実現します。

### ネットワーク HA
{: #net_ha}

ネットワーク接続は、冗長ネットワーク・インターフェース・カード (NIC) を使用してサービスをプロビジョンすることにより、高可用性を提供します。 

コンテナー・サービスがネットワークの問題を検出すると、短いダウン時間の後に、ポッドとコンテナーが自動的に再起動します。
