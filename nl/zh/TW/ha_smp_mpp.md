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

# 高可用性 (HA)：MPP 方案
{: #ha_smp_mpp}

{{site.data.keyword.dashdblong}} MPP 方案叢集佈建時具有高可用性。  
{: shortdesc}

當 MMP 方案的節點關閉時，HA 元件會在剩餘性能正常的節點中重新啟動您的資料庫分割區。在此階段期間會發生短暫的關閉時間。 

節點新增回叢集之後，資料庫引擎必須重新啟動，以便以完整容量執行。 

