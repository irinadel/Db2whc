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

# 專用網路環境
{: #priv_net_env}

## 部署
{: #deploy}

您可以要求將 {{site.data.keyword.dashdbshort_notm}} 服務部署在網路隔離的 {{site.data.keyword.Bluemix}} 環境。請與 [{{site.data.keyword.IBM_notm}} Analytics 業務代表 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/connect/ibm/us/en/?lnk=fcw){:new_window} 聯絡。
{: shortdesc}

## 連接
{: #connecting}

以下是您可以用來連接至 {{site.data.keyword.dashdbshort_notm}} 彈性方案專用網路環境的方法清單：

* [公用 IP](#pub_ip)
* [{{site.data.keyword.cloud_notm}} Service Endpoint](#serv_endpt)
* [{{site.data.keyword.cloud_notm}} Direct Link](#dl)
* [VPN](#vpn)
<!-- * [IP Whitelisting](#ip_wl) -->

### 公用 IP 
{: #pub_ip}

彈性方案的預設部署是`公用模式`與公用 IP 位址。公用 IP 位址表示您的公用網路環境可以從世上任意處存取。不過，在我們的防火牆只會開啟與公用網路環境通訊所需的埠。所有其他資料流量會予以封鎖。

登入 {{site.data.keyword.cloud_notm}} 之後，您將會看到服務實例。請按一下服務實例、新增認證，然後便會看到存取 {{site.data.keyword.dashdbshort_notm}} 公用實例所需的存取詳細資料。

### IBM Cloud Service Endpoint
{: #serv_endpt}

如果您要求所有資料流量都必須透過 SoftLayer Private Backplane 從您的 IaaS 環境傳送，則稱為 **{{site.data.keyword.cloud_notm}} Service Endpoint** 的供應項目可提供此功能。如需 {{site.data.keyword.cloud_notm}} Service Endpoint 選項的相關資訊，請參閱[Service Endpoint：關於](/docs/services/service-endpoint/getting-started.html)。

彈性方案服務必須使用**專用連線功能**佈建，才能使用 {{site.data.keyword.cloud_notm}} Service Endpoint。目前，此選項只能透過軟體報價單 (SQO) 要求取得。 

當您的彈性方案以此模式佈建時，完全沒有公用連線功能。
{: note} 

彈性環境使用**專用連線功能**佈建之後，您必須執行下列動作才能啟用從 IaaS 環境到彈性專用網路環境的連線功能： 

1. 若要開始使用，請參閱 [Service Endpoint：開始使用](/docs/services/service-endpoint/enable-servicepoint.html)

2. 使用 [{{site.data.keyword.cloud_notm}} Direct Link](#dl) 或 [VPN](#vpn) 設定 IaaS 環境的連線功能。

### IBM Cloud Direct Link
{: #dl}

您可以使用 {{site.data.keyword.cloud_notm}} Direct Link 將彈性專用網路環境連接至 IaaS 環境。請參閱[開始使用 {{site.data.keyword.cloud_notm}} Direct Link](/docs/infrastructure/direct-link/getting-started.html)。

### VPN
{: #vpn}

如果您必須有使用安全 SSL 埠 `50001` 及更高埠號的連線方法，您可以使用虛擬專用網路 (VPN) 通道處理公用連線功能，將彈性專用網路環境連接至 IaaS 環境。

若要建立對專用網路環境的 VPN 連線，您必須傳送 VPN 資訊給我們的 IBM Cloud 網路團隊，方法是填寫 VPN 表單（請從 IBM 支援中心要求表單）並將表單附加到 [ServiceNow ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/unifiedsupport/cases/add){:new_window} 問題單。有了此資訊，我們的 {{site.data.keyword.cloud_notm}} 網路團隊便能設定我們這端的 VPN 端點。

如需開始使用 VPN 的相關資訊，請參閱[開始使用 Virtual Private Networking (VPN)](/docs/infrastructure/iaas-vpn/getting-started.html)。

<!-- **Gopal's text**:

> For public connectivity, customers can setup a VPN tunnel if they need to use something over and beyond the secure SSL port of `50001` and send VPN information to our Networking team to set up VPN endpoints. This requires filling up a VPN form and attaching it to a Service Now Ticket. Should we attach the form template here? Customers need to order a particular part number for this (VPN part number to be provided by Ben)


Can we use any of this documentation?  [Getting started with Virtual Private Networking (VPN)](/docs/infrastructure/iaas-vpn/getting-started.html). -->



<!-- ### IP Whitelisting
{: #ip_wl}

IP whitelisting gives you the ability to specify which trusted IP addresses are granted access to your private network environment.


**Writer's notes**:
I need step-by-step instructions. -->


