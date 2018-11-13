---

copyright:
  years: 2014, 2018
lastupdated: "2018-09-25"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# JDBC를 사용하여 프로그래밍 방식으로 연결

Java™ 애플리케이션과 {{site.data.keyword.dashdbshort_notm}} 데이터베이스 간의 연결을 정의합니다.
{: shortdesc}

## 전제조건

{{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하기 전에 먼저 필수 [전제조건](connecting.html#prereqs)이 있는지 확인하십시오.

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## 프로시저

각 Java 애플리케이션에서 **DriverManager.getConnection** 메소드를 포함시켜 사용자 ID 및 비밀번호를 지정하고 다음 JDBC URL 문자열 중 하나를 포함시키십시오.

- SSL을 사용하는 연결의 경우:

  `jdbc:db2://<host_name>:50001/BLUDB:sslConnection=true;`

- SSL을 사용하지 않는 연결의 경우:

  `jdbc:db2://<host_name>:50000/BLUDB`


