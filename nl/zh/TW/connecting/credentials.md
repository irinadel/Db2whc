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

# 資料庫詳細資料及連線認證
{: #db_details_cxn_creds}

若要配置本端開發環境，以及將應用程式及工具連接至 {{site.data.keyword.dashdbshort_notm}} 資料庫，您需要知道資料庫詳細資料及連線認證。
{: shortdesc}

## 資料庫詳細資料
{: #db_details}

需有重要的資料庫詳細資料，才能將應用程式及工具連接至資料庫：

- *主機名稱* - 伺服器的主機名稱。
- *埠號* - 由資料庫管理程式用於 TCP/IP 通訊。（請注意，您的服務會佈建一個埠號來進行使用 Secure Sockets Layer (SSL) 的連線，並佈建不同的埠來進行非 SSL 連線。）

   必要的話，您可以使用 ping 指令或 nslookup 指令並指定主機名稱，來取得伺服器的 IP 位址。
- *資料庫名稱* - Db2 資料庫名稱，通常是 BLUDB。

## 連線認證
{: #cxn_creds}

有三種類型的認證：

- *IBM ID* - 如果您使用 {{site.data.keyword.Bluemix_notm}}，則這是您要用來登入 {{site.data.keyword.Bluemix_notm}} 的 ID。這不是您用來將應用程式或工具連接至 Db2 Warehouse on Cloud 資料庫的 ID。
- *Db2 資料庫認證* - 您的服務已佈建資料庫使用者 ID 及密碼，可用來將應用程式及工具連接至資料庫。
- *管理者建立的使用者* - 部分 {{site.data.keyword.dashdbshort_notm}} 方案可讓管理使用者建立新的使用者。這些管理者建立的使用者 ID 及密碼可以用來直接登入 Web 主控台 URL，並從應用程式或工具連接至 Db2 資料庫。

## 在何處尋找資料庫詳細資料及連線認證
{: #location}

您可以從下列位置收集此資訊：

- *您的管理者* - 如果您不是 Db2 實例的擁有者或管理者，則可以從管理者取得您的資料庫詳細資料及連線認證。
- *Db2 Web 主控台* - Web 主控台中提供資料庫詳細資料及認證。
- 如果您是使用 {{site.data.keyword.Bluemix_notm}}： 
   
   - *{{site.data.keyword.Bluemix_notm}}儀表板* - 當您在 {{site.data.keyword.Bluemix_notm}} 儀表板上檢視服務時，於「服務認證」區域中，您可以檢視資料庫詳細資料，以及資料庫使用者 ID 及密碼。
   - *`VCAP_SERVICES`* - `VCAP_SERVICES` 是 {{site.data.keyword.Bluemix_notm}} 中的環境變數，其中包含 JSON 格式的資料庫詳細資料及認證。當您在 {{site.data.keyword.Bluemix_notm}} 儀表板中檢視服務的服務認證時，會顯示 `VCAP_SERVICES` 的內容。當您將其他 {{site.data.keyword.Bluemix_notm}} 服務或應用程式連結至服務時，這些其他服務或應用程式可以讀取 `VCAP_SERVICES`，透過程式設計方式存取資料庫詳細資料及認證。
