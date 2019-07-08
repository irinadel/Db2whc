---

copyright:
  years: 2014, 2019
lastupdated: "2018-10-15"

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

# 데이터 사이언스
{: #ds}

외부 애플리케이션과 도구를 {{site.data.keyword.dashdbshort_notm}}에 연결하고 이 기능들을 사용하여 데이터를 더 정교하게 관리, 분석할 수도 있습니다. 
{: shortdesc}

## Watson Studio
{: #watson_studio}

IBM Watson Studio(이전의 Data Science Experience)에 프로젝트를 작성하는 경우 데이터에 대한 작업을 수행할 수 있도록 데이터 자산을 프로젝트에 추가합니다. 프로젝트의 모든 협업자에게 자동으로 프로젝트의 데이터에 액세스할 수 있는 권한이 부여됩니다.
{: shortdesc}

데이터를 추가하는 방법과 데이터를 추가할 수 있는 원본 위치는 레거시 프로젝트와 IBM Watson 프로젝트 간에 다릅니다. IBM Watson 프로젝트는 {{site.data.keyword.Bluemix_notm}} Object Storage를 사용합니다. Object Storage OpenStack Swift를 사용하는 경우 프로젝트는 레거시 프로젝트입니다. 

### IBM Watson 프로젝트에서 새 연결을 작성하려면 다음을 수행하십시오.

1. **프로젝트에 추가 > 연결**을 클릭하십시오.
    
2. 데이터 소스를 선택하십시오.
    
3. 데이터 소스에 필요한 연결 정보를 입력하십시오. 일반적으로 호스트, 포트 번호, 사용자 이름 및 비밀번호와 같은 정보를 제공해야 합니다.
    
4. {{site.data.keyword.dashdbshort_notm}}에 대한 연결에서 자산을 검색할 수 있으며, 연결의 모든 테이블을 데이터 자산으로 프로젝트에 추가할 수 있는 기능을 제공합니다. **데이터 자산 검색**을 선택하고 프로젝트를 선택하십시오.
    
5. **작성**을 클릭하십시오. 연결은 **자산** 페이지에 표시됩니다.

연결을 작성하고 연결된 데이터를 프로젝트에 추가하는 방법을 보려면 이 동영상을 시청하십시오.

<iframe class="embed-responsive-item" id="youtubeplayer" title="연결을 작성하고 연결된 데이터를 프로젝트에 추가" type="text/html" width="640" height="390" src="//www.youtube.com/embed/U7-gCbo4QtM?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

### 레거시 프로젝트에서 새 연결을 작성하려면 다음을 수행하십시오.

1. 프로젝트의 **자산** 페이지에서 **데이터 찾기 및 추가** 아이콘을 클릭하십시오.
    
2. **연결** 분할창에서 **연결 작성**을 클릭하십시오.

3. 이름 및 설명을 입력하고 서비스 카테고리를 선택하십시오.

   **데이터 서비스** = {{site.data.keyword.Bluemix_notm}} 데이터 서비스

   **데이터 서비스**를 선택하면 기존 {{site.data.keyword.Bluemix_notm}} 데이터 서비스가 **서비스 인스턴스** 목록에 표시됩니다.

4. 목록에서 서비스 또는 데이터베이스 서버를 선택하십시오.

5. 연결 정보를 입력하십시오.

   **데이터 서비스**를 선택하면 기존 {{site.data.keyword.Bluemix_notm}} 데이터 서비스가 **서비스 인스턴스** 목록에 표시됩니다.
    
6. **작성**을 클릭하십시오. 모든 레거시 프로젝트에서 연결을 사용할 수 있습니다.
    
7. **연결** 분할창에서 연결을 선택하고 **적용**을 클릭하십시오.

레거시 프로젝트에 기존 연결을 추가하려면 다음을 수행하십시오.

1. 프로젝트의 **자산** 페이지에서 **데이터 찾기 및 추가** 아이콘을 클릭하십시오.
    
2. **연결** 분할창에서 연결을 선택하고 **적용**을 클릭하십시오.

## SPSS Statistics
{: #spss_stats}

다음 지시사항은 IBM® SPSS® Statistics에서 {{site.data.keyword.dashdbshort_notm}} 데이터베이스로 연결을 작성하는 방법을 설명합니다.
{: shortdesc}

### 전제조건
{: #prereq11}

{{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하기 전에 먼저 필수 [전제조건](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs)이 있는지 확인하십시오.

### 프로시저
{: #proc11}

1. SPSS Statistics에서 **파일 > 데이터베이스 열기 > 새 조회**를 클릭하십시오.
    
2. 데이터베이스 마법사에서 **ODBC 데이터 소스 추가**를 클릭하십시오.
    
3. ODBC 데이터 소스 관리자 창을 사용하여 {{site.data.keyword.dashdbshort_notm}} 데이터베이스에 대한 ODBC 데이터 소스 이름(DSN)을 추가하십시오.
        
   a. **사용자 DSN** 탭에서 **추가**를 클릭하십시오.

   b. 새 데이터 소스 작성 창에서 이름이 **IBM DB2 ODBC DRIVER**인 드라이버를 선택하고 **완료**를 클릭하십시오.

   선택하는 드라이버가 `IBM DB2® ODBC DRIVER - DB2COPY`처럼 이와 유사한 이름을 가진 드라이버가 아니어야 합니다. 드라이버가 목록에 없으면 SPSS Statistics를 종료한 다음 드라이버를 다운로드하여 설치하십시오. [드라이버 패키지](/docs/services/Db2whc/connecting?topic=Db2whc-dr_pkg#dr_pkg)를 참조하십시오.
        
   c. ODBC IBM 드라이버 - 추가 창에서 데이터 소스 이름(일반적으로 연결 중인 데이터베이스의 이름)을 입력하고 **추가**를 클릭하십시오.
        
   d. CLI/ODBC 설정 창의 **데이터 소스** 탭에 미리 수집한 [연결 정보](/docs/services/Db2whc/connecting?topic=Db2whc-db_details_cxn_creds#db_details_cxn_creds)에 있는 사용자 ID와 비밀번호를 입력하십시오.
        
   e. 고급 설정 페이지에서 다음 각각의 매개변수에 대해 **추가**를 클릭하여 단계를 시작하는 CLI 매개변수 추가 창을 열고 **확인**을 클릭하여 고급 설정 페이지로 돌아가십시오.
            
   - `Database` 매개변수를 선택한 다음 **확인**을 클릭하여 CLI/ODBC 설정 창을 여십시오. **보류 중인 값** 필드에 미리 수집한 연결 정보에 있는 데이터베이스 이름을 입력하십시오.

   - `Hostname` 매개변수를 선택한 다음 **확인**을 클릭하여 CLI/ODBC 설정 창을 여십시오. **보류 중인 값** 필드에 미리 수집한 연결 정보에 있는 호스트 이름을 입력하십시오.

   - `Port` 매개변수를 선택한 다음 **확인**을 클릭하여 CLI/ODBC 설정 창을 여십시오. **보류 중인 값** 필드에 미리 수집한 연결 정보에 있는 포트 번호를 입력하십시오.
            
   - `Protocol` 매개변수를 선택한 다음 **확인**을 클릭하여 CLI/ODBC 설정 창을 여십시오. **TCP/IP**를 선택하십시오.
        
   f. **확인**을 클릭하여 ODBC 데이터 소스 관리자 창으로 돌아십시오.
        
   g. **사용자 DSN** 탭에서 데이터 소스 이름을 선택한 다음 **구성**을 클릭하십시오.
        
   h. CLI/ODBC 설정 창에서 **연결**을 클릭하여 연결을 테스트하십시오.
            
   - 연결이 성공하면 **확인**을 클릭하여 ODBC 데이터 소스 관리자 창으로 돌아간 다음 **확인**을 클릭하여 창을 종료하십시오.
            
   - 연결이 성공하지 못한 경우 연결을 다시 테스트하기 전에 오류를 기록하고 정정하십시오.

## SAS
{: #sas}

다음 지시사항은 SAS에서 {{site.data.keyword.dashdbshort_notm}} 데이터베이스로 연결을 작성하는 방법을 설명합니다.
{: shortdesc}

### 전제조건
{: #prereq12}

{{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하기 전에 먼저 필수 [전제조건](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs)이 있는지 확인하십시오.

### 프로시저
{: #proc12}

SAS에서 {{site.data.keyword.dashdbshort_notm}} 데이터베이스로 연결하는 방법에 대한 단계는 SAS 문서를 참조하십시오.
- [UNIX 및 PC 호스트에 있는 DB2에 대한 SAS/ACCESS 인터페이스](https://documentation.sas.com/?docsetId=acreldb&docsetTarget=p1dzq4zjg1iycgn16l4xj9nnvibt.htm&docsetVersion=9.4&locale=en){:external}

## R 개발 환경
{: #r_dev_env}

IBM Watson Studio에 통합되어 있는 RStudio® 환경을 사용하는 대신 로컬에 설치된 사용자 고유의 R 개발 환경을 사용하는 것이 좋습니다. 예를 들어, 고유의 RStudio를 설치하거나 Rcmdr 또는 Rattle과 같은 다른 개발 도구를 사용할 수 있습니다. 다음 지시사항은 R 개발 환경을 {{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하는 방법을 설명합니다.
{: shortdesc}

### 전제조건
{: #prereq13}

{{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하기 전에 먼저 필수 [전제조건](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs)이 있는지 확인하십시오.

### 프로시저
{: #proc13}

1. 로컬 R 환경에서 다음 명령을 입력하여 `ibmdbR` 패키지를 설치하십시오.

   `install.packages("ibmdbR")`

   로컬 R 환경에서 CRAN(Comprehensive R Archive Network)에 액세스하여 `ibmdbR` 패키지 및 아직 설치되지 않은 전제조건 패키지를 자동으로 다운로드하여 설치합니다.
    
2. R 개발 환경과 {{site.data.keyword.dashdbshort_notm}} 데이터베이스 간에 ODBC 드라이버 연결을 작성하십시오.
        
   a. [데이터베이스를 ODBC 데이터 소스로 설정](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_cli_and_odbc_applications.html){:external}하십시오.
        
   b. 로컬에 설치된 R 개발 환경을 여십시오.
        
   c. R 프롬프트에서 다음 명령문을 입력하여 연결을 작성하십시오. 플레이스홀더를 미리 수집한 [연결 정보](/docs/services/Db2whc/connecting?topic=Db2whc-db_details_cxn_creds#db_details_cxn_creds)로 바꾸십시오.

   - 로컬에 설치된 R 개발 환경이 {{site.data.keyword.dashdbshort_notm}} 데이터베이스에서 실행되는 경우:

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

   - 로컬에 설치된 R 개발 환경이 {{site.data.keyword.dashdbshort_notm}} 데이터베이스에서 실행되지 않는 경우:

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

     **참고**: 연결 오브젝트를 작성하는 데 사용되는 명령문은 `odbcConnect()` 또는 `odbcDriverConnect()` 메소드가 아닌 `idaConnect()` 메소드를 사용합니다.
        
   d. 다음 R 명령을 실행하여 분석 패키지를 초기화하십시오.

   `idaInit(con)`

   e. 연결이 작동하는지 테스트하려면 다음 R 명령을 실행하십시오.

   `idaShowTables()`

   콘솔이 현재 스키마에 있는 모든 테이블과 보기 목록을 표시합니다.

