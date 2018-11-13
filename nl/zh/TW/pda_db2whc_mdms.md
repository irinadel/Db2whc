---

copyright:
  years: 2014, 2018
lastupdated: "2018-06-15"

---

<!-- Attribute definitions -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 從 IBM PureData System for Analytics 移轉 (Netezza)
{: #pda}

{{site.data.keyword.Bluemix_notm}} IBM Cloud Mass Data Migration Service (MDMS) 可以用來將資料從大型 IBM PureData Systems for Analytics (Netezza) 資料庫（大約 25 TB 及更大）移轉至 {{site.data.keyword.Bluemix_notm}} 上完全管理的 {{site.data.keyword.dashdblong}} 資料庫。

MDMS 提供一種快速、簡單、安全方式，將多個 TB 到多個 PB 的資料實際傳送至 {{site.data.keyword.Bluemix_notm}}。MDMS 是可用儲存空間容量為 120 TB 的行動儲存裝置。此裝置可讓您克服常見的傳送挑戰，像是高成本、冗長的傳送時間及安全顧慮 - 全部只需單一服務即可解決。
{: shortdesc}

![Mass Data Migration Service 裝置的視圖](images/mdms.svg)

## 要求裝置時，您將需要什麼
{: #prereq}

1. 儲存裝置的網路設定
   - 靜態 IP 位址
   - 啟用資料傳送的網路遮罩
2. 遠端電腦的網路設定
   - 靜態 IP 位址
   - 網路遮罩 
   - 存取使用者介面 (UI) 的預設閘道
3. Cloud Object Storage 下載目的地<br/>
   **重要事項**：您在美國跨區域或美國南部位置必須至少具有一個 {{site.data.keyword.cos_full}} 帳戶及一個儲存區，才能完成要求表單。如果您尚未有 {{site.data.keyword.cos_full_notm}} 帳戶，請先建立一個，再要求 MDMS 裝置。如需相關資訊，請參閱：[關於 {{site.data.keyword.cos_full}}](/docs/services/cloud-object-storage/about-cos.html){:new_window}。

## 步驟 1：建立要求
{: #create-req}

1. 使用唯一認證來登入 [{{site.data.keyword.slportal}} ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://control.softlayer.com/){:new_window}。
2. 從「導覽列」中選取 **儲存空間 > 資料移轉 > Mass Data Migration**，來存取 MDMS 登陸頁面。
3. 按一下**要求裝置**，以開啟訂單表單。
4. 完成 **Mass Data Migration** 訂單表單中的每一個欄位。
   - **出貨地址**：不會預先填寫此表單，而且每個欄位皆可編輯。請在「注意」欄位中提供將接受裝置交付之人員的名稱。當挑選交付位置時，請考量裝置的重量（含盒子重達 30 公斤，或 66 磅）及可存取性。<br/> （**附註**：裝置配備滑輪與操作用的彈出式把手。）
   - **重要移轉聯絡人**：不會預先填寫此表單。每一個欄位都可編輯。可以新增多個人員。
   - **資料中心網路配置**：提供在裝運之前於 MDMS 裝置上預先佈建 Eth3 埠的網路配置詳細資料。
   - **資料卸載目的地**：從清單中選取現有的目標帳戶。
   - **要求名稱**：輸入名稱以協助您追蹤訂單。
5. 在閱讀每一個提供的服務合約之後，選取**我已閱讀並同意 Mass Data Migration 合約的完整條款**勾選框。
6. 按一下**提交要求**以提交要求。按一下**取消**，以完全放棄表單並回到 MDMS 登陸頁面。

## 步驟 2：準備與出貨
{: #prep-ship}

在提交要求之後，要求問題單的狀態會顯示為*正在處理要求*。當您的要求完成處理時，{{site.data.keyword.IBM}} 會開始預先配置下一個可用裝置，而且[要求 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://control.softlayer.com/storage/mdms){:new_window} 網格上的狀態將顯示*正在準備裝置*，後面跟著*正在等待出貨*。在要求進入*正在等待出貨* 狀態之後，再也無法取消它。 

裝置會由運輸者收取，以運送至您的位置。此時，要求狀態會更新為*裝置已出貨*。追蹤號碼是在[要求 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://control.softlayer.com/storage/mdms){:new_window} 網格的**訂單詳細資料**區段中與您共用。

## 步驟 3：接收與連接
{: #rec-con}

<!-- **[Editor's note: What to keep from this section immediately below?]**

&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
1. The device arrives pre-configured for you. Basic [powering/connectivity instructions](docs/infrastructure/mass-data-migration/user-instructions.html) are included.  **[Editor's note: Are the instructions included in the MDMS package? If so, are they different from the instructions found with the "powering/connectivity" link?]**<br/>
  **Note**: User name and storage pool password is provided separately. Check the **Request Details** in your [Requests ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://control.softlayer.com/storage/mdms){:new_window} grid for the credentials.
2. Point your browser to the static IP address that you provided in the order form. **[Editor's note: Is this done on PDA? What system is the static IP address for?]**
3. Log in. Enter password to unlock the empty storage pool. **[Editor's note: How is this done?]**<br/>
   **Note**: See the **Request Details** of your [Requests ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://control.softlayer.com/storage/mdms){:new_window} grid for the password.
4. Mount the NFS share on your server. **[Editor's note: How is this done?]**
5. Rerun your DataShuttle inventory to ensure any new files are captured. **[Editor's note: Is "DataShuttle inventory" a command that is run on PDA?]**

&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& -->

### 概觀

{{site.data.keyword.cloud}} Mass Data Migration 裝置是可攜式儲存裝置，能夠呈現可裝載的「網路檔案系統 (NFS)」或「FileNet 內容聯合服務 (CFS)」共用，並透過 Web 瀏覽器介面來管理。裝置會運輸至您的資料中心、載入站上資料、回到 {{site.data.keyword.BluSoftlayer_full}} 資料中心，然後您的資料會載入至您的 {{site.data.keyword.cos_full}} 帳戶。

### 電源

裝置隨附有 C13-US 電源線 ([IEC 60320 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://en.wikipedia.org/wiki/IEC_60320){:new_window})。如果在美國以外的地區使用裝置，則可能需要電源配接卡。

MDMS 裝置接受所有標準電源範圍。![電源範圍](/images/PowerRating.png)

### 乙太網路連線功能

有兩個要建立的乙太網路連線。一個用於透過瀏覽器進行裝置管理，另一個用於在來源資料所在的相同子網路上進行資料移動。

這兩個埠都來自裝置，如 RJ45，並提供 CAT6A 纜線。提供銅線 SFP+ 配接器，以從 RJ45 轉換。配接卡可與所有交換器製造商搭配使用。這些配接卡位於出貨蓋下方的口袋中。

- Eth1 (1GbE-B) 用於裝置管理，因此必須在 IP 位址配置中指定閘道。在開啟裝置電源之後，可在 LCD 螢幕上檢視此項（請參閱 [IP 位址配置](#ip_cfg)一節）。

- Eth3 (10GbE-B) 用於資料傳送。此連線必須與來源資料位於相同的子網路上，或在需要時可以直接連接至伺服器。

如果需要乙太網路連線的不同表單係數，則您必須提供轉換器。

### 逐步使用者指示

1. MDMS 裝置送達時會預先配置您的 IP 位址、使用者名稱、鎖定的儲存區，以及 NFS 共用。使用者密碼及儲存區密碼將透過個別的電子郵件傳達。

2. 決定裝置的最佳擺放位置；在該處，它應可連接電源及乙太網路（1GbE 及 10GbE）連線，而且附近人潮流量最少。

3. 讓裝置就定位以便連接。使用期間它可以留在運輸盒中。確定裝置處於室溫，且其上沒有凝結情況。使用盒蓋下方提供的電源線來連接電源。開啟裝置電源。<br/>
    **附註**：有兩個電源交換器。
    ![電源交換器](/images/MDMSPowerSwitch.png)
    **附註**：不需要從可攜式盒子中取出裝置。

4. 從盒蓋中取下 CAT6A 纜線，並將它連接至圖片中顯示的 Eth3 (10GbE-B) 埠。
    ![Eth1 及 Eth3 埠位置](/images/MDMSNewEth1and3.png)

5. 將提供的 CAT6A 連接至 SFP+ 配接卡，並連接至 10Gb 交換器。

6. 如果可以透過瀏覽器 `https://<your_Eth3_IP_Address>` 到達針對 Eth3 配置的 IP 位址，請繼續下一步。 

   否則，連接至 Eth1 (1GbE-B) 埠。開啟您的瀏覽器，並輸入 `https://<your_Eth1_IP_Address>`。輸入適合於網路配置的 Eth1 IP 位址。接受憑證條款。<br/>
   **附註**：如果您需要變更 Eth3 或 Eth1 的任何 IP 設定，請參閱 [IP 位址配置](#ip_cfg)一節。

7. 使用提供的使用者名稱及密碼來登入。<br/>
    ![登入頁面](/images/Login.png)

8. 工作流程精靈會從左至右依序呈現常用特定項目的存取。<br/>
    ![工作流程圖示](/images/workflow.png) <br/>
    **附註**：可以使用 GUI 左上方的**工作流程管理程式**來重新開啟工作流程。

9. 啟動預先配置的儲存區：
    - 按一下**解除鎖定並啟動儲存區**。
    - 輸入您的「儲存區通行詞組」，然後按一下**確定**。
    ![啟動儲存區](/images/UnlockPool.png)

10. 依預設，共用已同時啟用 NFS 及 SMB 通訊協定，且對共用沒有設下任何存取限制。若要限制存取此共用（適用於 NFS 或 SMB），請在共用名稱上按一下滑鼠右鍵並選取適當的功能表項目。<br/>
    ![限制共用存取](/images/ShareControls.png)

11. 啟用儲存區時，NFS 共用即可用來進行裝載。在工作流程中，按一下**檢視網路共用**，以查看網路共用視圖。關閉工作流程、在共用上按一下滑鼠右鍵，然後選取**檢視裝載指令**，以查看共用名稱及裝載資訊。在您的來源伺服器上裝載共用。裝載共用時，務必指定 10 GB 鏈結的 IP 位址。
    ![裝載共用](/images/MountCommand.png)

## 步驟 4：複製資料與出貨
{: #copy-ship}

<!-- &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&

1. Run the DataShuttle copy to move the data. **[Editor's note: What is "DataShuttle"? Is "DataShuttle copy" a command that is run on PDA?]**

&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& -->

1. 將您的資料複製到 NFS 共用。請選擇下列其中一種方法，從 Netezza 資料庫中擷取您的資料：
    1. 執行 **nz_backup** 公用程式的下列範例：

       `/nz/support/contrib/bin/nz_backup –db <db_name> –d <target_directory>  ascii threads 4`

       **附註**：`<target_directory>` 是 MDMS 裝置上裝載至 Netezza 伺服器的 NFS 共用。
   
    2. 執行 CREATE EXTERNAL TABLE 陳述式的下列範例：

       `CREATE EXTERNAL TABLE '<path_to_mdms_device>/<file_name>' SELECT * FROM <table name>`

       **附註：**如果您已使用 `USING` 子句選項進行資料匯出，請記住或儲存子句選項。稍後在從 {{site.data.keyword.Bluemix_notm}} Object Storage 進行外部表格載入處理程序期間會重複使用此子句。

       如需 SQL 陳述式的相關資訊，請參閱：[CREATE EXTERNAL TABLE 陳述式 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.sql.ref.doc/doc/r_create_ext_table.html){:new_window}。 

<!--       - Provide the {{site.data.keyword.Bluemix_notm}} team with the "USING" clause that was used for data export. The clause is reused during the load process on {{site.data.keyword.Bluemix_notm}}.
       - Select FORMAT = "Text"
-->

2. 在工作流程中，當資料傳送至 10Gb/秒鏈結上的裝置時，請按一下**檢視網路活動**，在 GUI 中顯示入埠乙太網路負載。
    ![檢視活動](/images/UserGuide13.png)

3. 在工作流程中，按一下**檢視儲存區**，來監視裝置上的儲存空間使用量及 IOPS。
    ![檢視儲存區](/images/UserGuide14.png)

4. 複製完成時，溫和地關閉系統電源。關閉裝置電源也會鎖定儲存區。在工作流程中，按一下**關閉應用裝置...**。  
    ![應用裝置關機使用者介面按鈕位置](/images/Shutdown.png)

5. 中斷連接裝置。將電源線、乙太網路纜線及 SFP+ 配接卡放回蓋子下的個別儲存位置。

6. 將提供的出貨標籤貼到裝置上。通知出貨者並將裝置退還給「{{site.data.keyword.BluSoftlayer_full}} 資料中心」。在送達資料中心之後，您的資料便會載入至 {{site.data.keyword.cos_full_notm}} 儲存區。

在裝置退還給 {{site.data.keyword.BluSoftlayer}} 團隊之後，要求狀態會變更為*已收到裝置*。

## 步驟 5：卸載與存取
{: #offload}

在資料傳送過程中，要求狀態會顯示為*正在卸載資料*。當移轉至 {{site.data.keyword.objectstorageshort}} 儲存區完成時，狀態會再次變更（*卸載完成*）。當高速卸載至 Cloud Object Storage 儲存區的作業完成時，便可以立即存取您的資料。 

當您的資料移轉至 Cloud Object Storage 儲存區完成時，可以繼續[將您的資料匯入至您的 {{site.data.keyword.dashdbshort_notm}} 資料庫](#import)。

## 步驟 6：從 {{site.data.keyword.Bluemix_notm}} Object Storage 匯入資料
{: #import}

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

**附註：** 
* 確定使用您已用來從 PureData System for Analytics (Netezza) 資料庫擷取資料的相同 `USING` 子句選項，方法為使用 CREATE EXTERNAL TABLE 陳述式。
* 若為 {{site.data.keyword.Bluemix_notm}} Object Storage，若要在建立新的服務認證時建立 HMAC 認證，請在*新增線型配置參數*欄位中指定 {"HMAC:true"}。

如需從 {{site.data.keyword.Bluemix_notm}} Object Storage 匯入資料的引導式指導教學，請參閱 [IBM Db2 Warehouse on Cloud 引導示範：探索資料載入 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/cloud/garage/demo/try-db2-warehouse-cloud/){:new_window}。

## 步驟 7：消除 MDMS 裝置
{: #erase}

{{site.data.keyword.IBM}} 會實作美國國防部需求層次的資料抹除，從 MDMS 裝置中永久地消除您的資料。完成時，您的要求狀態會顯示為*消除完成*。

## 其他附註
{: #notes}

### 儲存區中的唯一性

若要在物件名稱複製到儲存區時確保它們是唯一的，請包括檔案路徑作為物件名稱中的字首。例如，`/root/user/` 資料夾中的 config.ini 檔案在複製到儲存區時會重新命名為 "root/user/config.ini"。

### 儲存區

如果目標儲存區不存在，則會建立一個。如果它確實存在，則必須是空的，否則複製無法繼續進行。

### 檔案系統

在掃描過程中會跳過系統鏈結及固定鏈結。

### IP 位址配置
{: #ip_cfg}

裝置上的 LCD 顯示器可以用來配置乙太網路埠的 IP 位址。您可以使用**上移鍵**、**下移鍵**、**esc** 及 **enter** 按鈕，在 LCD 顯示器中導覽。**enter** 按鈕會將您帶至功能表，而 **esc** 會將您帶離功能表。

![LCD 顯示器](/images/MDMSLCD.png)

編輯 IP 位址或子網路遮罩時，**enter** 會讓您一次前進一個字元；**esc** 會讓您一次後退一個字元。**上移鍵**及**下移鍵**可切換所選取位置的號碼。

使用 **esc** 可讓您回到先前功能表。  

移至**更新...** 功能表項目，並按 **enter** 來儲存設定。
