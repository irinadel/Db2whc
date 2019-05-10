---

copyright:
  years: 2014, 2019
lastupdated: "2019-03-15"

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

# 套餐和配置
{: #plans_cfgs}

您可以选择针对您需要执行的工作所配置和优化的 {{site.data.keyword.dashdbshort_notm}} 套餐：
{: shortdesc}

   * 用于试用的入门级套餐。最多可免费试用 1 GB 存储。请参阅：[入门级套餐限制](#ep_restrictions)
   * 可独立扩展存储和计算资源的 Flex 套餐
   * 用于生产的各种规模的 SMP 套餐：小中大，包括单个节点和单个实例
   * 针对并行处理和高性能的 MPP 多节点集群配置
   * 针对高可用性配置的套餐
   * Oracle 兼容性

在 [{{site.data.keyword.Bluemix}} 目录](https://cloud.ibm.com/catalog/services/db2-warehouse){:new_window}中查看所有可用的 {{site.data.keyword.dashdbshort_notm}} 套餐。
<!--   * Plans configured for data warehouse and online analytical processing (OLAP) workloads: [{{site.data.keyword.dashdbshort_notm}}](https://console.bluemix.net/catalog/services/db2-warehouse){:new_window} -->
<!--   * Plans configured for high-speed, transactional processing (OLTP): [{{site.data.keyword.dashdbshort_notm}} for Transactions](https://console.ng.bluemix.net/catalog/services/dashdb-for-transactions-sql-database){:new_window} -->

观看以下视频以了解 {{site.data.keyword.dashdbshort_notm}} Flex Performance 套餐简介。

<iframe class="embed-responsive-item" id="youtubeplayer" title="通过 Cognos Analytics 创建连接" type="text/html" width="640" height="390" src="//www.youtube.com/embed/59PKSnzNQAg?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

您可以请求在 {{site.data.keyword.Bluemix}} 上的网络隔离环境中部署 {{site.data.keyword.dashdbshort_notm}} 服务。请联系 [{{site.data.keyword.IBM_notm}} 销售人员 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/connect/ibm/us/en/?lnk=fcw){:new_window}。

如果您在目录中看不到所需的配置，请联系 [{{site.data.keyword.IBM_notm}} 销售人员 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/connect/ibm/us/en/?lnk=fcw){:new_window}，以讨论其他选择。

## 套餐在各数据中心的可用性
{: #availability}

下表按位于地理区域中的数据中心提供了有关各种 {{site.data.keyword.dashdbshort_notm}} 套餐的可用性的信息：

|{{site.data.keyword.dashdbshort_notm}} 套餐|亚太地区|欧洲|北美/中美洲|南美|
|------------------------------|--------------|-----------|---------------------------|---------------|
|Flex|东京|法兰克福|华盛顿 (us-east) | *不适用           |
|                              |              |           |达拉斯 (us-south)|               |  
|      |||||
|SMP|中国香港特别行政区|阿姆斯特丹|华盛顿 (us-east) |圣保罗|
|                              |首尔|法兰克福|达拉斯 (us-south)|               | 
|                              |新加坡|伦敦|蒙特利尔|               | 
|                              |悉尼|米兰|克雷塔罗|               | 
|                              |东京|奥斯陆|多伦多|               | 
|                              |              |巴黎|                           |               |
|      |||||
| MPP               |中国香港特别行政区|阿姆斯特丹|华盛顿 (us-east) |圣保罗|
|                              |首尔|法兰克福|达拉斯 (us-south)|               | 
|                              |新加坡|伦敦|蒙特利尔|               | 
|                              |悉尼|米兰|克雷塔罗|               | 
|                              |东京|奥斯陆|多伦多|               | 
|                              |              |巴黎|                           |               |
{: caption="表 1. 支持 Db2 Warehouse on Cloud 服务套餐的数据中心" caption-side="top"}

*不适用 = 目前不可用

## 入门级套餐限制
{: #ep_restrictions}

强烈建议您对任务关键型或性能敏感的工作负载使用企业级服务套餐，而不使用入门级服务套餐。
{: important}

以下是 {{site.data.keyword.dashdbshort_notm}} 入门级套餐限制的表格：

|类别|项|限制| 
|----------|------|-------------|
|资源|存储|每个用户 20 GB 存储。仅在使用的存储小于 1 GB 时，该套餐免费。|
|  |连接|每个用户 50 个连接。可以动态调整此限制，以保持实例的系统完整性。|
|  |性能|性能可能由于多租户系统上的其他用户运行的工作负载而波动|
|  |  |
|功能部件和功能|联合|不受支持|
|  |Oracle 兼容性|不受支持|
|  |用户定义的扩展 (UDF) |不受支持|
|  |用户管理|未向用户授予管理权限|
|  |行和列访问控制 (RCAC) |不受支持|
|  |用于装入数据的 IBM InfoSphere Data Replication|不受支持|
|  |  |
|联网环境| IBM Cloud Integrated Analytics |不受支持|
|  | IBM Cloud Dedicated |不受支持|
|  |  |
|安全性合规性|1996 年的《健康保险可移植性和责任法案》(HIPAA) |不受支持。请参阅“服务描述”。|
|  |欧盟一般数据保护条例 (GDPR) |没有特定限制适用。|
|  |  |
|帐户管理|重新激活|无重新激活需求|
{: caption="表 1. {{site.data.keyword.dashdbshort_notm}} 入门级套餐限制" caption-side="top"}
