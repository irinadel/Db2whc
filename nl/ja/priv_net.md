---

copyright:
  years: 2014, 2019
lastupdated: "2019-02-26"

keywords: private network, public IP, VPN, IBM Cloud Service Endpoint, IBM Cloud Direct Link, Flex

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

# プライベート・ネットワーク環境
{: #priv_net_env}

## デプロイ
{: #deploy}

{{site.data.keyword.dashdbshort_notm}} サービスを、{{site.data.keyword.Bluemix}} のネットワーク分離環境にデプロイするように要求することができます。 [{{site.data.keyword.IBM_notm}} Analytics 営業担当員 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/connect/ibm/us/en/?lnk=fcw){:new_window} にお問い合わせください。
{: shortdesc}

## 接続
{: #connecting}

以下は、{{site.data.keyword.dashdbshort_notm}} Flex プランのプライベート・ネットワーク環境に接続できる方式のリストです。

* [パブリック IP](#pub_ip)
* [{{site.data.keyword.cloud_notm}} サービス・エンドポイント](#serv_endpt)
* [{{site.data.keyword.cloud_notm}} Direct Link](#dl)
* [VPN](#vpn)
<!-- * [IP Whitelisting](#ip_wl) -->

### パブリック IP 
{: #pub_ip}

Flex プランのデフォルト・デプロイメントは、パブリック IP アドレスを持つ `Public Mode` にあります。パブリック IP アドレスは、世界中のどこからでもパブリック・ネットワーク環境にアクセスできることを意味します。ただし、パブリック・ネットワーク環境との通信に必要なポートのみが、ファイアウォールで開かれます。他のすべてのトラフィックはブロックされます。

{{site.data.keyword.cloud_notm}} にログインすると、サービス・インスタンスが表示されます。サービス・インスタンスをクリックして資格情報を追加すると、{{site.data.keyword.dashdbshort_notm}} パブリック・インスタンスにアクセスするために必要なアクセスの詳細が表示されます。

### IBM Cloud サービス・エンドポイント
{: #serv_endpt}

すべてのトラフィックを IaaS 環境から SoftLayer プライベート・バックプレーンに送信する必要がある場合、「**{{site.data.keyword.cloud_notm}} サービス・エンドポイント**」と呼ばれるオファリングがこの機能を提供します。{{site.data.keyword.cloud_notm}} サービス・エンドポイント・オプションについて詳しくは、[サービス・エンドポイント: 概要](/docs/services/service-endpoint/getting-started.html)を参照してください。

{{site.data.keyword.cloud_notm}} サービス・エンドポイントを使用するには、**プライベート接続**で Flex プラン・サービスをプロビジョンする必要があります。現時点では、このオプションは、ソフトウェア見積り注文 (SQO) を介した要求によってのみ取得されます。 

Flex プランがこのモードでプロビジョンされている場合、パブリック接続はまったくありません。
{: note} 

Flex 環境が**プライベート接続**でプロビジョンされた後、次の操作を実行して、IaaS 環境から Flex プライベート・ネットワーク環境への接続を有効にする必要があります。 

1. 最初に、[サービス・エンドポイント: はじめに](/docs/services/service-endpoint/enable-servicepoint.html)を参照してください。

2. [{{site.data.keyword.cloud_notm}} Direct Link](#dl)または[VPN](#vpn) のどちらかを使用して、IaaS 環境への接続をセットアップします。

### IBM Cloud Direct Link
{: #dl}

{{site.data.keyword.cloud_notm}} Direct Link を使用して、Flex プライベート・ネットワーク環境を IaaS 環境に接続できます。[{{site.data.keyword.cloud_notm}} Direct Link の開始](/docs/infrastructure/direct-link/getting-started.html)を参照してください。

### VPN
{: #vpn}

Flex プライベート・ネットワーク環境を IaaS 環境に接続するには、`50001` のセキュア SSL ポートを超える接続方式が必要である場合は、パブリック接続用の仮想プライベート・ネットワーク (VPN) トンネルを使用します。

プライベート・ネットワーク環境への VPN 接続を確立するには、VPN フォーム (IBM サポートからの要求フォーム) に入力し、フォームを [ServiceNow ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://cloud.ibm.com/unifiedsupport/cases/add){:new_window} チケットに添付して、VPN 情報を IBM Cloud ネットワーキング・チームに送信する必要があります。<!-- , attaching the form to a [ServiceNow ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/unifiedsupport/cases/add){:new_window} ticket, and providing the following VPN part number `xxxx-xxxx-xxxx`. --> その情報が手元にあれば、{{site.data.keyword.cloud_notm}} ネットワーキング・チームは、VPN エンドポイントの終りをセットアップできます。<!-- Ben to provide VPN part number -->

VPN の概要については、[仮想プライベート・ネットワーキング (VPN) 入門](/docs/infrastructure/iaas-vpn/getting-started.html)を参照してください。

<!-- **Gopal's text**:

> For public connectivity, customers can setup a VPN tunnel if they need to use something over and beyond the secure SSL port of `50001` and send VPN information to our Networking team to set up VPN endpoints. This requires filling up a VPN form and attaching it to a Service Now Ticket. Should we attach the form template here? Customers need to order a particular part number for this (VPN part number to be provided by Ben)


Can we use any of this documentation?  [Getting started with Virtual Private Networking (VPN)](/docs/infrastructure/iaas-vpn/getting-started.html). -->



<!-- ### IP Whitelisting
{: #ip_wl}

IP whitelisting gives you the ability to specify which trusted IP addresses are granted access to your private network environment.


**Writer's notes**:
I need step-by-step instructions. -->


