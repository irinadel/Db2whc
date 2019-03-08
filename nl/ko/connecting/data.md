---

copyright:
  years: 2014, 2019
lastupdated: "2018-11-08"

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

# 데이터 통합
{: #data_int}

외부 애플리케이션과 도구를 {{site.data.keyword.dashdbshort_notm}}에 연결하고 이 기능들을 사용하여 데이터를 더 정교하게 관리, 분석할 수도 있습니다. 
{: shortdesc}

## DataStage
{: #datastage}

다음 지시사항은 데이터베이스를 카탈로그화하고 연결 오브젝트를 정의하여 IBM® InfoSphere® DataStage® <!--version 9.1 and later -->및 {{site.data.keyword.dashdbshort_notm}} 데이터베이스 간에 SSL을 사용하지 않고 연결을 정의하는 방법과 서드파티에서 발헹한 디지털 인증서를 사용하여 SSL로 연결을 작성하는 방법을 설명합니다.
{: shortdesc}

### 전제조건
{: #prereq1}

데이터 서버 클라이언트가 아직 설치되지 않은 경우, 클라이언트 시스템의 운영 체제에 적합한 IBM Data Server Client<!--Version 10.5 -->를 다운로드하여 설치하십시오. [IBM Data Server Client ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/marketing/iwm/iwm/web/preLogin.do?source=swg-idsc97){:new_window}.

SSL 프로토콜과 연결하려면 32비트 GSKit V8을 다운로드하여 설치하십시오. 클라이언트 시스템의 운영 체제에 적합한 OS 탭을 클릭하십시오. [GSKit V8 - 설치, 설치 제거 및 업그레이드 지시사항 ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.ibm.com/support/docview.wss?uid=swg21631462){:new_window}. 다음 운영 체제에서는 OS 특정 경로 환경 변수에 GSKit 설치 디렉토리 경로를 추가해야 합니다.

- AIX®: **LIBPATH**
   - `/usr/opt/ibm/gsk8/lib`
- Linux: **LD_LIBRARY_PATH**
    - `/usr/local/ibm/gsk8/lib`
- UNIX: **LD_LIBRARY_PATH**
    - `/opt/ibm/gsk8/lib`
- Windows: **PATH**
    - `<installation_directory>\gsk8\bin`
    - `<installation_directory>\gsk8\lib`

{{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하기 전에 먼저 필수 [전제조건](/docs/services/Db2whc/connecting/connecting.html#prereqs)이 있는지 확인하십시오.

### 프로시저
{: #proc1}

- SSL을 사용하여 연결을 작성하려면 다음 단계를 완료하십시오.

  1. 명령행 또는 터미널을 열고 DataStage 시스템에서 새 디렉토리를 작성하여 SSL 인증서와 키 파일을 저장하십시오.

     `# /home/db2inst2> mkdir SSL`

     `# /home/db2inst2> cd SSL`

  2. {{site.data.keyword.dashdbshort_notm}} 웹 콘솔의 **애플리케이션을 데이터베이스에 연결** 페이지에서 SSL 인증서를 다운로드하십시오.

     a. 기본 메뉴에서 **연결**을 클릭하십시오.
     
     b. **SSL을 사용하여 연결**을 클릭한 다음 **SSL 인증서(1KB)** 링크를 클릭하십시오.
     
     c. `DigiCertGlobalRootCA.crt` 인증서를 1단계에서 만든 SSL 디렉토리에 저장하십시오.
        
  3. **gsk8capicmd_64** 유틸리티를 사용하여 DataStage 시스템에 클라이언트 키 저장소를 작성하십시오.

     `# /home/db2inst2/SSL> gsk8capicmd_64 -keydb -create -db <keystore_db.kdb> -pw <ks_db_password> -stash`

     여기서, `<keystore_db.kdb>`는 클라이언트 키 저장소 데이터베이스를 나타내고 `<ks_db_password>`는 클라이언트 키 저장소 데이터베이스의 비밀번호를 나타냅니다.
        
  4. 클라이언트 키 저장소 데이터베이스에 인증서를 추가하십시오.

     `# /home/db2inst2/SSL> gsk8capicmd_64 -cert -add -db <keystore_db.kdb> -pw <ks_db_password> -label BLUDB_SSL -file DigiCertGlobalRootCA.crt`

     여기서, `<keystore_db.kdb>`는 클라이언트 키 저장소 데이터베이스를 나타내고 `<ks_db_password>`는 클라이언트 키 저장소 데이터베이스의 비밀번호를 나타냅니다.
    
  5. DataStage 서버에서 Db2 클라이언트를 구성하십시오.
            
     a. 데이터베이스 관리자에서 SSL 구성 매개변수를 업데이트하십시오.

     `# /home/db2inst2> db2 update dbm cfg using SSL_CLNT_KEYDB /home/db2inst2/SSL/<keystore_db.kdb>`

     여기서, `<keystore_db.kdb>`는 클라이언트 키 저장소 데이터베이스를 나타냅니다.

     `# /home/db2inst2> db2 update dbm cfg using SSL_CLNT_STASH /home/db2inst2/SSL/<keystore_db.sth>`

     여기서, `<keystore_db.sth>`는 클라이언트 키 저장소 데이터베이스 비밀번호 스태쉬를 나타냅니다.
            
     b. SSL 보안 옵션을 사용하여 대상 노드를 카탈로그화한 다음 대상 노드에서 BLUDB 데이터베이스를 카탈로그화하십시오.

     `# /home/db2inst2> db2 catalog tcpip node <node_name> remote <IP_addr_of_BLUDB_database_server> server 50001 security SSL`

     여기서, `<node_name>`은 대상 노드의 이름을 나타내고 `<IP_addr_of_BLUDB_database_server>`는 BLUDB 데이터베이스 서버의 IP 주소를 나타냅니다.

     `# /home/db2inst2> db2 catalog db BLUDB as <db_alias> at node <node_name>`

     여기서, `<db_alias>`는 {{site.data.keyword.dashdbshort_notm}} 데이터베이스의 이름입니다.

  6. 모든 사용자를 위해 SSL 디렉토리 내의 파일에 대해 읽기 및 실행 권한을 추가하십시오. 작업을 실행하는 DataStage 사용자는 이러한 파일에 액세스하여 Db2 데이터베이스에 대한 SSL 연결을 작성해야 합니다.

     `# /home/db2inst2/SSL> chmod 655 /home/db2inst2/SSL/*`

  7. 다음 방법 중 하나로 SSL 연결을 테스트하십시오.

     - CLP를 사용하여 연결을 테스트하십시오. 다음 명령을 실행하여 {{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하십시오.

       `db2 connect to <db_alias> user <user_id>`

       여기서, `<db_alias>`는 {{site.data.keyword.dashdbshort_notm}} 데이터베이스의 이름이고 `<user_id>`는 {{site.data.keyword.dashdbshort_notm}} 사용자 ID입니다. 비밀번호를 입력하라는 프롬프트가 표시됩니다.
    
     - CLI를 사용하여 연결을 테스트하십시오. 다음 명령을 실행하여 {{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하십시오.

       `db2cli validate -dsn <alias> -connect -user <user_id> -passwd <password>`

        여기서, `<alias>`는 **db2cli writecfg** 명령을 사용하여 작성한 별명이고, `<user_id>`는 {{site.data.keyword.dashdbshort_notm}} 사용자 ID이며, `<password>`는 {{site.data.keyword.dashdbshort_notm}} 비밀번호입니다.

- SSL을 사용하지 않고 연결을 작성하려면 다음 단계를 완료하여 대상 {{site.data.keyword.dashdbshort_notm}} 데이터베이스를 카탈로그화하십시오.

  1. 클라이언트 애플리케이션이 연결할 수 있도록 대상 {{site.data.keyword.dashdbshort_notm}} 노드를 카탈로그화하십시오. 다음 CLP 명령을 실행하십시오.

     `db2 catalog tcpip node <node_name> remote <IP_address_of_BLUDB_database_server> server <port_number_of_BLUDB_database>`

     여기서, `<node_name>`은 노드의 이름을 나타내고 `<IP_address_of_BLUDB_database_server>`는 BLUDB 데이터베이스 서버의 IP 주소를 나타내며 `<port_number_of_BLUDB_database>`는 BLUDB 데이터베이스의 포트 번호를 나타냅니다.

  2. 클라이언트 애플리케이션이 연결할 수 있도록 원격 {{site.data.keyword.dashdbshort_notm}} 데이터베이스를 카탈로그화하십시오. 다음 명령을 실행하십시오.

     `db2 catalog db BLUDB as <db_alias> at node <node_name>`

     여기서, `<db_alias>`는 {{site.data.keyword.dashdbshort_notm}} 데이터베이스의 이름을 나타내고 `<node_name>`은 노드의 이름을 나타냅니다.

  3. 다음 방법 중 하나로 비SSL 연결을 테스트하십시오.

      - CLP를 사용하여 연결을 테스트하십시오. 다음 명령을 실행하여 {{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하십시오.

        `db2 connect to <db_alias> user <user_id>`

        여기서, `<db_alias>`는 {{site.data.keyword.dashdbshort_notm}} 데이터베이스의 이름이고 `<user_id>`는 {{site.data.keyword.dashdbshort_notm}} 사용자 ID입니다. 비밀번호를 입력하라는 프롬프트가 표시됩니다.

        `db2 list tables`

      - CLI를 사용하여 연결을 테스트하십시오. 다음 명령을 실행하여 {{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하십시오.

        `db2cli validate -dsn <alias> -connect -user <user_id> -passwd <password>`

        여기서, `<alias>`는 **db2cli writecfg** 명령을 사용하여 작성한 별명이고, `<user_id>`는 {{site.data.keyword.dashdbshort_notm}} 사용자 ID이며, `<password>`는 {{site.data.keyword.dashdbshort_notm}} 비밀번호입니다.

  4. DataStage 클라이언트에서 연결을 정의하기 위해 미리 수집한 [연결 정보](/docs/services/Db2whc/connecting/credentials.html)를 사용하십시오. **매개변수** 탭에서 **스테이징 유형을 사용하여 연결** 필드에 **DB2 커넥터**를 선택해야 합니다.

     DataStage에서 연결을 정의하는 방법에 관한 세부사항은 다음 DataStage 문서 주제를 참조하십시오. 
     
     - [수동으로 데이터 연결 오브젝트 작성 ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/support/knowledgecenter/SSZJPZ_11.3.0/com.ibm.swg.im.iis.ds.design.doc/topics/t_ddesref_Creating_a_Data_Connection_Object_Manually.html){:new_window}
     - [Db2 데이터베이스에 대한 액세스 구성 ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/support/knowledgecenter/en/SSZJPZ_11.7.0/com.ibm.swg.im.iis.conn.common.usage.doc/topics/t_configuring_db2conn.html){:new_window}

## Informatica
{: #informatica}

데이터 관리를 위해 {{site.data.keyword.dashdbshort_notm}}에 Informatica를 연결할 수 있습니다.
{: shortdesc}

{{site.data.keyword.dashdbshort_notm}}를 Informatica 클라우드와 통합하는 방법을 보려면 이 동영상을 시청하십시오.

<iframe class="embed-responsive-item" id="youtubeplayer1" title="DB2 연결 - Informatica 클라우드와 빠르게 연결하는 방법" type="text/html" width="640" height="390" src="//www.youtube.com/embed/TUiS_HstLnU?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

<!-- To configure a native Db2 connection to connect to {{site.data.keyword.dashdbshort_notm}}, perform the following steps:

1. Run the `odbcad32.exe` file from your local system.
The ODBC Data Sources Administrator dialog box appears.

2. Create the 32-bit ODBC Data Source Name using the DataDirect Db2 drivers.

3. In the ODBC DB2 Wire Protocol Setup dialog box, click **Security** tab.

4. Set the value of the `Authentication Method` property as `1 -Encrypt Password`. The following image shows the **Security** tab in the ODBC DB2 Wire Protocol Setup dialog box where you can set the `Authentication Method` property:
             
   ![ODBC Db2 Wire Protocol Driver Setup - Security tab](images/odbc_driver.png)
       
5. In the ODBC DB2 Wire Protocol Setup dialog box, click **Modify Bindings** tab.

6. Enter your user name in the Package Collection property. The following image shows the **Modify Bindings** tab in the ODBC DB2 Wire Protocol Setup dialog box where you can set the `Package Collection` property: 

   ![ODBC Db2 Wire Protocol Driver Setup - Modify Bindings tab](images/odbc_driver_2.png)
            
7. In the PowerCenter Designer, use the data source name that you created to import the metadata.

8. In the PowerCenter Workflow Manager, create the required workflow.

9. Ensure that you have the {{site.data.keyword.dashdbshort_notm}} compatible 11.x Db2 clients when you run the workflow.

**Note**: If you want to set the authentication type when you create the Db2 client catalog, you could specify the value of the `AUTHENTICATION TYPE` property as `SERVER_ENCRYPT`. -->

<!-- Watch this video to see how to integrate Db2 and Salesforce with Informatica Cloud.

<iframe class="embed-responsive-item" id="youtubeplayer2" title="Integrate Db2 and Salesforce with Informatica Cloud" type="text/html" width="640" height="390" src="//www.youtube.com/watch?v=RGTLweZvKP8" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe> -->

<!-- [Informatica ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://kb.informatica.com/howto/6/Pages/20/522402.aspx?myk=Connect%20to%20Db2){:new_window} -->

## Lift
{: #lift}

Lift를 사용하여 데이터를 {{site.data.keyword.dashdbshort_notm}}에 마이그레이션하십시오.

[Lift ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://lift.ng.bluemix.net/#docs){:new_window}

## InfoSphere Data Replication
{: #idr}

IBM® InfoSphere® Data Replication<!--version 11.3.3.3-36 or later -->을 {{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결할 수 있습니다. 이 기능은 SMP및 MPP 환경 모두에 적용됩니다. 이는 {{site.data.keyword.dashdbshort_notm}}의 엔트리 플랜에는 적용되지 않습니다. 
{: shortdesc}

### 개요
{: #overview2}

이상적으로는 IBM InfoSphere Data Replication을 {{site.data.keyword.dashdbshort_notm}}에 연결하는 경우 IBM InfoSphere Data Replication은 {{site.data.keyword.dashdbshort_notm}}와 동일한 {{site.data.keyword.Bluemix_notm}} 데이터 센터에 있거나 {{site.data.keyword.dashdbshort_notm}}와 함께 있습니다. IBM InfoSphere Data Replication은 로컬 서버에서 원격 {{site.data.keyword.dashdbshort_notm}} 인스턴스로 연결합니다.

{{site.data.keyword.dashdbshort_notm}}를 연결 대상으로 사용하는 경우 IBM InfoSphere Data Replication의 부분적인 성능은 대상 엔진을 {{site.data.keyword.dashdbshort_notm}} 인스턴스에서 분리하는 네트워크의 대역폭에 따라 다릅니다. 물리적 거리도 성능에 영향을 줍니다. 이상적으로는 IBM InfoSphere Data Replication이 {{site.data.keyword.dashdbshort_notm}} 인스턴스에 가능한 한 가까이 있습니다. 네트워크 토폴로지도 성능에 영향을 줍니다. 예를 들어, 이상적으로는 IBM InfoSphere Data Replication 대상 엔진이 대상 인스턴스와 동일한 VPN(보안 도메인)에 있는 VM에서 실행됩니다. 순회할 네트워크 노드(예: 방화벽 또는 라우터) 수가 적을수록 좋습니다. 

### 전제조건
{: #prereq2}

SSL 프로토콜을 사용하여 연결하려면 GSKit V8을 다운로드하여 설치하십시오. [GSKit V8 - 설치, 설치 제거 및 업그레이드 지시사항 ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.ibm.com/support/docview.wss?uid=swg21631462){:new_window}. 클라이언트 시스템의 운영 체제에 해당되는 운영 체제 탭을 클릭하십시오. Windows 컴퓨터에 GSKit을 설치하는 경우 **`PATH`** 환경 변수에 GSKit 설치 디렉토리 경로(`<installation_directory>\gsk8\bin`)를 지정했는지 확인하십시오.

{{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하기 전에 먼저 필수 [전제조건](/docs/services/Db2whc/connecting/connecting.html#prereqs)이 있는지 확인하십시오.

SSL 프로토콜을 사용하여 연결하려면 웹 콘솔에서 클라이언트 시스템의 디렉토리로 `DigiCertGlobalRootCA.crt` SSL 인증서를 다운로드하십시오. 인증서를 다운로드하려면 **연결 > 연결 정보**를 클릭한 다음 **SSL을 사용하여 연결** 탭을 클릭하십시오.

### 프로시저
{: #proc2}

1. 다음 방법 중 하나를 선택하여 연결을 작성하십시오.

   - SSL을 사용하여 연결을 작성하려면 다음 단계를 완료하십시오.
            
     a. 다음 명령을 실행하십시오.

     `cd /<ssl_directory_name>/ssl`

     여기서, `/<ssl_directory_name>/ssl`은 `DigiCertGlobalRootCA.crt` SSL 인증서를 다운로드한 디렉토리 경로입니다.

     b. **GSKCapiCmd** 도구를 사용하여 클라이언트 키 데이터베이스 및 스태쉬 파일을 작성하십시오. 예를 들어, 다음 명령은 `dashclient.kdb`라는 클라이언트 키 데이터베이스 및 `dashclient.sth`라는 스태쉬 파일을 작성합니다.

     `gsk8capicmd_64 -keydb -create -db "dashclient.kdb" -pw "passw0rdpw0" -stash`

     여기서, `passw0rdpw0`은 비밀번호입니다. **-stash** 옵션은 클라이언트 키 데이터베이스와 동일한 경로에 파일 확장자가 `.sth`인 스태쉬 파일을 작성합니다. 연결 시에 GSKit가 스태쉬 파일을 사용하여 클라이언트 키 데이터베이스에 대한 비밀번호를 얻습니다.
            
     c. 클라이언트 키 데이터베이스에 인증서를 추가하십시오. 예를 들어, 다음 **gsk8capicmd** 명령은 `/<ssl_directory_name>/ssl/DigiCertGlobalRootCA.crt` 파일에서 `dashclient.kdb`라는 클라이언트 키 데이터베이스로 인증서를 가져옵니다.

     `gsk8capicmd_64 -cert -add -db "dashclient.kdb" -pw "passw0rdpw0" -label "DigiCert" -file "/<ssl_directory_name>/ssl/DigiCertGlobalRootCA.crt" -format ascii -fips`

     d. 클라이언트 키 데이터베이스 및 스태쉬 파일을 지정하려면 클라이언트에서 `SSL_CLNT_KEYDB` 및 `SSL_CLNT_STASH` 데이터베이스 관리자 구성 매개변수의 값을 업데이트하십시오. 예는 다음과 같습니다.

     `db2 update dbm cfg using SSL_CLNT_KEYDB /<ssl_directory_name>/ssl/dashclient.kdb`

     `db2 update dbm cfg using SSL_CLNT_STASH /<ssl_directory_name>/ssl/dashclient.sth`

     e. 클라이언트 애플리케이션이 연결할 수 있도록 {{site.data.keyword.dashdbshort_notm}} 노드를 카탈로그화하십시오. 다음 명령을 실행하십시오.

     `db2 catalog tcpip node <node_name> remote <Db2_Warehouse_IP_address> server <port_number> security ssl`

     여기서,
                
     `<node_name>`은 노드의 이름입니다.

     `<Db2_Warehouse_IP_address>`는 Db2 Warehouse on Cloud 서버의 IP 주소입니다.

     `<port_number>`는 SSL 연결을 사용하여 Db2 Warehouse에 연결하는 데 사용되는 포트입니다. 기본 포트를 사용하는 경우 `50001`을 지정하십시오.
            
     f. 클라이언트 애플리케이션이 연결할 수 있도록 원격 {{site.data.keyword.dashdbshort_notm}} 데이터베이스를 카탈로그화하십시오. 다음 명령을 실행하십시오.

     `db2 catalog database bludb as <db_alias> at node <node_name>`

     여기서, `db_alias`는 {{site.data.keyword.dashdbshort_notm}} 데이터베이스의 이름입니다.
            
     g. 다음 방법 중 하나로 SSL 연결을 테스트하십시오.
                
     - {{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하는 다음 명령을 실행하여 CLP를 사용하는 연결을 테스트하십시오.

       `db2 connect to <db_alias> user <user_id>`

       여기서, `<user_id>`는 {{site.data.keyword.dashdbshort_notm}} 사용자 ID입니다. 비밀번호를 입력하라는 프롬프트가 표시됩니다.
                
     - {{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하는 다음 명령을 실행하여 CLI를 사용하는 연결을 테스트하십시오.

       `db2cli validate -dsn <alias> -connect -user <user_id> -passwd <password>`

       여기서, `<alias>`는 **db2cli writecfg** 명령을 사용하여 작성한 DSN 별명이고, `<user_id>`는 {{site.data.keyword.dashdbshort_notm}} 사용자 ID이며, `<password>`는 {{site.data.keyword.dashdbshort_notm}} 데이터베이스 비밀번호입니다.
        
   - SSL을 사용하지 않고 연결을 작성하려면 다음 단계를 완료하십시오.

     a. 클라이언트 애플리케이션이 연결할 수 있도록 {{site.data.keyword.dashdbshort_notm}} 노드를 카탈로그화하십시오. 다음 명령을 실행하십시오.

     `db2 catalog tcpip node <node_name> remote <Db2_Warehouse_IP_address> server <port_number>`

     여기서,
                
     `<node_name>`은 노드의 이름입니다.

     `<Db2_Warehouse_IP_address>`는 {{site.data.keyword.dashdbshort_notm}} 서버의 IP 주소입니다.

     `<port_number>`는 SSL 연결을 사용하지 않고 {{site.data.keyword.dashdbshort_notm}}에 연결하는 데 사용되는 포트입니다. 기본 포트를 사용하는 경우 `50000`을 지정하십시오.
            
     b. 클라이언트 애플리케이션이 연결할 수 있도록 원격 {{site.data.keyword.dashdbshort_notm}} 데이터베이스를 카탈로그화하십시오. 다음 명령을 실행하십시오.

     `db2 catalog database bludb as <db_alias> at node <node_name>`

     여기서, `<db_alias>`는 {{site.data.keyword.dashdbshort_notm}} 데이터베이스의 이름입니다.

     c. 다음 방법 중 하나로 비SSL 연결을 테스트하십시오.

     - {{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하는 다음 명령을 실행하여 CLP를 사용하는 연결을 테스트하십시오.

       `db2 connect to <db_alias> user <user_id>`

       여기서, `<user_id>`는 {{site.data.keyword.dashdbshort_notm}} 사용자 ID입니다. 비밀번호를 입력하라는 프롬프트가 표시됩니다.
                
     - {{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하는 다음 명령을 실행하여 CLI를 사용하는 연결을 테스트하십시오.

       `db2cli validate -dsn <alias> -connect -user <user_id> -passwd <password>`

       여기서, `<alias>`는 **db2cli writecfg** 명령을 사용하여 작성한 DSN 별명이고, `<user_id>`는 {{site.data.keyword.dashdbshort_notm}} 사용자 ID이며, `<password>`는 Db2 Warehouse on Cloud 비밀번호입니다.
    
2. InfoSphere Data Replication 구성 도구를 실행하고 다음 단계를 수행하십시오. 화면 캡처에 표시되는 값은 예입니다.
        
   a. **인스턴스 구성** 탭을 사용하여 소스 데이터베이스를 지정하도록 소스 인스턴스를 추가하십시오.

   ![IIDR 새 인스턴스 - 소스 인스턴스](images/IIDR_source_instance.jpg)

   b. **인스턴스 구성** 탭을 사용하여 대상 Db2 데이터베이스를 지정하도록 대상 인스턴스를 추가하십시오. IBM InfoSphere Data Replication 11.3.3.3-50 이상을 사용하지 않는 경우 **새로 고침 로더 경로 지정** 선택란을 선택하지 마십시오.

   ![IIDR 새 인스턴스 - 대상 인스턴스](images/IIDR_target_instance.jpg)

   c. 각 인스턴스를 시작하십시오.

   ![IIDR 구성 도구](images/IIDR_instances.jpg)

3. InfoSphere Data Replication 관리 콘솔을 실행하고 액세스 관리자를 사용하여 다음 단계를 완료하십시오.
        
   a. **데이터 저장소** 탭을 사용하여 소스 인스턴스에 연결할 데이터 저장소를 작성하십시오. Db2 데이터베이스는 원래 소스 데이터베이스로 지원되지 않으므로 **연결 매개변수**를 클릭하여 소스 데이터베이스에 대한 사용자 및 비밀번호 정보를 제공해야 합니다.

   ![데이터 저장소 특성 - 소스](images/IIDR_source_datastore.jpg)

   b. **데이터 저장소** 탭을 사용하여 대상 인스턴스에 연결할 데이터 저장소를 작성하십시오. **연결 매개변수**를 클릭하여 사용자 및 비밀번호 정보를 제공해야 합니다.

   ![데이터 저장소 특성 - 대상](images/IIDR_target_datastore.jpg)

   c. 액세스 서버에 연결할 사용자(예: admin)가 없으면 해당 사용자를 작성하십시오.

   ![새 사용자](images/IIDR_management_user.jpg)

   d. **액세스 관리자** 탭을 클릭하십시오.
        
   e. **데이터 저장소 관리** 탭에서 각 데이터 저장소를 마우스 오른쪽 단추로 클릭한 다음 **사용자 지정**을 클릭하여 사용자를 소스 및 대상 데이터 저장소 모두에 지정하십시오. 각 인스턴스에 액세스하는 데 필요한 인증 정보가 올바른지 확인하십시오.

   ![IIDR 관리 콘솔 - 액세스 관리자](images/IIDR_management_assign_user.jpg)

### 다음에 수행할 작업
{: #what2}

구독을 정의하고 데이터 복제를 수행하십시오. 자세한 정보는 다음을 참조하십시오.

- [InfoSphere Data Replication에서 데이터 로드 ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/learn_how/loaddata_iidr.html){:new_window} 

## Segment
{: #segment}

Segment를 {{site.data.keyword.dashdbshort_notm}} 데이터베이스와 통합할 수 있습니다. Segment는 사용자 데이터를 수 백개의 여러 도구에 수집, 저장 및 라우팅하는 단일 플랫폼입니다.
{: shortdesc}

[Segment ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://segment.com/docs/destinations/db2/){:new_window}

## Data Studio
{: #data_studio}

다음 지시사항은 IBM® Data Studio<!--version 4.1.x -->에서 {{site.data.keyword.dashdbshort_notm}} 데이터베이스로 연결을 작성하는 방법을 설명합니다.
{: shortdesc}

### 전제조건
{: #prereq3}

{{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하기 전에 먼저 필수 [전제조건](/docs/services/Db2whc/connecting/connecting.html#prereqs)이 있는지 확인하십시오.

### 프로시저
{: #proc3}

1. Data Studio에서 **모든 데이터베이스 > 데이터베이스에 대한 새 연결**을 클릭하십시오.

2. **로컬** 탭에서 **Linux, UNIX 및 Windows용 DB2**를 데이터베이스 관리자로 선택하십시오.
    
3. **일반** 탭에서 다음 값을 입력하십시오.
   - *데이터베이스*: `BLUDB`
   - *호스트*: 호스트 이름.
   - *포트*: SSL을 사용하지 않는 연결의 경우 `50000`을 입력하십시오. SSL을 사용하는 연결의 경우 `50001`을 입력하십시오. 
   - *사용자 이름*: 로그인하는 데 사용하는 사용자 이름.
   - *비밀번호*: 로그인하는 데 사용하는 비밀번호.

4. SSL 연결의 경우, **선택사항** 탭을 클릭한 다음 **추가**를 클릭하십시오. `sslConnection` 특성의 경우, `true`를 지정하십시오.

5. [*선택사항*]: 단추 **연결 테스트**를 클릭하여 연결이 성공적인지 확인하십시오.

## Data Server Manager(DSM)
{: #dsm}

IBM® Data Server Manager 및 {{site.data.keyword.dashdbshort_notm}} 데이터베이스 간의 연결을 사용하면 Data Server Manager 웹 콘솔에서 데이터베이스를 모니터하고 관리할 수 있습니다. 
{: shortdesc}

### 전제조건
{: #prereq4}

{{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하기 전에 먼저 필수 [전제조건](/docs/services/Db2whc/connecting/connecting.html#prereqs)이 있는지 확인하십시오.

### 프로시저
{: #proc4}

<!--The connection procedure was tested on Data Server Manager version 1.1. The same procedure applies to all of the other versions of the Data Server Manager software.
-->
연결을 작성하려면 다음 단계를 완료하십시오.

1. Data Server Manager 웹 콘솔에 로그인하십시오.
    
2. Data Server Manager 웹 콘솔에서 **설정 > 데이터베이스 연결**로 이동하십시오.
    
3. ![원 내의 + 부호](images/icon_R_plus.gif) 아이콘을 클릭하여 데이터베이스 연결을 추가하십시오. **데이터베이스 연결** 탭 아래의 **데이터베이스 연결 추가** 페이지에서 다음 필드에 필수 정보를 입력하십시오.

   - *데이터베이스 연결 이름*: 이 이름은 Data Server Manager에 고유해야 합니다.
   - *데이터 서버 유형*: 드롭 다운 메뉴에서 **Linux, UNIX 및 Windows용 DB2**를 선택하십시오.
   - *데이터베이스 이름*: `BLUDB`
   - *호스트 이름*: {{site.data.keyword.dashdbshort_notm}} 호스트 이름을 입력하십시오. 
   - *포트 번호*: SSL을 사용하지 않는 연결의 경우 `50000`을 입력하십시오. SSL을 사용하는 연결의 경우 `50001`을 입력하십시오. 
   - *JDBC 보안*: 드롭 다운 메뉴에서 **텍스트 비밀번호 지우기**를 선택하십시오.
   - *사용자 ID*: {{site.data.keyword.dashdbshort_notm}} 사용자 ID 
   - *비밀번호*: {{site.data.keyword.dashdbshort_notm}} 비밀번호 

4. SSL을 사용하는 연결의 경우 **고급 JDBC 특성** 탭을 선택하십시오. 다음 필드에 필수 정보를 입력하십시오.

   - *특성*: `sslConnection`
   - *값*: `true`

    **추가** 단추를 클릭하십시오. **데이터베이스 연결** 탭을 선택하십시오.
    
5. **연결 테스트** 단추를 클릭하여 연결을 테스트하십시오. 연결에 성공하면 **확인**을 클릭하십시오.

## InfoSphere Data Architect
{: #ida}

다음 지시사항은 InfoSphere® Data Architect<!--version 9.1.x -->에서 {{site.data.keyword.dashdbshort_notm}} 데이터베이스로 연결을 작성하는 방법을 설명합니다.
{: shortdesc}

### 전제조건
{: #prereq5}

{{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하기 전에 먼저 필수 [전제조건](/docs/services/Db2whc/connecting/connecting.html#prereqs)이 있는지 확인하십시오.

### 프로시저
{: #proc5}

1. InfoSphere Data Architect의 Data Source Explorer 보기에서 **데이터베이스 연결**을 마우스 오른쪽 단추로 클릭한 다음 **새로 작성**을 선택하십시오.
    
2. **로컬** 탭에서 **Linux, UNIX 및 Windows용 DB2**를 데이터베이스 관리자로 선택하십시오.
    
3. **일반** 탭에서 다음 값을 입력하십시오.

   - *데이터베이스*: `BLUDB`
   - *호스트*: 미리 수집한 호스트 이름.
   - *포트*: SSL을 사용하지 않는 연결의 경우 `50000`을 입력하십시오. SSL을 사용하는 연결의 경우 `50001`을 입력하십시오. 
   - *사용자 이름*: 미리 수집한 사용자 ID.
   - *비밀번호*: 미리 수집한 비밀번호.

4. SSL 연결의 경우, **선택사항** 탭을 클릭하십시오. `sslConnection` 특성을 입력하고 `true` 값을 지정하십시오. **추가**를 클릭하십시오.
    
5. [*선택사항*]: 단추 **연결 테스트**를 클릭하여 연결이 성공적인지 확인하십시오.

## Aginity Workbench
{: #aginity_wb}

다음 지시사항은 Aginity Workbench<!--4.3 -->를 {{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하는 방법을 설명합니다. Aginity Workbench를 사용하여 IBM PureData for Analytics(Netezza) 데이터 모델과 데이터를 {{site.data.keyword.dashdbshort_notm}}로 마이그레이션할 수 있습니다.
{: shortdesc}

### 전제조건
{: #prereq6}

{{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하기 전에 먼저 필수 [전제조건](/docs/services/Db2whc/connecting/connecting.html#prereqs)이 있는지 확인하십시오.

### 프로시저
{: #proc6}

1. Aginity Workbench를 다운로드하여 설치하십시오.

2. 앞에서 언급한 연결 정보에서 ODBC DSN을 판별하십시오.

3. Aginity Workbench를 실행하십시오. 데이터베이스 연결 대화 상자가 자동으로 열리지 않으면 도구 모음에서 **연결**을 클릭하여 여십시오.

4. [데이터베이스 연결 설정 ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.aginity.com/documentation/WB/dashDB/Default.htm#Aginity_Topics/Aginity_Workbench/Database_Connection_Dialog_Box.htm){:new_window}. 앞에서 언급한 연결 정보에서 호스트 이름, 사용자 ID 및 비밀번호를 사용하십시오.

## CLPPlus
{: #clpplus}

명령행 프로세서 플러스(CLPPlus)는 Db2 드라이버 패키지에 포함되어 있습니다. CLPPlus는 {{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하는 데 사용할 수 있는 명령행 인터페이스를 제공합니다. CLPPlus를 사용하여 명령문, 스크립트 및 명령을 정의, 편집 및 실행할 수 있습니다.
{: shortdesc}

### 전제조건
{: #prereq7}

{{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하기 전에 먼저 필수 [전제조건](/docs/services/Db2whc/connecting/connecting.html#prereqs)이 있는지 확인하십시오.

CLPPlus를 사용하려면 소프트웨어 개발 킷(SDK) 또는 Java 버전 1.5.0 이상용 Java 런타임 환경(JRE)이 컴퓨터에 설치되어 있고 해당 환경 변수가 다음과 같이 설정되어야 합니다.

- `JAVA_HOME` 환경 변수가 컴퓨터의 Java 설치 디렉토리로 설정되어 있습니다.
- `PATH` 환경 변수 설정이 컴퓨터에 있는 Java 설치 디렉토리의 `bin` 서브디렉토리를 포함합니다.

### 프로시저
{: #proc7}

1. Linux 운영 체제의 명령 쉘, Windows 명령 프롬프트 또는 Windows 운영 체제의 DB2 명령 창에서 다음 명령을 실행하십시오.

   이 명령은 컴퓨터의 드라이버 구성 파일(`db2dsdriver.cfg`)에 새 항목을 작성하고 연결 속성을 설정합니다. 이 단계는 한 번만 수행해야 합니다.

   - SSL을 사용하는 연결의 경우:

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50001 -parameter "SecurityTransportMode=SSL"`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50001`  

     여기서,
     
     - `<hostname>`은 서버의 호스트 이름입니다.
     - `<alias>`는 사용자가 선택한 별명입니다.

   - SSL을 사용하지 않는 연결의 경우:

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50000`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50000`

2. `db2dsdriver.cfg` 파일의 항목을 사용하는 {{site.data.keyword.dashdbshort_notm}} 데이터베이스에 대한 연결을 통해 CLPPlus를 시작하려면 다음 명령을 실행하십시오.

   - Windows 환경: 

     `clpplus <userid>@<alias>`

   - Linux 환경:

     `clpplus -nw <userid>@<alias>`

     여기서,
     
     - `<userid>`는 미리 수집한 연결 인증 정보의 사용자 ID입니다.
     - `<alias>`는 **db2cli writecfg** 명령을 사용하여 작성한 별명입니다.

   이 명령을 실행하면 CLPPlus 창이 열립니다.

3. CLPPlus 창에서 비밀번호를 입력하십시오. 데이터베이스 정보가 표시되고 그 뒤에 SQL 프롬프트가 표시됩니다. 샘플 출력은 다음과 같습니다.

```
   Hostname = 192.0.2.0
   Database server = DB2/LINUXX8664  SQL10054
   SQL authorization ID = smith
   Local database alias = BLUDB
   Port = 50001
   
   SQL>
```

### 결과
{: #results7}

이제 CLPPlus 명령 또는 SELECT문을 입력하고 스크립트를 실행하여 데이터베이스의 데이터에 대한 작업을 수행할 수 있습니다.

### 예

다음 예에서는 샘플 테이블 `GOSALES.BRANCH`에서 행을 검색하는 짧은 스크립트를 사용합니다. 스크립트 파일의 이름은 `cities.sql`이고 이 파일은 로컬 Windows 컴퓨터의 `C:\temp` 디렉토리에 있습니다. `cities.sql` 파일에는 다음 텍스트가 포함되어 있습니다.

```
SET ECHO ON
SELECT branch_code, city from GOSALES.BRANCH;
```

#### 예 1 

스크립트를 대화식으로 실행하려면 다음을 수행하십시오.

1. 다음 명령을 실행하여 `db2dsdriver.cfg` 파일에 작성한 사용자 ID와 별명으로 CLPPlus를 시작하십시오.

   `clpplus <user_id>@<alias>`
2. 비밀번호를 입력하십시오.
3. SQL 프롬프트에 다음 텍스트를 입력하십시오.

   `start C:\temp\cities.sql`

#### 예 2

`db2dsdriver.cfg` 파일에 작성한 사용자 ID와 별명을 사용하여 CLPPlus를 시작하고 스크립트를 한 번에 실행하십시오.

`clpplus <user_id>/<password>@<alias> @C:\temp\cities.sql`

`cities.sql` 스크립트의 샘플 출력은 다음과 같습니다.

```
BRANCH_CODE CITY
----------- --------------------------------------------------
          6 Paris
          7 Milano
          9 Amsterdam
         13 Hamburg
         14 München
         15 Kista
         17 Calgary
         18 Toronto
         19 Boston
         20 Seattle
         21 Los Angeles
         22 Miami
         23 Lyon
         24 Distrito Federal
         25 Tokyo
         26 Osaka City
         28 Melbourne
         29 Bilbao
         30 Sao Paulo
         31 Kuopio
         32 Seoul
         33 Singapore

BRANCH_CODE CITY
----------- --------------------------------------------------
         34 Shanghai
         35 London
         36 Birmingham
         37 Zürich
         38 Heverlee
         39 Wien
         40 Geneve

29 rows were retrieved.
```


