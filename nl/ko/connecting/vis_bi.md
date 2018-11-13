---

copyright:
  years: 2014, 2018
lastupdated: "2018-10-24"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 데이터 시각화/BI
{: #overview}

외부 애플리케이션과 도구를 {{site.data.keyword.dashdbshort_notm}}에 연결하고 이 기능들을 사용하여 데이터를 더 정교하게 관리, 분석할 수도 있습니다. 
{: shortdesc}

## Cognos Analytics
{: #cognos}

온프레미스 데이터베이스의 데이터가 아닌 클라우드의 데이터에 대해 IBM Cognos® 보고서를 실행할 수 있습니다. 데이터를 {{site.data.keyword.dashdbshort_notm}} 데이터베이스에 로드한 후 JDBC 드라이버를 설정하고 Cognos 관리 도구를 사용하여 데이터베이스 연결을 작성합니다. <!--These instructions explain how to connect to the database from Cognos version 10.2.1.-->
{: shortdesc}

연결 작성 방법을 보려면 이 동영상을 시청하십시오.

<iframe class="embed-responsive-item" id="youtubeplayer" title="Cognos Analytics에서 연결 작성" type="text/html" width="640" height="390" src="//www.youtube.com/embed/TRUEPVHGi0s?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

자세한 정보는 [Cognos Analytics 연결 ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/support/knowledgecenter/en/SSEP7J_11.0.0/com.ibm.swg.ba.cognos.ug_cra.doc/c_create_ds.html#create_ds){:new_window}을 참조하십시오.

## Looker
{: #looker}

Looker를 {{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결할 수 있습니다. Looker는 실시간 비즈니스 분석을 탐색, 분석 및 공유하는 데 사용되는 비즈니스 인텔리전스 앱이자 빅데이터 분석 플랫폼입니다.
{: shortdesc}

[Looker 연결 ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.looker.com/setup-and-management/connecting-to-db){:new_window}

## Tableau
{: #tableau}

다음 지시사항은 Tableau를 {{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하여 Tableau Desktop<!--version 8.x-->에 적용하는 방법을 설명합니다. 그러나 다른 Tableau 도구에 대해 비슷한 단계를 사용할 수 있습니다.
{: shortdesc}

### 전제조건

{{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하기 전에 먼저 필수 [전제조건](connecting.html#prereqs)이 있는지 확인하십시오.

### 프로시저

1. Tableau Desktop에서 데이터베이스 연결을 정의하는 데 사용되는 도구의 창이나 페이지를 여십시오.
2. 시작 페이지에서 **데이터에 연결**을 클릭하십시오.
3. **데이터 소스** 목록에서 데이터베이스 연결에 사용할 데이터 소스 또는 드라이버를 선택하십시오. 목록의 **서버에서** 섹션에서 **IBM Db2**를 선택하십시오.
4. **IBM DB2 연결** 창에서 다음 표를 사용하여 연결 정보를 연결하십시오.

| Tableau 필드 | Db2 연결 정보 필드 |
|---------------|-----------------------------------|
| 1단계: 서버 이름 입력 | 호스트 이름 |
| 2단계: 포트 | 포트 번호 |
| 3단계: 서버에 데이터베이스 입력 | 데이터베이스 이름 |
| 사용자 이름 | 사용자 ID |
| 비밀번호 | 비밀번호 |
{: caption="표 1. Tableau의 연결 정보 필드" caption-side="top"}

5. **연결**을 클릭하여 연결을 설정하십시오. Tableau는 데이터 연결을 위해 몇 가지 옵션을 제공합니다. {{site.data.keyword.dashdbshort_notm}} 데이터베이스를 완전히 사용하려면 **라이브 연결** 옵션을 선택하십시오.

## Microsoft Excel
{: #excel}

다음 지시사항은 Microsoft Excel<!--2010-->을 {{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하는 방법을 설명합니다.
{: shortdesc}

### 전제조건

{{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하기 전에 먼저 필수 [전제조건](connecting.html#prereqs)이 있는지 확인하십시오.

Db2 드라이버 패키지 또는 IBM® Data Server Driver Package가 로컬 컴퓨터에 설치되어 있어야 합니다. 

**제한사항**: Excel과 {{site.data.keyword.dashdbshort_notm}} 간의 연결은 Windows 운영 체제에서만 지원됩니다.

### 프로시저

1. 웹 콘솔에서 **SQL 실행** 페이지로 이동하십시오.
    
2. 편집기 텍스트 상자에 하나 이상의 SELECT문을 입력하십시오.

3. 실행 옵션 중 하나를 클릭하십시오.

4. **Excel ODC 파일**을 클릭하십시오.

5. `BLUExcel.odc` 파일을 다운로드하여 Excel에서 여십시오. 보안 주의사항이 표시되면 **사용**을 클릭하십시오.

6. **열기**를 클릭하여 {{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하십시오. **DB2 데이터베이스에 연결** 대화 상자가 열립니다.

7. {{site.data.keyword.dashdbshort_notm}}에 로그인하는 데 사용하는 사용자 ID 및 비밀번호를 입력하십시오. 사용자 ID 및 비밀번호를 얻으려면 웹 콘솔에서 **연결**을 클릭하거나 웹 콘솔에서 **연결 > 연결 정보**를 클릭하십시오.

8. 연결 모드가 `Share`인지 확인한 다음 **확인**을 클릭하십시오.

### 결과

Excel 스프레드시트에 조회 결과가 표시됩니다. 결과 표시기에 표시되는 결과와 동일한 결과가 표시됩니다. 이제 차트 및 보고서를 생성하고 Excel을 사용하여 데이터를 분석할 수 있습니다. 이를 수행하는 방법과 웹 콘솔에서 데이터에 대한 SQL 조회를 실행하는 방법에 대한 자세한 정보는 다음을 참조하십시오. 
- [튜토리얼: Excel을 사용하여 차트 및 보고서 생성 ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.analytics.doc/doc/explore_excel_reports.html){:new_window}
- [Excel을 사용하여 분석 ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.analytics.doc/doc/exploreexcel.html){:new_window}

## Esri ArcGIS for Desktop
{: #esri_arcgis}

Esri ArcGIS for Desktop<!--version 10.3.1 -->을 {{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결한 다음 이를 사용하여 지리공간 데이터를 분석하고 시각화할 수 있습니다.
{: shortdesc}

### 전제조건

{{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하기 전에 먼저 필수 [전제조건](connecting.html#prereqs)이 있는지 확인하십시오.

Db2 드라이버 패키지 또는 IBM® Data Server Driver Package가 컴퓨터에 설치되어 있어야 합니다.

### 프로시저

1. 미리 수집한 [연결 정보](credentials.html)에서 ODBC DSN 데이터를 판별하십시오.

2. 새 연결을 작성하십시오.
      
   a. ArcCatalog 카탈로그 트리에서 데이터베이스 연결 노드를 열고 **데이터베이스 연결 추가**를 클릭하십시오.
        
   b. 데이터베이스 연결 마법사에서 다음을 수행하십시오.
   - 데이터베이스 플랫폼 드롭 다운 목록에서 **DB2**를 선택하십시오.
   - **데이터 소스** 필드에 다음 문자열을 입력하십시오.
     ```
     HostName=<hostname>;Port=<port>;Database=<database>;
     CLIENTBUFFERSUNBOUNDLOBS=1;LOBCACHESIZE=50000000;
     FET_BUF_SIZE=256K  
     ```

     여기서, `<hostname>`, `<port>` 및 `<database>`는 이전에 언급한 호스트 이름, 포트 번호 및 데이터베이스 이름을 나타내는 플레이스홀더입니다.
            
   - 인증 유형으로 **데이터베이스 인증**을 선택하십시오.
            
   - 해당 필드에 사용자 이름 및 비밀번호(이전에 언급한 사용자 ID 및 비밀번호)를 지정하십시오.
            
   - **확인**을 누르십시오.
        
     ![데이터베이스 연결 마법사](images/2_gs_conn.jpg)

### 결과

Esri ArcGIS for Desktop의 ArcCatalog 구성요소가 {{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결되었습니다. 


