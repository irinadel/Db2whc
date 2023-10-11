---

copyright:
  years: 2014, 2021
lastupdated: "2023-07-04"

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

Disaster recovery (DR) backups for {{site.data.keyword.dashdblong}} are enabled by default.

If a disaster event occurs at the data center where your Db2 Warehouse on Cloud instance is deployed, IBM service operators will work with you to stand up a new data warehouse in a different data center, by using the most recent disaster recovery backup.

For more information about DR and replication on Db2 Warehouse on Cloud, see [Replication](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.idrca.doc/overview/ovu-db2woc.html).
{: shortdesc}

## IBM Cloud
{: #ibm_cloud_dr}

For instances deployed on IBM Cloud, disaster recovery (DR) backups supplement daily snapshot backups. They are used exclusively for system recovery purposes by IBM service operators if there is a disaster or system loss.

A full backup of the database is taken once a week for disaster recovery. This DR backup is encrypted and stored in {{site.data.keyword.Bluemix_notm}} Object Storage (COS). IBM COS replicates each DR backup across multiple {{site.data.keyword.Bluemix_notm}} regions to ensure availability if a single zone fails. You can open a support ticket to ask which regions your backups are being replicated to.

DR backups of the last 2 weeks are retained by default. The RPO for DR backups on {{site.data.keyword.Bluemix_notm}} is 1 week. The RTO if a disaster occurs is dependent upon the size of the database – 1.5 hours per terabyte of data. 

It is essential for disaster recovery backups to be taken regularly as part of this managed service. If you have concerns about the time window in which backups run and want to schedule the backup for a less busy time on your system, open a support case.{: important} 

<!--For the first-generation SMP Small, Medium, Large, and MPP Small plans, a backup is taken once a day and deployed to the {{site.data.keyword.Bluemix_notm}} Object Storage service. From there, the backup is replicated to multiple availability zones. If a disaster event occurs at the primary data center, our service operators work with you to stand up a new data warehouse in a different data center. We will use the daily backup that resides in the {{site.data.keyword.Bluemix_notm}} Object Storage service. -->

## Amazon Web Services
{: #aws_dr}

When deployed on Amazon Web Services, the daily snapshot backup described in https://cloud.ibm.com/docs/Db2whc?topic=Db2whc-br is also used for disaster recovery purposes. This DR backup is encrypted and stored in Amazon Web Services S3 across 3 availability zones (AZs) in each region. Regional DR backups allow you to restore your instance to another zone in the same region if needed. The RPO for DR backups on Amazon Web Services is 24 hours. The RTO if a disaster occurs is approximately 4 hours. 

<!--For the second-generation Flex plans on {{site.data.keyword.Bluemix_notm}} and Amazon Web Services, a backup is taken once a week and deployed to the {{site.data.keyword.Bluemix_notm}} Object Storage service. From there, the backup is replicated to multiple availability zones. If a disaster event occurs at the primary data center, our service operators work with you to stand up a new data warehouse in a different data center. We will use the weekly backup that resides in the {{site.data.keyword.Bluemix_notm}} Object Storage service.-->

<!--## Second-generation Flex plans on Amazon Web Services
{: #flex_aws}

For the second-generation Flex plans on Amazon Web Services, a daily self-service backup is automatically offloaded to Amazon Web Services S3. When in S3, the backup is replicated to multiple regions. If a disaster event occurs, the most recent backup is used to restore your cluster to a secondary data center. -->

## **Brazil: Supplementary Rule 14** (applies to systems provisioned for the Brazilian federal government)
{: #rule_14}

For the current generation of plans hosted on AWS, the disaster recovery (DR) option for {{site.data.keyword.dashdbshort_notm}} offerings is not available in Brazil for the federal government due to Supplementary Rule 14.

