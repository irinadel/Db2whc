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

# 將資料移轉至 IBM Cloud
{: #migration}

您可以將資料從位於本端網路上或物件儲存庫（Amazon S3 或 IBM Cloud Object Storage）中的定界格式（CSV 或 TXT）資料檔案載入至 {{site.data.keyword.dashdblong}}。您甚至可以從內部部署系統移轉資料。
{: shortdesc}

## 從物件儲存庫載入資料
{: #cos}

若要從 Amazon S3 載入資料，請選取下列其中一種方法：
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

若要直接從 IBM Cloud Object Storage 使用「外部表格」來載入資料，下列是範例 SQL 陳述式：

```
INSERT INTO <table-name> SELECT * FROM EXTERNAL '<mys3file.txt>' USING
  (CCSID 1208 s3('s3-api.us-geo.objectstorage.softlayer.net', 
  '<S3-access-key-ID>',
  '<S3-secret-access-key>', 
  '<my_bucket>'
     )
  )      
```

**附註：**若為 IBM Cloud Object Storage，若要在建立新的服務認證時建立 HMAC 認證，請在*新增線型配置參數* 欄位中指定 {"HMAC:true"}。

## 從內部部署系統移轉資料
{: #onprem}

若要從內部部署系統移轉您的資料，請選擇下列其中一種方法，視您的資料集大小而定：
* 小於 25 TB 的資料：[IBM Lift](#lift)
* 25 TB 或更大的資料：[IBM Cloud Mass Data Migration Service](#mdms)

### Lift
{: #lift}

Lift 應用程式可供您免費用來將資料從「表 1」中列出的各種資料來源，移轉至 {{site.data.keyword.Bluemix_notm}}。 

| IBM Cloud 上的目標資料庫 | 資料來源 |
|------------------------------|-------------|
| IBM Db2 Warehouse on Cloud   | IBM Db2 |
|                              | IBM Db2 Warehouse |
|                              | IBM Integrated Analytics System |
|                              | IBM PureData System for Analytics |
|                              |Oracle Database|
|                              | Microsoft SQL Server |
|                              | CSV 檔案格式 |
{: caption="表 1. 移轉資料來源" caption-side="top"}

若要下載並安裝 Lift，請參閱[下載 Lift ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://lift.ng.bluemix.net/#download){:new_window}。

如需使用 Lift 將您的資料移轉至 {{site.data.keyword.Bluemix_notm}} 的逐步指示，請參閱：[移轉至 Db2 Warehouse on Cloud](/docs/services/lift-cli/index.html#about-lift){:new_window}。

### IBM Cloud Mass Data Migration Service
{: #mdms}

IBM Cloud Mass Data Migration Service (MDMS) 可以用來將資料從大型 IBM PureData Systems for Analytics (Netezza) 資料庫（大約 25 TB 及更大）移轉至 {{site.data.keyword.Bluemix_notm}} 上完全管理的 {{site.data.keyword.dashdblong}} 資料庫。

MDMS 提供一種快速、簡單、安全方式，將多個 TB 到多個 PB 的資料實際傳送至 {{site.data.keyword.Bluemix_notm}}。MDMS 是可用儲存空間容量為 120 TB 的行動儲存裝置。此裝置可讓您克服常見的傳送挑戰，像是高成本、冗長的傳送時間及安全顧慮 - 全部只需單一服務即可解決。


![Mass Data Migration Service 裝置的視圖](images/mdms.svg)

如需 MDMS 裝置的相關資訊，請參閱：[開始使用 IBM Cloud Mass Data Migration](/docs/infrastructure/mass-data-migration/index.html#getting-started-with-ibm-cloud-mass-data-migration){:new_window}。

如需使用 MDMS 裝置將您的資料從 IBM PureData System for Analytics (Netezza) 資料庫移轉至 {{site.data.keyword.dashdblong}} 資料庫，請參閱：[從 IBM PureData System for Analytics (Netezza) 移轉](/docs/services/Db2whc/pda_db2whc_mdms.html)。

