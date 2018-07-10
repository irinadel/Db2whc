---

copyright:
  years: 2014, 2018
lastupdated: "2018-04-30"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 高可用性 (HA) 
{: #ha}

成功資料庫解決方案的測量是其可用性。{{site.data.keyword.dashdblong}} 具有高度可用的方案，讓您的工作負載持續進行。
{: shortdesc}

## MPP 方案
{: #ha_mpp}

{{site.data.keyword.dashdbshort_notm}} MPP 方案叢集佈建時具有高可用性。  

當 MMP 方案的節點關閉時，HA 元件會在剩餘性能正常的節點中重新啟動您的資料庫分割區。在此階段期間會發生短暫的關閉時間。 

節點新增回叢集之後，資料庫引擎必須重新啟動，以便以完整容量執行。 

## 彈性效能方案
{: #ha_flex}

如果發生非預期的節點失效，您的彈性效能 MPP 叢集會在短暫的關閉時間之後回到完整容量，這是因為使用了 IBM Container Service（以 Kubernetes 為基礎）。會使用來自儲存區的節點來移動失效的實體。
 

### 運算 HA
{: #compute_ha}

任何節點失效都會立即被容器服務偵測到。在失效節點中執行的容器與 Pod，會排定到來自節點儲存區的新節點。在短暫的關閉時間之後，系統便會回到 100% 正常作業。

### 儲存空間 HA
{: #storage_ha}

您的儲存空間配置了雙同位元 RAID6 實作，該實作提供對於在相同 RAID 群組發生雙重磁碟故障的防禦，以確保系統具有高效能和高度可用的儲存空間。

### 網路 HA
{: #net_ha}

藉由使用備援網路介面卡 (NIC) 佈建您的服務，網路連線便成為高度可用。 

如果容器服務偵測到網路問題，Pod 和容器可以在短暫的關閉時間之後自動重新啟動。
