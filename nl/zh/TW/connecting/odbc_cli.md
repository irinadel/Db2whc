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

# 使用 ODBC 或 CLI 以程式設計方式連接
{: #con_prog_odbc_cli}

定義 Microsoft Windows ODBC 或 CLI 應用程式與 {{site.data.keyword.dashdbshort_notm}} 資料庫之間的連線。
{: shortdesc}

## 必要條件
{: #prereq81}

在嘗試連接至您的 {{site.data.keyword.dashdbshort_notm}} 資料庫之前，請驗證您是否具有必要的[必備項目](/docs/services/Db2whc/connecting/connecting.html#prereqs)。

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## 程序
{: #proc81}

1. 在 Linux 作業系統上的指令 Shell、Windows 命令提示字元，或 Windows 作業系統上的 Db2 指令視窗中，輸入下列指令：

   **附註**：這些指令會在電腦的驅動程式配置檔 (`db2dsdriver.cfg`) 中建立新項目，並設定連線屬性。您只需執行此步驟一次。
   
   - 若為使用 SSL 的連線：

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50001 -parameter "SecurityTransportMode=SSL"`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50001`

   - 若為不使用 SSL 的連線：

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50000`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50000`

   其中：

   `<hostname>` 是伺服器的主機名稱

   `<alias>` 是您選擇的 DSN 別名
    
2. [*選用*] 若要測試資料庫的連線，請從命令提示字元中執行此指令：

   `db2cli validate -dsn <alias> -connect -user <user_id> -passwd <password>`

   其中：

   `<alias>` 是您使用 **db2cli writecfg** 指令所建立的 DSN 別名。

   `<user_id>` 是來自您預先收集的連接認證

   `<password>` 是來自您預先收集的連接認證

3. [*選用*] 若要向 Microsoft ODBC Driver Manger 登錄資料來源名稱 (DSN)，並使用 Microsoft ODBC 應用程式，請執行下列指令。依預設，DSN 會建立為使用者 DSN。

   `db2cli registerdsn -add -dsn <alias>`

   其中：
        
   `<alias>` 是您使用 **db2cli writecfg** 指令所建立的 DSN 別名。



