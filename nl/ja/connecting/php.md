---

copyright:
  years: 2014, 2019
lastupdated: "2018-09-25"

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

# PHP でのプログラマチック接続
{: #con_prog_php}

PHP アプリケーションと {{site.data.keyword.dashdbshort_notm}} データベースの間の接続を定義します。
{: shortdesc}

## 前提条件
{: #prereq101}

{{site.data.keyword.dashdbshort_notm}} データベースへの接続を試行する前に、必要な[前提条件](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs)を満たしていることを確認します。

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## 手順
{: #proc101}

### シナリオ 1: {{site.data.keyword.Bluemix_notm}} の外部からの接続:
{: #scen1}

1. Web コンソールから [Db2 ドライバー・パッケージ](/docs/services/Db2whc?topic=Db2whc-dr_pkg#dr_pkg)をダウンロードして、PHP アプリケーションが実行されるマシンにドライバー・パッケージをインストールします。
                
2. [`odbc_connect` 関数](http://php.net/manual/en/function.odbc-connect.php){:external}を使用して BLUDB データベースに接続します。
    
   次に PHP コードの例を示します。

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
              "PORT=$port; " .
              "PROTOCOL=TCPIP; " .
              "UID=$user;" .
              "PWD=$password;";
   $ssl_dsn = "DATABASE=$database; " .
              "HOSTNAME=$hostname;" .
              "PORT=$ssl_port; " .
              "PROTOCOL=TCPIP; " .
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

   この PHP コードの例を `C:\sample.php` と呼ばれるスクリプト・ファイルに保存してから、スクリプトをコマンド・ラインから実行すると、以下の出力が作成されます。

   ```
   C:\> php –f sample.php

   Connection succeeded.
   ```

### シナリオ 2: {{site.data.keyword.Bluemix_notm}} での PHP Web アプリからの接続
{: #scen2}

1. {{site.data.keyword.Bluemix_notm}} カタログから、新しい PHP アプリを作成します。
        
2. {{site.data.keyword.Bluemix_notm}} ダッシュボード内の新しい PHP アプリの「開始」セクションから、アプリのスターター・コードをローカル作業ディレクトリーにダウンロードします。
        
3. {{site.data.keyword.Bluemix_notm}} ダッシュボードで、Db2 サービスから新しい PHP アプリへの新しい接続を作成します。 ({{site.data.keyword.Bluemix_notm}} でこの接続を作成すると、PHP アプリに `VCAP_SERVICES` 環境変数を使用できるようになります。 `VCAP_SERVICES` 環境変数には、Db2 サービスに関するデータベースの詳細が含まれています。 `VCAP_SERVICES` を使用する方が、PHP アプリ内でデータベースの詳細をハードコーディングするより便利です。)
        
4. ローカル作業ディレクトリーで、[`db2_connect` 関数](http://php.net/manual/en/function.db2-connect.php){:external}を使用して BLUDB データベースに接続するように、`index.php` ファイルを更新します。
        
   次に例を示します。

   ```
   <!DOCTYPE html>
   <html>
   <head>
       <title>PHP スターター・アプリケーション</title>
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

5. ローカル作業ディレクトリーから、{{site.data.keyword.Bluemix_notm}} ダッシュボード内の PHP アプリの「開始」セクションの指示に従って、更新内容を {{site.data.keyword.Bluemix_notm}} にプッシュします。 それから、{{site.data.keyword.Bluemix_notm}} でアプリを再始動し、ブラウザーでアプリを表示します。


