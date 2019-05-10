---

copyright:
  years: 2014, 2019
lastupdated: "2019-03-29"

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

# 資料整合
{: #data_int}

您也可以將外部應用程式和工具連接到 {{site.data.keyword.dashdbshort_notm}}，並使用它們進一步管理或分析您的資料。
{: shortdesc}

## DataStage
{: #datastage}

這些指示說明如何藉由編目資料庫及定義連線物件，在 IBM® InfoSphere® DataStage® <!--version 9.1 and later -->與 {{site.data.keyword.dashdbshort_notm}} 資料庫之間定義不使用 SSL 的連線，或如何使用協力廠商所發出的數位憑證，來使用 SSL 建立連線。
{: shortdesc}

### 必要條件
{: #prereq1}

強烈建議您將 DataStage 更新為最新版本，讓您可以利用外部表格，將資料載入至 {{site.data.keyword.dashdbshort_notm}}。
{: important}

如果您尚未安裝資料伺服器用戶端，請下載並安裝適用於用戶端機器作業系統的 IBM Data Server Client<!--Version 10.5 -->：[IBM Data Server Client ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/marketing/iwm/iwm/web/preLogin.do?source=swg-idsc97){:new_window}。

若要使用 SSL 通訊協定建立連線，請下載並安裝 32 位元 GSKit 第 8 版。按一下適用於用戶端機器作業系統的「作業系統」標籤：[GSKit 第 8 版 - 安裝、解除安裝及升級指示 ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.ibm.com/support/docview.wss?uid=swg21631462){:new_window}。對於下列作業系統，請確定您將 GSKit 安裝目錄路徑新增至 OS 特定路徑環境變數：

- AIX®：**LIBPATH**
   - `/usr/opt/ibm/gsk8/lib`
- Linux：**LD_LIBRARY_PATH**
    - `/usr/local/ibm/gsk8/lib`
- UNIX：**LD_LIBRARY_PATH**
    - `/opt/ibm/gsk8/lib`
- Windows：**PATH**
    - `<installation_directory>\gsk8\bin`
    - `<installation_directory>\gsk8\lib`

在嘗試連接至您的 {{site.data.keyword.dashdbshort_notm}} 資料庫之前，請驗證您是否具有必要的[必備項目](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs)。

### 程序
{: #proc1}

- 若要使用 SSL 來建立連線，請完成下列步驟：

  1. 開啟指令行或終端機，並在 DataStage 系統中建立新的目錄，以儲存 SSL 憑證及金鑰檔。

     `# /home/db2inst2> mkdir SSL`

     `# /home/db2inst2> cd SSL`

  2. 在 {{site.data.keyword.dashdbshort_notm}} Web 主控台中，從**將應用程式連接至資料庫**頁面下載 SSL 憑證。

     a. 從主功能表中，按一下**連接**。
     
     b. 按一下**使用 SSL 的連線**，然後按一下 **SSL 憑證 (1 KB)** 鏈結。
     
     c. 將 `DigiCertGlobalRootCA.crt` 憑證儲存在步驟 1 中所做的 SSL 目錄中。
        
  3. 使用 **gsk8capicmd_64** 公用程式，在 DataStage 系統中建立一個用戶端金鑰儲存資料庫。

     `# /home/db2inst2/SSL> gsk8capicmd_64 -keydb -create -db <keystore_db.kdb> -pw <ks_db_password> -stash`

     其中 `<keystore_db.kdb>` 代表用戶端金鑰儲存資料庫，而 `<ks_db_password>` 代表用戶端金鑰儲存資料庫的密碼。
        
  4. 將憑證新增至用戶端金鑰儲存資料庫。

     `# /home/db2inst2/SSL> gsk8capicmd_64 -cert -add -db <keystore_db.kdb> -pw <ks_db_password> -label BLUDB_SSL -file DigiCertGlobalRootCA.crt`

     其中 `<keystore_db.kdb>` 代表用戶端金鑰儲存資料庫，而 `<ks_db_password>` 代表用戶端金鑰儲存資料庫的密碼。
    
  5. 在 DataStage Server 上配置 Db2 用戶端。
            
     a. 更新資料庫管理程式中的 SSL 配置參數。

     `# /home/db2inst2> db2 update dbm cfg using SSL_CLNT_KEYDB /home/db2inst2/SSL/<keystore_db.kdb>`

     其中 `<keystore_db.kdb>` 代表用戶端金鑰儲存資料庫。

     `# /home/db2inst2> db2 update dbm cfg using SSL_CLNT_STASH /home/db2inst2/SSL/<keystore_db.sth>`

     其中 `<keystore_db.sth>` 代表用戶端金鑰儲存資料庫密碼隱藏。
            
     b. 使用 SSL 安全選項編目目標節點，然後編目該目標節點上的 BLUDB 資料庫。

     `# /home/db2inst2> db2 catalog tcpip node <node_name> remote <IP_addr_of_BLUDB_database_server> server 50001 security SSL`

     其中 `<node_name>` 代表您的目標節點名稱，而 `<IP_addr_of_BLUDB_database_server>` 代表 BLUDB 資料庫伺服器的 IP 位址。

     `# /home/db2inst2> db2 catalog db BLUDB as <db_alias> at node <node_name>`

     其中 `<db_alias>` 是您的 {{site.data.keyword.dashdbshort_notm}} 資料庫名稱。

  6. 對於所有人，新增 SSL 目錄中檔案的讀取及執行許可權。執行工作的 DataStage 使用者需要存取這些檔案，才能建立與 Db2 資料庫的 SSL 連線。

     `# /home/db2inst2/SSL> chmod 655 /home/db2inst2/SSL/*`

  7. 使用下列其中一種方式來測試 SSL 連線：

     - 使用 CLP 測試連線。發出下列指令來連接至 {{site.data.keyword.dashdbshort_notm}} 資料庫：

       `db2 connect to <db_alias> user <user_id>`

       其中 `<db_alias>` 是您的 {{site.data.keyword.dashdbshort_notm}} 資料庫名稱，而 `<user_id>` 是您的 {{site.data.keyword.dashdbshort_notm}} 使用者 ID。系統會提示您輸入密碼。
    
     - 使用 CLI 測試連線。發出下列指令來連接至 {{site.data.keyword.dashdbshort_notm}} 資料庫：

       `db2cli validate -dsn <alias> -connect -user <user_id> -passwd <password>`

        其中 `<alias>` 是您使用 **db2cli writecfg** 指令建立的別名、`<user_id>` 是您的 {{site.data.keyword.dashdbshort_notm}} 使用者 ID，而 `<password>` 是您的 {{site.data.keyword.dashdbshort_notm}} 密碼。

- 若要建立不使用 SSL 的連線，請完成下列步驟，編目 {{site.data.keyword.dashdbshort_notm}} 上的目標資料庫：

  1. 編目目標 {{site.data.keyword.dashdbshort_notm}} 節點，讓用戶端應用程式可以與其連接。執行下列 CLP 指令：

     `db2 catalog tcpip node <node_name> remote <IP_address_of_BLUDB_database_server> server <port_number_of_BLUDB_database>`

     其中 `<node_name>` 代表您的節點名稱、`<IP_address_of_BLUDB_database_server>` 代表 BLUDB 資料庫伺服器的 IP 位址，而 `<port_number_of_BLUDB_database>` 代表 BLUDB 資料庫的埠號。

  2. 編目遠端 {{site.data.keyword.dashdbshort_notm}} 資料庫，讓用戶端應用程式可以與其連接。執行下列指令：

     `db2 catalog db BLUDB as <db_alias> at node <node_name>`

     其中 `<db_alias>` 代表您的 {{site.data.keyword.dashdbshort_notm}} 資料庫名稱，而 `<node_name>` 代表您的節點名稱。

  3. 使用下列其中一種方式來測試非 SSL 連線：

      - 使用 CLP 測試連線。發出下列指令來連接至 {{site.data.keyword.dashdbshort_notm}} 資料庫：

        `db2 connect to <db_alias> user <user_id>`

        其中 `<db_alias>` 是您的 {{site.data.keyword.dashdbshort_notm}} 資料庫名稱，而 `<user_id>` 是您的 {{site.data.keyword.dashdbshort_notm}} 使用者 ID。系統會提示您輸入密碼。

        `db2 list tables`

      - 使用 CLI 測試連線。發出下列指令來連接至 {{site.data.keyword.dashdbshort_notm}} 資料庫：

        `db2cli validate -dsn <alias> -connect -user <user_id> -passwd <password>`

        其中 `<alias>` 是您使用 **db2cli writecfg** 指令建立的別名、`<user_id>` 是您的 {{site.data.keyword.dashdbshort_notm}} 使用者 ID，而 `<password>` 是您的 {{site.data.keyword.dashdbshort_notm}} 密碼。

  4. 使用您預先收集的[連線資訊](/docs/services/Db2whc/connecting?topic=Db2whc-db_details_cxn_creds#db_details_cxn_creds)來定義 DataStage 用戶端中的連線。在**參數**標籤上，您必須針對**使用暫置類型連接**欄位選取 **Db2 連接器**。

     如需在 DataStage 中定義連線的詳細資料，請參閱下列 DataStage 文件主題： 
     
     - [手動建立資料連線物件 ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/support/knowledgecenter/SSZJPZ_11.3.0/com.ibm.swg.im.iis.ds.design.doc/topics/t_ddesref_Creating_a_Data_Connection_Object_Manually.html){:new_window}
     - [Configuring access to Db2 databases ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/support/knowledgecenter/en/SSZJPZ_11.7.0/com.ibm.swg.im.iis.conn.common.usage.doc/topics/t_configuring_db2conn.html){:new_window}

## Informatica
{: #informatica}

您可以將 Informatica 連接至 {{site.data.keyword.dashdbshort_notm}}，以協助您管理資料。
{: shortdesc}

觀看此視訊以查看如何整合 {{site.data.keyword.dashdbshort_notm}} 與 Informatica Cloud。

<iframe class="embed-responsive-item" id="youtubeplayer1" title="DB2 Connections - Lightening Fast How-To with Informatica Cloud" type="text/html" width="640" height="390" src="//www.youtube.com/embed/TUiS_HstLnU?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

<!-- To configure a native Db2 connection to connect to {{site.data.keyword.dashdbshort_notm}}, perform the following steps:

1. Run the `odbcad32.exe` file from your local system.
The ODBC Data Sources Administrator dialog box appears.

2. Create the 32-bit ODBC Data Source Name using the DataDirect Db2 drivers.

3. In the ODBC DB2 Wire Protocol Setup dialog box, click **Security** tab.

4. Set the value of the `Authentication Method` property as `1 -Encrypt Password`. The following image shows the **Security** tab in the ODBC DB2 Wire Protocol Setup dialog box where you can set the `Authentication Method` property:
             
   ![ODBC Db2 Wire Protocol Driver Setup - Security tab](images/odbc_driver.png)
       
5. In the ODBC DB2 Wire Protocol Setup dialog box, click **Modify Bindings** tab.

6. Enter your user name in the Package Collection property. The following image shows the **Modify Bindings** tab in the ODBC DB2 Wire Protocol Setup dialog box where you can set the `Package Collection` property: 

   ![ODBC Db2 Wire Protocol Driver Setup - Modify Bindings tab](images/odbc_driver_2.png)
            
7. In the PowerCenter Designer, use the data source name that you created to import the metadata.

8. In the PowerCenter Workflow Manager, create the required workflow.

9. Ensure that you have the {{site.data.keyword.dashdbshort_notm}} compatible 11.x Db2 clients when you run the workflow.

**Note**: If you want to set the authentication type when you create the Db2 client catalog, you could specify the value of the `AUTHENTICATION TYPE` property as `SERVER_ENCRYPT`. -->

<!-- Watch this video to see how to integrate Db2 and Salesforce with Informatica Cloud.

<iframe class="embed-responsive-item" id="youtubeplayer2" title="Integrate Db2 and Salesforce with Informatica Cloud" type="text/html" width="640" height="390" src="//www.youtube.com/watch?v=RGTLweZvKP8" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe> -->

<!-- [Informatica ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://kb.informatica.com/howto/6/Pages/20/522402.aspx?myk=Connect%20to%20Db2){:new_window} -->

## Lift
{: #lift}

使用 Lift 將您的資料移轉至 {{site.data.keyword.dashdbshort_notm}}。

[Lift ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.lift-cli.cloud.ibm.com/#docs){:new_window}

## InfoSphere Data Replication
{: #idr}

您可以將 IBM® InfoSphere® Data Replication <!--version 11.3.3.3-36 or later -->連接至 {{site.data.keyword.dashdbshort_notm}} 資料庫。此功能同時適用於 SMP 及 MPP 環境。此功能不適用於 {{site.data.keyword.dashdbshort_notm}} 的入門方案。
{: shortdesc}

### 概觀
{: #overview2}

在理想情況下，當您將 IBM InfoSphere Data Replication 連接至 {{site.data.keyword.dashdbshort_notm}} 時，IBM InfoSphere Data Replication 位於與 {{site.data.keyword.dashdbshort_notm}} 相同的「{{site.data.keyword.Bluemix_notm}} 資料中心」，或與 {{site.data.keyword.dashdbshort_notm}} 並存。IBM InfoSphere Data Replication 會從本端伺服器連接至遠端 {{site.data.keyword.dashdbshort_notm}} 實例。

當您使用 {{site.data.keyword.dashdbshort_notm}} 作為連線目標時，IBM InfoSphere Data Replication 的效能局部取決於將其目標引擎與 {{site.data.keyword.dashdbshort_notm}} 實例區隔之網路的頻寬。實體距離也會影響效能：在理想情況下，IBM InfoSphere Data Replication 會盡可能靠近 {{site.data.keyword.dashdbshort_notm}} 實例。網路拓蹼也會影響效能。例如，在理想情況下，IBM InfoSphere Data Replication 目標引擎會在與目標實例相同的 VPN（安全網域）中執行於 VM 上。要遍訪的網路節點（例如，防火牆或路由器）數目越少，效能就越佳。 

### 必要條件
{: #prereq2}

如果您要使用 SSL 通訊協定進行連接，請下載並安裝 GSKit 第 8 版。請參閱 [GSKit 第 8 版 - 安裝、解除安裝及升級指示 ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.ibm.com/support/docview.wss?uid=swg21631462){:new_window}。按一下套用至用戶端機器作業系統的作業系統標籤。如果您是在 Windows 電腦上安裝 GSKit，請確定您針對 **`PATH`** 環境變數指定 GSKit 安裝目錄路徑 (`<installation_directory>\gsk8\bin`)。

在嘗試連接至您的 {{site.data.keyword.dashdbshort_notm}} 資料庫之前，請驗證您是否具有必要的[必備項目](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs)。

如果您要使用 SSL 通訊協定進行連接，請將 `DigiCertGlobalRootCA.crt` SSL 憑證從 Web 主控台下載至用戶端機器上的目錄。若要下載憑證，請按一下**連線 > 連線資訊**，然後按一下**使用 SSL 的連線**標籤。

### 程序
{: #proc2}

1. 選擇下列其中一種方法進行連線：

   - 若要使用 SSL 來建立連線，請完成下列步驟：
            
     a. 發出下列指令：

     `cd /<ssl_directory_name>/ssl`

     其中 `/<ssl_directory_name>/ssl` 是您已將 `DigiCertGlobalRootCA.crt` SSL 憑證下載至其中之目錄的路徑。

     b. 使用 **GSKCapiCmd** 工具，以建立用戶端金鑰資料庫及隱藏檔。例如，下列指令會建立稱為 `dashclient.kdb` 的用戶端金鑰資料庫及稱為 `dashclient.sth` 的隱藏檔：

     `gsk8capicmd_64 -keydb -create -db "dashclient.kdb" -pw "passw0rdpw0" -stash`

     其中 `passw0rdpw0` 是密碼。**-stash** 選項會在與用戶端金鑰資料庫相同的路徑中建立隱藏檔，且副檔名為 `.sth`。在連線期間，GSKit 會使用隱藏檔來取得用戶端金鑰資料庫的密碼。
            
     c. 將憑證新增至用戶端金鑰資料庫。例如，下列 **gsk8capicmd** 指令將 `/<ssl_directory_name>/ssl/DigiCertGlobalRootCA.crt` 檔案中的憑證匯入至稱為 `dashclient.kdb` 的用戶端金鑰資料庫：

     `gsk8capicmd_64 -cert -add -db "dashclient.kdb" -pw "passw0rdpw0" -label "DigiCert" -file "/<ssl_directory_name>/ssl/DigiCertGlobalRootCA.crt" -format ascii -fips`

     d. 更新用戶端上的 `SSL_CLNT_KEYDB` 及 `SSL_CLNT_STASH` 資料庫管理程式配置參數值，以指定用戶端金鑰資料庫及隱藏檔。範例如下：

     `db2 update dbm cfg using SSL_CLNT_KEYDB /<ssl_directory_name>/ssl/dashclient.kdb`

     `db2 update dbm cfg using SSL_CLNT_STASH /<ssl_directory_name>/ssl/dashclient.sth`

     e. 編目 {{site.data.keyword.dashdbshort_notm}} 節點，讓用戶端應用程式可以與其連接。發出下列指令：

     `db2 catalog tcpip node <node_name> remote <Db2_Warehouse_IP_address> server <port_number> security ssl`

     其中：
                
     `<node_name>` 是節點的名稱。

     `<Db2_Warehouse_IP_address>` 是 Db2 Warehouse on Cloud 伺服器的 IP 位址。

     `<port_number>` 是使用 SSL 連線連接至 Db2 Warehouse 時所使用的埠。如果您是使用預設埠，請指定 `50001`。
            
     f. 編目遠端 {{site.data.keyword.dashdbshort_notm}} 資料庫，讓用戶端應用程式可以與其連接。發出下列指令：

     `db2 catalog database bludb as <db_alias> at node <node_name>`

     其中 `db_alias` 是 {{site.data.keyword.dashdbshort_notm}} 資料庫的名稱。
            
     g. 使用下列其中一種方式來測試 SSL 連線：
                
     - 使用 CLP 測試連線，方法是發出下列指令來連接至 {{site.data.keyword.dashdbshort_notm}} 資料庫：

       `db2 connect to <db_alias> user <user_id>`

       其中 `<user_id>` 是您的 {{site.data.keyword.dashdbshort_notm}} 使用者 ID。系統會提示您輸入密碼。
                
     - 使用 CLI 測試連線，方法是發出下列指令來連接至 {{site.data.keyword.dashdbshort_notm}} 資料庫：

       `db2cli validate -dsn <alias> -connect -user <user_id> -passwd <password>`

       其中 `<alias>` 是您使用 **db2cli writecfg** 指令建立的 DSN 別名、`<user_id>` 是您的 {{site.data.keyword.dashdbshort_notm}} 使用者 ID，而 `<password>` 是您的 {{site.data.keyword.dashdbshort_notm}} 資料庫密碼。
        
   - 若要建立不使用 SSL 的連線，請完成下列步驟：

     a. 編目 {{site.data.keyword.dashdbshort_notm}} 節點，讓用戶端應用程式可以與其連接。發出下列指令：

     `db2 catalog tcpip node <node_name> remote <Db2_Warehouse_IP_address> server <port_number>`

     其中：
                
     `<node_name>` 是節點的名稱。

     `<Db2_Warehouse_IP_address>` 是 {{site.data.keyword.dashdbshort_notm}} 伺服器的 IP 位址。

     `<port_number>` 是不使用 SSL 連線連接至 {{site.data.keyword.dashdbshort_notm}} 時所使用的埠。如果您是使用預設埠，請指定 `50000`。
            
     b. 編目遠端 {{site.data.keyword.dashdbshort_notm}} 資料庫，讓用戶端應用程式可以與其連接。發出下列指令：

     `db2 catalog database bludb as <db_alias> at node <node_name>`

     其中 `<db_alias>` 是您的 {{site.data.keyword.dashdbshort_notm}} 資料庫名稱。

     c. 使用下列其中一種方式來測試非 SSL 連線：

     - 使用 CLP 測試連線，方法是發出下列指令來連接至 {{site.data.keyword.dashdbshort_notm}} 資料庫：

       `db2 connect to <db_alias> user <user_id>`

       其中 `<user_id>` 是您的 {{site.data.keyword.dashdbshort_notm}} 使用者 ID。系統會提示您輸入密碼。
                
     - 使用 CLI 測試連線，方法是發出下列指令來連接至 {{site.data.keyword.dashdbshort_notm}} 資料庫：

       `db2cli validate -dsn <alias> -connect -user <user_id> -passwd <password>`

       其中 `<alias>` 是您使用 **db2cli writecfg** 指令建立的 DSN 別名、`<user_id>` 是您的 {{site.data.keyword.dashdbshort_notm}} 使用者 ID，而 `<password>` 是您的 Db2 Warehouse on Cloud 密碼。
    
2. 啟動 InfoSphere Data Replication 配置工具，並執行下列步驟。畫面擷取中所顯示的值是範例。
        
   a. 使用**實例配置**標籤，以新增來源實例來指向來源資料庫：

   ![IIDR 新實例 - 來源實例](images/IIDR_source_instance.jpg)

   b. 使用**實例配置**標籤，以新增目標實例來指向目標 Db2 資料庫。如果您不是使用 IBM InfoSphere Data Replication 11.3.3.3-50 或更新版本，請不要選取**指定重新整理載入器路徑**勾選框。

   ![IIDR 新實例 - 目標實例](images/IIDR_target_instance.jpg)

   c. 啟動每一個實例：

   ![IIDR 配置工具](images/IIDR_instances.jpg)

3. 啟動 InfoSphere Data Replication 管理主控台，並使用「存取權管理程式」來完成下列步驟：
        
   a. 使用**資料儲存庫**標籤，以建立資料儲存庫來連接至來源實例。因為 Db2 資料庫原本並不支援作為來源資料庫，所以您必須按一下**連線參數**，來提供來源資料庫的使用者和密碼資訊。

   ![資料儲存庫內容 - 來源](images/IIDR_source_datastore.jpg)

   b. 使用**資料儲存庫**標籤，以建立資料儲存庫來連接至目標實例。您必須按一下**連線參數**來提供使用者及密碼資訊。

   ![資料儲存庫內容 - 目標](images/IIDR_target_datastore.jpg)

   c. 如果將連接至「存取伺服器」的使用者（例如，admin）不存在，請建立該使用者：

   ![新增使用者](images/IIDR_management_user.jpg)

   d. 按一下**存取權管理程式**標籤。
        
   e. 在**資料儲存庫管理**標籤上，於每一個資料儲存庫上按一下滑鼠右鍵，然後按一下**指派使用者**，將使用者指派給來源及目標資料儲存庫。請確定用來存取每一個實例的認證都正確。

   ![IIDR 管理主控台 - 存取權管理程式](images/IIDR_management_assign_user.jpg)

### 下一步
{: #what2}

定義訂閱，並執行資料抄寫。如需相關資訊，請參閱：

- [從 InfoSphere Data Replication 載入資料![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/learn_how/loaddata_iidr.html){:new_window} 

## Segment
{: #segment}

您可以整合 Segment 與 {{site.data.keyword.dashdbshort_notm}} 資料庫。Segment 是用於收集、儲存及遞送使用者資料至數百個工具的單一平台。
{: shortdesc}

[Segment ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](https://segment.com/docs/destinations/db2/){:new_window}

## Data Studio
{: #data_studio}

這些指示說明如何建立從 IBM® Data Studio <!--version 4.1.x -->到 {{site.data.keyword.dashdbshort_notm}} 資料庫的連線。
{: shortdesc}

### 必要條件
{: #prereq3}

在嘗試連接至您的 {{site.data.keyword.dashdbshort_notm}} 資料庫之前，請驗證您是否具有必要的[必備項目](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs)。

### 程序
{: #proc3}

1. 在 Data Studio 中，按一下**所有資料庫 > 新建資料庫連線**。

2. 在**本端**標籤上，選取 **Db2 for Linux, UNIX, and Windows** 作為資料庫管理程式。
    
3. 在**一般**標籤上，輸入下列值：
   - *資料庫*：`BLUDB`
   - *主機*：主機名稱。
   - *埠*：若為不使用 SSL 的連線，請輸入 `50000`。若為使用 SSL 的連線，請輸入 `50001`。 
   - *使用者名稱*：您用來登入的使用者名稱。
   - *使用者名稱*：您用來登入的密碼。

4. 若為 SSL 連線，請按一下**選用**標籤，然後按一下**新增**。對於 `sslConnection` 內容，請指定 `true`。

5. [*Optional*]: Click **測試連線**來驗證連線是否成功。

## Data Server Manager (DSM)
{: #dsm}

IBM® Data Server Manager 與 {{site.data.keyword.dashdbshort_notm}} 資料庫之間的連線，可讓您從 Data Server Manager Web 主控台監視及管理資料庫。
{: shortdesc}

### 必要條件
{: #prereq4}

在嘗試連接至您的 {{site.data.keyword.dashdbshort_notm}} 資料庫之前，請驗證您是否具有必要的[必備項目](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs)。

### 程序
{: #proc4}

<!--The connection procedure was tested on Data Server Manager version 1.1. The same procedure applies to all of the other versions of the Data Server Manager software.
-->
若要建立連線，請完成下列步驟：

1. 登入 Data Server Manager Web 主控台。
    
2. 在 Data Server Manager Web 主控台中，移至**設定 > 資料庫連線**。
    
3. 按一下 ![圓圈內的 + 符號](images/icon_R_plus.gif) 圖示以新增資料庫連線。在**新增資料庫連線**頁面的**資料庫連線**標籤下，於下列欄位中輸入必要資訊：


   - *資料庫連線名稱*：名稱必須是 Data Server Manager 的唯一名稱
   - *資料伺服器類型*：從下拉功能表中，選取 **Db2 for Linux, UNIX, and Windows**
   - *資料庫名稱*：`BLUDB`
   - *主機名稱*：輸入 {{site.data.keyword.dashdbshort_notm}} 主機名稱 
   - *埠號*：若為不使用 SSL 的連線，請輸入 `50000`。若為使用 SSL 的連線，請輸入 `50001`。 
   - *JDBC 安全*：從下拉功能表中，選取**清除文字密碼**
   - *使用者 ID*：您的 {{site.data.keyword.dashdbshort_notm}} 使用者 ID 
   - *密碼*：您的 {{site.data.keyword.dashdbshort_notm}} 密碼 

4. 若為使用 SSL 的連線，請選取**進階 JDBC 內容**標籤。在下列欄位中輸入必要資訊：

   - *內容*：`sslConnection`
   - *值*：`true`

    按一下**新增**按鈕。選取**資料庫連線**標籤。
    
5. 按一下**測試連線**按鈕來測試連線。如果連線成功，請按一下**確定**。

## InfoSphere Data Architect
{: #ida}

這些指示說明如何建立從 InfoSphere® Data Architect <!--version 9.1.x -->到 {{site.data.keyword.dashdbshort_notm}} 資料庫的連線。
{: shortdesc}

### 必要條件
{: #prereq5}

在嘗試連接至您的 {{site.data.keyword.dashdbshort_notm}} 資料庫之前，請驗證您是否具有必要的[必備項目](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs)。

### 程序
{: #proc5}

1. 在 InfoSphere Data Architect 的「資料來源瀏覽器」視圖中，於**資料庫連線**上按一下滑鼠右鍵，然後選取**新建**。
    
2. 在**本端**標籤上，選取 **Db2 for Linux, UNIX, and Windows** 作為資料庫管理程式。
    
3. 在**一般**標籤上，輸入下列值：

   - *資料庫*：`BLUDB`
   - *主機*：您預先收集的主機名稱。
   - *埠*：若為不使用 SSL 的連線，請輸入 `50000`。若為使用 SSL 的連線，請輸入 `50001`。 
   - *使用者名稱*：您預先收集的使用者 ID。
   - *密碼*：您預先收集的密碼。

4. 若為 SSL 連線，請按一下**選用**標籤。輸入 `sslConnection` 內容，並指定 `true` 值。按一下**新增 **。
    
5. [*Optional*]: Click **測試連線**來驗證連線是否成功。

## Aginity Workbench
{: #aginity_wb}

這些指示說明如何將 Aginity Workbench <!--4.3 -->連接至 {{site.data.keyword.dashdbshort_notm}} 資料庫。您可以使用 Aginity Workbench，將 IBM PureData for Analytics (Netezza) 資料模型和資料移轉至 {{site.data.keyword.dashdbshort_notm}}。
{: shortdesc}

### 必要條件
{: #prereq6}

在嘗試連接至您的 {{site.data.keyword.dashdbshort_notm}} 資料庫之前，請驗證您是否具有必要的[必備項目](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs)。

### 程序
{: #proc6}

1. 下載並安裝 Aginity Workbench。

2. 從您先前記下的連線資訊，判定您的 ODBC DSN。

3. 啟動 Aginity Workbench。如果未自動開啟資料庫連線對話框，請按一下工具列上的**連接**予以開啟。

4. [建立資料庫連線 ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.aginity.com/documentation/WB/dashDB/Default.htm#Aginity_Topics/Aginity_Workbench/Database_Connection_Dialog_Box.htm){:new_window}。使用您先前記下的連線資訊中的主機名稱、使用者 ID 及密碼。

## CLPPlus
{: #clpplus}

Db2 驅動程式套件中包含 Command Line Processor Plus (CLPPlus)。CLPPlus 提供一個指令行介面，您可以用來連接至 {{site.data.keyword.dashdbshort_notm}} 資料庫。您可以使用 CLPPlus 來定義、編輯及執行陳述式、Script 和指令。
{: shortdesc}

### 必要條件
{: #prereq7}

在嘗試連接至您的 {{site.data.keyword.dashdbshort_notm}} 資料庫之前，請驗證您是否具有必要的[必備項目](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs)。

若要使用 CLPPlus，請確定已在電腦上安裝 Java 1.5.0 版或更新版本的軟體開發套件 (SDK) 或 Java 執行時期環境 (JRE)，而且環境變數設定如下：

- `JAVA_HOME` 環境變數設為電腦上的 Java 安裝目錄。
- `PATH` 環境變數設定包括電腦上 Java 安裝目錄的 `bin` 子目錄。

### 程序
{: #proc7}

1. 在 Linux 作業系統上的指令 Shell、Windows 命令提示字元，或 Windows 作業系統上的 Db2 指令視窗中，執行下列指令：

   這些指令會在電腦的驅動程式配置檔 (`db2dsdriver.cfg`) 中建立新項目，並設定連線屬性。您只需執行此步驟一次。

   - 若為使用 SSL 的連線：

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50001 -parameter "SecurityTransportMode=SSL"`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50001`  

     其中：
     
     - `<hostname>` 是伺服器的主機名稱。
     - `<alias>` 是您選擇的別名。

   - 若為不使用 SSL 的連線：

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50000`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50000`

2. 若要啟動 CLPPlus 並連接至使用 `db2dsdriver.cfg` 檔案中項目的 {{site.data.keyword.dashdbshort_notm}} 資料庫，請執行下列指令：

   - Windows 環境： 

     `clpplus <userid>@<alias>`

   - Linux 環境：

     `clpplus -nw <userid>@<alias>`

     其中：
     
     - `<userid>` 是來自您預先收集之連接認證的使用者 ID。
     - `<alias>` 是您使用 **db2cli writecfg** 指令所建立的別名。

   執行此指令會開啟 CLPPlus 視窗。

3. 在 CLPPlus 視窗中，輸入您的密碼。即會顯示資料庫資訊，後面接著 SQL 提示。範例輸出如下：

```
   Hostname = 192.0.2.0
   Database server = DB2/LINUXX8664  SQL10054
   SQL authorization ID = smith
   Local database alias = BLUDB
   Port = 50001
   
   SQL>
```

### 結果
{: #results7}

您現在可以輸入 CLPPlus 指令或 SELECT 陳述式，然後執行 Script 來使用資料庫中的資料。

### 範例

下列範例使用簡短 Script，以從範例表格 `GOSALES.BRANCH` 中擷取列。Script 檔命名為 `cities.sql`，並且位於本端 Windows 電腦的 `C:\temp` 目錄中。`cities.sql` 檔案包含下列文字：

```
SET ECHO ON
SELECT branch_code, city from GOSALES.BRANCH;
```

#### 範例 1 

若要以互動方式執行 Script，請執行下列動作：

1. 執行下列指令，以您在 `db2dsdriver.cfg` 檔案中所建立的使用者 ID 和別名來啟動 CLPPlus：

   `clpplus <user_id>@<alias>`
2. 輸入您的密碼。
3. 在 SQL 提示中，輸入下列文字：

   `start C:\temp\cities.sql`

#### 範例 2

以您在 `db2dsdriver.cfg` 檔案中所建立的使用者 ID 和別名來啟動 CLPPlus，並以一個步驟執行 Script：

`clpplus <user_id>/<password>@<alias> @C:\temp\cities.sql`

`cities.sql` Script 的輸出範例如下：

```
BRANCH_CODE CITY
----------- --------------------------------------------------
          6 Paris
          7 Milano
          9 Amsterdam
         13 Hamburg
         14 München
         15 Kista
         17 Calgary
         18 Toronto
         19 Boston
         20 Seattle
         21 Los Angeles
         22 Miami
         23 Lyon
         24 Distrito Federal
         25 Tokyo
         26 Osaka City
         28 Melbourne
         29 Bilbao
         30 Sao Paulo
         31 Kuopio
         32 Seoul
         33 Singapore

BRANCH_CODE CITY
----------- --------------------------------------------------
         34 Shanghai
         35 London
         36 Birmingham
         37 Zürich
         38 Heverlee
         39 Wien
         40 Geneve

29 rows were retrieved.
```


