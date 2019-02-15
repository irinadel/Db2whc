---

copyright:
  years: 2014, 2019
lastupdated: "2018-09-25"

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

# JDBC でのプログラマチック接続
{: #con_prog_jdbc}

Java™ アプリケーションと {{site.data.keyword.dashdbshort_notm}} データベースの間の接続を定義します。
{: shortdesc}

## 前提条件

{{site.data.keyword.dashdbshort_notm}} データベースへの接続を試行する前に、必要な[前提条件](connecting.html#prereqs)を満たしていることを確認します。

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## 手順

各 Java アプリケーションで、**DriverManager.getConnection** メソッドを組み込んでユーザー ID とパスワードを指定し、次のいずれかの JDBC URL ストリングを組み込みます。

- SSL を使用する接続の場合:

  `jdbc:db2://<host_name>:50001/BLUDB:sslConnection=true;`

- SSL を使用しない接続の場合:

  `jdbc:db2://<host_name>:50000/BLUDB`


