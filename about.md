---

copyright:
  years: 2014, 2019
lastupdated: "2019-11-22"

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

# About
{: #about}

{{site.data.keyword.dashdblong}} is a fully-managed, elastic cloud data warehouse that delivers independent scaling of storage and compute. It delivers a highly optimized columnar data store, actionable compression, and in-memory processing to supercharge your analytics and machine learning workloads.
{: shortdesc}

## Key features
{: #key_features}

### Blazingly-fast engine

{{site.data.keyword.dashdbshort_notm}} is a column-organized, in-memory data warehouse designed for complex analytics and extreme concurrency. {{site.data.keyword.dashdbshort_notm}} delivers high performance on complex analytics workloads by using IBM BLU Acceleration, a collection of technologies pioneered by IBM Research that features the following key optimizations: 
- A columnar organized storage model 
- In-memory processing 
- Querying of compressed data sets
- Data skipping

### Scalable and elastic cloud service

{{site.data.keyword.dashdbshort_notm}} is an elastic service, and allows you to independently scale compute and storage through an intuitive UI or REST API.

### Expertly managed and highly secure

Day-to-day operations for {{site.data.keyword.dashdbshort_notm}}, including database monitoring, uptime checks and failovers, are fully automated. Operations are supplemented by a DevOps team that are on call to handle unexpected system failures. Data is encrypted at rest and in motion by default. Administrators can also restrict access to sensitive data through data masking, row permissions, and role-based security, and can utilize database audit utilities to maintain audit trails for their data warehouse.

### Highly resilient and reliable

{{site.data.keyword.dashdbshort_notm}} provides double protection for your data with built-in snapshot backups and geo-replicated disaster recovery backups.

### Compatible with on-premises data warehouses​

{{site.data.keyword.dashdbshort_notm}} can be configured with Oracle compatibility, so applications that were written for an Oracle database can run against {{site.data.keyword.dashdbshort_notm}} without having to be rewritten. {{site.data.keyword.dashdbshort_notm}} also comes with nearly 100% DDL, DML, and stored procedure compatibility with IBM Netezza®.

### Built-in machine learning and geospatial capabilities​

Train and run machine learning models directly in the {{site.data.keyword.dashdbshort_notm}} engine, using SQL, Python, or R. {{site.data.keyword.dashdbshort_notm}} also supports spatial analytics with Esri compatibility, including Esri data types such as GML, and integration with Jupyter Notebooks.

## Plans and configurations
{: #plans_cfgs}

{{site.data.keyword.dashdbshort_notm}} offers several elastic data warehouse configurations to meet your workload requirements:

- **Flex One**: a single-partitioned plan designed for growing enterprises and new data warehouse projects.
- **Flex**: a multi-partitioned plan designed for storage-dense workloads, inexpensive querying of large data sets, and development and test environments.
- **Flex Performance**: a multi-partitioned plan designed for high-performance, production workloads that prioritize compute performance over storage density.

All plans offer the [key features](#key_features) described in the previous section.

## Supported cloud providers and data centers
{: #sup_cp_dc}

{{site.data.keyword.dashdbshort_notm}} can be deployed on both {{site.data.keyword.cloud_notm}} and Amazon Web Services.

### Availability of plans in IBM Cloud data centers
{: #availability}

The following table provides information about the availability of the various {{site.data.keyword.dashdbshort_notm}} plans by {{site.data.keyword.cloud_notm}} data centers that are located in geographical regions:

| {{site.data.keyword.dashdbshort_notm}} plans | Asia/Pacific | Europe    | North/Central America     | South America |
|------------------------------|--------------|-----------|---------------------------|---------------|
| Flex                         | Tokyo        | Frankfurt | Washington D.C. (us-east) | *NA           |
|                              |              |           | Dallas (us-south)         |               |  
|      |||||
| Flex Performance             | Tokyo        | Frankfurt | Washington D.C. (us-east) | *NA           |
|                              |              |           | Dallas (us-south)         |               |  
|      |||||
| Flex One                     | Tokyo        | Frankfurt | Washington D.C. (us-east) | *NA           |
|                              |              | London    | Dallas (us-south)         |               | 
{: caption="Table 1. IBM Cloud data centers supporting Db2 Warehouse on Cloud service plans" caption-side="top"}

*NA = Not available at this time

You can request to deploy your {{site.data.keyword.dashdbshort_notm}} service in a network-isolated environment on the {{site.data.keyword.cloud_notm}}. Contact [IBM Sales](https://www.ibm.com/contact/us/en/){:external} to learn more.

### Availability of plans in Amazon Web Services data centers
{: #availability_aws}

The following table provides information about the availability of the various {{site.data.keyword.dashdbshort_notm}} plans by Amazon Web Services data centers that are located in geographical regions:

| {{site.data.keyword.dashdbshort_notm}} plans | Asia/Pacific | Europe    | North/Central America     | South America |
|------------------------------|--------------|-----------|---------------------------|---------------|
| Flex                         | Seoul        | Frankfurt | N. Virginia | *NA           |
|                              | Singapore    | London    |             |               |
|                              | Sydney       |           |             |               |
|                              | Tokyo        |           |             |               |  
|      |||||
| Flex Performance             | Seoul        | Frankfurt | N. Virginia | *NA           |
|                              | Singapore    | London    |             |               | 
|                              | Sydney       |           |             |               |
|                              | Tokyo        |           |             |               |  
{: caption="Table 2. Amazon Web Services data centers supporting Db2 Warehouse on Cloud service plans" caption-side="top"}

*NA = Not available at this time




<!--

{{site.data.keyword.dashdblong}} is a fully managed, high performance, petabyte-scale cloud data warehouse.

It delivers true elasticity with independent scaling of storage and compute, a highly optimized columnar data store, actionable compression and in-memory processing, all working together to supercharge your analytics workloads.
{: shortdesc}

## Db2 Warehouse on Cloud managed service
{: #managed_service}

The fully managed service of {{site.data.keyword.dashdbshort_notm}} handles all of the software upgrades, operating system updates, and hardware maintenance. The service includes 24x7 health monitoring of the database and infrastructure. If there is a hardware or software failure, the service is automatically restarted.
{: shortdesc} -->

<!-- ## Provisioning of Db2 Warehouse on Cloud
{: #whse_provision}

The {{site.data.keyword.dashdbshort_notm}} database can be provisioned on {{site.data.keyword.BluSoftlayer_full}} and for AWS.
{: shortdesc}

If you want to have the data warehouse provisioned for AWS, select the **MPP Small for AWS** plan. -->

<!--
## Data visualization
{: #visualize}

You can analyze and visualize your analysis by connecting to the following applications:

- [Watson Studio (formerly Data Science Experience)](/docs/Db2whc/connecting?topic=Db2whc-ds#watson_studio)
- [Cognos Analytics](/docs/Db2whc/connecting?topic=Db2whc-data_vis_bi#cognos)
- [Looker](https://docs.looker.com/setup-and-management/connecting-to-db){:external}
- [Tableau](/docs/Db2whc/connecting?topic=Db2whc-data_vis_bi#tableau)
- [SPSS Statistics](/docs/Db2whc/connecting?topic=Db2whc-ds#spss_stats)
- [SAS](/docs/Db2whc/connecting?topic=Db2whc-ds#sas)
- [Microsoft Excel](/docs/Db2whc/connecting?topic=Db2whc-data_vis_bi#excel)
- [Esri ArcGIS for Desktop](/docs/Db2whc/connecting?topic=Db2whc-data_vis_bi#esri_arcgis)

-->
