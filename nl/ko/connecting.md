---

copyright:
  years: 2014, 2018
lastupdated: "2018-03-21"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 연결
{: #connect}

Db2® 데이터베이스에는 명령행 인터페이스, IBM® 또는 써드파티 애플리케이션 도구, 직접 작성한 앱을 연결할 수 있습니다. 
{: shortdesc}

## 전제조건
{: #connect_prereq}

Db2 관리 서비스 데이터베이스에 연결하려면 먼저 [전제조건 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connecting_applications_to_dashdb_database.html){:new_window}을 완료하십시오.
{: shortdesc}

### 환경 구성
{: #cfg_env}

로컬 애플리케이션 및 도구를 Db2 데이터베이스에 연결하려면 [환경 구성 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_driver_package_config.html){:new_window}을 수행해야 합니다. 
{: shortdesc}

## 프로그래밍 방식으로 연결
{: #conx_prgrm}

일반적인 프로그래밍 언어를 사용하여 Db2 데이터베이스에 연결하는 애플리케이션을 작성할 수 있습니다.
{: shortdesc}

<!--* [Java ![External link icon](../../icons/launch-glyph.svg "External link icon")](){:new_window} -->
* [JDBC ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_jdbc_applications.html){:new_window}
* [ODBC ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_cli_and_odbc_applications.html){:new_window}
* [.NET ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting__net_applications.html){:new_window}
* [PHP ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_php.html){:new_window}

## 앱 및 도구 연결
{: #conx_apps_tools}

외부 애플리케이션과 도구를 {{site.data.keyword.dashdbshort_notm}}에 연결하고 이 기능들을 사용하여 데이터를 더 정교하게 관리, 분석할 수도 있습니다. 예를 들어, 다음과 같습니다.
   * 분석 데이터베이스가 필요한 {{site.data.keyword.Bluemix_short}} 애플리케이션을 연결합니다.
   * [{{site.data.keyword.DSX_full}}(이전 이름은 IBM Data Science Experience)에서 연결합니다. ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://datascience.ibm.com/docs/content/manage-data/create-conn.html?context=analytics&linkInPage=true){:new_window}
   * [데이터베이스 스키마를 디자인하고 배치하기 위해 {{site.data.keyword.IBM_notm}} InfoSphere® Data Architect를 연결합니다. ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_ibm_data_architect.html){:new_window}
<!--   * Connect Esri ArcGIS to perform geospatial analytics and map publishing with your data. -->
   * [데이터에 대해 Cognos 보고서를 실행하기 위해 {{site.data.keyword.IBM_notm}} Cognos® 서버를 연결합니다. ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_cognos.html){:new_window}
   * 데이터를 조작하거나, 분석하거나 시각화하기 위해 Tableau 또는 Microsoft Excel과 같은 SQL 기반 도구를 연결합니다. 
       * [Tableau ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_tableau.html){:new_window}
       * [Microsoft Excel ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_excel.html){:new_window}
   * [Netezza® 데이터 모델 및 데이터를 {{site.data.keyword.dashdbshort_notm}}로 마이그레이션하기 위해 Aginity Workbench를 연결합니다. ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_aginity.html){:new_window}
