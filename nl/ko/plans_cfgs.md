---

copyright:
  years: 2014, 2019
lastupdated: "2019-06-05"

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

# 플랜 및 구성
{: #plans_cfgs}

수행해야 하는 작업에 맞게 구성되고 최적화된 {{site.data.keyword.dashdbshort_notm}} 플랜을 선택할 수 있습니다.
{: shortdesc}

   * 테스트를 위한 엔트리 플랜. 최대 1GB의 저장 공간을 갖춘 무료 평가판입니다. [엔트리 플랜 제한사항](#ep_restrictions)을 참조하십시오.
   * 스토리지 및 컴퓨팅 리소스를 독립적으로 스케일링할 수 있는 Flex 플랜
   * 다양한 크기의 프로덕션을 위한 SMP 플랜: 단일 노드 및 단일 인스턴스로 구성된 소형, 중형 및 대형
   * 병렬 처리 및 고성능용 MPP 다중-노드 클러스터 구성
   * 고가용성을 위해 구성된 플랜
   * Oracle 호환성

[{{site.data.keyword.Bluemix}} 카탈로그](https://cloud.ibm.com/catalog/services/db2-warehouse){:external}에서 모든 사용 가능한 {{site.data.keyword.dashdbshort_notm}} 플랜을 보십시오.
<!--   * Plans configured for data warehouse and online analytical processing (OLAP) workloads: [{{site.data.keyword.dashdbshort_notm}}](https://console.bluemix.net/catalog/services/db2-warehouse){:external} -->
<!--   * Plans configured for high-speed, transactional processing (OLTP): [{{site.data.keyword.dashdbshort_notm}} for Transactions](https://console.ng.bluemix.net/catalog/services/dashdb-for-transactions-sql-database){:external} -->

{{site.data.keyword.dashdbshort_notm}} Flex Performance 플랜에 대한 소개를 보려면 이 동영상을 시청하십시오.

<iframe class="embed-responsive-item" id="youtubeplayer" title="Cognos Analytics에서 연결 작성" type="text/html" width="640" height="390" src="//www.youtube.com/embed/59PKSnzNQAg?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

{{site.data.keyword.dashdbshort_notm}} 서비스를 {{site.data.keyword.Bluemix}}의 네트워크 격리 환경에 배치하도록 요청할 수 있습니다. [{{site.data.keyword.IBM_notm}} 영업 팀](https://www.ibm.com/connect/ibm/us/en/?lnk=fcw){:external}에 문의하십시오.

카탈로그에서 필요한 구성을 찾을 수 없는 경우 [{{site.data.keyword.IBM_notm}} 영업 팀](https://www.ibm.com/connect/ibm/us/en/?lnk=fcw){:external}에 문의하여 다른 옵션에 대해 논의하십시오.

## IBM Cloud 데이터 센터의 플랜 가용성
{: #availability}

다음 표는 실제 지역에 있는 IBM Cloud 데이터 센터에서 제공하는 다양한 {{site.data.keyword.dashdbshort_notm}} 플랜의 가용성에 대한 정보를 제공합니다.

| {{site.data.keyword.dashdbshort_notm}} 플랜 | 아시아/태평양 |유럽    | 북/중앙아메리카     |남미 |
|------------------------------|--------------|-----------|---------------------------|---------------|
| Flex / Flex Performance      | 도쿄        | 프랑크푸르트 | 워싱턴 D.C. (미국 동부) | *해당사항 없음           |
|                              |              |           | 댈러스(미국 남부)         |               |  
|      |||||
| Flex One                     | *해당사항 없음   | *해당사항 없음   | 댈러스(미국 남부)         | *해당사항 없음           |
|      |||||
| SMP                          | 홍콩    | 암스테르담 | 워싱턴 D.C. (미국 동부) | 상파울루     |
|                              | 서울        | 프랑크푸르트 | 댈러스(미국 남부)         |               | 
|                              | 싱가포르    | 런던    | 몬트리올                  |               | 
|                              | 시드니       | 밀라노     | 케레타로                 |               | 
|                              | 도쿄        | 오슬로      | 토론토                   |               | 
|                              |              | 파리     |                           |               |
|      |||||
| MPP                          | 홍콩    | 암스테르담 | 워싱턴 D.C. (미국 동부) | 상파울루     |
|                              | 서울        | 프랑크푸르트 | 댈러스(미국 남부)         |               | 
|                              | 싱가포르    | 런던    | 몬트리올                  |               | 
|                              | 시드니       | 밀라노     | 케레타로                 |               | 
|                              | 도쿄        | 오슬로      | 토론토                   |               | 
|                              |              | 파리     |                           |               |
{: caption="표 1. Db2 Warehouse on Cloud 서비스 플랜을 지원하는 IBM Cloud 데이터 센터" caption-side="top"}

*NA = 현재 사용할 수 없음

## Amazon Web Services 데이터 센터의 플랜 가용성
{: #availability_aws}

다음 표는 실제 지역에 있는 Amazon Web Services 데이터 센터에서 제공하는 다양한 {{site.data.keyword.dashdbshort_notm}} 플랜의 가용성에 대한 정보를 제공합니다.

| {{site.data.keyword.dashdbshort_notm}} 플랜 | 아시아/태평양 |유럽    | 북/중앙아메리카     |남미 |
|------------------------------|--------------|-----------|---------------------------|---------------|
| Flex                         | 시드니       | 프랑크푸르트 | 북버지니아 | *해당사항 없음           |
|                              | 싱가포르    | 런던    |             |               |  
|      |||||
| Flex Performance             | 시드니       | 프랑크푸르트 | 북버지니아 | *해당사항 없음           |
|                              | 싱가포르    | 런던    |             |               | 
{: caption="표 2. Db2 Warehouse on Cloud 서비스 플랜을 지원하는 Amazon Web Services 데이터 센터" caption-side="top"}

*NA = 현재 사용할 수 없음


## 엔트리 플랜 제한사항
{: #ep_restrictions}

미션을 이행하는 데 중요하거나 성능에 민감한 워크로드의 경우 엔트리 서비스 플랜이 아니라 엔터프라이즈 레벨 서비스 플랜을 사용하는 것이 좋습니다. 
{: important}

다음은 {{site.data.keyword.dashdbshort_notm}} 엔트리 플랜 제한사항을 나타내는 표입니다.

| 카테고리 | 항목 | 제한사항 | 
|----------|------|-------------|
| 리소스 | 스토리지 | 사용자당 20GB의 스토리지. 1GB 미만의 스토리지를 사용하는 경우에만 플랜이 무료입니다. |
|  | 연결 | 사용자당 50개의 연결. 이 한계는 인스턴스의 시스템 무결성을 유지보수하기 위해 동적으로 조정될 수 있습니다. |
|  | 성능 | 다중 테넌트 시스템에서 다른 사용자가 실행하는 워크로드 때문에 성능이 변동될 수 있음 |
|  |  |
| 특징 & 기능 | 연합 | 지원되지 않음 |
|  | Oracle 호환성 | 지원되지 않음 |
|  | 사용자 정의 확장기능(UDF) | 지원되지 않음 |
|  | 사용자 관리 | 사용자에게 관리 권한이 부여되지 않음 |
|  | 행 및 열 액세스 제어(RCAC) | 지원되지 않음 |
|  | 데이터 로드에 사용하는 IBM InfoSphere Data Replication | 지원되지 않음 |
|  |  |
| 네트워킹 환경 | IBM Cloud Integrated Analytics | 지원되지 않음 |
|  | IBM Cloud Dedicated | 지원되지 않음 |
|  |  |
| 보안 준수 | HIPAA(Health Information Portability and Accountability Act of 1996) | 지원되지 않음. 서비스 설명을 참조하십시오. |
|  | EU 일반 개인정보 보호법률(GDPR) | 특정 제한사항이 적용되지 않음 |
|  |  |
| 계정 관리 | 재활성화 | 재활성화 요구사항이 없음 |
{: caption="표 3. {{site.data.keyword.dashdbshort_notm}} 엔트리 플랜 제한사항" caption-side="top"}
