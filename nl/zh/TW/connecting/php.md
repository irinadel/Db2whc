---

copyright:
  years: 2014, 2018
lastupdated: "2018-09-25"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 使用 PHP 以程式設計方式連接

定義 PHP 應用程式與 {{site.data.keyword.dashdbshort_notm}} 資料庫之間的連線。
{: shortdesc}

## 必要條件

在嘗試連接至您的 {{site.data.keyword.dashdbshort_notm}} 資料庫之前，請驗證您是否具有必要的[必備項目](connecting.html#prereqs)。

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## 程序

### 情境 1：從 {{site.data.keyword.Bluemix_notm}} 外部連接：
        
1. 從 Web 主控台下載 [Db2 驅動程式套件](driver_pkg.html)，然後將驅動程式套件安裝在將執行 PHP 應用程式的機器上。
                
2. 使用 [`odbc_connect` 函數 ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](http://php.net/manual/en/function.odbc-connect.php){:new_window} 來連接至 BLUDB 資料庫。
    
   PHP 程式碼範例：

   ```
   <?php
   $database = "BLUDB";        # Get these database details from
   $hostname = "<Host-name>";  # the web console
   $user     = "<User-ID >";   #
   $password = "<Password>";   #
   $port     = 50000;          #
   $ssl_port = 50001;          #
   # Build the connection string
   #
   $driver  = "DRIVER={IBM DB2 ODBC DRIVER};";
   $dsn     = "DATABASE=$database; " .
              "HOSTNAME=$hostname;" .
                   "PORT=$port;" .
                   "PROTOCOL=TCPIP;" .
                   "UID=$user;" .
                   "PWD=$password;";
   $ssl_dsn = "DATABASE=$database; " .
              "HOSTNAME=$hostname;" .
                   "PORT=$ssl_port; " .
              "PROTOCOL=TCPIP;" .
                   "UID=$user;" .
                   "PWD=$password;" .
              "SECURITY=SSL;";
   $conn_string = $driver . $dsn;     # Non-SSL
   $conn_string = $driver . $ssl_dsn; # SSL
   # Connect
   #
   $conn = odbc_connect( $conn_string, "", "" );
   if( $conn )
   {
       echo "Connection succeeded.";
       # Disconnect
       #
       odbc_close( $conn );
   }
   else
   {
       echo "Connection failed.";
   }
   ?>
   ```

   將此 PHP 程式碼範例儲存至稱為 `C:\sample.php` 的 Script 檔案，然後從指令行執行此 Script 時會產生下列輸出：

   ```
   C:\> php –f sample.php

   Connection succeeded.
   ```

### 情境 2：從 {{site.data.keyword.Bluemix_notm}} 中的 PHP Web 應用程式連接

1. 從 {{site.data.keyword.Bluemix_notm}} 型錄中，建立新的 PHP 應用程式。
        
2. 從 {{site.data.keyword.Bluemix_notm}} 儀表板中新的 PHP 應用程式的「開始使用」區段中，將應用程式入門範本程式碼下載至本端工作目錄。
        
3. 在 {{site.data.keyword.Bluemix_notm}} 儀表板中，建立從 Db2 服務到新的 PHP 應用程式的新連線。（在 {{site.data.keyword.Bluemix_notm}} 中建立此「連線」可讓 PHP 應用程式能夠使用 `VCAP_SERVICES` 環境變數。`VCAP_SERVICES` 環境變數包含 Db2 服務的資料庫詳細資料。相較於將資料庫詳細資料寫在 PHP 應用程式中，使用 `VCAP_SERVICES` 更為方便）。
        
4. 在本端工作目錄中，使用 [`db2_connect` 函數 ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](http://php.net/manual/en/function.db2-connect.php){:new_window} 來更新`index.php` 檔案，以連接至 BLUDB 資料庫。
        
   範例：

   ```
   <!DOCTYPE html>
   <html>
   <head>
       <title>PHP 入門範本應用程式</title>
       <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
       <link rel="stylesheet" href="style.css" />
   </head>
   <body>
   <?php
   if( getenv( "VCAP_SERVICES" ) )
   {
       # Get database details from the VCAP_SERVICES environment variable
       #
       # *This can only work if you have used the Bluemix dashboard to 
       # create a connection from your dashDB service to your PHP App.
       #
       $details  = json_decode( getenv( "VCAP_SERVICES" ), true );
       $dsn      = $details [ "dashDB" ][0][ "credentials" ][ "dsn" ];
       $ssl_dsn  = $details [ "dashDB" ][0][ "credentials" ][ "ssldsn" ];
       # Build the connection string
       #
       $driver = "DRIVER={IBM DB2 ODBC DRIVER};";
       $conn_string = $driver . $dsn;     # Non-SSL
       $conn_string = $driver . $ssl_dsn; # SSL
       $conn = db2_connect( $conn_string, "", "" );
       if( $conn )
       {
           echo "<p>Connection succeeded.</p>";
           db2_close( $conn );
       }
       else
       {
           echo "<p>Connection failed.</p>";
       }
   } else {
echo "<p>No credentials.</p>";
   }
   ?>
   </body>
   </html>
   ```

5. 遵循 {{site.data.keyword.Bluemix_notm}} 儀表板中 PHP 應用程式的「開始使用」區段中的指示，從本端工作目錄將更新推送至 {{site.data.keyword.Bluemix_notm}}。然後在 {{site.data.keyword.Bluemix_notm}} 中重新啟動應用程式，並在瀏覽器中檢視該應用程式。


