---

copyright:
  years: 2014, 2019
lastupdated: "2018-09-25"

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

# 使用 PHP 以编程方式连接
{: #con_prog_php}

定义 PHP 应用程序与 {{site.data.keyword.dashdbshort_notm}} 数据库之间的连接。
{: shortdesc}

## 先决条件
{: #prereq101}

在尝试连接到 {{site.data.keyword.dashdbshort_notm}} 数据库之前，请验证您是否具有必需的[先决条件](/docs/services/Db2whc/connecting/connecting.html#prereqs)。

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## 过程
{: #proc101}

### 方案 1：从 {{site.data.keyword.Bluemix_notm}} 外部进行连接：
{: #scen1}

1. 通过 Web 控制台下载 [Db2 驱动程序包](/docs/services/Db2whc/connecting/driver_pkg.html)，然后在将运行 PHP 应用程序的机器上安装该驱动程序包。
                
2. 使用 [`odbc_connect` 函数 ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](http://php.net/manual/en/function.odbc-connect.php){:new_window} 连接到 BLUDB 数据库。
    
   PHP 代码示例：

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

   将此 PHP 代码示例保存到名为 `C:\sample.php` 的脚本文件中，然后通过命令行运行该脚本，这将生成以下输出：


   ```
   C:\> php –f sample.php

   Connection succeeded.
   ```

### 方案 2：从 {{site.data.keyword.Bluemix_notm}} 中的 PHP Web 应用程序进行连接
{: #scen2}

1. 在 {{site.data.keyword.Bluemix_notm}}“目录”中，创建新的 PHP 应用程序。
        
2. 在 {{site.data.keyword.Bluemix_notm}}“仪表板”中新 PHP 应用程序的“入门”部分中，将应用程序入门模板代码下载到本地工作目录。
        
3. 在 {{site.data.keyword.Bluemix_notm}}“仪表板”中，创建从 Db2 服务到新 PHP 应用程序的新连接。（在 {{site.data.keyword.Bluemix_notm}} 中创建此连接将使 `VCAP_SERVICES` 环境变量可供 PHP 应用程序使用。`VCAP_SERVICES` 环境变量包含 Db2 服务的数据库详细信息。与在 PHP 应用程序中对数据库详细信息进行硬编码相比，使用 `VCAP_SERVICES` 更方便。）
        
4. 在本地工作目录中，将 `index.php` 文件更新为使用 [`db2_connect` 函数 ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](http://php.net/manual/en/function.db2-connect.php){:new_window} 连接到 BLUDB 数据库。
        
   示例：

   ```
   <!DOCTYPE html>
   <html>
   <head>
       <title>PHP 入门模板应用程序</title>
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
   }
   else
   {
       echo "<p>No credentials.</p>";
   }
   ?>
   </body>
   </html>
   ```

5. 按照 {{site.data.keyword.Bluemix_notm}}“仪表板”中 PHP 应用程序的“入门”部分中的指示信息进行操作，将更新从本地工作目录推送到 {{site.data.keyword.Bluemix_notm}}。然后，在 {{site.data.keyword.Bluemix_notm}} 中重新启动该应用程序，并在浏览器中查看该应用程序。


