---

copyright:
  years: 2014, 2019
lastupdated: "2019-11-06"

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

# Loading data from IBM Cloud Object Storage
{: #load_cos}

The best way to load data from IBM Cloud Object Storage (COS) into {{site.data.keyword.dashdblong}} is through the External Tables functionality. 
{: shortdesc}

Here's a sample SQL statement that inserts COS data into a {{site.data.keyword.dashdbshort_notm}} table by using External Tables:

```
INSERT INTO <table-name> SELECT * FROM EXTERNAL '<mys3file.txt>' USING
  (CCSID 1208 s3('s3-api.us-geo.objectstorage.softlayer.net', 
  '<S3-access-key-ID>',
  '<S3-secret-access-key>', 
  '<my_bucket>'
     )
  )      
```

For {{site.data.keyword.Bluemix_notm}} Object Storage, to create HMAC credentials when creating new service credentials, specify {"HMAC:true"} in the *Add Inline Configuration Parameters* field.
{: note}

Watch this video about how to access COS data quickly by using External Tables.

<iframe class="embed-responsive-item" id="youtubeplayer1" title="Loading data from COS into IBM Db2 Warehouse on Cloud" type="text/html" width="640" height="390" src="//www.youtube.com/embed/RMMExarvBVk?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

