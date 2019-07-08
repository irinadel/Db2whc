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

# 將資料載入至 {{site.data.keyword.dashdbshort_notm}}
{: #loading_data}

您可以將資料從位於本端網路上或物件儲存庫（Amazon S3 或 {{site.data.keyword.Bluemix_notm}} Object Storage）中的定界格式（CSV 或 TXT）資料檔案載入至 {{site.data.keyword.dashdblong}}。您甚至可以從內部部署系統移轉資料。
{: shortdesc}

## 從物件儲存庫載入資料
{: #cos}

若要從 Amazon S3 或 {{site.data.keyword.Bluemix_notm}} Object Storage 載入資料至 {{site.data.keyword.dashdblong}}，請選取下列其中一種方法：
* {{site.data.keyword.dashdbshort_notm}} Web 主控台。**載入 > Amazon S3**。 
* 直接從外部表格。以下是範例 SQL 陳述式：

    ```
      INSERT INTO <table-name> SELECT * FROM EXTERNAL '<mys3file.txt>' USING
        (CCSID 1208 s3('s3.amazonaws.com', 
        '<S3-access-key-ID>',
        '<S3-secret-access-key>', 
        '<my_bucket>'
           )
        )      
    ```

  若要直接從 {{site.data.keyword.Bluemix_notm}} Object Storage 使用「外部表格」來載入資料，下列是範例 SQL 陳述式：

  ```
INSERT INTO <table-name> SELECT * FROM EXTERNAL '<mys3file.txt>' USING
  (CCSID 1208 s3('s3-api.us-geo.objectstorage.softlayer.net', 
  '<S3-access-key-ID>',
  '<S3-secret-access-key>', 
  '<my_bucket>'
     )
  )      
  ```

  對於 {{site.data.keyword.Bluemix_notm}} Object Storage，若要在建立新的服務認證時建立 HMAC 認證，請在*新增線型配置參數*欄位中指定 {"HMAC:true"}。
  {: note}

* 為了提升效能，也可以使用 Db2 **LOAD** 指令，利用下列指令範例從 Amazon S3 載入資料：

  ```
  CALL SYSPROC.ADMIN_CMD('LOAD FROM "S3::<amazon-s3-URL>::<s3-access-key-id>::<s3-secret-access-key>:
  :<s3-bucket-name>::<path-to-data-file>" OF <filetype> <additional-load-options> INTO <table-name>)
  ```

  以下是 Db2 **LOAD** 指令的使用範例：

  ```
  CALL SYSPROC.ADMIN_CMD('load from "S3::s3-us-west-2.amazonaws.com::<s3-access-key-id>:
  :<s3-secret-access-key>::ibm-state-store::bdidata2TB/web_site.dat" of DEL modified by codepage=1208 
  coldel0x7c WARNINGCOUNT 1000 MESSAGES ON SERVER INSERT into BDINSIGHTS2.web_site ');
  ```

  如需支援的指令選項，請參閱 [**LOAD** 指令](https://www.ibm.com/support/knowledgecenter/en/SSEPGG_11.1.0/com.ibm.db2.luw.admin.cmd.doc/doc/r0008305.html){:external}。 

如需有關從 {{site.data.keyword.Bluemix_notm}} Object Storage 載入資料的引導式示範，請參閱：[{{site.data.keyword.dashdblong}} guided demo: Explore data loading](https://www.ibm.com/cloud/garage/demo/try-db2-warehouse-cloud){:external}

## 從內部部署系統移轉資料
{: #onprem}

若要從內部部署系統移轉您的資料，請選擇下列其中一種方法，視您的資料集大小而定：
* 小於 25 TB 的資料：[IBM Lift](#lift)
* 25 TB 及更大的資料：[{{site.data.keyword.Bluemix_notm}} Mass Data Migration Service](#mdms)

### Lift
{: #lift}

Lift 應用程式可供您免費用來將資料從「表 1」中列出的各種資料來源，移轉至 {{site.data.keyword.Bluemix_notm}}。 

| {{site.data.keyword.Bluemix_notm}} 上的目標資料庫 | 資料來源 |
|------------------------------|-------------|
| IBM Db2 Warehouse on Cloud   | IBM Db2 |
|                              | IBM Db2 Warehouse |
|                              | IBM Integrated Analytics System |
|                              | IBM PureData System for Analytics |
|                              |Oracle Database|
|                              | Microsoft SQL Server |
|                              | CSV 檔案格式 |
{: caption="表 1. 移轉資料來源" caption-side="top"}

若要下載並安裝 Lift，請參閱：[Download Lift](https://www.lift-cli.cloud.ibm.com/#download){:external}。

如需使用 Lift 將您的資料移轉至 {{site.data.keyword.Bluemix_notm}} 的逐步指示，請參閱 [Migrate data to {{site.data.keyword.dashdblong}}](https://www.lift-cli.cloud.ibm.com/#docs){:external}。

### {{site.data.keyword.Bluemix_notm}} Mass Data Migration Service
{: #mdms}

{{site.data.keyword.Bluemix_notm}} IBM Cloud Mass Data Migration Service (MDMS) 可以用來將資料從大型 IBM PureData Systems for Analytics (Netezza) 資料庫（大約 25 TB 及更大）移轉至 {{site.data.keyword.Bluemix_notm}} 上完全管理的 {{site.data.keyword.dashdblong}} 資料庫。

MDMS 提供一種快速、簡單、安全方式，將多個 TB 到多個 PB 的資料實際傳送至 {{site.data.keyword.Bluemix_notm}}。MDMS 是可用儲存空間容量為 120 TB 的行動儲存裝置。此裝置可讓您克服常見的傳送挑戰，像是高成本、冗長的傳送時間及安全顧慮 - 全部只需單一服務即可解決。


![Mass Data Migration Service 裝置的視圖](images/mdms.svg)

如需 MDMS 裝置的相關資訊，請參閱：[入門指導教學](/docs/infrastructure/mass-data-migration?topic=mass-data-migration-getting-started-tutorial#getting-started-with-ibm-cloud-mass-data-migration){:external}。

如需使用 MDMS 裝置，將資料從 IBM PureData System for Analytics (Netezza) 資料庫移轉至 {{site.data.keyword.dashdblong}} 資料庫的相關資訊，請參閱：[從 IBM PureData System for Analytics (Netezza) 移轉](/docs/services/Db2whc/connecting?topic=Db2whc-pda#pda){:external}。

## 指導教學：從內部部署關聯式資料庫移轉資料
{: #tutorial}

此指導教學示範如何將內部部署關聯式資料庫中的資料移轉至商業分析應用程式的 {{site.data.keyword.dashdbshort_notm}}。 

[Hybrid data warehousing with {{site.data.keyword.dashdbshort_notm}}](https://www.ibm.com/cloud/garage/tutorials/ibm-db2-warehouse-on-cloud/hybrid-data-warehousing-with-db-2-warehouse-on-cloud){:external}

