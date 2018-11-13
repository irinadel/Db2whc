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

# PHP를 사용하여 프로그래밍 방식으로 연결

PHP 애플리케이션과 {{site.data.keyword.dashdbshort_notm}} 데이터베이스 간의 연결을 정의합니다.
{: shortdesc}

## 전제조건

{{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하기 전에 먼저 필수 [전제조건](connecting.html#prereqs)이 있는지 확인하십시오.

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## 프로시저

### 시나리오 1: {{site.data.keyword.Bluemix_notm}} 외부에서 연결:
        
1. 웹 콘솔에서 [Db2 드라이버 패키지](driver_pkg.html)를 다운로드한 다음 PHP 애플리케이션이 실행되는 시스템에 드라이버 패키지를 설치하십시오.
                
2. [`odbc_connect` 함수 ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](http://php.net/manual/en/function.odbc-connect.php){:new_window}를 사용하여 BLUDB 데이터베이스에 연결하십시오.
    
   PHP 코드 예:

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

   이 PHP 코드 예를 `C:\sample.php`라는 스크립트 파일에 저장한 다음 명령행에서 스크립트를 실행하면 다음 출력이 생성됩니다.


   ```
   C:\> php –f sample.php

   Connection succeeded.
   ```

### 시나리오 2: {{site.data.keyword.Bluemix_notm}} 내의 PHP 웹 앱에서 연결

1. {{site.data.keyword.Bluemix_notm}} 카탈로그에서 새 PHP 앱을 작성하십시오.
        
2. {{site.data.keyword.Bluemix_notm}} 대시보드에 있는 새 PHP 앱의 "시작하기" 섹션에서 앱 스타터 코드를 로컬 작업 디렉토리에 다운로드하십시오.
        
3. {{site.data.keyword.Bluemix_notm}} 대시보드에서, Db2 서비스에서 새 PHP 앱으로 새 연결을 작성하십시오. ({{site.data.keyword.Bluemix_notm}} 내에서 이 연결을 작성하면 `VCAP_SERVICES` 환경 변수를 사용자의 PHP 앱에서 사용할 수 있습니다. `VCAP_SERVICES` 환경 변수에는 Db2 서비스에 대한 데이터베이스 세부사항이 포함되어 있습니다. `VCAP_SERVICES`를 사용하는 것이 PHP 앱에서 데이터베이스 세부사항을 하드 코딩하는 것보다 편리합니다.)
        
4. 로컬 작업 디렉토리에서 [`db2_connect` 함수 ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](http://php.net/manual/en/function.db2-connect.php){:new_window}를 사용하여 BLUDB 데이터베이스에 연결하기 위해 `index.php` 파일을 업데이트하십시오.
        
   예:

   ```
   <!DOCTYPE html>
   <html>
   <head>
       <title>PHP Starter Application</title>
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

5. 로컬 작업 디렉토리에서 {{site.data.keyword.Bluemix_notm}} 대시보드에 있는 PHP 앱에 대한 "시작하기" 섹션의 지시사항을 수행하여 {{site.data.keyword.Bluemix_notm}}에 업데이트를 푸시하십시오. 그런 다음 {{site.data.keyword.Bluemix_notm}}에서 앱을 다시 시작하고 브라우저에서 앱을 보십시오.


