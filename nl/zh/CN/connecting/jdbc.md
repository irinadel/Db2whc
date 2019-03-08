---

copyright:
  years: 2014, 2019
lastupdated: "2018-09-25"

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

# 使用 JDBC 以编程方式连接
{: #con_prog_jdbc}

定义 Java™ 应用程序与 {{site.data.keyword.dashdbshort_notm}} 数据库之间的连接。
{: shortdesc}

## 先决条件
{: #prereq61}

在尝试连接到 {{site.data.keyword.dashdbshort_notm}} 数据库之前，请验证您是否具有必需的[先决条件](/docs/services/Db2whc/connecting/connecting.html#prereqs)。

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## 过程
{: #proc61}

在每个 Java 应用程序中，通过包含 **DriverManager.getConnection** 方法来指定用户标识和密码，然后包含下列其中一个 JDBC URL 字符串：

- 对于使用 SSL 的连接：

  `jdbc:db2://<host_name>:50001/BLUDB:sslConnection=true;`

- 对于不使用 SSL 的连接：

  `jdbc:db2://<host_name>:50000/BLUDB`


