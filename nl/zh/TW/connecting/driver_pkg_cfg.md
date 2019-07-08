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

# 配置本端環境
{: #cfg_loc_env}

若要將本端應用程式及工具連接至 {{site.data.keyword.dashdbshort_notm}} 資料庫，您需要配置環境。  
{: shortdesc}

## 必要條件
{: #prereq21}

在嘗試連接至您的 {{site.data.keyword.dashdbshort_notm}} 資料庫之前，請驗證您是否具有必要的[必備項目](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs)。

<!-- 1. Install the Db2 driver package for your operating system.

   - [Installing on Windows](install_win.html)
   - [Installing on Linux or PowerLinux](install_linux.html)
   - [Installing on Mac OS X](install_mac.html)
2. Decide whether or not you will be using Secure Sockets Layer (SSL) to connect to your database.
3. Collect database details and connect credentials, including the host name of your server, and your database user ID and password. -->

## 程序
{: #proc21}

1. 將項目新增至資料庫的驅動程式配置檔 `db2dsdriver.cfg`。

   根據您是否要使用 SSL 來連接至您的資料庫，配置步驟會有所不同：

   **使用 SSL**

   若要在使用 SSL 的情況下，將應用程式及工具連接至資料庫，請在 Linux 作業系統的指令 Shell、Windows 命令提示字元或 Db2 指令視窗中輸入下列指令： 

   `db2cli writecfg add -database BLUDB -host <hostname> -port 50001`

   `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50001`

   `db2cli writecfg add -database BLUDB -host <hostname> -port 50001 -parameter "SecurityTransportMode=SSL"`

    其中：

   - `<hostname>` 是伺服器的主機名稱。
   - `<alias>` 是您選擇的別名。別名不能與資料庫名稱 `BLUDB` 相同。如果您的別名中有空格，請使用雙引號括住別名。

   **不使用 SSL**

   若要在不使用 SSL 的情況下，將應用程式及工具連接至資料庫，請在 Linux 作業系統的指令 Shell、Windows 命令提示字元或 Db2 指令視窗中輸入下列指令： 

   `db2cli writecfg add -database BLUDB -host <hostname> -port 50000`

   `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50000`

    其中：

   - `<hostname>` 是伺服器的主機名稱。
   - `<alias>` 是您選擇的別名。別名不能與資料庫名稱 `BLUDB` 相同。如果您的別名中有空格，請使用雙引號括住別名。

2. 從命令提示字元中發出 **db2cli validate** 指令，以測試連接：

   `db2cli validate -dsn <alias> -connect -user <userid> -passwd <password>`

   其中： 
   
   - `<alias>` 是您使用 **db2cli writecfg** 指令所建立的別名。
   - `<userid>` 是您的 Db2 使用者 ID。
   - `<password>` 是您的 Db2 密碼。

3. [*選用*] 若要能夠將本端 ODBC 應用程式及工具連接至資料庫，請使用 ODBC 驅動程式管理程式來登錄 DSN：
 
   從指令行執行下列指令： 

   `db2cli registerdsn -add -dsn <alias>`

   其中： 

   - `<alias>` 是您使用 **db2cli writecfg** 指令所建立的別名。

   依預設，DSN 會建立為使用者 DSN。

