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

# 在 Windows 上安装驱动程序包
{: #install_dr_pkg_windows}

您可以使用安装程序在 Windows 上安装 {{site.data.keyword.dashdbshort_notm}} 驱动程序包。
{: shortdesc}

## 先决条件
{: #prereq51}

在尝试连接到 {{site.data.keyword.dashdbshort_notm}} 数据库之前，请验证您是否具有必需的[先决条件](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs)。

<!-- Download the driver package for your operating system from the web console and install it. -->

## 过程
{: #proc51}

1. 以管理员身份运行下载的可执行文件。

   驱动程序包的缺省安装路径为：`Program Files\IBM\IBM DATA SERVER DRIVER`
2. [*可选*] 将驱动程序包安装目录的 `bin` 子目录添加到 `%PATH%` 环境变量（以便可以在不指定命令可执行文件完整路径的情况下运行 **db2cli** 命令。）

## 后续操作
{: #wn51}

为了能够将本地应用程序或客户机工具连接到 {{site.data.keyword.dashdbshort_notm}} 数据库，请[配置本地环境](/docs/services/Db2whc?topic=Db2whc-cfg_loc_env#cfg_loc_env)。
