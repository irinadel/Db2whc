---

copyright:
  years: 2014, 2019
lastupdated: "2018-05-10"

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

# 백업 및 복원
{: #br}

전체 {{site.data.keyword.dashdbshort_notm}} 데이터베이스에 대한 암호화된 백업은 하루에 한 번 수행됩니다.
{: shortdesc}

| 플랜              | 백업 빈도 | 보존되는 백업 수 | 백업 보존 기간   | 셀프 서비스 |
|-------------------|------------------|----------------------------|---------------------------|--------------|
| MPP               | 1/일          |2                          | 2일: FIFO* 롤오버   |아니오           |
| Flex Performance  | 1/일          |7                          | 7일: FIFO* 롤오버   |예          |
{: caption="표 1. 백업 빈도 및 보존" caption-side="top"}

*선입선출(FIFO)

## SMP 및 MPP 플랜
{: #smp_mpp}

최근 2일의 일별 백업이 보존됩니다.

유지하고 있는 백업은 재해 또는 시스템 손상이 발생한 상황에서 오직 IBM에 의해 시스템 복구용으로만 사용됩니다. 백업을 사용한 데이터베이스 복원 요청은 지원되지 않습니다. IBM Data Studio 와 같은 Db2 도구를 사용하거나 **db2 export** 명령을 사용하여 데이터를 내보낼 수 있습니다. 

## Flex Performance 플랜
{: #flex}

최근 7일의 일별 스냅샷이 보존됩니다.

{{site.data.keyword.dashdbshort_notm}} 콘솔에서 가장 편리한 시간에 백업을 실행하도록 스케줄할 수 있으며 선택한 시간에 유지하고 있는 백업으로부터 데이터베이스를 복원할 수 있습니다. 시스템은 복원 기간 중에 작동을 중지합니다. 복원 오퍼레이션이 완료되었음을 알리는 이메일이 발송됩니다.

![웹 콘솔 백업 및 복원 페이지의 보기](images/br.png)

