---

copyright:
  years: 2014, 2018
lastupdated: "2018-03-16"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 高可用性 (HA): MPP プラン
{: #ha_smp_mpp}

{{site.data.keyword.dashdblong}} MPP プラン・クラスターは、高可用性でプロビジョンされます。  
{: shortdesc}

MPP プランのためにノードがダウンすると、HA コンポーネントは残りの正常なノードでデータベース・パーティションを再起動します。 このフェーズでは、短いダウン時間が発生します。 

ノードをクラスターに追加し直した後、フル・キャパシティーで実行するために、データベース・エンジンを再起動する必要があります。 

