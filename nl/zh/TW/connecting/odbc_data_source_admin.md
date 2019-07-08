---

copyright:
  years: 2014, 2019
lastupdated: "2018-09-25"

keywords:

subcollection: Db2whc

---

<!-- Attribute definitions --> 
{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}

# 使用 ODBC 資料來源管理員進行連線
{: #con_prog_odbc_dsa}

使用「Microsoft ODBC 資料來源管理員」工具，可以定義 ODBC 或 CLI 應用程式與 {{site.data.keyword.dashdbshort_notm}} 資料庫之間的連線。
{: shortdesc}

## 必要條件
{: #prereq91}

在嘗試連接至您的 {{site.data.keyword.dashdbshort_notm}} 資料庫之前，請驗證您是否具有必要的[必備項目](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs)。

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## 程序
{: #proc91}

1. 安裝 [Db2 驅動程式套件](/docs/services/Db2whc?topic=Db2whc-dr_pkg#dr_pkg)。

2. 開啟「ODBC 資料來源管理員」，並建立 Db2 驅動程式套件的「使用者 DSN」或「系統 DSN」。
    
3. 按一下**進階**設定。在下列 CLI 參數中輸入其適用於 {{site.data.keyword.dashdbshort_notm}} 伺服器的值：**Hostname**、**Port** 及 **Database**。
    
4. 若為 SSL 連線，請在 CLI 參數 **Security** 中輸入值 `SSL`。
    
5. 按一下**套用**。
    
6. 若要測試連線，請回到「ODBC 資料來源管理員」的主頁面。針對您所建立的 DSN，按一下**配置**。請輸入伺服器的使用者 ID 及密碼，然後按一下**連接**。

