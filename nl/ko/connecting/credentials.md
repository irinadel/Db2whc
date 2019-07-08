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

# 데이터베이스 세부사항 및 연결 인증 정보
{: #db_details_cxn_creds}

로컬 개발 환경을 구성하고 애플리케이션 및 도구를 {{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하려면 데이터베이스 세부사항 및 연결 인증 정보를 알아야 합니다.
{: shortdesc}

## 데이터베이스 세부사항
{: #db_details}

애플리케이션 및 도구를 데이터베이스에 연결하는 데 필요한 중요한 데이터베이스 세부사항이 있습니다.

- *호스트 이름* - 서버의 호스트 이름입니다.
- *포트 번호* - TCP/IP 통신을 위해 데이터베이스 관리자가 사용합니다. (SSL(Secure Socket Layer)을 사용하는 연결에 필요한 한 포트와 비SSL 연결에 필요한 다른 포트를 사용하여 서비스를 프로비저닝합니다.)

   필요한 경우 호스트 이름을 지정하고 ping 명령 또는 nslookup 명령을 사용하여 서버의 IP 주소를 가져올 수 있습니다.
- *데이터베이스 이름* - Db2 데이터베이스 이름(일반적으로 BLUDB)입니다.

## 연결 인증 정보
{: #cxn_creds}

다음과 같은 세 가지 유형의 인증 정보가 있습니다.

- *IBM ID* - {{site.data.keyword.Bluemix_notm}}를 사용하는 경우 {{site.data.keyword.Bluemix_notm}}에 로그인하기 위해 사용하는 ID입니다. 이 ID는 애플리케이션 또는 도구를 Db2 Warehouse on Cloud 데이터베이스에 연결하는 데 사용되지는 않습니다.
- *Db2 데이터베이스 인증 정보* - 애플리케이션 및 도구를 데이터베이스에 연결하는 데 사용할 수 있는 데이터베이스 사용자 ID 및 비밀번호를 사용하여 서비스를 프로비저닝합니다.
- *관리자 작성 사용자* - 일부 {{site.data.keyword.dashdbshort_notm}} 플랜에서는 관리자가 새 사용자를 작성할 수 있습니다. 이러한 관리자 작성 사용자 ID와 비밀번호를 사용하여 웹 콘솔 URL에 직접 로그인하고 애플리케이션 또는 도구에서 Db2 데이터베이스에 연결할 수 있습니다.

## 데이터베이스 세부사항 및 연결 인증 정보를 찾을 수 있는 위치
{: #location}

다음 위치에서 이 정보를 수집할 수 있습니다.

- *관리자* Db2 인스턴스의 소유자 또는 관리자가 아닌 경우 데이터베이스 세부사항을 가져오고 관리자의 인증 정보를 연결할 수 있습니다.
- *Db2 웹 콘솔* - 웹 콘솔에서 데이터베이스 세부사항 및 인증 정보를 사용할 수 있습니다.
- {{site.data.keyword.Bluemix_notm}}를 사용하는 경우 다음을 수행하십시오. 
   
   - *{{site.data.keyword.Bluemix_notm}} 대시보드* - "서비스 인증 정보" 영역의 {{site.data.keyword.Bluemix_notm}} 대시보드에서 서비스를 볼 때 데이터베이스 사용자 ID 및 비밀번호를 비롯하여 데이터베이스 세부사항을 볼 수 있습니다.
   - *`VCAP_SERVICES`* - `VCAP_SERVICES`는 {{site.data.keyword.Bluemix_notm}}의 환경 변수이며 JSON 형식의 데이터베이스 세부사항 및 인증 정보를 포함합니다. {{site.data.keyword.Bluemix_notm}} 대시보드에서 서비스에 대한 서비스 인증 정보를 보는 경우 `VCAP_SERVICES`의 컨텐츠가 표시됩니다. 기타 {{site.data.keyword.Bluemix_notm}} 서비스 또는 앱을 서비스에 바인딩하는 경우 이러한 기타 서비스 또는 앱은 `VCAP_SERVICES`를 읽어 프로그래밍 방식으로 데이터베이스 세부사항 및 인증 정보에 액세스할 수 있습니다.
