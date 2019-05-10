---

copyright:
  years: 2014, 2019
lastupdated: "2019-04-01"

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

# 연결 개요
{: #connect_ov}

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

- [데이터베이스 세부사항 및 연결 인증 정보](/docs/services/Db2whc/connecting?topic=Db2whc-db_details_cxn_creds#db_details_cxn_creds)

### 드라이버 패키지 다운로드 및 설치
{: #dl_install}

- [드라이버 패키지 다운로드](/docs/services/Db2whc/connecting?topic=Db2whc-dr_pkg#dr_pkg)
- [Linux 또는 PowerLinux에서 설치](/docs/services/Db2whc/connecting?topic=Db2whc-install_dr_pkg_linux#install_dr_pkg_linux)
- [Mac OS X에서 설치](/docs/services/Db2whc/connecting?topic=Db2whc-install_dr_pkg_mac#install_dr_pkg_mac)
- [Windows에서 설치](/docs/services/Db2whc/connecting?topic=Db2whc-install_dr_pkg_windows#install_dr_pkg_windows)

### 환경 구성
{: #cfg_env}

- [환경 구성](/docs/services/Db2whc/connecting?topic=Db2whc-cfg_loc_env#cfg_loc_env)
- [SSL(Secure Sockets Layer) 지원](/docs/services/Db2whc/connecting?topic=Db2whc-ssl_support#ssl_support)

## 연결 옵션
{: #connect_opts}

{{site.data.keyword.dashdbshort_notm}}는 애플리케이션 연결 요구사항에 따라 여러 가지 보안 연결 옵션을 제공합니다.   
{: shortdesc}

[연결 옵션](/docs/services/Db2whc/connecting?topic=Db2whc-connect_options#connect_options)을 참조하십시오.

## 프로그래밍 방식으로 연결
{: #conx_prgrm}

공통 프로그래밍 언어를 사용하여 {{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하는 애플리케이션을 작성할 수 있습니다.
{: shortdesc}

- [JDBC](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_jdbc#con_prog_jdbc)
- [Microsoft Windows ODBC 또는 CLI](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_odbc_cli#con_prog_odbc_cli)
- [.NET](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_net#con_prog_net)
- [ODBC 데이터 소스 관리자](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_odbc_dsa#con_prog_odbc_dsa)
- [PHP](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_php#con_prog_php)
- [REST API](/docs/services/Db2whc/connecting?topic=Db2whc-con_rest_api#con_rest_api)
<!-- - [C++]() -->
<!-- - [Java]() -->
<!-- - [Node.js]() -->
<!-- - [Perl]() -->
<!-- - [Python]() -->

## 앱 및 도구 통합
{: #conx_apps_tools}

외부 애플리케이션과 도구를 {{site.data.keyword.dashdbshort_notm}}에 연결하고 이 기능들을 사용하여 데이터를 더 정교하게 관리, 분석할 수도 있습니다. 예를 들어, 다음과 같습니다.

### 데이터 통합
{: #di}

- 분석 데이터베이스가 필요한 {{site.data.keyword.Bluemix_short}} 애플리케이션을 연결합니다.
- [DataStage](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#datastage)
- [Informatica](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#informatica)
- [Lift ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.lift-cli.cloud.ibm.com/#docs){:new_window}
- [InfoSphere Data Replication](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#idr)
- [Segment ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://segment.com/docs/destinations/db2/){:new_window}
- [Data Studio](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#data_studio)
- [Data Server Manager](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#dsm)
- [CLPPLUS](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#clpplus)
- [Aginity Workbench - Netezza® 데이터 모델 및 데이터를 {{site.data.keyword.dashdbshort_notm}}](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#aginity_wb)로 마이그레이션
- [InfoSphere Data Architect - 데이터베이스 스키마 설계 및 배치](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#ida)

### 데이터 시각화/BI
{: #dvis_bi}

- [Cognos Analytics - 데이터에 대한 Business Intelligence 보고서 실행](/docs/services/Db2whc/connecting?topic=Db2whc-data_vis_bi#cognos)
- [Looker ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.looker.com/setup-and-management/connecting-to-db){:new_window}
- [Tableau](/docs/services/Db2whc/connecting?topic=Db2whc-data_vis_bi#tableau)
- [Microsoft Excel](/docs/services/Db2whc/connecting?topic=Db2whc-data_vis_bi#excel)
- [Esri ArcGIS for Desktop - 데이터를 사용하여 지리공간 분석 및 지도 발행](/docs/services/Db2whc/connecting?topic=Db2whc-data_vis_bi#esri_arcgis)

### 데이터 사이언스
{: #dsci}

- [Watson Studio(이전의 IBM Data Science Experience)](/docs/services/Db2whc/connecting?topic=Db2whc-ds#watson_studio)
- [SPSS Statistics](/docs/services/Db2whc/connecting?topic=Db2whc-ds#spss_stats)
- [SAS](/docs/services/Db2whc/connecting?topic=Db2whc-ds#sas)
- [로컬 R 개발 환경](/docs/services/Db2whc/connecting?topic=Db2whc-ds#r_dev_env)

## 다른 Db2 데이터베이스에 연결
{: #fed}

Db2 데이터 가상화(연합이라고도 함)는 {{site.data.keyword.dashdbshort_notm}}를 통해 지원합니다. 데이터 가상화를 사용하면 조직 전체의 여러 분산 데이터베이스에 있는 모든 데이터에 단일 조회 액세스가 가능합니다. 클라우드와 온프레미스 둘 다에서 Db2 또는 Informix 데이터 소스에 있는 데이터에 액세스할 수 있습니다. 

이 기능은 엔트리 플랜을 제외한 모든 버전의 {{site.data.keyword.dashdbshort_notm}}에서 지원됩니다. 그러나 데이터를 가져올 수 있는 대상으로 엔트리 플랜을 사용할 수 있습니다.

- [데이터 가상화(연합)](/docs/services/Db2whc?topic=Db2whc-data_virt_fed#data_virt_fed)


