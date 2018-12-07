---

copyright:
  years: 2014, 2018
lastupdated: "2018-12-07"

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

View all of the available {{site.data.keyword.dashdbshort_notm}} plans in the [{{site.data.keyword.Bluemix}} catalog](https://console.bluemix.net/catalog/services/db2-warehouse){:new_window}.
<!--   * Plans configured for data warehouse and online analytical processing (OLAP) workloads: [{{site.data.keyword.dashdbshort_notm}}](https://console.bluemix.net/catalog/services/db2-warehouse){:new_window} -->
<!--   * Plans configured for high-speed, transactional processing (OLTP): [{{site.data.keyword.dashdbshort_notm}} for Transactions](https://console.ng.bluemix.net/catalog/services/dashdb-for-transactions-sql-database){:new_window} -->

Watch this video to see an introduction to the {{site.data.keyword.dashdbshort_notm}} Flex Performance plan.

<iframe class="embed-responsive-item" id="youtubeplayer" title="Creating a connection from Cognos Analytics" type="text/html" width="640" height="390" src="//www.youtube.com/embed/59PKSnzNQAg?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

You can request to have your {{site.data.keyword.dashdbshort_notm}} service deployed in a network-isolated environment on the {{site.data.keyword.Bluemix}}. Contact [{{site.data.keyword.IBM_notm}} Sales ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/connect/ibm/us/en/?lnk=fcw){:new_window}.

If you don't see a configuration in the catalog that you need, contact [{{site.data.keyword.IBM_notm}} Sales ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/connect/ibm/us/en/?lnk=fcw){:new_window} to discuss other options.

## Availability of plans in data centers
{: #availability}

The following tables provide information about the availability of the various {{site.data.keyword.dashdbshort_notm}} plans by data centers located in geographical regions:

<!-- ### Asia/Pacific
{: #ap}

| Db2 Warehouse on Cloud plans | Data center availability |
|------------------------------|------------------------|
| Flex | *NA |
|      ||
| SMP  | Hong Kong |
|      | Seoul |
|      | Singapore |
|      | Sydney |
|      | Tokyo |
|      ||
| MPP  | Hong Kong |
|      | Seoul |
|      | Singapore |
|      | Sydney |
|      | Tokyo |
{: caption="Table 1. Asia/Pacific data centers supporting Db2 Warehouse on Cloud service plans" caption-side="top"}

### Europe
{: #eu}

| Db2 Warehouse on Cloud plans | Data center availability |
|------------------------------|------------------------|
| Flex | Frankfurt |
|      ||
| SMP  | Amsterdam |
|      | Frankfurt |
|      | London |
|      | Milan |
|      | Oslo |
|      | Paris |
|      ||
| MPP  | Amsterdam |
|      | Frankfurt |
|      | London |
|      | Milan |
|      | Oslo |
|      | Paris |
{: caption="Table 2. Europe data centers supporting Db2 Warehouse on Cloud service plans" caption-side="top"}

### North/Central America
{: #nca}

| Db2 Warehouse on Cloud plans | Data center availability |
|------------------------------|------------------------|
| Flex | Washington D.C. (us-east) |
|      | Dallas (us-south) |
|      ||
| SMP  | Washington D.C. (us-east) |
|      | Dallas (us-south) |
|      | Montréal |
|      | Querétaro |
|      | Toronto |
|      ||
| MPP  | Washington D.C. (us-east) |
|      | Dallas (us-south) |
|      | Montréal |
|      | Querétaro |
|      | Toronto |
{: caption="Table 3. North and Central America data centers supporting Db2 Warehouse on Cloud service plans" caption-side="top"}

### South America
{: #sa}

| Db2 Warehouse on Cloud plans | Data center availability |
|------------------------------|------------------------|
| Flex | *NA |
|      ||
| SMP  | Sao Paulo |
|      ||
| MPP  | Sao Paulo |
{: caption="Table 4. South America data centers supporting Db2 Warehouse on Cloud service plans" caption-side="top"}
-->

| {{site.data.keyword.dashdbshort_notm}} plans | Asia/Pacific | Europe    | North/Central America     | South America |
|------------------------------|--------------|-----------|-----------------------    |---------------|
| Flex                         | *NA          | Frankfurt | Washington D.C. (us-east) | *NA           |
|                              |              |           | Dallas (us-south)         |               |  
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
{: caption="Table 1. Data centers supporting Db2 Warehouse on Cloud service plans" caption-side="top"}

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
{: caption="Table 1. {{site.data.keyword.dashdbshort_notm}} Entry plan restrictions" caption-side="top"}
