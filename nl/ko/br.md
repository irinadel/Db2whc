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

# 백업 및 복원
{: #br}

전체 {{site.data.keyword.dashdbshort_notm}} 데이터베이스에 대한 암호화된 백업은 하루에 한 번 수행됩니다. Flex Performance 플랜의 경우에는 최근 7일의 일별 백업 스냅샷이 유지됩니다. SMP 및 MPP 플랜의 경우에는 최근 2일의 일별 백업이 유지됩니다.
{: shortdesc}

Flex Performance 플랜에서는 가장 편리한 시간에 백업을 실행하도록 스케줄할 수 있으며 선택한 시간에 유지하고 있는 백업으로부터 데이터베이스를 복원할 수 있습니다. 시스템은 복원 기간 중에 작동을 중지합니다. 복원 오퍼레이션이 완료되었음을 알리는 이메일이 발송됩니다. 

SMP 및 MPP 플랜의 경우 유지하고 있는 백업은 재해 또는 시스템 손상이 발생한 상황에서 오직 IBM에 의해 시스템 복구용으로만 사용됩니다. 백업을 사용한 데이터베이스 복원 요청은 지원되지 않습니다. IBM Data Studio 와 같은 Db2 도구를 사용하거나 **db2 export** 명령을 사용하여 데이터를 내보낼 수 있습니다.  
