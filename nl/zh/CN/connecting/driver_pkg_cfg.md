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

# 配置本地环境
{: #cfg_loc_env}

要将本地应用程序和工具连接到 {{site.data.keyword.dashdbshort_notm}} 数据库，您需要配置环境。  
{: shortdesc}

## 先决条件
{: #prereq21}

在尝试连接到 {{site.data.keyword.dashdbshort_notm}} 数据库之前，请验证您是否具有必需的[先决条件](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs)。

<!-- 1. Install the Db2 driver package for your operating system.

   - [Installing on Windows](install_win.html)
   - [Installing on Linux or PowerLinux](install_linux.html)
   - [Installing on Mac OS X](install_mac.html)
2. Decide whether or not you will be using Secure Sockets Layer (SSL) to connect to your database.
3. Collect database details and connect credentials, including the host name of your server, and your database user ID and password. -->

## 过程
{: #proc21}

1. 在驱动程序配置文件 `db2dsdriver.cfg` 中，添加数据库的相应条目。

   根据您是否要使用 SSL 来连接到数据库，配置步骤有所不同：

   **使用 SSL**

   要使用 SSL 将应用程序和工具连接到数据库，请在 Linux 操作系统上的命令 Shell 中、Windows 命令提示符处或者在 Db2 命令窗口中输入以下命令：
 

   `db2cli writecfg add -database BLUDB -host <hostname> -port 50001`

   `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50001`

   `db2cli writecfg add -database BLUDB -host <hostname> -port 50001 -parameter "SecurityTransportMode=SSL"`

    其中：

   - `<hostname>` 是服务器的主机名。
   - `<alias>` 是您选择的别名。别名不能与数据库名称 `BLUDB` 相同。如果要在别名中包含空格，请将别名用双引号括起。

   **不使用 SSL**

   要不使用 SSL 将应用程序和工具连接到数据库，请在 Linux 操作系统上的命令 Shell 中、Windows 命令提示符处或者在 Db2 命令窗口中输入以下命令：
 

   `db2cli writecfg add -database BLUDB -host <hostname> -port 50000`

   `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50000`

    其中：

   - `<hostname>` 是服务器的主机名。
   - `<alias>` 是您选择的别名。别名不能与数据库名称 `BLUDB` 相同。如果要在别名中包含空格，请将别名用双引号括起。

2. 通过从命令提示符发出 **db2cli validate** 命令来测试连接：

   `db2cli validate -dsn <alias> -connect -user <userid> -passwd <password>`

   其中： 
   
   - `<alias>` 是您已使用 **db2cli writecfg** 命令创建的别名。
   - `<userid>` 是您的 Db2 用户标识。
   - `<password>` 是您的 Db2 密码。

3. [*可选*] 要将本地 ODBC 应用程序和工具连接到数据库，请向 ODBC 驱动程序管理器注册 DSN：
 
   通过命令行运行以下命令： 

   `db2cli registerdsn -add -dsn <alias>`

   其中： 

   - `<alias>` 是您已使用 **db2cli writecfg** 命令创建的别名。

   缺省情况下，该 DSN 会创建为用户 DSN。

