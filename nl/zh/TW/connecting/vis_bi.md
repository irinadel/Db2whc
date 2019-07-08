---

copyright:
  years: 2014, 2019
lastupdated: "2018-10-24"

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

# 資料視覺化/BI
{: #data_vis_bi}

您也可以將外部應用程式和工具連接到 {{site.data.keyword.dashdbshort_notm}}，並使用它們進一步管理或分析您的資料。
{: shortdesc}

## Cognos Analytics
{: #cognos}

您可以針對雲端中的資料而非內部部署資料庫中的資料，執行 IBM Cognos® 報告。在將您的資料載入至 {{site.data.keyword.dashdbshort_notm}} 資料庫之後，您可以設定 JDBC 驅動程式，然後使用 Cognos 管理工具來建立資料庫連線。<!--These instructions explain how to connect to the database from Cognos version 10.2.1.-->
{: shortdesc}

觀看此視訊以查看如何建立連線。

<iframe class="embed-responsive-item" id="youtubeplayer" title="從 Cognos Analytics 建立連線" type="text/html" width="640" height="390" src="//www.youtube.com/embed/TRUEPVHGi0s?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

如需相關資訊，請參閱 [Connecting Cognos Analytics](https://www.ibm.com/support/knowledgecenter/en/SSEP7J_11.0.0/com.ibm.swg.ba.cognos.ug_cra.doc/c_create_ds.html#create_ds){:external}

## Looker
{: #looker}

您可以將 Looker 連接至 {{site.data.keyword.dashdbshort_notm}} 資料庫。Looker 是一個商業智慧應用程式及海量資料分析平台，您可以利用它來探索、分析及共用即時商業分析。
{: shortdesc}

[連接 Looker](https://docs.looker.com/setup-and-management/connecting-to-db){:external}

## Tableau
{: #tableau}

這些指示說明如何將 Tableau 連接至 {{site.data.keyword.dashdbshort_notm}} 資料庫，並套用至「Tableau 桌面」<!--version 8.x-->，但您可以針對其他 Tableau 工具使用類似步驟。
{: shortdesc}

### 必要條件
{: #prereq8}

在嘗試連接至您的 {{site.data.keyword.dashdbshort_notm}} 資料庫之前，請驗證您是否具有必要的[必備項目](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs)。

### 程序
{: #proc8}

1. 在「Tableau 桌面」中，於您的工具中開啟用來定義資料庫連線的視窗或頁面。
2. 從開始頁面中，按一下**連接至資料**。
3. 從**資料來源**清單中，選取要用於資料庫連線的資料來源或驅動程式。在清單的**在伺服器上**區段中，選取 **IBM Db2**。
4. 從 **IBM Db2 連線**視窗中，使用下表來輸入連線資訊。

| Tableau 欄位 | Db2 連線資訊欄位 |
|---------------|-----------------------------------|
| 步驟 1：輸入伺服器名稱 | 主機名稱 |
| 步驟 2：埠 | 埠號 |
| 步驟 3：輸入伺服器上的資料庫 | 資料庫名稱 |
| 使用者名稱 | 使用者 ID |
| 密碼 | 密碼 |
{: caption="表 1. Tableau 中針對連線資訊的欄位" caption-side="top"}

5. 按一下**連接**，以建立連線。Tableau 提供數個選項來連接您的資料。若要充分利用 {{site.data.keyword.dashdbshort_notm}} 資料庫，請選擇**即時連接**選項。

## Microsoft Excel
{: #excel}

這些指示說明如何將 Microsoft Excel <!--2010-->連接至 {{site.data.keyword.dashdbshort_notm}} 資料庫。
{: shortdesc}

### 必要條件
{: #prereq9}

在嘗試連接至您的 {{site.data.keyword.dashdbshort_notm}} 資料庫之前，請驗證您是否具有必要的[必備項目](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs)。

您必須在本端電腦上安裝 Db2 驅動程式套件或 IBM® Data Server Driver Package。 

**限制**：只在 Windows 作業系統上，才支援 Excel 與 {{site.data.keyword.dashdbshort_notm}} 之間的連線。

### 程序
{: #proc9}

1. 在 Web 主控台中，移至**執行 SQL** 頁面。
    
2. 在編輯器文字框中，鍵入一個以上的 SELECT 陳述式。

3. 按一下其中一個「執行」選項。

4. 按一下 **Excel ODC 檔案**。

5. 下載 `BLUExcel.odc` 檔案，並在 Excel 中予以開啟。如果顯示安全注意事項，請按一下**啟用**。

6. 按一下**開啟**，以連接至 {{site.data.keyword.dashdbshort_notm}} 資料庫。即會開啟**連接至 Db2 資料庫**對話框。

7. 鍵入您用來登入 {{site.data.keyword.dashdbshort_notm}} 的使用者 ID 及密碼。若要取得使用者 ID 及密碼，請按一下 Web 主控台中的**連接**，或按一下 Web 主控台中的**連接 > 連線資訊**。

8. 確定連線模式是 `Share`，然後按一下**確定**。

### 結果
{: #results2}

即會以 Excel 試算表顯示查詢結果。這些是「結果」檢視器中所顯示的相同結果。現在，您可以使用 Excel 來產生圖表及報告並分析資料。如需如何執行此動作，以及如何從 Web 主控台對資料執行 SQL 查詢的相關資訊，請參閱： 
- [Tutorial: Generating charts and reports by using Excel](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.analytics.doc/doc/explore_excel_reports.html){:external}
- [Analyzing with Excel](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.analytics.doc/doc/exploreexcel.html){:external}

## Esri ArcGIS for Desktop
{: #esri_arcgis}

您可以將 Esri ArcGIS for Desktop <!--version 10.3.1 -->連接至 {{site.data.keyword.dashdbshort_notm}} 資料庫，然後使用它來分析地理空間資料，並將其視覺化。
{: shortdesc}

### 必要條件
{: #prereq10}

在嘗試連接至您的 {{site.data.keyword.dashdbshort_notm}} 資料庫之前，請驗證您是否具有必要的[必備項目](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs)。

您必須在電腦上安裝 Db2 驅動程式套件或 IBM® Data Server Driver Package。

### 程序
{: #proc10}

1. 從您預先收集的[連線資訊](/docs/services/Db2whc/connecting?topic=Db2whc-db_details_cxn_creds#db_details_cxn_creds)中，判定您的 ODBC DSN 資料。

2. 建立新的連線：
      
   a. 在「ArcCatalog 型錄」樹狀結構中，開啟「資料庫連線」節點，然後按一下**新增資料庫連線**。
        
   b. 在「資料庫連線」精靈中：
   - 從「資料庫平台」下拉清單中，選取 **Db2**。
   - 在**資料來源**欄位中，輸入下列字串：
     ```
     HostName=<hostname>;Port=<port>;Database=<database>;
     CLIENTBUFFERSUNBOUNDLOBS=1;LOBCACHESIZE=50000000;
     FET_BUF_SIZE=256K  
     ```

     其中 `<hostname>`、`<port>` 及 `<database>` 是代表您稍早記下之主機名稱、埠號及資料庫名稱的位置保留元。
            
   - 選取**資料庫鑑別**作為鑑別類型。
            
   - 在對應欄位中，指定您的使用者名稱和密碼（您先前記下的使用者 ID 和密碼）。
            
   - 按下**確定**。
        
     ![資料庫連線精靈](images/2_gs_conn.jpg "資料庫連線精靈"){: caption="圖 1. 資料庫連線精靈" caption-side="bottom"}

### 結果
{: #results3}

Esri ArcGIS for Desktop 的 ArcCatalog 元件現在已連接至 {{site.data.keyword.dashdbshort_notm}} 資料庫。 


