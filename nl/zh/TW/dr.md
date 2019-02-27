---

copyright:
  years: 2014, 2019
lastupdated: "2018-11-21"

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

# 災難回復 (DR)
{: #dr}

如果您的資料倉儲實例部署在發生重大中斷的資料中心，預期的關閉時間超過 8 小時，則在災難回復動作開始之前，會先傳送要求給您，請您容許維修操作員將您的實例由另一個資料中心進行失效接手。
{: shortdesc}

您的資料庫每天都會進行 Db2 備份，彈性方案例外，該方案中每 7 天會執行一次 Db2 備份，且每天會執行一次 Snapshot 備份。每日備份儲存在 IBM Cloud Object Storage 服務中，而這些備份會從這個服務抄寫至多個可用性區域。萬一您的主要資料中心發生一些情況，我們的服務操作員將與您合作，在次要資料中心提供回復的資料庫。

## **巴西：增補規則 14**（適用於針對巴西聯邦政府所佈建的系統）
{: #rule_14}

目前，由於「增補規則 14」，無法在巴西為聯邦政府提供 Db2 Warehouse on Cloud 供應項目的災難回復 (DR) 選項。

