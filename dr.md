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

# Disaster recovery (DR)
{: #dr}

<!-- If your data warehouse instance is deployed in a data center that suffers a significant data center outage with an expected downtime of more than 8 hours, you will be sent a request to allow service operators to fail over your instance to another data center before disaster recovery actions can begin.
{: shortdesc}

A Db2 backup of your database is done every day, except for the Flex plan where a Db2 backup is done every 7 days and a snapshot backup is done daily. Daily backups are stored in the IBM Cloud Object Storage service from which it is replicated to multiple availability zones. If something should happen to your primary data center, our service operators will work with you to stand up your recovered database in a secondary data center. -->

The disaster recovery strategy depends on the type of plan and data warehouse generation you’re running today.
{: shortdesc}

For the first generation SMP Small, Medium, Large and MPP Small plans, a backup is taken once a day and deployed to the {{site.data.keyword.Bluemix_notm}} Object Storage service. From there, the backup is replicated to multiple availability zones. If a disaster event occurs at the primary data center, our service operators will work with you to stand up a new data warehouse in a different data center. We will use the daily backup residing in the {{site.data.keyword.Bluemix_notm}} Object Storage service.

For the second generation Flex plans on {{site.data.keyword.Bluemix_notm}}, a backup is taken once a week and deployed to the {{site.data.keyword.Bluemix_notm}} Object Storage service. From there, the backup is replicated to multiple availability zones. If a disaster event occurs at the primary data center, our service operators will work with you to stand up a new data warehouse in a different data center. We will use the weekly backup residing in the {{site.data.keyword.Bluemix_notm}} Object Storage service.

For the second generation Flex plans on Amazon Web Services, a daily self-service backup is automatically offloaded to AWS S3. When in S3, the backup is replicated to multiple regions. If a disaster event occurs, the most recent backup will be used to restore your cluster to a secondary data center.

## **Brazil: Supplementary Rule 14** (applies to systems provisioned for the Brazilian federal government)
{: #rule_14}

At this time, the disaster recovery (DR) option for {{site.data.keyword.dashdbshort_notm}} offerings is not available in Brazil for the federal government due to Supplementary Rule 14.

