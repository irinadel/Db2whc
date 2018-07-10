---

copyright:
  years: 2014, 2018
lastupdated: "2018-05-10"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 備份及還原
{: #br}

每天會對完整 {{site.data.keyword.dashdbshort_notm}} 資料庫進行一次加密的備份。
{: shortdesc}

| 方案              | 備份頻率 | 保留的備份數目 | 備份保留期間   | 自助服務 |
|-------------------|------------------|----------------------------|---------------------------|--------------|
| MPP               | 1 / 日          | 2                          | 2 天；FIFO* 輪替   | 否           |
| 彈性效能  | 1 / 日          | 7                          | 7 天；FIFO* 輪替   | 是          |
{: caption="表 1. 備份頻率與保留" caption-side="top"}

*先進，先出

## SMP 與 MPP 方案
{: #smp_mpp}

保留最後 2 個每日備份。

保留的備份僅供 IBM 在發生災難或系統流失時，專門用於系統回復目的。不支援從備份還原資料庫的要求。您可以使用例如 IBM Data Studio 的 Db2 工具，或使用 **db2 export** 指令來匯出資料。 

## 彈性效能方案
{: #flex}

保留最後 7 個每日備份 Snapshot。

從 {{site.data.keyword.dashdbshort_notm}} 主控台中，您可以將備份排定在最方便的時間執行，且您可以在選擇的任何時間，從您保留的任何備份 Snapshot 還原資料庫。系統會在還原期間關閉。將會傳送電子郵件以通知您還原作業已完成。

![Web 主控台備份及還原頁面的視圖](images/br.png)

