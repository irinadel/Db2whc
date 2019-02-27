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

# Secure Sockets Layer (SSL) 支援
{: #ssl_support}

{{site.data.keyword.dashdbshort_notm}} 資料庫使用由協力廠商數位憑證管理中心 (CA) 發出的 SSL 連線憑證。
{: shortdesc}

CA 憑證是 Db2 驅動程式套件的一部分。如果您的應用程式與來自 Db2 驅動程式套件的驅動程式進行連線，則不需要個別下載憑證。您可以從 Web 主控台下載 Db2 驅動程式套件。

不過，如果您的應用程式具有自己的驅動程式，則您可能需要個別下載憑證。您可以從 Web 主控台下載憑證。

Secure Sockets Layer (SSL) 是一種提供通訊隱私權的安全通訊協定。SSL 可讓用戶端和伺服器應用程式以一種專門設計的方式進行通訊，以防止竊聽、竄改及訊息偽造。啟用 SSL 的用戶端應用程式使用標準加密技術，以協助確保安全通訊。

將應用程式配置為使用 SSL 來連接至 {{site.data.keyword.dashdbshort_notm}} 資料庫，取決於您的公司原則。您可以用來連接至資料庫的標準及 SSL 通訊協定，會將使用者名稱及密碼當作加密資料傳輸。如果您要確保完整的端對端安全，請透過 SSL 連線傳輸所有資料庫資訊（包括機密資料及 meta 資料）。管理者可以在 Web 主控台上變更設定，以強制進行 SSL 連線。


