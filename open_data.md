---

copyright:
  years: 2014, 2023
lastupdated: "2023-09-08"

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

# Open data format table support

The current generation of {{site.data.keyword.dashdblong}} plans on AWS supports open data formats as DATALAKE tables, allowing for seamless access to other data within your enterprise for integrated workloads.
You can:

- Browse, explore, and query enterprise data in both Db2 and DATALAKE formats, using either the web-based UI, or through SQL
- Access data in place within DATALAKE tables, joining as necessary with Db2 based data for queries
- Access data within DATALAKE tables and import into Db2 formatted tables
- Create new DATALAKE tables in S3 and export from Db2 formatted tables

Supported open table and data formats include Iceberg, Parquet, ORC, and CSV. Both regular and Iceberg DATALAKE table types are supported, based on existing data formats or for business/technical requirements such as ACID compliance.  For more information about open data format support in Db2 Warehouse on Cloud, see [Using DATALAKE tables](https://www.ibm.com/docs/en/db2woc?topic=using-datalake-tables){: external}



{{site.data.keyword.dashdblong}} also provides seamless integration and common metadata service with the new IBM watsonx.data service. You can use the web-based UI to register your watsonx.data service, to allow the import and export of data between the services.  For more information about integration with watsonx.data, see [watsonx.data Integration](https://www.ibm.com/docs/en/db2woc?topic=tables-accessing-watsonxdata){: external}

