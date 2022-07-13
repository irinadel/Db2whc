---

copyright:
  years: 2014, 2019
lastupdated: "2022-04-08"

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

# Loading data from on-premises systems with IBM Lift CLI
{: #onprem}

[IBM Lift CLI](https://www.lift-cli.cloud.ibm.com){: external} is a free ground-to-cloud data migration tool that securely moves your data from on-premises systems to {{site.data.keyword.dashdblong}} plans hosted on IBM Cloud. Beginning in April 2022, IBM Lift CLI is not available on the Flex One plan on IBM Cloud, or on AWS plans. It is also not available on newly deployed Flex and Flex Performance instances on IBM Cloud.
{: shortdesc}

The Lift application migrates your data to the {{site.data.keyword.Bluemix_notm}} from the various data sources listed in Table 1. 

| Target database on {{site.data.keyword.Bluemix_notm}} | Data source |
|------------------------------|-------------|
| IBM Db2 Warehouse on Cloud (Flex and Flex Performance plans)    | IBM Db2 |
|                              | IBM Db2 Warehouse |
|                              | IBM Integrated Analytics System |
|                              | IBM PureData System for Analytics |
|                              | Oracle Database |
|                              | Microsoft SQL Server |
|                              | CSV file format |
{: caption="Table 1. Migration data sources" caption-side="top"}

To download and install Lift, see: [Download Lift](https://www.lift-cli.cloud.ibm.com/#download){:external}.

For step-by-step instructions about migrating your data to the {{site.data.keyword.Bluemix_notm}} by using Lift, see: [Migrate data to {{site.data.keyword.dashdblong}}](https://www.lift-cli.cloud.ibm.com/#docs){:external}.

For data volumes greater than 25 TB, we recommend using the [IBM Cloud Mass Data Migration Service](https://cloud.ibm.com/docs/mass-data-migration?topic=mass-data-migration-getting-started-tutorial){:external}.


