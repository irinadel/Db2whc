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

# ODBC 또는 CLI를 사용하여 프로그래밍 방식으로 연결
{: #con_prog_odbc_cli}

Microsoft Windows ODBC 또는 CLI 애플리케이션과 {{site.data.keyword.dashdbshort_notm}} 데이터베이스 간의 연결을 정의합니다.
{: shortdesc}

## 전제조건
{: #prereq81}

{{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하기 전에 먼저 필수 [전제조건](/docs/services/Db2whc/connecting/connecting.html#prereqs)이 있는지 확인하십시오.

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## 프로시저
{: #proc81}

1. Linux 운영 체제의 명령 쉘, Windows 명령 프롬프트 또는 Windows 운영 체제의 Db2 명령 창에서 다음 명령을 입력하십시오.

   **참고**: 이 명령은 컴퓨터의 드라이버 구성 파일(`db2dsdriver.cfg`)에 새 항목을 작성하고 연결 속성을 설정합니다. 이 단계는 한 번만 수행해야 합니다.
   
   - SSL을 사용하는 연결의 경우:

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50001 -parameter "SecurityTransportMode=SSL"`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50001`

   - SSL을 사용하지 않는 연결의 경우:

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50000`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50000`

   여기서,

   `<hostname>`은 서버의 호스트 이름입니다.

   `<alias>`는 사용자가 선택하는 DSN 별명입니다.
    
2. [*선택사항*]: 데이터베이스에 대한 연결을 테스트하려면 명령 프롬프트에서 다음 명령을 실행하십시오.

   `db2cli validate -dsn <alias> -connect -user <user_id> -passwd <password>`

   여기서,

   `<alias>`는 **db2cli writecfg** 명령을 사용하여 작성한 DSN 별명입니다.

   `<user_id>`는 미리 수집한 연결 인증 정보에서 가져온 것입니다.

   `<password>`는 미리 수집한 연결 인증 정보에서 가져온 것입니다.

3. [*선택사항*]: Microsoft ODBC 드라이버 관리자를 사용하여 데이터 소스 이름(DSN)을 등록하고 Microsoft ODBC 애플리케이션에 대한 작업을 수행하려면 다음 명령을 실행하십시오. 기본적으로 DSN은 사용자 DSN으로 작성됩니다.

   `db2cli registerdsn -add -dsn <alias>`

   여기서,
        
   `<alias>`는 **db2cli writecfg** 명령을 사용하여 작성한 DSN 별명입니다.



