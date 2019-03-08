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

# 在 Linux 或 PowerLinux 上安裝驅動程式套件
{: #install_dr_pkg_linux}

您可以在 Linux 或 PowerLinux 上使用 `installDSDriver`，來安裝 {{site.data.keyword.dashdbshort_notm}} 驅動程式套件。
{: shortdesc}

## 必要條件
{: #prereq31}

在嘗試連接至您的 {{site.data.keyword.dashdbshort_notm}} 資料庫之前，請驗證您是否具有必要的[必備項目](/docs/services/Db2whc/connecting/connecting.html#prereqs)。

<!-- Download the Db2 driver package for your operating system from the web console and install it. -->

**僅限在 PowerLinux 上**，完成下列步驟來安裝 XL C/C++ 編譯器運行環境套件：

1. 從 FTP 網站中，下載 XL C/C++ 編譯器運行環境套件。例如，若要使用 **wget** 工具下載 Linux 小序排列法 Ubuntu 14 的運行環境套件，請發出下列指令：
 

   `wget ftp://public.dhe.ibm.com/software/server/POWER/Linux/rte/xlcpp/le/ubuntu/dists/trusty/main/binary-ppc64el/*`
2. 發出下列指令，以安裝運行環境套件：

   `sudo dpkg -iG *.deb` 

## 程序
{: #proc31}

1. 解壓縮先前下載的壓縮驅動程式套件檔。

   範例： 

   `gunzip file_name.tar.gz`

   `tar -xvf file_name.tar`

    即會在已執行解壓縮指令的目錄中建立 `dsdriver` 子目錄。
2. 解壓縮 Java 及 ODBC/CLI 驅動程式。

   a. 在 `dsdriver` 子目錄中，執行 **installDSDriver** 指令。
   
   **installDSDriver** 指令會在 `dsdriver` 目錄中建立 `db2profile` 及 `db2cshrc` Script 檔案。

   b. 根據 Shell 環境，執行下列其中一個 Script 檔案：

   - **Bash 或 Korn Shell**：`source db2profile`
   - **C Shell**：`source db2cshrc`

## 下一步為何？
{: #wn}

若要能夠將本端應用程式或用戶端工具連接至 {{site.data.keyword.dashdbshort_notm}} 資料庫，請[配置本端環境](/docs/services/Db2whc/connecting/driver_pkg_cfg.html)。   




