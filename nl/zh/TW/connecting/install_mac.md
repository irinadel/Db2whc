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

# 在 Mac OS X 上安裝驅動程式套件
{: #install_dr_pkg_mac}

您可以使用 `installDSDriver.sh` Script ，在 Mac OS X 上安裝 {{site.data.keyword.dashdbshort_notm}} 驅動程式套件。
{: shortdesc}

## 必要條件
{: #prereq41}

在嘗試連接至您的 {{site.data.keyword.dashdbshort_notm}} 資料庫之前，請驗證您是否具有必要的[必備項目](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs)。

<!-- Download the Db2 driver package for your operating system from the web console and install it. -->

## 程序
{: #proc41}

- **若為全新安裝**

  1. 按兩下 `macos_dsdriver.dmg` 檔案，以裝載磁碟映像檔。
   
     即會開啟新的**搜尋器**視窗，其中含有磁碟映像檔的內容。

     如果**搜尋器**視窗未開啟，請按兩下桌面上的 `macos_dsdriver` 圖示。
  2. 在**搜尋器**視窗中，按兩下 `installDSDriver.sh` 檔案。

     驅動程式套件即會安裝在預設位置中：`/Applications/dsdriver`。

- **若為更新現有的驅動程式套件安裝**

  1. 備份現行配置檔：

     a. 移至 `Applications/dsdriver/cfg` 資料夾。

     b. 將下列檔案複製到不同的資料夾： 
    
        `db2cli.ini`

        `db2dsdriver.cfg`
  2. 在 `dsdriver` 資料夾上按一下滑鼠右鍵，並選取**移至垃圾筒**，來移除目前安裝的驅動程式套件。
  3. 如先前的**若為全新安裝**一節所述，安裝新的驅動程式套件：
     
     a. 按兩下 `macos_dsdriver.dmg` 檔案，以裝載磁碟映像檔。
     b. 在**搜尋器**視窗中，按兩下 `installDSDriver.sh` 檔案。
  4. 還原配置檔：

     將您從「步驟 1」儲存的 `db2cli.ini` 和 `db2dsdriver.cfg` 檔複製到 `/Applications/dsdriver/cfg` 資料夾。

## 下一步為何？
{: #wn41}

若要能夠將本端應用程式或用戶端工具連接至 {{site.data.keyword.dashdbshort_notm}} 資料庫，請[配置本端環境](/docs/services/Db2whc?topic=Db2whc-cfg_loc_env#cfg_loc_env)。
