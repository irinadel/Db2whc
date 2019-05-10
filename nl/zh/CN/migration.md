---

copyright:
  years: 2014, 2019
lastupdated: "2018-11-20"

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

# 将数据迁移到 {{site.data.keyword.Bluemix_notm}}
{: #migration}

您可以从本地网络、对象存储（Amazon S3 或 {{site.data.keyword.Bluemix_notm}} Object Storage）上定界格式（CSV 或 TXT）的数据文件将数据装入到 {{site.data.keyword.dashdblong}}。您甚至可以从内部部署系统迁移数据。
{: shortdesc}

## 从对象存储装入数据
{: #cos}

要从 Amazon S3 装入数据，请选择以下一种方法：
  * {{site.data.keyword.dashdbshort_notm}} Web 控制台。**装入 > Amazon S3**。 
  * 直接从外部表。以下是示例 SQL 语句：

    ```
      INSERT INTO <table-name> SELECT * FROM EXTERNAL '<mys3file.txt>' USING
        (CCSID 1208 s3('s3.amazonaws.com', 
        '<S3-access-key-ID>',
        '<S3-secret-access-key>', 
        '<my_bucket>'
           )
        )      
    ```

要直接使用“外部表”从 {{site.data.keyword.Bluemix_notm}} Object Storage 装入数据，以下是示例 SQL 语句：

```
INSERT INTO <table-name> SELECT * FROM EXTERNAL '<mys3file.txt>' USING
  (CCSID 1208 s3('s3-api.us-geo.objectstorage.softlayer.net', 
  '<S3-access-key-ID>',
  '<S3-secret-access-key>', 
  '<my_bucket>'
     )
  )      
```

对于 {{site.data.keyword.Bluemix_notm}} Object Storage，要在创建新服务凭证时创建 HMAC 凭证，请在*添加内联配置参数*字段中指定 {"HMAC:true"}。
{: note}

有关从 {{site.data.keyword.Bluemix_notm}} Object Storage 装入数据的指导式演示，请参阅 [{{site.data.keyword.dashdblong}} guided demo: Explore data loading ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/cloud/garage/demo/try-db2-warehouse-cloud){:new_window}

## 从内部部署系统迁移数据
{: #onprem}

要从内部部署系统迁移数据，请根据数据集大小选择以下一种方法：
* 不到 25 TB 数据：[IBM Lift](#lift)
* 25 TB 数据和更多：[{{site.data.keyword.Bluemix_notm}} Mass Data Migration Service](#mdms)

### Lift
{: #lift}

Lift 是可用于将数据从表 1 中列出的各个数据源迁移至 {{site.data.keyword.Bluemix_notm}} 的免费应用程序。 

|{{site.data.keyword.Bluemix_notm}} 上的目标数据库| 数据源 |
|------------------------------|-------------|
| IBM Db2 Warehouse on Cloud   | IBM Db2 |
|                              | IBM Db2 Warehouse |
|                              | IBM Integrated Analytics System |
|                              | IBM PureData System for Analytics |
|                              | Oracle 数据库 |
|                              | Microsoft SQL Server |
|                              | CSV 文件格式 |
{: caption="表 1. 迁移数据源" caption-side="top"}

要下载并安装 Lift，请参阅：[下载 Lift ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.lift-cli.cloud.ibm.com/#download){:new_window}。

有关使用 Lift 将数据迁移至 {{site.data.keyword.Bluemix_notm}} 的逐步指示信息，请参阅：[将数据迁移至 {{site.data.keyword.dashdblong}} ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.lift-cli.cloud.ibm.com/#docs){:new_window}。

### {{site.data.keyword.Bluemix_notm}} Mass Data Migration Service
{: #mdms}

{{site.data.keyword.Bluemix_notm}} Mass Data Migration Service (MDMS) 可用于将数据从约 25 TB 及更大的大型 IBM PureData Systems for Analytics (Netezza) 数据库迁移至 {{site.data.keyword.Bluemix_notm}} 上完全受管的 {{site.data.keyword.dashdblong}} 数据库。

MDMS 提供快速、简单且安全的方式将太字节级别到拍字节级别的数据物理传输至 {{site.data.keyword.Bluemix_notm}}。MDMS 是具有 120 TB 可用存储容量的移动存储设备。此设备使您只需采用单个服务，就能克服各种常规传输难题（例如，高成本、长传输时间和安全问题）。

![Mass Data Migration Service 设备的视图](images/mdms.svg)

有关 MDMS 设备的更多信息，请参阅[开始使用教程](/docs/infrastructure/mass-data-migration?topic=mass-data-migration-getting-started-tutorial#getting-started-with-ibm-cloud-mass-data-migration){:new_window}。

有关使用 MDMS 设备将数据从 IBM PureData System for Analytics (Netezza) 数据库迁移至 {{site.data.keyword.dashdblong}} 数据库的信息，请参阅[从 IBM PureData System for Analytics (Netezza) 迁移](/docs/services/Db2whc/connecting?topic=Db2whc-pda#pda){:new_window}。

## 教程：从内部部署关系数据库迁移数据
{: #tutorial}

本教程演示如何将数据从内部部署关系数据库迁移到 {{site.data.keyword.dashdbshort_notm}}，以用于业务分析应用程序。 

[使用 {{site.data.keyword.dashdbshort_notm}} 进行混合数据仓储 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/cloud/garage/tutorials/ibm-db2-warehouse-on-cloud/hybrid-data-warehousing-with-db-2-warehouse-on-cloud){:new_window}

