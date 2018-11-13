---

copyright:
  years: 2014, 2018
lastupdated: "2018-10-15"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 연결 개요
{: #overview}

명령행 인터페이스, IBM® 또는 서드파티 애플리케이션 및 도구, 또는 {{site.data.keyword.dashdbshort_notm}} 데이터베이스에 작성하는 앱을 연결할 수 있습니다.
{: shortdesc}

## 전제조건
{: #prereqs}

{{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하기 전에 먼저 필수 전제조건이 있는지 확인하십시오. 

- 데이터베이스 세부사항 및 인증 정보 수집

   데이터베이스에 연결하려면 데이터베이스 세부사항(예: 호스트 이름) 및 인증 정보(예: 사용자 ID 및 비밀번호)가 필요합니다. {{site.data.keyword.dashdbshort_notm}} 웹 콘솔에서 이 연결 정보를 수집할 수 있습니다.

- 지원되는 드라이버의 설치 여부 확인

   - 애플리케이션 또는 도구에 이미 Db2 v11.1 IBM Data Server Driver Package가 포함된 경우 애플리케이션 또는 도구는 해당 드라이버를 사용하여 {{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결할 수 있습니다.
   - 그렇지 않은 경우 {{site.data.keyword.dashdbshort_notm}} 웹 콘솔에서 다운로드할 수 있는 Db2 드라이버 패키지를 설치하십시오.

- 사용자 환경 구성

  - 데이터베이스의 드라이버 구성 파일인 `db2dsdriver.cfg`에 항목을 추가하십시오.
  - SSL(Secure Socket Layer)

    SSL을 사용하거나 사용하지 않고 연결하도록 선택할 수 있습니다. 사용할 포트 및 연결 문자열과 같은 연결 세부사항은 사용자가 SSL 연결을 사용하는지 여부에 따라 다릅니다.

    SSL 연결을 사용하려면 CA 인증서가 필요합니다.
    - 최신 {{site.data.keyword.dashdbshort_notm}} 드라이버 패키지를 사용하는 경우 인증서 파일은 패키지와 함께 번들로 제공되어 연결에 사용됩니다.
    - IBM Data Server Driver Package를 사용하는 경우 {{site.data.keyword.dashdbshort_notm}} 웹 콘솔에서 SSL 인증서를 다운로드할 수 있습니다.

- 포트 사용 가능성 확인

   네트워크가 방화벽 뒤에 있는 경우 표준 프로토콜에 포트 번호 `50000`가 허용되거나 SSL 연결에 포트 번호 `50001`이 허용되는지 확인하십시오.

<!-- Before you can connect to your {{site.data.keyword.dashdbshort_notm}} database, verify that you completed downloading and installing the necessary components on the prerequisites checklist: 

- [Prerequisites checklist](prereqs.html) -->

### 연결 정보 수집
{: #collect_info}

- [데이터베이스 세부사항 및 연결 인증 정보](credentials.html)

### 드라이버 패키지 다운로드 및 설치
{: #dl_install}

- [드라이버 패키지 다운로드](driver_pkg.html)
- [Linux 또는 PowerLinux에서 설치](install_linux.html)
- [Mac OS X에서 설치](install_mac.html)
- [Windows에서 설치](install_win.html)

### 환경 구성
{: #cfg_env}

- [환경 구성](driver_pkg_cfg.html)
- [SSL(Secure Sockets Layer) 지원](ssl.html)

## 프로그래밍 방식으로 연결
{: #conx_prgrm}

공통 프로그래밍 언어를 사용하여 {{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하는 애플리케이션을 작성할 수 있습니다.
{: shortdesc}

- [JDBC](jdbc.html)
- [Microsoft Windows ODBC 또는 CLI](odbc_cli.html)
- [.NET](net_apps.html)
- [ODBC 데이터 소스 관리자](odbc_data_source_admin.html)
- [PHP](php.html)
- [REST API](rest_api.html)
<!-- - [C++]() -->
<!-- - [Java]() -->
<!-- - [Node.js]() -->
<!-- - [Perl]() -->
<!-- - [Python]() -->

## 앱 및 도구 통합
{: #conx_apps_tools}

외부 애플리케이션과 도구를 {{site.data.keyword.dashdbshort_notm}}에 연결하고 이 기능들을 사용하여 데이터를 더 정교하게 관리, 분석할 수도 있습니다. 예를 들어, 다음과 같습니다.

### 데이터 통합
- 분석 데이터베이스가 필요한 {{site.data.keyword.Bluemix_short}} 애플리케이션을 연결합니다.
- [DataStage](data.html#datastage)
- [Informatica](data.html#informatica)
- [Lift ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://lift.ng.bluemix.net/#docs){:new_window}
- [InfoSphere Data Replication](data.html#idr)
- [Segment ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://segment.com/docs/destinations/db2/){:new_window}
- [Data Studio](data.html#data_studio)
- [Data Server Manager](data.html#dsm)
- [CLPPLUS](data.html#clpplus)
- [Aginity Workbench - Netezza® 데이터 모델 및 데이터를 {{site.data.keyword.dashdbshort_notm}}](data.html#aginity_wb)로 마이그레이션
- [InfoSphere Data Architect - 데이터베이스 스키마 설계 및 배치](data.html#ida)

### 데이터 시각화/BI
- [Cognos Analytics - 데이터에 대한 Business Intelligence 보고서 실행](vis_bi.html#cognos)
- [Looker ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.looker.com/setup-and-management/connecting-to-db){:new_window}
- [Tableau](vis_bi.html#tableau)
- [Microsoft Excel](vis_bi.html#excel)
- [Esri ArcGIS for Desktop - 데이터를 사용하여 지리공간 분석 및 지도 발행](vis_bi.html#esri_arcgis)

### 데이터 사이언스
- [Watson Studio(이전의 IBM Data Science Experience)](data_sci.html#watson_studio)
- [SPSS Statistics](data_sci.html#spss_stats)
- [SAS](data_sci.html#sas)
- [로컬 R 개발 환경](data_sci.html#r_dev_env)

## 다른 Db2 데이터베이스에 연결
{: #fed}

Db2 데이터 가상화(연합이라고도 함)는 {{site.data.keyword.dashdbshort_notm}}를 통해 지원합니다. 데이터 가상화를 사용하면 조직 전체의 여러 분산 데이터베이스에 있는 모든 데이터에 단일 조회 액세스가 가능합니다. 클라우드와 온프레미스 둘 다에서 Db2 또는 Informix 데이터 소스에 있는 데이터에 액세스할 수 있습니다. 

이 기능은 엔트리 플랜을 제외한 모든 버전의 {{site.data.keyword.dashdbshort_notm}}에서 지원됩니다. 그러나 데이터를 가져올 수 있는 대상으로 엔트리 플랜을 사용할 수 있습니다.

- [데이터 가상화(연합)](../federation.html)


