---

copyright:
  years: 2014, 2018
lastupdated: "2018-05-08"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# IBM Cloud로 데이터 마이그레이션
{: #migration}

로컬 네트워크 또는 오브젝트 저장소(Amazon S3 또는 IBM Cloud Object Storage)에 있는 CSV 또는 TXT와 같은 구분된 형식의 데이터 파일에서 데이터를 {{site.data.keyword.dashdblong}}로 로드할 수 있습니다. 온프레미스 시스템에서도 데이터를 마이그레이션할 수 있습니다.
{: shortdesc}

## 오브젝트 저장소에서 데이터 로드
{: #cos}

Amazon S3에서 데이터를 로드하려면 다음 방법 중 하나를 사용하십시오.
  * {{site.data.keyword.dashdbshort_notm}} 웹 콘솔을 사용하십시오. **로드 > Amazon S3**를 선택하십시오. 
  * 외부 테이블에서 직접 로드하십시오. 다음은 예제 SQL문입니다.

    ```
INSERT INTO <table-name> SELECT * FROM EXTERNAL '<mys3file.txt>' USING
        (CCSID 1208 s3('s3.amazonaws.com',
        '<S3-access-key-ID>',
        '<S3-secret-access-key>',
        '<my_bucket>'
           )
      )      
    ```

외부 테이블을 직접 사용하여 IBM Cloud Object Storage에서 데이터를 로드하는 경우, 예제 SQL문은 다음과 같습니다.

```
INSERT INTO <table-name> SELECT * FROM EXTERNAL '<mys3file.txt>' USING
  (CCSID 1208 s3('s3-api.us-geo.objectstorage.softlayer.net',
  '<S3-access-key-ID>',
  '<S3-secret-access-key>',
  '<my_bucket>'
     )
  )      
```

**참고:** IBM Cloud Object Storage의 경우, 새 서비스 신임 정보를 작성할 때 HMAC 신임 정보를 작성하려면 *인라인 구성 매개변수* 필드에서 {"HMAC:true"}를 지정하십시오.

## 온프레미스 시스템에서 데이터 마이그레이션
{: #onprem}

온프레미스 시스템에서 데이터를 마이그레이션하려면 데이터 세트의 크기에 따라 다음 방법 중 하나를 선택하십시오.
* 25TB 미만의 데이터: [IBM Lift](#lift)
* 25TB 이상의 데이터: [IBM Cloud 대량 데이터 마이그레이션 서비스](#mdms)

### Lift
{: #lift}

Lift는 표 1에 나열된 다양한 데이터 소스에서 {{site.data.keyword.Bluemix_notm}}로 데이터를 무료로 마이그레이션할 수 있는 애플리케이션입니다. 

| IBM Cloud의 대상 데이터베이스 | 데이터 소스 |
|------------------------------|-------------|
| IBM Db2 Warehouse on Cloud   | IBM Db2 |
|                              | IBM Db2 Warehouse |
|                              | IBM Integrated Analytics System |
|                              | IBM PureData System for Analytics |
|                              | Oracle 데이터베이스 |
|                              | Microsoft SQL Server |
|                              | CSV 파일 형식 |
{: caption="표 1. 마이그레이션 데이터 소스" caption-side="top"}

Lift를 다운로드하고 설치하려면 [Lift 다운로드 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://lift.ng.bluemix.net/#download){:new_window}를 참조하십시오.

Lift를 사용하여 {{site.data.keyword.Bluemix_notm}}에 데이터를 마이그레이션하는 데 관한 단계별 지침은 [{{site.data.keyword.dashdblong}}로 데이터 마이그레이션 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://lift.ng.bluemix.net/#docs){:new_window}을 참조하십시오.

### IBM Cloud 대량 데이터 마이그레이션 서비스
{: #mdms}

IBM Cloud 대량 데이터 마이그레이션 서비스(MDMS)는 25TB 이상의 대형 IBM PureData Systems for Analytics(Netezza) 데이터베이스에서 {{site.data.keyword.Bluemix_notm}}의 완전히 관리되는 {{site.data.keyword.dashdblong}} 데이터베이스로 데이터를 마이그레이션하는 데 사용될 수 있습니다.

MDMS는 테라바이트에서 페타바이트까지의 데이터를 {{site.data.keyword.Bluemix_notm}}에 물리적으로 전송하는 빠르고 단순하고 안전한 방법을 제공합니다. MDMS는 120TB의 사용 가능한 스토리지 용량이 있는 모바일 스토리지 디바이스입니다. 이 디바이스를 사용하면 높은 비용, 긴 전송 시간 및 보안 문제와 같은 일반적인 전송의 어려움을 단일 서비스 내에서 모두 해결할 수 있습니다.

![대량 데이터 마이그레이션 서비스 디바이스의 보기](images/mdms.svg)

MDMS 디바이스에 대한 자세한 정보는 [IBM Cloud 대량 데이터 마이그레이션 시작하기](/docs/infrastructure/mass-data-migration/index.html#getting-started-with-ibm-cloud-mass-data-migration){:new_window}를 참조하십시오.

MDMS 디바이스를 사용하여 IBM PureData System for Analytics(Netezza) 데이터베이스에서 {{site.data.keyword.dashdblong}} 데이터베이스로 데이터를 마이그레이션하는 방법에 대한 자세한 정보는 [IBM PureData System for Analytics(Netezza)에서 마이그레이션](/docs/services/Db2whc/pda_db2whc_mdms.html)을 참조하십시오.

