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

# 高可用性 (HA)：MPP 套餐
{: #ha_smp_mpp}

{{site.data.keyword.dashdblong}} MPP 套餐集群配备高可用性。  
{: shortdesc}

在 MPP 套餐的节点停机时，HA 组件重新启动剩余正常运行的节点中的数据库分区。此阶段将发生短暂停机。 

在将节点添加回集群后，必须重新启动数据库引擎才能以完整容量运行。 

