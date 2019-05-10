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

# 灾难恢复 (DR)
{: #dr}

<!-- If your data warehouse instance is deployed in a data center that suffers a significant data center outage with an expected downtime of more than 8 hours, you will be sent a request to allow service operators to fail over your instance to another data center before disaster recovery actions can begin.
{: shortdesc}

A Db2 backup of your database is done every day, except for the Flex plan where a Db2 backup is done every 7 days and a snapshot backup is done daily. Daily backups are stored in the IBM Cloud Object Storage service from which it is replicated to multiple availability zones. If something should happen to your primary data center, our service operators will work with you to stand up your recovered database in a secondary data center. -->

灾难恢复策略取决于您正在执行的计划类型和数据仓库代系。
{: shortdesc}

对于第一代 SMP 小型、中型、大型计划以及 MPP 小型计划，每日都会进行一次备份，并且会将其部署到 {{site.data.keyword.Bluemix_notm}} Object Storage 服务。从其中，备份将会复制到多个可用性区域。如果主数据中心发生灾难事件，那么我们的服务操作员将会与您一起在其他数据中心建立新的数据仓库。我们将会用到驻留在 {{site.data.keyword.Bluemix_notm}} Object Storage 服务的每日备份。

对于 {{site.data.keyword.Bluemix_notm}} 上的第二代 Flex 计划，将会一周进行一次备份，并且会将其部署到 {{site.data.keyword.Bluemix_notm}} Object Storage 服务。从其中，备份将会复制到多个可用性区域。如果主数据中心发生灾难事件，那么我们的服务操作员将会与您一起在其他数据中心建立新的数据仓库。我们将会用到驻留在 {{site.data.keyword.Bluemix_notm}} Object Storage 服务的每周备份。

对于 Amazon Web Services 上的第二代 Flex 计划，每日的自助服务备份将会自动卸载到 AWS S3。使用 S3 时，备份将会复制到多个区域。如果发生灾难事件，那么最新的备份将会用来将集群复原到第二个数据中心。

## **巴西：补充规则 14**（适用于为巴西联邦政府供应的系统）
{: #rule_14}

目前，根据补充规则 14，针对 {{site.data.keyword.dashdbshort_notm}} 产品的灾难恢复 (DR) 选项不再可供巴西的联邦政府使用。

