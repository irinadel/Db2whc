---

copyright:
  years: 2014, 2019
lastupdated: "2018-04-30"

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

# 高可用性 (HA) 
{: #ha}

成功数据库解决方案的度量是其可用性。{{site.data.keyword.dashdblong}} 具有高可用性套餐，可使您的工作负载保持运行。
{: shortdesc}

## MPP 套餐
{: #ha_mpp}

{{site.data.keyword.dashdbshort_notm}} MPP 套餐集群配备高可用性。  

在 MPP 套餐的节点停机时，HA 组件重新启动剩余正常运行的节点中的数据库分区。此阶段将发生短暂停机。 

在将节点添加回集群后，必须重新启动数据库引擎才能以完整容量运行。 

## Flex Performance 套餐
{: #ha_flex}

如果发生意外的节点故障，由于使用 IBM Container Service（基于 Kubernetes），Flex Performance MPP 集群将在短暂停机后恢复到完全容量。池中的节点用于移动发生故障的节点实体。
 

### 计算 HA
{: #compute_ha}

容器服务将立即检测任何节点故障。在发生故障的节点中运行的容器和 pod 将被安排到节点池中的新节点。在短暂停机后，系统返回到 100% 正常操作。

### 存储 HA
{: #storage_ha}

使用双奇偶性校验 RAID6 实施配置存储，可在相同 RAID 组中提供双磁盘故障保护，从而为系统提供高性能和高可用性存储。

### 网络 HA
{: #net_ha}

通过使用冗余网络接口卡 (NIC) 供应服务，实现网络连接高可用性。 

如果容器服务检测到网络问题，pod 和容器可在短暂停机后自动重新启动。
