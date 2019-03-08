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

# 로컬 환경 구성
{: #cfg_loc_env}

로컬 애플리케이션 및 도구를 {{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하려면 환경을 구성해야 합니다.  
{: shortdesc}

## 전제조건
{: #prereq21}

{{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하기 전에 먼저 필수 [전제조건](/docs/services/Db2whc/connecting/connecting.html#prereqs)이 있는지 확인하십시오.

<!-- 1. Install the Db2 driver package for your operating system.

   - [Installing on Windows](install_win.html)
   - [Installing on Linux or PowerLinux](install_linux.html)
   - [Installing on Mac OS X](install_mac.html)
2. Decide whether or not you will be using Secure Sockets Layer (SSL) to connect to your database.
3. Collect database details and connect credentials, including the host name of your server, and your database user ID and password. -->

## 프로시저
{: #proc21}

1. 데이터베이스의 드라이버 구성 파일인 `db2dsdriver.cfg`에 항목을 추가하십시오.

   구성 단계는 SSL을 사용하여 데이터베이스에 연결할 것인지 여부에 따라 다릅니다.

   **SSL 사용**

   SSL을 사용하여 애플리케이션 및 도구를 데이터베이스에 연결하려면 Linux 운영 체제의 명령 쉘, Windows 명령 프롬프트 또는 DB2 명령 창에서 다음 명령을 입력하십시오. 

   `db2cli writecfg add -database BLUDB -host <hostname> -port 50001`

   `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50001`

   `db2cli writecfg add -database BLUDB -host <hostname> -port 50001 -parameter "SecurityTransportMode=SSL"`

    여기서,

   - `<hostname>`은 서버의 호스트 이름입니다.
   - `<alias>`는 사용자가 선택한 별명입니다. 별명은 데이터베이스 이름 `BLUDB`와 같을 수 없습니다. 별명에 공백을 사용하려면 별명을 큰따옴표로 묶으십시오.

   **SSL 사용 안함**

   SSL을 사용하지 않고 애플리케이션 및 도구를 데이터베이스에 연결하려면 Linux 운영 체제의 명령 쉘, Windows 명령 프롬프트 또는 DB2 명령 창에서 다음 명령을 입력하십시오. 

   `db2cli writecfg add -database BLUDB -host <hostname> -port 50000`

   `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50000`

    여기서,

   - `<hostname>`은 서버의 호스트 이름입니다.
   - `<alias>`는 사용자가 선택한 별명입니다. 별명은 데이터베이스 이름 `BLUDB`와 같을 수 없습니다. 별명에 공백을 사용하려면 별명을 큰따옴표로 묶으십시오.

2. 명령 프롬프트에서 **db2cli validate** 명령을 실행하여 연결을 테스트하십시오.

   `db2cli validate -dsn <alias> -connect -user <userid> -passwd <password>`

   여기서, 
   
   - `<alias>`는 **db2cli writecfg** 명령을 사용하여 작성한 별명입니다.
   - `<userid>`는 Db2 사용자 ID입니다.
   - `<password>`는 Db2 비밀번호입니다.

3. [*선택사항*] 로컬 ODBC 애플리케이션 및 도구를 데이터베이스에 연결하려면 ODBC 드라이버 관리자를 사용하여 DSN을 등록하십시오.
 
   명령행에서 다음 명령을 실행하십시오. 

   `db2cli registerdsn -add -dsn <alias>`

   여기서, 

   - `<alias>`는 **db2cli writecfg** 명령을 사용하여 작성한 별명입니다.

   기본적으로 DSN은 사용자 DSN으로 작성됩니다.

