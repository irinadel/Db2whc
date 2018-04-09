---

copyright:
  years: 2014, 2018
lastupdated: "2018-03-15"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 高可用性 (HA)：Flex Performance 套餐
{: #ha_flex}

如果发生意外的节点故障，由于使用 IBM Container Service（基于 Kubernetes），Flex Performance MPP 集群将在短暂停机后恢复到完全容量。池中的节点用于移动发生故障的节点实体。
{: shortdesc}

## 计算 HA
{: #compute_ha}

容器服务将立即检测任何节点故障。在发生故障的节点中运行的容器和 pod 将被安排到节点池中的新节点。在短暂停机后，系统返回到 100% 正常操作。

## 存储 HA
{: #storage_ha}

使用双奇偶性校验 RAID6 实施配置存储，可在相同 RAID 组中提供双磁盘故障保护，从而为系统提供高性能和高可用性存储。

## 网络 HA
{: #net_ha}

通过使用冗余网络接口卡 (NIC) 供应服务，实现网络连接高可用性。 

如果容器服务检测到网络问题，pod 和容器可在短暂停机后自动重新启动。
