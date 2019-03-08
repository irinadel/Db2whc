---

copyright:
  years: 2014, 2019
lastupdated: "2018-07-18"

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

# 데이터 가상화(연합)
{: #data_virt_fed}

Db2 데이터 가상화(연합이라고도 함)는 {{site.data.keyword.dashdbshort_notm}}를 통해 지원합니다. 데이터 가상화를 사용하면 조직 전체의 여러 분산 데이터베이스에 있는 모든 데이터에 단일 조회 액세스가 가능합니다. 클라우드와 온프레미스 둘 다에서 Db2 또는 Informix 데이터 소스에 있는 데이터에 액세스할 수 있습니다. 
{: shortdesc}

이 기능은 엔트리 플랜을 제외한 모든 버전의 {{site.data.keyword.dashdbshort_notm}}에서 지원됩니다. 그러나 데이터를 가져올 수 있는 대상으로 엔트리 플랜을 사용할 수 있습니다.

## 유스 케이스
{: #use_cases}

### 데이터 소스 통합

조직 전체의 클라우드와 온프레미스 둘 다에 있는 데이터 소스를 연합하면 가상화된 데이터를 단일 소스에서 검색하는 것처럼 보입니다. 데이터 가상화를 수행하면 고비용의 부담스러운 데이터 마이그레이션 프로세스가 제거되므로 모든 데이터를 효과적이고 비용 효율적인 방식으로 분석할 수 있습니다.

<!-- A company may have started their operations with an on-premises Db2 server. As cloud technology becomes more widespread and companies start to operate on cloud in a cost-effective fashion, there will be continued Cloud growth. However, the organization’s data on both sources remain as a critical component to their decision-making processes. By way of example, a client operating in retail industry needs to be able to access all data, say customer information, to run further analysis on their customers’ consumption behaviors. They need to be able to identify customers, match their records on cloud with already existing ones from an on-premises database and compose them as if the data is being retrieved from a single source. Federation capability here prevents the burdensome data migration process and allows the user to access the data without moving the data.

located in the cloud and on-premises -->

### Db2 on Cloud에 접속

Db2 제품군의 제품 사용자는 {{site.data.keyword.Db2_on_Cloud_short}} 및 {{site.data.keyword.dashdbshort_notm}} 데이터베이스의 데이터를 연합할 수 있습니다. 데이터에 액세스하는 일반적인 인터페이스를 통해 복잡한 ETL 프로세스와 추가 코드 없이 쉽게 데이터를 추가, 조회 및 분석할 수 있습니다.

<!-- Db2 family users would now be able to federate data between Db2 on Cloud and Db2 Warehouse on Cloud. By being provided a common interface for accessing the data, a user can now easily add or query data from or to the Warehouse without complex ETL processes or any additional code. -->

<!-- ### Sharded data across multiple servers

At times, you might choose to partition (shard) your data. With federation capabilities, sharded data can be queried with a unified interface. Federation gives you the ability to better balance your workloads, scale specific parts of an app, and create microservices that work together. -->

<!-- At times, users may choose to partition (shard). With federation capabilities, data can be queried with a unified interface and this lets the user better balance the workload, scale specific parts of an app or create microservices that work together. -->

### 고정 한계 이상으로 데이터베이스 용량 증가

연합하면 클라우드의 데이터베이스와 연합하여 온프레미스 데이터베이스의 용량을 늘릴 수 있습니다. 따라서 온프레미스 데이터베이스의 스토리지 공간이 부족한 경우 데이터 가상화를 선택하는 것이 좋습니다. 개발자가 프로덕션에 있는 기존 데이터베이스를 변경하지 않아도 되므로 새로 개발할 때 연합을 사용하여 데이터베이스 용량을 늘리면 유용합니다. 두 {{site.data.keyword.dashdbshort_notm}} 데이터베이스를 연합하여 데이터 용량을 현재 Flex 플랜 한계 이상으로 늘릴 수 있습니다.

<!-- By using federation, users can increase capacity of an on premises database by federating to or from the cloud. This is a great option if your on premises database is running out of storage. Increased capacity will also be useful for new development as our users no longer need to change a database in production. You can also use this feature to federate between two Db2 on Cloud databases to increase the capacity beyond the current limits of the Flex plan. -->

## 시작하기
{: #gtng_strtd}

다음 단계는 서로 다른 데이터 소스를 연합하여 단일 소스에서 데이터를 검색하는 것처럼 보이게 하는 방법을 보여주는 예입니다. 다음 예에서는 두 개의 {{site.data.keyword.dashdbshort_notm}} 데이터베이스를 연합하는 데 관해 설명합니다.

### Db2 Warehouse on Cloud 대상 시스템의 경우
{: #targ}

호스트 이름: targetdotcom

1. `admin2` 스키마에서 `testdata` 테이블을 작성합니다.

2. {{site.data.keyword.dashdbshort_notm}} 콘솔에서 `admin2`로 비밀번호 `YYYY`를 사용하여 `testdata` 테이블을 로드합니다.

### 연합 소스로 사용 중인 Db2 Warehouse on Cloud 시스템의 경우
{: #fed_src}

{{site.data.keyword.dashdbshort_notm}} 콘솔에서 다음을 수행하십시오.

<!-- 1. Catalog the target machine:<br/>
   `db2 catalog tcpip node <node_name> remote <host_name> server 50000`<br/>

   For example:<br/>
   `db2 catalog tcpip node fedS remote targetdotcom server 50000`

2. Catalog the database on fedS:<br/>
   `db2 catalog db bludb as <db_name> at node <node_name>`

   For example:<br/>
   `db2 catalog db bludb as srcdb at node fedS`

3. Connect to the database on fedS:<br/>
   `db2 connect to <catalog_db_name> user <admin_user> using '<admin_password>'`

   For example:<br/>
   `db2 connect to srcdb user 'admin1' with password 'XXXX'`

4. Create a wrapper on fedS:<br/>
   `db2 "create wrapper drda"` -->

1. 대상 시스템과 통신할 서버를 작성합니다.<br/>
   `create server <server_name> type dashdb version 11 wrapper drda authorization "<admin_user_on_target>" password "<admin_password_on_target>" options (host '<target_host_name>', port '50000', dbname 'bludb')`

   예를 들어, 다음과 같습니다.<br/>
   `create server db2server type dashdb version 11 wrapper drda authorization "admin2" password "YYYY" options (host 'targetdotcom', port '50000', dbname 'bludb')`

2. admin2의 사용자 맵핑을 작성합니다.<br/>
   `create user mapping for <admin_user> server db2server options (remote_authid '<admin_user_on_target>', remote_password '<admin_password_on_target>')`

   예를 들어, 다음과 같습니다.<br/>
   `create user mapping for admin1 server db2server options (remote_authid 'admin2', remote_password 'YYYY')`

3. 데이터베이스의 닉네임을 작성합니다.<br/>
   `create nickname <nickname> for <server_name>.<schema_name>.<table_name>`

   예를 들어, 다음과 같습니다.<br/>
   `create nickname ntest1 for db2server.admin2.testdata`

4. 대상 서버에서 데이터를 가져올 수 있는지 테스트합니다.<br/>
   `select * from <nickname>`

   예를 들어, 다음과 같습니다.<br/>
   `select * from ntest1`

## 추가 정보

데이터 가상화(연합)에 관한 자세한 정보는 [연합 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/fcontainer.html){:new_window}을 참조하십시오.

연합을 통해 지원하는 데이터 소스에 관한 정보는 [연합 지원 데이터 소스 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/support/docview.wss?uid=swg27050561){:new_window}를 참조하십시오.
