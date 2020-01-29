---

copyright:
  years: 2014, 2019
lastupdated: "2019-05-08"

keywords: Db2 Warehouse on Cloud, loading data, object store, IBM Cloud Object Storage, Amazon S3, LOAD command, Mass Data Migration Service (MDMS), migration, Lift

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

# Loading data to {{site.data.keyword.dashdbshort_notm}}
{: #loading_data}

You can load data from a data file in a delimited format (CSV or TXT) on a local network or in an object store (Amazon S3 or {{site.data.keyword.Bluemix_notm}} Object Storage) to {{site.data.keyword.dashdblong}}. You can even migrate your data from an on-premises system.
{: shortdesc}

## Loading data from an object store
{: #cos}

To load data from Amazon S3 or {{site.data.keyword.Bluemix_notm}} Object Storage to {{site.data.keyword.dashdblong}}, select one of the following methods:
* {{site.data.keyword.dashdbshort_notm}} web console. **Load > Amazon S3**. 
* External Tables directly. The following is an example SQL statement:

    ```
    INSERT INTO <table-name> SELECT * FROM EXTERNAL '<mys3file.txt>' USING
      (CCSID 1208 s3('s3.amazonaws.com', 
      '<S3-access-key-ID>',
      '<S3-secret-access-key>', 
      '<my_bucket>'
         )
      )      
    ```
    {: codeblock}

  To load data from {{site.data.keyword.Bluemix_notm}} Object Storage by using External Tables directly, the following is an example SQL statement:

  ```
  INSERT INTO <table-name> SELECT * FROM EXTERNAL '<mys3file.txt>' USING
    (CCSID 1208 s3('s3-api.us-geo.objectstorage.softlayer.net', 
    '<S3-access-key-ID>',
    '<S3-secret-access-key>', 
    '<my_bucket>'
       )
    )      
  ```
  {: codeblock}

  For {{site.data.keyword.Bluemix_notm}} Object Storage, to create HMAC credentials when creating new service credentials, specify {"HMAC:true"} in the *Add Inline Configuration Parameters* field.
  {: note}

* For improved performance, the Db2 **LOAD** command can also be used to load data from Amazon S3 by using the following example command:

  ```
  CALL SYSPROC.ADMIN_CMD('LOAD FROM "S3::<amazon-s3-URL>::<s3-access-key-id>::<s3-secret-access-key>:
  :<s3-bucket-name>::<path-to-data-file>" OF <filetype> <additional-load-options> INTO <table-name>)
  ```
  {: codeblock}

  The following is an example usage of the Db2 **LOAD** command:

  ```
  CALL SYSPROC.ADMIN_CMD('load from "S3::s3-us-west-2.amazonaws.com::<s3-access-key-id>:
  :<s3-secret-access-key>::ibm-state-store::bdidata2TB/web_site.dat" of DEL modified by codepage=1208 
  coldel0x7c WARNINGCOUNT 1000 MESSAGES ON SERVER INSERT into BDINSIGHTS2.web_site ');
  ```
  {: codeblock}

  For supported command options. see [**LOAD** command](https://www.ibm.com/support/knowledgecenter/en/SSEPGG_11.1.0/com.ibm.db2.luw.admin.cmd.doc/doc/r0008305.html){:external}. 

For a guided demonstration about loading data from {{site.data.keyword.Bluemix_notm}} Object Storage, see: [{{site.data.keyword.dashdblong}} guided demo: Explore data loading](https://www.ibm.com/cloud/garage/demo/try-db2-warehouse-cloud){:external}

## Migrating data from on-premises system
{: #onprem}

To migrate your data from an on-premises system, choose one of the following methods depending on the size of your data set:
* Less than 25 TB of data: [IBM Lift](#lift)
* 25 TB of data and greater: [{{site.data.keyword.Bluemix_notm}} Mass Data Migration Service](#mdms)

### Lift
{: #lift}

The Lift is an application that you can use without charge to migrate your data to the {{site.data.keyword.Bluemix_notm}} from the various data sources listed in Table 1. 

| Target database on {{site.data.keyword.Bluemix_notm}} | Data source |
|------------------------------|-------------|
| IBM Db2 Warehouse on Cloud   | IBM Db2 |
|                              | IBM Db2 Warehouse |
|                              | IBM Integrated Analytics System |
|                              | IBM PureData System for Analytics |
|                              | Oracle Database |
|                              | Microsoft SQL Server |
|                              | CSV file format |
{: caption="Table 1. Migration data sources" caption-side="top"}

To download and install Lift, see: [Download Lift](https://www.lift-cli.cloud.ibm.com/#download){:external}.

For step-by-step instructions about migrating your data to the {{site.data.keyword.Bluemix_notm}} by using Lift, see: [Migrate data to {{site.data.keyword.dashdblong}}](https://www.lift-cli.cloud.ibm.com/#docs){:external}.

### {{site.data.keyword.Bluemix_notm}} Mass Data Migration Service
{: #mdms}

The {{site.data.keyword.Bluemix_notm}} Mass Data Migration Service (MDMS) can be used to migrate data from large IBM PureData Systems for Analytics (Netezza) databases of about 25 TB and greater to a fully managed {{site.data.keyword.dashdblong}} database on {{site.data.keyword.Bluemix_notm}}.

MDMS offers a fast, simple, secure way to physically transfer terabytes to petabytes of data to the {{site.data.keyword.Bluemix_notm}}. The MDMS is a mobile storage device with 120 TB of usable storage capacity. This device gives you the ability to overcome common transfer challenges like high costs, long transfer times, and security concerns – all in a single service.

![View of the Mass Data Migration Service device](images/mdms.svg)

For more information about the MDMS device, see: [Getting started tutorial](/docs/infrastructure/mass-data-migration?topic=mass-data-migration-getting-started-tutorial#getting-started-with-ibm-cloud-mass-data-migration){:external}.

For information about migrating your data from an IBM PureData System for Analytics (Netezza) database to an {{site.data.keyword.dashdblong}} database by using the MDMS device, see: [Migrating from IBM PureData System for Analytics (Netezza)](/docs/Db2whc/connecting?topic=Db2whc-pda#pda){:external}.

## Tutorial: Migrating data from on-premises relational databases
{: #tutorial}

This tutorial demonstrates how to migrate data from on-premises relational databases into {{site.data.keyword.dashdbshort_notm}} for business analytics applications. 

[Hybrid data warehousing with {{site.data.keyword.dashdbshort_notm}}](https://www.ibm.com/cloud/garage/tutorials/ibm-db2-warehouse-on-cloud/hybrid-data-warehousing-with-db-2-warehouse-on-cloud){:external}

