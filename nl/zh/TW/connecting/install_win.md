---

copyright:
  years: 2014, 2018
lastupdated: "2018-09-25"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 在 Windows 上安裝驅動程式套件

您可以使用安裝程式，在 Windows 上安裝 {{site.data.keyword.dashdbshort_notm}} 驅動程式套件。
{: shortdesc}

## 必要條件

在嘗試連接至您的 {{site.data.keyword.dashdbshort_notm}} 資料庫之前，請驗證您是否具有必要的[必備項目](connecting.html#prereqs)。

<!-- Download the driver package for your operating system from the web console and install it. -->

## 程序

1. 以管理者身分執行已下載的執行檔。

   驅動程式套件的預設安裝路徑為：`Program`
2. [*選用*] 將驅動程式套件安裝目錄的 `bin` 子目錄新增至 `%PATH%`環境變數（因此，您不必指定指令執行檔的完整路徑，即可執行 **db2cli** 指令）。

## 下一步為何？

若要能夠將本端應用程式或用戶端工具連接至 {{site.data.keyword.dashdbshort_notm}} 資料庫，請[配置本端環境](driver_pkg_cfg.html)。
