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
{:video: .video}

# Loading data from your local system
{: #load_local}

You can load data in a delimited format file (CSV or TXT) from your local system into {{site.data.keyword.dashdblong}}. For files less than 500 MB in size, simply drag and drop them onto the **Load** page in the {{site.data.keyword.dashdbshort_notm}} web console.
{: shortdesc}

When loading data through the web console, {{site.data.keyword.dashdbshort_notm}} autodetects and infers column types for your file. You can also configure delimiters and date/time formats for your data.

Watch this video to see a demonstration about loading data into {{site.data.keyword.dashdbshort_notm}} through the web console. 

![Loading data into IBM Db2 Warehouse on Cloud](https://www.youtube.com/embed/7wufZd_Lw9w?rel=0){: video output="iframe" data-script="none" id="youtubeplayer1" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen}

<!-- <iframe class="embed-responsive-item" id="youtubeplayer1" title="Loading data into IBM Db2 Warehouse on Cloud" type="text/html" width="640" height="390" src="//www.youtube.com/embed/7wufZd_Lw9w?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe> -->

If you want to load larger CSV files on the gigabyte or terabyte scale into {{site.data.keyword.dashdbshort_notm}}, we recommend using [IBM Lift CLI](https://www.lift-cli.cloud.ibm.com){: external}, a free ground-to-cloud data migration tool that uses Aspera technology for high-speed data transfer.

For a tutorial about loading CSV files from a local system into {{site.data.keyword.dashdbshort_notm}}, see [How to use IBM Lift CLI to migrate large CSV files to {{site.data.keyword.dashdbshort_notm}}](https://www.ibm.com/cloud/garage/dte/tutorial/moving-ibm-db2-warehouse-cloud-using-ibm-lift){: external}
