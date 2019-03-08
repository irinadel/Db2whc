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

# ODBC 데이터 소스 관리자를 사용하여 연결
{: #con_prog_odbc_dsa}

Microsoft ODBC 데이터 소스 관리자 도구를 사용하여 ODBC 또는 CLI 애플리케이션과 {{site.data.keyword.dashdbshort_notm}} 데이터베이스 간의 연결을 정의합니다.
{: shortdesc}

## 전제조건
{: #prereq91}

{{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하기 전에 먼저 필수 [전제조건](/docs/services/Db2whc/connecting/connecting.html#prereqs)이 있는지 확인하십시오.

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## 프로시저
{: #proc91}

1. [Db2 드라이버 패키지](/docs/services/Db2whc/connecting/driver_pkg.html)를 설치하십시오.

2. ODBC 데이터 소스 관리자를 열고 Db2 드라이버 패키지에 대한 사용자 DSN 또는 시스템 DSN을 작성하십시오.
    
3. **고급** 설정을 클릭하십시오. 다음 CLI 매개변수를 {{site.data.keyword.dashdbshort_notm}} 서버에 대한 값과 함께 입력하십시오. **Hostname**, **Port** 및 **Database**
    
4. SSL 연결의 경우 CLI 매개변수 **Security**를 `SSL` 값으로 입력하십시오.
    
5. **적용**을 클릭하십시오.
    
6. 연결을 테스트하려면 ODBC 데이터 소스 관리자의 기본 페이지로 돌아가십시오. 작성한 DSN에 대해 **구성**을 클릭하십시오. 서버에 대한 사용자 ID 및 비밀번호를 입력하고 **연결**을 클릭하십시오.

