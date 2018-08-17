---

copyright:
  years: 2014, 2018
lastupdated: "2018-05-08"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Migrating data to IBM Cloud
{: #migration}

You can load data from a data file in a delimited format (CSV or TXT) located on a local network or in an object store (Amazon S3 or IBM Cloud Object Storage) to {{site.data.keyword.dashdblong}}. You can even migrate your data from an on-premises system.
{: shortdesc}

## Loading data from object store
{: #cos}

To load data from Amazon S3, select one of the following methods:
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

To load data from IBM Cloud Object Storage by using External Tables directly, the following is an example SQL statement:

```
INSERT INTO <table-name> SELECT * FROM EXTERNAL '<mys3file.txt>' USING
  (CCSID 1208 s3('s3-api.us-geo.objectstorage.softlayer.net', 
  '<S3-access-key-ID>',
  '<S3-secret-access-key>', 
  '<my_bucket>'
     )
  )      
```

**Note:** For IBM Cloud Object Storage, to create HMAC credentials when creating new service credentials, specify {"HMAC:true"} in the *Add Inline Configuration Parameters* field.

## Migrating data from on-premises system
{: #onprem}

To migrate your data from an on-premises system, choose one of the following methods depending on the size of your data set:
* Less than 25 TB of data: [IBM Lift](#lift)
* 25 TB of data and greater: [IBM Cloud Mass Data Migration Service](#mdms)

### Lift
{: #lift}

The Lift is an application that you can use without charge to migrate your data to the {{site.data.keyword.Bluemix_notm}} from the various data sources listed in Table 1. 

| Target database on IBM Cloud | Data source |
|------------------------------|-------------|
| IBM Db2 Warehouse on Cloud   | IBM Db2 |
|                              | IBM Db2 Warehouse |
|                              | IBM Integrated Analytics System |
|                              | IBM PureData System for Analytics |
|                              | Oracle Database |
|                              | Microsoft SQL Server |
|                              | CSV file format |
{: caption="Table 1. Migration data sources" caption-side="top"}

To download and install Lift, see: [Download Lift ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://lift.ng.bluemix.net/#download){:new_window}.

For step-by-step instructions about migrating your data to the {{site.data.keyword.Bluemix_notm}} by using Lift, see: [Migrate data to {{site.data.keyword.dashdblong}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://lift.ng.bluemix.net/#docs){:new_window}.

### IBM Cloud Mass Data Migration Service
{: #mdms}

The IBM Cloud Mass Data Migration Service (MDMS) can be used to migrate data from large IBM PureData Systems for Analytics (Netezza) databases of about 25 TB and greater to a fully-managed {{site.data.keyword.dashdblong}} database on {{site.data.keyword.Bluemix_notm}}.

MDMS offers a fast, simple, secure way to physically transfer terabytes to petabytes of data to the {{site.data.keyword.Bluemix_notm}}. The MDMS is a mobile storage device with 120 TB of usable storage capacity. This device gives you the ability to overcome common transfer challenges like high costs, long transfer times, and security concerns – all in a single service.

![View of the Mass Data Migration Service device](images/mdms.svg)

For more information about the MDMS device, see: [Getting started with IBM Cloud Mass Data Migration](/docs/infrastructure/mass-data-migration/index.html#getting-started-with-ibm-cloud-mass-data-migration){:new_window}.

For information about migrating your data from an IBM PureData System for Analytics (Netezza) database to an {{site.data.keyword.dashdblong}} database by using the MDMS device, see: [Migrating from IBM PureData System for Analytics (Netezza)](/docs/services/Db2whc/pda_db2whc_mdms.html).

