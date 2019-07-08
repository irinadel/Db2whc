---

copyright:
  years: 2014, 2019
lastupdated: "2018-04-30"

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

# 고가용성(HA) 
{: #ha}

성공적인 데이터베이스 솔루션의 측도는 가용성입니다. {{site.data.keyword.dashdblong}}에는 사용자의 워크로드가 계속 진행될 수 있도록 고가용성 플랜이 있습니다.
{: shortdesc}

## MPP 플랜
{: #ha_mpp}

{{site.data.keyword.dashdbshort_notm}} MPP 플랜 클러스터는 고가용성을 갖춰 프로비저닝됩니다.  

MPP 플랜에서 노드가 작동을 중지하는 경우, HA 컴포넌트는 남은 정상 노드에서 데이터베이스 파티션을 다시 시작합니다. 이 단계 동안 짧은 작동 중지 시간이 발생합니다. 

노드가 클러스터에 다시 추가된 후, 데이터베이스 엔진을 완전한 기능으로 실행하려면 이를 다시 시작해야 합니다. 

## Flex Performance 플랜
{: #ha_flex}

예기치 않은 노드 실패가 발생하는 경우 Flex Performance MPP 클러스터는 IBM Container Service(Kubernetes 기반) 사용으로 인한 짧은 작동 중지 시간 후 완전한 기능을 회복합니다. 풀의 노드는 실패한 노드 엔티티를 이동하는 데 사용됩니다. 

### 컴퓨팅 HA
{: #compute_ha}

모든 노드 실패는 컨테이너 서비스에 의해 즉시 발견됩니다. 실패한 노드에서 실행 중이던 컨테이너 및 포드는 노드 풀의 새 노드로 스케줄됩니다. 시스템은 짧은 작동 중지 시간 후 100% 정상 작동 상태로 돌아옵니다.

### 스토리지 HA
{: #storage_ha}

스토리지는 시스템을 위한 고성능 및 고가용성 스토리지를 위해 동일한 RAID 그룹 내의 이중 디스크 실패에 대한 보호를 제공하는 듀얼 패리티 RAID6 구현으로 구성됩니다.

### 네트워크 HA
{: #net_ha}

중복 네트워크 인터페이스 카드(NIC)를 사용하여 서비스를 프로비저닝함으로써 네트워크 연결에서 고가용성을 달성할 수 있습니다. 

컨테이너 서비스에서 네트워크 문제를 발견하는 경우, 포드 및 컨테이너는 짧은 작동 중지 시간 후 자동으로 다시 시작할 수 있습니다.
