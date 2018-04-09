---

copyright:
  years: 2014, 2018
lastupdated: "2018-03-16"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 備份及還原
{: #br}

每天會對完整 {{site.data.keyword.dashdbshort_notm}} 資料庫進行一次加密的備份。對於彈性效能方案，會保留最後 7 天的每日備份 Snapshot。對於 SMP 及 MPP 方案，會保留最後 2 天的每日備份。
{: shortdesc}

在彈性效能方案中，您可以將備份排定在最方便的時間執行，且您可以在選擇的任何時間，從您保留的任何備份 Snapshot 還原資料庫。系統會在還原期間關閉。將會傳送電子郵件以通知您還原作業已完成。

若是 SMP 及 MPP 方案，保留的備份會由 IBM 在發生災難或系統流失時專門用於系統回復目的。不支援從備份還原資料庫的要求。您可以使用例如 IBM Data Studio 的 Db2 工具，或使用 **db2 export** 指令來匯出資料。 
