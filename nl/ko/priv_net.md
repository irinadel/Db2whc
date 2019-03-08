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

# 사설 네트워크 환경
{: #priv_net_env}

## 배치
{: #deploy}

{{site.data.keyword.dashdbshort_notm}} 서비스를 {{site.data.keyword.Bluemix}}의 네트워크 격리 환경에 배치하도록 요청할 수 있습니다. [{{site.data.keyword.IBM_notm}} Analytics 영업 담당자 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/connect/ibm/us/en/?lnk=fcw){:new_window}에게 문의하십시오.
{: shortdesc}

## 연결
{: #connecting}

다음은 {{site.data.keyword.dashdbshort_notm}} Flex 플랜 사설 네트워크 환경에 연결할 수 있는 방법의 목록입니다. 

* [공인 IP](#pub_ip)
* [{{site.data.keyword.cloud_notm}} Service Endpoint](#serv_endpt)
* [{{site.data.keyword.cloud_notm}} Direct Link](#dl)
* [VPN](#vpn)
<!-- * [IP Whitelisting](#ip_wl) -->

### 공인 IP 
{: #pub_ip}

Flex 플랜의 기본 배치는 공인 IP 주소와 함께 `Public Mode`에 있습니다. 공인 IP는 전세계 어디에서도 공용 네트워크 환경에 액세스할 수 있음을 의미합니다. 그러나 공용 네트워크 환경과의 통신에 필요한 포트만 방화벽에 열려 있습니다. 기타 모든 트래픽은 차단됩니다. 

{{site.data.keyword.cloud_notm}}에 로그인하면 서비스 인스턴스가 표시됩니다. 서비스 인스턴스를 클릭하고 인증 정보를 추가하면 {{site.data.keyword.dashdbshort_notm}} Public Instance에 액세스하는 데 필요한 액세스 세부사항이 제공됩니다. 

### IBM Cloud Service Endpoint
{: #serv_endpt}

모든 트래픽이 IaaS 환경의 SoftLayer Private Backplane과 함께 전송되어야 하는 경우 **{{site.data.keyword.cloud_notm}} Service Endpoint**라고 하는 오퍼링에서 이 기능을 제공합니다. {{site.data.keyword.cloud_notm}} Service Endpoint 옵션에 대한 자세한 정보는 [Service Endpoint: 정보](/docs/services/service-endpoint/getting-started.html)를 참조하십시오.

Flex 플랜 서비스는 {{site.data.keyword.cloud_notm}} Service Endpoint를 사용하도록 **Private Connectivity**로 프로비저닝되어야 합니다. 이때 SQO(Software Quote Order)를 통해 요청해야만 이 옵션이 제공됩니다.  

Flex 플랜이 이 모드에서 프로비저닝되는 경우 공용 연결은 없습니다.
{: note} 

Flex 환경이 **Private Connectivity**로 프로비저닝된 후 IaaS 환경과 사설 네트워크 환경 간의 연결을 사용으로 설정하려면 다음을 수행해야 합니다.  

1. 시작하려면 [Service Endpoint: 시작하기](/docs/services/service-endpoint/enable-servicepoint.html)를 참조하십시오. 

2. [{{site.data.keyword.cloud_notm}} Direct Link](#dl) 또는 [VPN](#vpn)을 사용하여 IaaS 환경에 연결을 설정하십시오.

### IBM Cloud Direct Link
{: #dl}

{{site.data.keyword.cloud_notm}} Direct Link를 사용하여 Flex 사설 네트워크 환경을 IaaS 환경에 연결할 수 있습니다. [{{site.data.keyword.cloud_notm}} Direct Link 시작하기](/docs/infrastructure/direct-link/getting-started.html)를 참조하십시오.

### VPN
{: #vpn}

`50001`의 보안 SSL 포트 이상의 연결 방법이 있는 경우 공용 연결을 위해 가상 사설망(VPN)을 사용하여 Flex 사설 네트워크 환경을 IaaS 환경에 연결할 수 있습니다. 

사설 네트워크 환경에 대한 VPN 연결을 설정하려면 VPN 양식(IBM Support의 요청 양식)을 작성하고 이 양식을 [ServiceNow ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://cloud.ibm.com/unifiedsupport/cases/add){:new_window} 티켓에 첨부하여 VPN 정보를 IBM Cloud 네트워킹 팀에 전송해야 합니다.<!-- , attaching the form to a [ServiceNow ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/unifiedsupport/cases/add){:new_window} ticket, and providing the following VPN part number `xxxx-xxxx-xxxx`. --> 그러면 해당 정보를 사용하여 {{site.data.keyword.cloud_notm}} 네트워킹 팀에서 VPN 엔드포인트의 IBM 측 종단을 설정할 수 있습니다. <!-- Ben to provide VPN part number -->

VPN 시작하기에 대한 자세한 정보는 [가상 사설망(VPN) 시작하기](/docs/infrastructure/iaas-vpn/getting-started.html)를 참조하십시오.

<!-- **Gopal's text**:

> For public connectivity, customers can setup a VPN tunnel if they need to use something over and beyond the secure SSL port of `50001` and send VPN information to our Networking team to set up VPN endpoints. This requires filling up a VPN form and attaching it to a Service Now Ticket. Should we attach the form template here? Customers need to order a particular part number for this (VPN part number to be provided by Ben)


Can we use any of this documentation?  [Getting started with Virtual Private Networking (VPN)](/docs/infrastructure/iaas-vpn/getting-started.html). -->



<!-- ### IP Whitelisting
{: #ip_wl}

IP whitelisting gives you the ability to specify which trusted IP addresses are granted access to your private network environment.


**Writer's notes**:
I need step-by-step instructions. -->


