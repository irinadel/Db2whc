---

copyright:
  years: 2014, 2018
lastupdated: "2018-03-23"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 데이터 로드
{: #load}

로컬 네트워크, 오브젝트 저장소(Amazon S3 또는 IBM Cloud Object Storage(이전 이름은 SoftLayer Swift)) 또는 Db2® 서버에 있는 CSV 또는 TXT와 같은 구분된 형식의 데이터 파일에서 데이터를 로드할 수 있습니다. Cloudant® 데이터베이스에서 직접, 또는 InfoSphere® DataStage®와 같은 애플리케이션에서 로드 프로세스를 수행하여 데이터베이스 인스턴스에 데이터를 채울 수 있습니다.
{: shortdesc}

* [PureData System for Analytics(Netezza)에서 데이터 로드 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://lift.ng.bluemix.net/#docs){:new_window}
* [Oracle에서 데이터 로드 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://lift.ng.bluemix.net/#docs){:new_window}
* [SQL Server에서 데이터 로드 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://lift.ng.bluemix.net/#docs){:new_window}
* [CSV 파일에서 데이터 로드 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://lift.ng.bluemix.net/#docs){:new_window}
<!-- * [Loading data from IBM Cloud Object Storage (formerly SoftLayer Swift) ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/learn_how/loaddata_swift.html){:new_window} -->
* 다음 방법 중 하나를 사용하여 Amazon S3에서 데이터를 로드하십시오. 
    * {{site.data.keyword.dashdbshort_notm}} 웹 콘솔을 사용하십시오. **로드 > Amazon S3**를 선택하십시오.  
    * 외부 테이블에서 직접 로드하십시오. SQL문 예는 다음과 같습니다. 

    ```
      INSERT INTO <table-name> SELECT * FROM EXTERNAL '<mys3file.txt>' USING
        (CCSID 1208 s3('s3.amazonaws.com', 
        '<S3-access-key-ID>',
        '<S3-secret-access-key>', 
        '<my_bucket>'
           )
        )      
    ```

<!-- [Loading data from Amazon S3 ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/learn_how/s3.html){:new_window} -->
