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

# 在 Mac OS X 上安装驱动程序包
{: #install_dr_pkg_mac}

您可以使用 `installDSDriver.sh` 脚本在 Mac OS X 上安装 {{site.data.keyword.dashdbshort_notm}} 驱动程序包。
{: shortdesc}

## 先决条件
{: #prereq41}

在尝试连接到 {{site.data.keyword.dashdbshort_notm}} 数据库之前，请验证您是否具有必需的[先决条件](/docs/services/Db2whc/connecting/connecting.html#prereqs)。

<!-- Download the Db2 driver package for your operating system from the web console and install it. -->

## 过程
{: #proc41}

- **对于新安装**

  1. 通过双击 `macos_dsdriver.dmg` 文件来安装磁盘映像。
   
     这将打开新的**访达**窗口，其中会显示该磁盘映像的内容。

     如果**访达**窗口未打开，请双击桌面上的 `macos_dsdriver` 图标。
  2. 在**访达**窗口中，双击 `installDSDriver.sh` 文件。

     驱动程序包会安装在缺省位置：`/Applications/dsdriver`。

- **对于现有驱动程序包安装的更新**

  1. 备份当前配置文件：

     a. 转至 `Applications/dsdriver/cfg` 文件夹。

     b. 将以下文件复制到其他文件夹： 
    
        `db2cli.ini`

        `db2dsdriver.cfg`
  2. 通过右键单击 `dsdriver` 文件夹，并选择**移到废纸篓**来除去当前安装的驱动程序包。
  3. 如前面的**对于新安装**部分中所述，安装新的驱动程序包：
     
     a. 通过双击 `macos_dsdriver.dmg` 文件来安装磁盘映像。
     b. 在**访达**窗口中，双击 `installDSDriver.sh` 文件。
  4. 复原配置文件：

     将步骤 1 中保存的 `db2cli.ini` 和 `db2dsdriver.cfg` 文件复制到 `/Applications/dsdriver/cfg` 文件夹。

## 后续操作
{: #wn41}

为了能够将本地应用程序或客户机工具连接到 {{site.data.keyword.dashdbshort_notm}} 数据库，请[配置本地环境](/docs/services/Db2whc/connecting/driver_pkg_cfg.html)。
