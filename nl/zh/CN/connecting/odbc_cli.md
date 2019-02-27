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

# 使用 ODBC 或 CLI 以编程方式连接
{: #con_prog_odbc_cli}

定义 Microsoft Windows ODBC 或 CLI 应用程序与 {{site.data.keyword.dashdbshort_notm}} 数据库之间的连接。
{: shortdesc}

## 先决条件

在尝试连接到 {{site.data.keyword.dashdbshort_notm}} 数据库之前，请验证您是否具有必需的[先决条件](connecting.html#prereqs)。

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## 过程

1. 在 Linux 操作系统上的命令 shell 中、Windows 命令提示符处或 Windows 操作系统上的 Db2 命令窗口中，输入以下命令：

   **注**：这些命令将在计算机上的驱动程序配置文件 (`db2dsdriver.cfg`) 中创建新条目，并设置连接属性。此步骤只需执行一次。
   
   - 对于使用 SSL 的连接：

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50001 -parameter "SecurityTransportMode=SSL"`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50001`

   - 对于不使用 SSL 的连接：

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50000`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50000`

   其中：

   `<hostname>` 是服务器的主机名

   `<alias>` 是您选择的 DSN 别名
    
2. [*可选*]: 要实现测试与数据库的连接，请在命令提示符处运行以下命令：

   `db2cli validate -dsn <alias> -connect -user <user_id> -passwd <password>`

   其中：

   `<alias>` 是您已使用 **db2cli writecfg** 命令创建的 DSN 别名

   `<user_id>` 是预先收集的连接凭证中的值

   `<password>` 是预先收集的连接凭证中的值

3. [*可选*]: 要向 Microsoft ODBC 驱动程序管理器注册数据源名称 (DSN)，并使用 Microsoft ODBC 应用程序，请运行以下命令。缺省情况下，会将 DSN 创建为用户 DSN。

   `db2cli registerdsn -add -dsn <alias>`

   其中：
        
   `<alias>` 是您已使用 **db2cli writecfg** 命令创建的 DSN 别名



