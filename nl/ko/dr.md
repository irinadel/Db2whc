---

copyright:
  years: 2014, 2019
lastupdated: "2018-11-21"

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

# 재해 복구(DR)
{: #dr}

데이터 웨어하우스 인스턴스가 데이터 센터에 배치되고, 이 데이터 센터에서 예상 가동 중단 시간이 8시간 이상인 심각한 가동 중단 상황이 발생하는 경우 재해 복구 조치를 시작하려면 먼저 서비스 운영자가 인스턴스를 다른 데이터 센터로 장애 복구할 수 있도록 요청을 보내야 합니다.
{: shortdesc}

데이터베이스의 Db2 백업은 매일 수행됩니다. 단, Db2 백업이 7일마다 수행되고 스냅샷 백업이 매일 수행되는 Flex 플랜은 예외입니다. 일별 백업은 여러 가용성 지역에 복제되는 원본 IBM Cloud Object Storage 서비스에 저장됩니다. 기본 데이터 센터에 어떤 상황이 발생해야 하는 경우 서비스 운영자는 보조 데이터 센터에서 복구된 데이터베이스를 유지하기 위해 사용자와 함께 작업을 수행할 것입니다.

## **브라질: 보충 규칙 14**(브라질 연방 정부를 위해 프로비저닝되는 시스템에 적용됨)
{: #rule_14}

현재 브라질에서는 보충 규칙 14로 인해 Db2 Warehouse on Cloud 오퍼링의 재해 복구(DR) 옵션을 연방 정부용으로 사용할 수 없습니다.

