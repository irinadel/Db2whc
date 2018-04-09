---

copyright:
  years: 2014, 2018
lastupdated: "2018-03-16"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 고가용성(HA): MPP 플랜
{: #ha_smp_mpp}

{{site.data.keyword.dashdblong}} MPP 플랜 클러스터는 고가용성을 갖춰 프로비저닝됩니다.   
{: shortdesc}

MPP 플랜에서 노드가 작동을 중지하는 경우, HA 컴포넌트는 남은 정상 노드에서 데이터베이스 파티션을 다시 시작합니다. 이 단계 동안 짧은 작동 중지 시간이 발생합니다.  

노드가 클러스터에 다시 추가된 후, 데이터베이스 엔진을 완전한 기능으로 실행하려면 이를 다시 시작해야 합니다.  

