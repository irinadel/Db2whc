---

copyright:
  years: 2014, 2019
lastupdated: "2019-05-08"

keywords: Db2 Warehouse on Cloud, loading data, object store, IBM Cloud Object Storage, Amazon S3, LOAD command, Mass Data Migration Service (MDMS), migration, Lift

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

# {{site.data.keyword.dashdbshort_notm}}로 데이터 로드
{: #loading_data}

로컬 네트워크 또는 오브젝트 저장소(Amazon S3 또는 {{site.data.keyword.Bluemix_notm}} Object Storage)에 있는 CSV 또는 TXT와 같은 구분된 형식의 데이터 파일에서 데이터를 {{site.data.keyword.dashdblong}}로 로드할 수 있습니다. 온프레미스 시스템에서 데이터를 마이그레이션할 수도 있습니다.
{: shortdesc}

## 오브젝트 저장소에서 데이터 로드
{: #cos}

Amazon S3 또는 {{site.data.keyword.Bluemix_notm}} Object Storage에서 {{site.data.keyword.dashdblong}}로 데이터를 로드하려면 다음 방법 중 하나를 선택하십시오.
* {{site.data.keyword.dashdbshort_notm}} 웹 콘솔 사용. **로드 > Amazon S3**를 선택하십시오. 
* 외부 테이블에서 직접 로드. 다음은 SQL문의 예입니다.

    ```
    INSERT INTO <table-name> SELECT * FROM EXTERNAL '<mys3file.txt>' USING
      (CCSID 1208 s3('s3.amazonaws.com',
      '<S3-access-key-ID>',
      '<S3-secret-access-key>',
      '<my_bucket>'
         )
      )      
    ```

  외부 테이블을 직접 사용하여 {{site.data.keyword.Bluemix_notm}} Object Storage에서 데이터를 로드하는 경우 예제 SQL문은 다음과 같습니다.

  ```
  INSERT INTO <table-name> SELECT * FROM EXTERNAL '<mys3file.txt>' USING
    (CCSID 1208 s3('s3-api.us-geo.objectstorage.softlayer.net',
    '<S3-access-key-ID>',
    '<S3-secret-access-key>',
    '<my_bucket>'
       )
    )      
  ```

  {{site.data.keyword.Bluemix_notm}} Object Storage의 경우, 새 서비스 인증 정보를 작성할 때 HMAC 인증 정보를 작성하려면 *인라인 구성 매개변수 추가* 필드에 {"HMAC:true"}를 지정하십시오.
  {: note}

* 성능 향상을 위해 Db2 **LOAD** 명령을 사용하여 다음 예제 명령을 통해 Amazon S3에서 데이터를 로드할 수도 있습니다.

  ```
  CALL SYSPROC.ADMIN_CMD('LOAD FROM "S3::<amazon-s3-URL>::<s3-access-key-id>::<s3-secret-access-key>:
  :<s3-bucket-name>::<path-to-data-file>" OF <filetype> <additional-load-options> INTO <table-name>)
  ```

  다음은 Db2 **LOAD** 명령의 사용 예제입니다.

  ```
  CALL SYSPROC.ADMIN_CMD('load from "S3::s3-us-west-2.amazonaws.com::<s3-access-key-id>:
  :<s3-secret-access-key>::ibm-state-store::bdidata2TB/web_site.dat" of DEL modified by codepage=1208 
  coldel0x7c WARNINGCOUNT 1000 MESSAGES ON SERVER INSERT into BDINSIGHTS2.web_site ');
  ```

  지원되는 명령 옵션은 [**LOAD** 명령](https://www.ibm.com/support/knowledgecenter/en/SSEPGG_11.1.0/com.ibm.db2.luw.admin.cmd.doc/doc/r0008305.html){:external}을 참조하십시오. 

{{site.data.keyword.Bluemix_notm}} Object Storage에서 데이터를 로드하는 방법에 대한 안내 데모를 보려면 [{{site.data.keyword.dashdblong}} 안내 데모: 데이터 로드 탐색](https://www.ibm.com/cloud/garage/demo/try-db2-warehouse-cloud){:external}을 참조하십시오.

## 온프레미스 시스템에서 데이터 마이그레이션
{: #onprem}

온프레미스 시스템에서 데이터를 마이그레이션하려면 데이터 세트의 크기에 따라 다음 방법 중 하나를 선택하십시오.
* 25TB 미만의 데이터: [IBM Lift](#lift)
* 25TB 이상의 데이터: [{{site.data.keyword.Bluemix_notm}} Mass Data Migration 서비스](#mdms)

### Lift
{: #lift}

Lift는 표 1에 나열된 다양한 데이터 소스에서 {{site.data.keyword.Bluemix_notm}}로 데이터를 무료로 마이그레이션할 수 있는 애플리케이션입니다. 

| {{site.data.keyword.Bluemix_notm}}의 대상 데이터베이스 | 데이터 소스 |
|------------------------------|-------------|
| IBM Db2 Warehouse on Cloud   | IBM Db2 |
|                              | IBM Db2 Warehouse |
|                              | IBM Integrated Analytics System |
|                              | IBM PureData System for Analytics |
|                              | Oracle 데이터베이스 |
|                              | Microsoft SQL Server |
|                              | CSV 파일 형식 |
{: caption="표 1. 마이그레이션 데이터 소스" caption-side="top"}

Lift를 다운로드하고 설치하려면 [Lift 다운로드](https://www.lift-cli.cloud.ibm.com/#download){:external}를 참조하십시오.

Lift를 사용하여 데이터를 {{site.data.keyword.Bluemix_notm}}로 마이그레이션하는 방법에 대한 단계별 지시사항은 [데이터를 {{site.data.keyword.dashdblong}}로 마이그레이션](https://www.lift-cli.cloud.ibm.com/#docs){:external}을 참조하십시오.

### {{site.data.keyword.Bluemix_notm}} Mass Data Migration 서비스
{: #mdms}

{{site.data.keyword.Bluemix_notm}} Mass Data Migration 서비스(MDMS)는 25TB 이상의 대형 IBM PureData Systems for Analytics(Netezza) 데이터베이스에서 {{site.data.keyword.Bluemix_notm}}의 완전히 관리되는 {{site.data.keyword.dashdblong}} 데이터베이스로 데이터를 마이그레이션하는 데 사용될 수 있습니다.

MDMS는 테라바이트에서 페타바이트까지의 데이터를 {{site.data.keyword.Bluemix_notm}}에 물리적으로 전송하는 빠르고 단순하고 안전한 방법을 제공합니다. MDMS는 120TB의 사용 가능한 스토리지 용량이 있는 모바일 스토리지 디바이스입니다. 이 디바이스를 사용하면 높은 비용, 긴 전송 시간 및 보안 문제와 같은 일반적인 전송의 어려움을 단일 서비스 내에서 모두 해결할 수 있습니다.

![Mass Data Migration 서비스 디바이스의 보기](images/mdms.svg)

MDMS 디바이스에 대한 자세한 정보는 [시작하기 튜토리얼](/docs/infrastructure/mass-data-migration?topic=mass-data-migration-getting-started-tutorial#getting-started-with-ibm-cloud-mass-data-migration){:external}을 참조하십시오.

MDMS 디바이스를 사용하여 IBM PureData System for Analytics(Netezza) 데이터베이스에서 {{site.data.keyword.dashdblong}} 데이터베이스로 데이터를 마이그레이션하는 방법에 대한 자세한 정보는 [IBM PureData System for Analytics(Netezza)에서 마이그레이션](/docs/services/Db2whc/connecting?topic=Db2whc-pda#pda){:external}을 참조하십시오.

## 튜토리얼: 온프레미스 관계형 데이터베이스에서 데이터 마이그레이션
{: #tutorial}

이 튜토리얼에서는 온프레미스 관계형 데이터베이스에서 비즈니스 분석 애플리케이션용 {{site.data.keyword.dashdbshort_notm}}로 데이터를 마이그레이션하는 방법을 설명합니다. 

[{{site.data.keyword.dashdbshort_notm}}를 사용한 하이브리드 데이터 웨어하우징](https://www.ibm.com/cloud/garage/tutorials/ibm-db2-warehouse-on-cloud/hybrid-data-warehousing-with-db-2-warehouse-on-cloud){:external}

