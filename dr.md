---

copyright:
  years: 2014, 2021
lastupdated: "2021-03-15"

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

# Disaster recovery
{: #dr}

Geo-replicated disaster recovery (DR) backups for {{site.data.keyword.dashdblong}} are enabled by default and supplement daily snapshot backups. DR backups are used exclusively for system recovery purposes by IBM service operators if there is a disaster or system loss. 
{: shortdesc}

If a disaster event occurs at the data center where your {{site.data.keyword.dashdbshort_notm}} instance is deployed, IBM service operators will work with you to stand up a new data warehouse in a different data center, by using the most recent disaster recovery backup. There is no additional charge for these backups.

The RPO and RTO for DR backups for each cloud provider are described in the following sections. DR backups are also geo-replicated by default. You can open a support ticket to not have your DR backups replicated to certain regions to comply with your data retention policies.

For more information about DR and replication on {{site.data.keyword.dashdbshort_notm}}, see [Replication](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.idrca.doc/overview/ovu-db2woc.html){: external}.

## IBM Cloud
{: #ibm_cloud_dr}

When deployed on {{site.data.keyword.Bluemix_notm}}, a full backup of the database is taken once a week for disaster recovery. This DR backup is encrypted and stored in {{site.data.keyword.Bluemix_notm}} Object Storage (COS).

IBM COS replicates each DR backup across multiple {{site.data.keyword.Bluemix_notm}} regions to ensure availability if a single zone fails.

DR backups of the last 2 weeks are retained by default. The RPO for DR backups on {{site.data.keyword.Bluemix_notm}} is 1 week. The RTO if a disaster occurs is dependent upon the size of the database – 1.5 hours per terabyte of data.

<!--For the first-generation SMP Small, Medium, Large, and MPP Small plans, a backup is taken once a day and deployed to the {{site.data.keyword.Bluemix_notm}} Object Storage service. From there, the backup is replicated to multiple availability zones. If a disaster event occurs at the primary data center, our service operators work with you to stand up a new data warehouse in a different data center. We will use the daily backup that resides in the {{site.data.keyword.Bluemix_notm}} Object Storage service. -->

## Amazon Web Services
{: #aws_dr}

When deployed on Amazon Web Services, a full backup of the database is taken once a week for disaster recovery. This DR backup is encrypted and stored in Amazon Web Services S3.

DR backups are also replicated to a secondary Amazon Web Services region by using Cross-Region replication. S3 keeps copies of each DR backup across 3 availability zones (AZs) in each region by default, so there are 6 copies of each DR backup in total.

DR backups of the last 2 weeks are retained by default. The RPO for DR backups on Amazon Web Services is 1 week. The RTO if a disaster occurs is dependent upon the size of the database – 1.5 hours per terabyte of data.

Secondary regions for each Amazon Web Services primary region are listed in the following table:

| Primary region | Secondary region |
|----------------|------------------|
| us-east-1      | us-west-2        |
| ap-southeast-1 | ap-southeast-2   |
| eu-central-1   | eu-west-2        |
{: caption="Table 1. Secondary regions for each Amazon Web Services primary region" caption-side="top"}

<!--For the second-generation Flex plans on {{site.data.keyword.Bluemix_notm}} and Amazon Web Services, a backup is taken once a week and deployed to the {{site.data.keyword.Bluemix_notm}} Object Storage service. From there, the backup is replicated to multiple availability zones. If a disaster event occurs at the primary data center, our service operators work with you to stand up a new data warehouse in a different data center. We will use the weekly backup that resides in the {{site.data.keyword.Bluemix_notm}} Object Storage service.-->

<!--## Second-generation Flex plans on Amazon Web Services
{: #flex_aws}

For the second-generation Flex plans on Amazon Web Services, a daily self-service backup is automatically offloaded to Amazon Web Services S3. When in S3, the backup is replicated to multiple regions. If a disaster event occurs, the most recent backup is used to restore your cluster to a secondary data center. -->

## **Brazil: Supplementary Rule 14** (applies to systems provisioned for the Brazilian federal government)
{: #rule_14}

At this time, the disaster recovery (DR) option for {{site.data.keyword.dashdbshort_notm}} offerings is not available in Brazil for the federal government due to Supplementary Rule 14.

