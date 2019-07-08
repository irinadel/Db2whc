---

copyright:
  years: 2014, 2019
lastupdated: "2019-04-16"

keywords:

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

# 재해 복구(DR)
{: #dr}

<!-- If your data warehouse instance is deployed in a data center that suffers a significant data center outage with an expected downtime of more than 8 hours, you will be sent a request to allow service operators to fail over your instance to another data center before disaster recovery actions can begin.
{: shortdesc}

A Db2 backup of your database is done every day, except for the Flex plan where a Db2 backup is done every 7 days and a snapshot backup is done daily. Daily backups are stored in the IBM Cloud Object Storage service from which it is replicated to multiple availability zones. If something should happen to your primary data center, our service operators will work with you to stand up your recovered database in a secondary data center. -->

재해 복구 전략은 현재 실행 중인 플랜 및 데이터 웨어하우스 생성 유형에 따라 달라집니다.
{: shortdesc}

## 1세대 SMP 소형, 중형, 대형 및 MPP 소형 플랜
{: #sml_mpp}

1세대 SMP 소형, 중형, 대형 및 MPP 소형 플랜의 경우 하루에 한 번 백업을 수행하고  {{site.data.keyword.Bluemix_notm}} Object Storage 서비스에 배치됩니다. 여기서 백업은 여러 가용성 영역으로 복제됩니다. 기본 데이터 센터에서 재해 이벤트가 발생할 경우, IBM의 서비스 운영자는 사용자와 협력하여 다른 데이터 센터에 새로운 데이터 웨어하우스를 구축합니다. {{site.data.keyword.Bluemix_notm}} Object Storage 서비스에 상주하는 일일 백업을 사용합니다.

## IBM Cloud의 2세대 Flex 플랜
{: #flex_ibm_cloud}

{{site.data.keyword.Bluemix_notm}}의 2세대 Flex 플랜의 경우 일주일에 한 번 백업을 수행하고 {{site.data.keyword.Bluemix_notm}} Object Storage 서비스에 배치합니다. 여기서 백업은 여러 가용성 영역으로 복제됩니다. 기본 데이터 센터에서 재해 이벤트가 발생할 경우, IBM의 서비스 운영자는 사용자와 협력하여 다른 데이터 센터에 새로운 데이터 웨어하우스를 구축합니다. {{site.data.keyword.Bluemix_notm}} Object Storage 서비스에 상주하는 주간 백업을 사용합니다.

## Amazon Web Services의 2세대 Flex 플랜
{: #flex_aws}

Amazon Web Services의 2세대 Flex 플랜의 경우 일일 셀프 서비스 백업이 Amazon Web Services S3에 자동으로 오프로드됩니다. S3에서 백업이 여러 지역으로 복제됩니다. 재해 이벤트가 발생하면 최신 백업을 사용하여 클러스터를 보조 데이터 센터로 복원합니다.

## **브라질: 보충 규칙 14**(브라질 연방 정부를 위해 프로비저닝되는 시스템에 적용됨)
{: #rule_14}

현재 브라질에서는 보충 규칙 14로 인해 {{site.data.keyword.dashdbshort_notm}} 오퍼링의 재해 복구(DR) 옵션을 연방 정부용으로 사용할 수 없습니다.

