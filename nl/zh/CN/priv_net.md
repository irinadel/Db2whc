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

# 专用网络环境
{: #priv_net_env}

## 部署
{: #deploy}

您可以请求在 {{site.data.keyword.Bluemix}} 上的网络隔离环境中部署 {{site.data.keyword.dashdbshort_notm}} 服务。请联系 [{{site.data.keyword.IBM_notm}} Analytics 销售代表 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/connect/ibm/us/en/?lnk=fcw){:new_window}。
{: shortdesc}

## 连接

{: #connecting}

以下是您可以用于连接到 {{site.data.keyword.dashdbshort_notm}} Flex 套餐专用网络环境的方法列表：

* [公用 IP](#pub_ip)
* [{{site.data.keyword.cloud_notm}} Service Endpoint](#serv_endpt)
* [{{site.data.keyword.cloud_notm}} Direct Link](#dl)
* [VPN](#vpn)
<!-- * [IP Whitelisting](#ip_wl) -->

### 公用 IP 
{: #pub_ip}

Flex 套餐的缺省部署是`公用模式`，具有公用 IP 地址。公用 IP 地址意味着您可以从全球任意位置访问公用网络环境。但是，防火墙上仅开放了与公用网络环境通信所需的端口。将阻止所有其他流量。

登录到 {{site.data.keyword.cloud_notm}} 后，您将看到您的服务实例。单击该服务实例，添加您的凭证，您将获取访问 {{site.data.keyword.dashdbshort_notm}} 公用实例所需的访问权详细信息。

### IBM Cloud Service Endpoint
{: #serv_endpt}

如果要求所有流量都必须从 IaaS 环境沿着 SoftLayer 专用底板发送，名为 **{{site.data.keyword.cloud_notm}} Service Endpoint** 的产品可以提供此功能。有关 {{site.data.keyword.cloud_notm}} Service Endpoint 选项的更多信息，请参阅 [Service Endpoint：关于](/docs/services/service-endpoint/getting-started.html)。

Flex 套餐服务必须供应有**专用连接**才能使用 {{site.data.keyword.cloud_notm}} Service Endpoint。此时，仅可通过请求“软件报价单”(SQO) 才能获得此选项。 

当以此模式供应 Flex 套餐时，根本没有任何公用连接。
{: note} 

使用**专用连接**供应 Flex 环境后，必须执行以下操作才能启用从 IaaS 环境到 Flex 专用网络环境的连接： 

1. 要开始使用，请参阅 [Service Endpoint：入门](/docs/services/service-endpoint/enable-servicepoint.html)

2. 使用 [{{site.data.keyword.cloud_notm}} Direct Link](#dl) 或 [VPN](#vpn) 来设置与 IaaS 环境的连接。

### IBM Cloud Direct Link
{: #dl}

通过使用 {{site.data.keyword.cloud_notm}} Direct Link，可以将 Flex 专用网络环境连接到 IaaS 环境。请参阅[开始使用 {{site.data.keyword.cloud_notm}} Direct Link](/docs/infrastructure/direct-link/getting-started.html)。

### VPN
{: #vpn}

如果必须具有一个超过安全 SSL 端口 `50001` 的连接方法，那么通过对公用连接使用虚拟专用网络 (VPN) 隧道，可以将 Flex 专用网络环境连接到 IaaS 环境。

要建立与专用网络环境的 VPN 连接，必须通过填写 VPN 表单（IBM 支持的请求表单）并将该表单附加到 [ServiceNow ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://cloud.ibm.com/unifiedsupport/cases/add){:new_window} 凭单，以将您的 VPN 信息发送到 IBM Cloud 网络团队。<!-- , attaching the form to a [ServiceNow ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/unifiedsupport/cases/add){:new_window} ticket, and providing the following VPN part number `xxxx-xxxx-xxxx`. -->有了这些信息，我们的 {{site.data.keyword.cloud_notm}} 网络团队才可以设置 VPN 端点中的我们这一端。<!-- Ben to provide VPN part number -->

有关 VPN 入门的信息，请参阅[虚拟专用网络 (VPN) 入门](/docs/infrastructure/iaas-vpn/getting-started.html)。

<!-- **Gopal's text**:

> For public connectivity, customers can setup a VPN tunnel if they need to use something over and beyond the secure SSL port of `50001` and send VPN information to our Networking team to set up VPN endpoints. This requires filling up a VPN form and attaching it to a Service Now Ticket. Should we attach the form template here? Customers need to order a particular part number for this (VPN part number to be provided by Ben)


Can we use any of this documentation?  [Getting started with Virtual Private Networking (VPN)](/docs/infrastructure/iaas-vpn/getting-started.html). -->



<!-- ### IP Whitelisting
{: #ip_wl}

IP whitelisting gives you the ability to specify which trusted IP addresses are granted access to your private network environment.


**Writer's notes**:
I need step-by-step instructions. -->


