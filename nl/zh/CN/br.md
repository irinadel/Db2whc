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

# 备份和复原
{: #br}

每天完成一次完整 {{site.data.keyword.dashdbshort_notm}} 数据库加密备份。
{: shortdesc}

| 套餐              | 备份频率         | 保留的备份数量             | 备份保留期                | 自助服务     |
|-------------------|------------------|----------------------------|---------------------------|--------------|
| MPP               | 每天 1 次        | 2                          | 2 天；FIFO* 滚动          | 否           |
| Flex Performance  | 每天 1 次        | 7                          | 7 天；FIFO* 滚动          | 是           |
{: caption="表 1. 备份频率和保留时间" caption-side="top"}

*先进先出

## SMP 和 MPP 套餐
{: #smp_mpp}

保留最近 2 个每日备份。

IBM 专门只将保留的备份用于发生灾难或系统丢失时的系统恢复。不支持从备份复原数据库的请求。您可以使用 Db2 工具（例如，IBM Data Studio）或使用 **db2 export** 命令导出数据。 

## Flex Performance 套餐
{: #flex}

保留最近 7 个每日备份快照。

从 {{site.data.keyword.dashdbshort_notm}} 控制台，您可以安排备份以在最方便时运行，并且可在选择的任何时间从任何保留的备份快照复原数据库。复原期间，系统停止运行。将发送一封电子邮件，通知您复原操作已完成。

![Web 控制台备份和复原页面的视图](images/br.png)

