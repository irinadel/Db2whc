---

copyright:
  years: 2014, 2019
lastupdated: "2019-04-16"

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

# 災難回復 (DR)
{: #dr}

<!-- If your data warehouse instance is deployed in a data center that suffers a significant data center outage with an expected downtime of more than 8 hours, you will be sent a request to allow service operators to fail over your instance to another data center before disaster recovery actions can begin.
{: shortdesc}

A Db2 backup of your database is done every day, except for the Flex plan where a Db2 backup is done every 7 days and a snapshot backup is done daily. Daily backups are stored in the IBM Cloud Object Storage service from which it is replicated to multiple availability zones. If something should happen to your primary data center, our service operators will work with you to stand up your recovered database in a secondary data center. -->

災難回復策略取決於方案類型，以及您今日執行的資料倉儲產生作業。
{: shortdesc}

## 第一代 SMP 小型、中型、大型及 MPP 小型方案
{: #sml_mpp}

若為第一代 SMP「小型」、「中型」、「大型」及 MPP「小型」方案，每天會備份一次，並將備份部署至 {{site.data.keyword.Bluemix_notm}} Object Storage 服務。從這裡，備份會抄寫至多個可用性區域。如果主要資料中心發生災難事件，我們的服務操作員將與您合作，在不同的資料中心提供新的資料倉儲。我們將使用位於 {{site.data.keyword.Bluemix_notm}} Object Storage 服務的每日備份。

## IBM Cloud 上的第二代彈性方案
{: #flex_ibm_cloud}

若為 {{site.data.keyword.Bluemix_notm}} 上的第二代「彈性」方案，每週會備份一次，並將備份部署至 {{site.data.keyword.Bluemix_notm}} Object Storage 服務。從這裡，備份會抄寫至多個可用性區域。如果主要資料中心發生災難事件，我們的服務操作員將與您合作，在不同的資料中心提供新的資料倉儲。我們將使用位於 {{site.data.keyword.Bluemix_notm}} Object Storage 服務的每週備份。

## Amazon Web Services 上的第二代彈性方案
{: #flex_aws}

若為 Amazon Web Services 上的第二代「彈性」方案，每日自助式備份會自動卸載至 Amazon Web Services S3。在 S3 時，備份會抄寫至多個地區。如果發生災難事件，則會使用最新備份，將您的叢集還原至次要資料中心。

## **巴西：增補規則 14**（適用於針對巴西聯邦政府所佈建的系統）
{: #rule_14}

目前，由於「增補規則 14」，無法在巴西為聯邦政府提供 {{site.data.keyword.dashdbshort_notm}} 供應項目的災難回復 (DR) 選項。

