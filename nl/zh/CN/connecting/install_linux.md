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

# 在 Linux 或 PowerLinux 上安装驱动程序包
{: #install_dr_pkg_linux}

您可以使用 `installDSDriver` 在 Linux 或 PowerLinux 上安装 {{site.data.keyword.dashdbshort_notm}} 驱动程序包。
{: shortdesc}

## 先决条件

在尝试连接到 {{site.data.keyword.dashdbshort_notm}} 数据库之前，请验证您是否具有必需的[先决条件](connecting.html#prereqs)。

<!-- Download the Db2 driver package for your operating system from the web console and install it. -->

**仅在 PowerLinux 上**，完成以下步骤来安装 XL C/C++ 编译器运行时软件包：

1. 从 FTP 站点下载 XL C/C++ 编译器运行时软件包。例如，要使用 **wget** 工具下载适用于 Linux 小尾数法 Ubuntu 14 的运行时软件包，请发出以下命令：
 

   `wget ftp://public.dhe.ibm.com/software/server/POWER/Linux/rte/xlcpp/le/ubuntu/dists/trusty/main/binary-ppc64el/*`
2. 通过发出以下命令，安装该运行时软件包：

   `sudo dpkg -iG *.deb` 

## 过程

1. 解压缩先前下载的压缩驱动程序包文件。

   示例： 

   `gunzip file_name.tar.gz`

   `tar -xvf file_name.tar`

    这将在您运行解压缩命令的目录中创建 `dsdriver` 子目录。
2. 解压缩 Java 和 ODBC/CLI 驱动程序。

   a. 在 `dsdriver` 子目录中，运行 **installDSDriver** 命令。
   
   **installDSDriver** 命令将在 `dsdriver` 目录中创建 `db2profile` 和 `db2cshrc` 脚本文件。

   b. 根据您的 Shell 环境，运行下列其中一个脚本文件：

   - **Bash 或 Korn shell**：`source db2profile`
   - **C shell**：`source db2cshrc`

## 后续操作

为了能够将本地应用程序或客户机工具连接到 {{site.data.keyword.dashdbshort_notm}} 数据库，请[配置本地环境](driver_pkg_cfg.html)。   




