---

copyright:
  years: 2014, 2018
lastupdated: "2018-02-09"

---

<!-- Attribute definitions --> 
{:javascript: #javascript .ph data-hd-programlang='javascript'}
{:java: #java .ph data-hd-programlang='java'}
{:ruby: #ruby .ph data-hd-programlang='ruby'}
{:php: #php .ph data-hd-programlang='php'}
{:python: #python .ph data-hd-programlang='python'}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:pre: .pre}

# 시작하기
{: #getting_started}

{{site.data.keyword.dashdblong}} 관리 서비스는 클라우드에서 사용자를 위해 프로비저닝된 SQL 데이터베이스입니다. 데이터베이스 소프트웨어를 사용하는 것과 동일하게 Db2 웨어하우스를 사용할 수 있지만, 하드웨어 설정이나 소프트웨어 설치 및 관리에 대한 오버헤드와 비용이 없습니다. 
{: shortdesc}

## 무료 평가판
{: #freetrial}

최대 1GB의 저장 공간을 갖춘 {{site.data.keyword.dashdbshort_notm}} 엔트리 플랜을 무료로 사용할 수 있습니다. [무료 평가판 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.bluemix.net/catalog/services/dashdb){:new_window}

## 인터페이스
{: #interfaces}

다음과 같은 방법으로 웨어하우스 데이터베이스 관련 작업을 수행할 수 있습니다.
{: shortdesc}

   * 웹 콘솔에서
   * REST API
   * 로컬 컴퓨터에서 애플리케이션 또는 선호하는 도구 연결
   * {{site.data.keyword.Bluemix_notm}} 앱 또는 서비스의 데이터 소스로 {{site.data.keyword.dashdbshort_notm}} 사용

### 웹 콘솔
{: #web_console}

웹 콘솔은 데이터베이스를 사용하는 데 필요한 모든 기능(로드 기능, SQL 편집기, 드라이버 다운로드 등)에 대한 그래픽 인터페이스를 제공합니다.
{: shortdesc}

![웹 콘솔 대시보드 페이지의 보기](images/console_v3.png)

<!-- Click the link to take a tour of the {{site.data.keyword.dashdbshort_notm}} for Analytics web console: [General tour ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://ibm.biz/dashdb-general-quick-tour){:new_window}. -->

다음과 같은 방법으로 웹 콘솔에 액세스할 수 있습니다.
   * {{site.data.keyword.Bluemix_notm}} 대시보드를 통해 - {{site.data.keyword.dashdbshort_notm}} 서비스의 서비스 세부사항 페이지에서 웹 콘솔을 열 수 있습니다.
   * 직접 URL - {{site.data.keyword.dashdbshort_notm}} 서비스의 웹 콘솔 URL에 책갈피를 지정할 수 있습니다.

### REST API
{: #api}

{{site.data.keyword.dashdbshort_notm}} 서비스 플랜을 사용하는 경우 [{{site.data.keyword.dashdbshort_notm}} REST API ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://ibm.biz/dashdb-api){:new_window}를 사용하여 파일 관리, 데이터 로드 및 R 스크립트 실행과 관련된 태스크를 수행할 수 있습니다.
{: shortdesc}

### 로컬 컴퓨터에서 애플리케이션 또는 선호하는 도구 연결
{: #connect_apps}

다음 단계를 완료하여 Db2 웨어하우스 데이터베이스에 연결하기 위한 로컬 환경을 구성하십시오.
{: shortdesc}

1. Db2 Warehouse on Cloud 웹 콘솔에서 [드라이버 패키지 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_driver_package.html){:new_window}를 다운로드하십시오.
2. 앱 또는 도구가 실행 중인 컴퓨터에서 [드라이버 패키지 설치 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_driver_package_install.html){:new_window}를 수행하십시오.
3. Db2 웨어하우스 데이터베이스에 대해 [드라이버 파일 구성 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/support/knowledgecenter/en/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_driver_package_config.html){:new_window}을 수행하십시오.

### {{site.data.keyword.Bluemix_notm}} 앱 또는 서비스의 데이터 소스로 Db2 Warehouse on Cloud 사용
{: #data_src}

{{site.data.keyword.Bluemix_notm}}에서 호스팅되는 앱은 로컬 애플리케이션을 {{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하는 것과 동일한 방식으로 {{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결할 수 있습니다.
{: shortdesc}

앱이 {{site.data.keyword.Bluemix_notm}} 플랫폼을 사용할 때 `VCAP _SERVICES` 환경 변수를 이용하여 데이터베이스 세부사항 및 신임 정보를 지정하는 태스크를 단순화할 수 있습니다.
1. {{site.data.keyword.Bluemix_notm}} 대시보드에 있는 {{site.data.keyword.dashdbshort_notm}} 서비스를 위한 서비스 세부사항 페이지의 **연결** 탭에서 **연결 작성** 단추를 클릭하십시오.
2. {{site.data.keyword.dashdbshort_notm}} 데이터베이스에 데이터 소스로 사용할 {{site.data.keyword.Bluemix_notm}} 앱을 선택한 다음 **연결** 단추를 클릭하십시오.
3. 애플리케이션 코드를 업데이트하여 `VCAP_SERVICES` 환경 변수에서 데이터베이스 세부사항 및 신임 정보를 검색하십시오.

    **`VCAP_SERVICES`가 없는 예제**

    ```php
    <?php
    $driver      = "DRIVER={IBM DB2 ODBC DRIVER};";

    $database    = "BLUDB";         # Get these database details from
    $hostname    = "<Host-name>";   # the Connection info page of the
    $port        = 50000;           # web console.
    $user        = "<User-ID >";    #
    $password    = "<Password>";    #
    $dsn         = "DATABASE=$database;" .
                   "HOSTNAME=$hostname;" .
                   "PORT=$port;" .
                   "PROTOCOL=TCPIP;" .
                   "UID=$user;" .
                   "PWD=$password;";

    $conn_string = $driver . $dsn;

    $conn        = db2_connect( $conn_string, "", "" );
    ?>
    ```

    **`VCAP_SERVICES`가 있는 예제**

    ```php
    <?php
    $driver      = "DRIVER={IBM DB2 ODBC DRIVER};";

    $vcap        = json_decode( getenv( "VCAP_SERVICES" ), true );
    $dsn         = $vcap[ "dashDB" ][0][ "credentials" ][ "dsn" ];

    $conn_string = $driver . $dsn;
                                   
    $conn        = db2_connect( $conn_string, "", "" );
    ?>
    ```

## 샘플
{: #samples}

다음은 여러 언어로 된 애플리케이션에서 사용자의 {{site.data.keyword.dashdbshort_notm}} 데이터베이스로 연결하는 방법을 보여주는 샘플에 대한 링크입니다.
{: shortdesc}

   * [.NET ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting__net_applications.html){:new_window}
<!-- * [JAVA ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_java.html){:new_window} -->
   * [JDBC ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_jdbc_applications.html){:new_window}
<!-- * [Node.js ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_nodejs.html){:new_window} -->
   * [PHP ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_php.html){:new_window}
<!-- * [Python ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_python.html){:new_window} -->
   * [GitHub의 {{site.data.keyword.dashdbshort_notm}} 샘플 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/IBM-Bluemix/dashdb-nodejs-helloworld){:new_window}


