---

copyright:
  years: 2014, 2019
lastupdated: "2019-06-05"

keywords:

subcollection: Db2whc

---

<!-- Attribute definitions --> 
{:external: target="_blank" .external}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}

# Plans and configurations
{: #plans_cfgs}

You can choose a {{site.data.keyword.dashdbshort_notm}} plan that is configured and optimized for the work that you need to do:
{: shortdesc}

   * An entry plan to try things out. It's a free trial with up to 1 GB of storage. See: [Entry plan restrictions](#ep_restrictions)
   * Flex plans in which you can independently scale storage and compute resources
   * SMP plans of various sizes for production: small, medium, and large consist of a single node and a single instance
   * MPP multiple-node cluster configurations for parallel processing and high performance
   * Plans configured for High Availability
   * Oracle compatibility

View all of the available {{site.data.keyword.dashdbshort_notm}} plans in the [{{site.data.keyword.Bluemix}} catalog](https://cloud.ibm.com/catalog/services/db2-warehouse){:external}.
<!--   * Plans configured for data warehouse and online analytical processing (OLAP) workloads: [{{site.data.keyword.dashdbshort_notm}}](https://console.bluemix.net/catalog/services/db2-warehouse){:external} -->
<!--   * Plans configured for high-speed, transactional processing (OLTP): [{{site.data.keyword.dashdbshort_notm}} for Transactions](https://console.ng.bluemix.net/catalog/services/dashdb-for-transactions-sql-database){:external} -->

Watch this video to see an introduction to the {{site.data.keyword.dashdbshort_notm}} Flex Performance plan.

<iframe class="embed-responsive-item" id="youtubeplayer" title="Creating a connection from Cognos Analytics" type="text/html" width="640" height="390" src="//www.youtube.com/embed/59PKSnzNQAg?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

You can request to have your {{site.data.keyword.dashdbshort_notm}} service deployed in a network-isolated environment on the {{site.data.keyword.Bluemix}}. Contact [{{site.data.keyword.IBM_notm}} Sales](https://www.ibm.com/connect/ibm/us/en/?lnk=fcw){:external}.

If you don't see a configuration in the catalog that you need, contact [{{site.data.keyword.IBM_notm}} Sales](https://www.ibm.com/connect/ibm/us/en/?lnk=fcw){:external} to discuss other options.

## Availability of plans in IBM Cloud data centers
{: #availability}

The following table provides information about the availability of the various {{site.data.keyword.dashdbshort_notm}} plans by IBM Cloud data centers located in geographical regions:

| {{site.data.keyword.dashdbshort_notm}} plans | Asia/Pacific | Europe    | North/Central America     | South America |
|------------------------------|--------------|-----------|---------------------------|---------------|
| Flex / Flex Performance      | Tokyo        | Frankfurt | Washington D.C. (us-east) | *NA           |
|                              |              |           | Dallas (us-south)         |               |  
|      |||||
| Flex One                     | *NA          | *NA       | Dallas (us-south)         | *NA           |
|      |||||
| SMP                          | Hong Kong    | Amsterdam | Washington D.C. (us-east) | Sao Paulo     |
|                              | Seoul        | Frankfurt | Dallas (us-south)         |               | 
|                              | Singapore    | London    | Montréal                  |               | 
|                              | Sydney       | Milan     | Querétaro                 |               | 
|                              | Tokyo        | Oslo      | Toronto                   |               | 
|                              |              | Paris     |                           |               |
|      |||||
| MPP                          | Hong Kong    | Amsterdam | Washington D.C. (us-east) | Sao Paulo     |
|                              | Seoul        | Frankfurt | Dallas (us-south)         |               | 
|                              | Singapore    | London    | Montréal                  |               | 
|                              | Sydney       | Milan     | Querétaro                 |               | 
|                              | Tokyo        | Oslo      | Toronto                   |               | 
|                              |              | Paris     |                           |               |
{: caption="Table 1. IBM Cloud data centers supporting Db2 Warehouse on Cloud service plans" caption-side="top"}

*NA = Not available at this time

## Availability of plans in Amazon Web Services data centers
{: #availability_aws}

The following table provides information about the availability of the various {{site.data.keyword.dashdbshort_notm}} plans by Amazon Web Services data centers located in geographical regions:

| {{site.data.keyword.dashdbshort_notm}} plans | Asia/Pacific | Europe    | North/Central America     | South America |
|------------------------------|--------------|-----------|---------------------------|---------------|
| Flex                         | Sydney       | Frankfurt | N. Virginia | *NA           |
|                              | Singapore    | London    |             |               |  
|      |||||
| Flex Performance             | Sydney       | Frankfurt | N. Virginia | *NA           |
|                              | Singapore    | London    |             |               | 
{: caption="Table 2. Amazon Web Services data centers supporting Db2 Warehouse on Cloud service plans" caption-side="top"}

*NA = Not available at this time


## Entry plan restrictions
{: #ep_restrictions}

You are strongly recommended to use an enterprise-level service plan rather than an Entry service plan for mission-critical or performance-sensitive workloads. 
{: important}

The following is a table of {{site.data.keyword.dashdbshort_notm}} Entry plan restrictions:

| Category | Item | Restriction | 
|----------|------|-------------|
| Resources | Storage | 20 GB of storage per user. The plan is free only if less than 1 GB of storage is used. |
|  | Connections | 50 connections per user. This limit might be adjusted dynamically to maintain system integrity of the instance. |
|  | Performance | Performance might fluctuate due to workloads run by other users on the multi-tenant system |
|  |  |
| Features & functions | Federation | Not supported |
|  | Oracle compatibility | Not supported |
|  | User-defined extensions (UDFs) | Not supported |
|  | User management | User not given administrative authority |
|  | Row and column access control (RCAC) | Not supported |
|  | IBM InfoSphere Data Replication for use in loading data | Not supported |
|  |  |
| Networking environment | IBM Cloud Integrated Analytics | Not supported |
|  | IBM Cloud Dedicated | Not supported |
|  |  |
| Security compliances | Health Information Portability and Accountability Act of 1996 (HIPAA) | Not supported. Refer to your Service Description. |
|  | EU General Data Protection Regulation (GDPR) | No specific restrictions apply |
|  |  |
| Account management | Reactivation | No reactivation requirement |
{: caption="Table 3. {{site.data.keyword.dashdbshort_notm}} Entry plan restrictions" caption-side="top"}
