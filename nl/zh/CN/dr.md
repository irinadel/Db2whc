---

copyright:
  years: 2014, 2019
lastupdated: "2018-11-21"

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

# 灾难恢复 (DR)
{: #dr}

如果部署您的数据仓库实例的数据中心遭受严重中断，预计停机时间超过 8 小时，那么将向您发送请求以允许服务操作员在灾难恢复操作开始前将该实例故障转移到其他数据中心。
{: shortdesc}

数据库的 Db2 备份每天执行一次，Flex 套餐除外，其中 Db2 备份每 7 天执行一次并且快照备份每天执行一次。每日备份存储在 IBM Cloud Object Storage 服务中，备份可从该服务复制到多个可用性专区。如果主数据中心发生问题，那么我们的服务操作员将与您一起在辅助数据中心建立恢复的数据库。

## **巴西：补充规则 14**（适用于为巴西联邦政府供应的系统）
{: #rule_14}

目前，根据补充规则 14，针对 Db2 Warehouse on Cloud 产品的灾难恢复 (DR) 选项不再可供巴西的联邦政府使用。

