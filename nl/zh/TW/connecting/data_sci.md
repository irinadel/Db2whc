---

copyright:
  years: 2014, 2019
lastupdated: "2018-10-15"

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

# 資料科學
{: #ds}

您也可以將外部應用程式和工具連接到 {{site.data.keyword.dashdbshort_notm}}，並使用它們進一步管理或分析您的資料。
{: shortdesc}

## Watson Studio
{: #watson_studio}

在 IBM Watson Studio（先前稱為 Data Science Experience）中建立專案之後，您可以將資料資產新增至其中，以便能夠使用資料。專案中的所有合作人員都會自動獲得授權，以存取專案中的資料。
{: shortdesc}

您如何新增資料以及您可以從何處新增資料，在舊式專案與 IBM Watson 專案之間有所不同。IBM Watson 專案會使用 {{site.data.keyword.Bluemix_notm}} Object Storage。如果專案使用 Object Storage OpenStack Swift，則為舊式專案。 

### 若要在 IBM Watson 專案中建立新連線，請執行下列動作：

1. 按一下**新增至專案 > 連線**。
    
2. 選擇資料來源。
    
3. 輸入資料來源所需的連線資訊。通常，您需要提供主機、埠號、使用者名稱及密碼之類的資訊。
    
4. 您可以探索從連線到 {{site.data.keyword.dashdbshort_notm}} 的資產，這可讓您將連線中的所有表格，作為資料資產新增至專案。選取**探索資料資產**，然後選擇專案。
    
5. 按一下**建立**。連線即會出現在**資產**頁面上。

觀看此視訊以查看如何建立連線並將連接的資料新增至專案。

<iframe class="embed-responsive-item" id="youtubeplayer" title="建立連線並將連接的資料新增至專案" type="text/html" width="640" height="390" src="//www.youtube.com/embed/U7-gCbo4QtM?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

### 若要在舊式專案中建立新連線，請執行下列動作：

1. 從專案的**資產**頁面中，按一下**尋找並新增資料**圖示。
    
2. 在**連線**窗格上，按一下**建立連線**。

3. 輸入名稱及說明，並選擇「服務種類」：

   **資料服務** = {{site.data.keyword.Bluemix_notm}} 資料服務

   當您選擇**資料服務**時，現有的 {{site.data.keyword.Bluemix_notm}} 資料服務會出現在**服務實例**清單中。

4. 從清單中選擇服務或資料庫伺服器。

5. 輸入連線資訊：

   當您選擇**資料服務**時，現有的 {{site.data.keyword.Bluemix_notm}} 資料服務會出現在**服務實例**清單中。
    
6. 按一下**建立**。所有舊式專案都可以使用連線。
    
7. 在**連線**窗格上，選取連線並按一下**套用**。

若要將現有連線新增至舊式專案，請執行下列動作：

1. 從專案的**資產**頁面中，按一下**尋找並新增資料**圖示。
    
2. 在**連線**窗格上，選取連線並按一下**套用**。

## SPSS Statistics
{: #spss_stats}

這些指示說明如何建立從 IBM® SPSS® Statistics 到 {{site.data.keyword.dashdbshort_notm}} 資料庫的連線。
{: shortdesc}

### 必要條件
{: #prereq1}

在嘗試連接至您的 {{site.data.keyword.dashdbshort_notm}} 資料庫之前，請驗證您是否具有必要的[必備項目](connecting.html#prereqs)。

### 程序
{: #proc1}

1. 在 SPSS Statistics 中，按一下**檔案 > 開啟資料庫 > 新建查詢**。
    
2. 在「資料庫精靈」中，按一下**新增 ODBC 資料來源**。
    
3. 使用「ODBC 資料來源管理員」視窗，來新增 {{site.data.keyword.dashdbshort_notm}} 資料庫的 ODBC 資料來源名稱 (DSN)：
        
   a. 在**使用者 DSN** 標籤上，按一下**新增**。

   b. 在「建立新的資料來源」視窗上，選取名稱為 **IBM DB2 ODBC DRIVER** 的驅動程式，然後按一下**完成**。

   確定您選取的驅動程式不是具有類似名稱的驅動程式，例如 `IBM DB2® ODBC DRIVER - DB2COPY`。如果該驅動程式未顯示在清單中，請結束 SPSS Statistics，然後下載並安裝驅動程式。請參閱 [Db2 驅動程式套件](driver_pkg.html)。
        
   c. 在「ODBC IBM 驅動程式 - 新增」視窗中，輸入資料來源名稱（通常是您要連接的資料庫名稱），然後按一下**新增**。
        
   d. 從「CLI/ODBC 設定」視窗中，在**資料來源**標籤上，輸入您預先收集的[連線資訊](credentials.html)中的使用者 ID 及密碼。
        
   e. 在「進階設定」頁面上，針對下列每一個參數，按一下**新增**以開啟「新增 CLI 參數」視窗來開始步驟，然後按一下**確定**以回到「進階設定」頁面：
            
   - 選取 `Database` 參數，然後按一下**確定**以開啟「CLI/ODBC 設定」視窗。在**擱置值**欄位中，輸入您預先收集的連線資訊中的資料庫名稱。

   - 選取 `Hostname` 參數，然後按一下**確定**以開啟「CLI/ODBC 設定」視窗。在**擱置值**欄位中，輸入您預先收集的連線資訊中的主機名稱。

   - 選取 `Port` 參數，然後按一下**確定**以開啟「CLI/ODBC 設定」視窗。在**擱置值**欄位中，輸入您預先收集的連線資訊中的埠號。
            
   - 選取 `Protocol` 參數，然後按一下**確定**以開啟「CLI/ODBC 設定」視窗。選取 **TCP/IP**。
        
   f. 按一下**確定**以回到「ODBC 資料來源管理員」視窗。
        
   g. 在**使用者 DSN** 標籤上，選取資料來源名稱，然後按一下**配置**。
        
   h. 在「CLI/ODBC 設定」視窗上，按一下**連接**以測試連線。
            
   - 如果連線成功，請按一下**確定**以回到「ODBC 資料來源管理員」視窗，然後按一下**確定**以結束視窗。
            
   - 如果連線不成功，請先記下並更正任何錯誤，再重新測試連線。

## SAS
{: #sas}

這些指示說明如何建立從 SAS 到 {{site.data.keyword.dashdbshort_notm}} 資料庫的連線。
{: shortdesc}

### 必要條件
{: #prereq2}

在嘗試連接至您的 {{site.data.keyword.dashdbshort_notm}} 資料庫之前，請驗證您是否具有必要的[必備項目](connecting.html#prereqs)。

### 程序
{: #proc2}

如需如何從 SAS 連接至 {{site.data.keyword.dashdbshort_notm}} 資料庫的步驟，請參閱 SAS 文件：
- [UNIX 及 PC 主機下 Db2 的 SAS/ACCESS 介面 ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](https://documentation.sas.com/?docsetId=acreldb&docsetTarget=p1dzq4zjg1iycgn16l4xj9nnvibt.htm&docsetVersion=9.4&locale=en){:new_window}

## R 開發環境
{: #r_dev_env}

您可能喜好使用自己本端安裝的 R 開發環境，而非使用 IBM Watson Studio 內整合的 RStudio® 環境。例如，您可能有自己的 RStudio 安裝，或者喜好使用某些其他開發工具，例如 Rcmdr 或 Rendo。這些指示說明如何將 R 開發環境連接至 {{site.data.keyword.dashdbshort_notm}} 資料庫。
{: shortdesc}

### 必要條件
{: #prereq3}

在嘗試連接至您的 {{site.data.keyword.dashdbshort_notm}} 資料庫之前，請驗證您是否具有必要的[必備項目](connecting.html#prereqs)。

### 程序
{: #proc3}

1. 在本端 R 環境中，輸入下列指令，以安裝 `ibmdbR` 套件：

   `install.packages("ibmdbR")`

   本端 R 環境會存取「綜合性 R 保存網路 (CRAN)」，並自動下載及安裝 `ibmdbR` 套件以及任何尚未安裝的必備套件。
    
2. 在 R 開發環境與 {{site.data.keyword.dashdbshort_notm}} 資料庫之間建立 ODBC 驅動程式連線：
        
   a. [將資料庫設為 ODBC 資料來源 ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_cli_and_odbc_applications.html){:new_window}。
        
   b. 開啟本端安裝的 R 開發環境。
        
   c. 在 R 提示中，輸入下列陳述式來建立連線。將位置保留元取代為預先收集的[連線資訊](credentials.html)。

   - 如果本端安裝的 R 開發環境執行於 {{site.data.keyword.dashdbshort_notm}} 資料庫中：

     ```
     library(ibmdbR)
     host.name <- "placeholderForYourHostName"
     port <-"placeholderForPortNumber" # 50000 if not using SSL or 50001 if using SSL
     user.name <-"placeholderForYourUserName"
     pwd <- "placeholderForYourPassword"
     con.text <- paste("placeholderForYourDSNName;DRIVER=BLUDB",
                       ";Database=BLUDB",
                       ";Hostname=",host.name,
                       ";Port=",port,
                       ";PROTOCOL=TCPIP",
                       ";UID=", user.name,
                       ";PWD=",pwd,sep="")
     # Connect to using a odbc Driver Connection string to a remote database
     con <- idaConnect(con.text)
     ```

   - 如果本端安裝的 R 開發環境未執行於 {{site.data.keyword.dashdbshort_notm}} 資料庫中：

     ```
     library(ibmdbR)
     driver.name <- "{placeholderForYourDriverName}"
     db.name <- "placeholderForYourDatabaseName"
     host.name <- "placeholderForYourHostName"
     port <-"placeholderForYourPort"
     user.name <-"placeholderForYourUserName"
     pwd <- "placeholderForYourPassword"
     con.text <- paste("placeholderForYourDSNName;DRIVER=",driver.name,
                       ";Database=",db.name,
                       ";Hostname=",host.name,
                       ";Port=",port,
                       ";PROTOCOL=TCPIP",
                       ";UID=", user.name,
                       ";PWD=",pwd,sep="")
     # Connect to using a odbc Driver Connection string to a remote database
     con <- idaConnect(con.text)
     ```

     **附註**：用來建立連線物件的陳述式，會使用 `idaConnect()` 方法，而不是 `odbcConnect()` 或 `odbcDriverConnect()` 方法。
        
   d. 發出下列 R 指令，以起始設定分析套件：

   `idaInit(con)`

   e. 若要測試連線是否可運作，請發出下列 R 指令：

   `idaShowTables()`

   主控台會顯示現行綱目中所有表格及視圖的清單。

