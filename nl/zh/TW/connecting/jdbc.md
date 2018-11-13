---

copyright:
  years: 2014, 2018
lastupdated: "2018-09-25"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 使用 JDBC 以程式設計方式連接

定義 Java™ 應用程式與 {{site.data.keyword.dashdbshort_notm}} 資料庫之間的連線。
{: shortdesc}

## 必要條件

在嘗試連接至您的 {{site.data.keyword.dashdbshort_notm}} 資料庫之前，請驗證您是否具有必要的[必備項目](connecting.html#prereqs)。

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## 程序

在每一個 Java 應用程式中，請包括 **DriverManager.getConnection** 方法，然後包括下列其中一個 JDBC URL 字串，來指定使用者 ID 及密碼：

- 若為使用 SSL 的連線：

  `jdbc:db2://<host_name>:50001/BLUDB:sslConnection=true;`

- 若為不使用 SSL 的連線：

  `jdbc:db2://<host_name>:50000/BLUDB`


