---

copyright:
  years: 2014, 2019
lastupdated: "2018-12-07"

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

# 方案及配置
{: #plans_cfgs}

您可以選擇 {{site.data.keyword.dashdbshort_notm}} 方案，該方案已針對您需要執行的工作進行配置且最佳化：
{: shortdesc}

   * 嘗試各種事物的入門方案。它是免費試用版，儲存空間高達 1 GB。請參閱：[入門方案限制](#ep_restrictions)
   * 彈性方案，您可以在其中獨立地調整儲存空間及運算資源
   * 正式作業之各種大小的 SMP 方案：小型、中型及大型，由單一節點及單一實例組成。
   * MPP 多節點叢集配置，用於平行處理及取得高效能
   * 針對高可用性配置的方案
   * Oracle 相容性

檢視 [{{site.data.keyword.Bluemix}} 型錄](https://console.bluemix.net/catalog/services/db2-warehouse){:new_window}中所有可用的 {{site.data.keyword.dashdbshort_notm}} 方案。
<!--   * Plans configured for data warehouse and online analytical processing (OLAP) workloads: [{{site.data.keyword.dashdbshort_notm}}](https://console.bluemix.net/catalog/services/db2-warehouse){:new_window} -->
<!--   * Plans configured for high-speed, transactional processing (OLTP): [{{site.data.keyword.dashdbshort_notm}} for Transactions](https://console.ng.bluemix.net/catalog/services/dashdb-for-transactions-sql-database){:new_window} -->

觀看此視訊，以查看「{{site.data.keyword.dashdbshort_notm}} 彈性效能」方案的簡介。

<iframe class="embed-responsive-item" id="youtubeplayer" title="從 Cognos Analytics 建立連線" type="text/html" width="640" height="390" src="//www.youtube.com/embed/59PKSnzNQAg?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

您可以要求將 {{site.data.keyword.dashdbshort_notm}} 服務部署在網路隔離的 {{site.data.keyword.Bluemix}} 環境。請與 [{{site.data.keyword.IBM_notm}} 業務 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/connect/ibm/us/en/?lnk=fcw){:new_window} 聯絡。


如果您在型錄中看不到所需要的配置，請與 [{{site.data.keyword.IBM_notm}} 銷售人員 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/connect/ibm/us/en/?lnk=fcw){:new_window} 聯絡，來討論其他選項。

## 資料中心內方案的可用性
{: #availability}

下表提供各種 {{site.data.keyword.dashdbshort_notm}} 方案可用性的相關資訊，依位於地理區域中的資料中心排列：


| {{site.data.keyword.dashdbshort_notm}} 方案| 亞太地區 | 歐洲    | 北美洲/中美洲     | 南美洲 |
|------------------------------|--------------|-----------|-----------------------    |---------------|
| 彈性                         | *NA          | 法蘭克福 | 華盛頓特區（美國東部）| *NA           |
|                              |              |           | 達拉斯（美國南部）         |               |  
|      |||||
| SMP                          | 香港    | 阿姆斯特丹 | 華盛頓特區（美國東部）| 聖保羅     |
|                              | 首爾        | 法蘭克福 | 達拉斯（美國南部）         |               | 
|                              | 新加坡    | 倫敦    | 蒙特利爾                  |               | 
|                              | 雪梨       | 米蘭     | 克雷塔羅                 |               | 
|                              | 東京        | 奧斯陸      | 多倫多                   |               | 
|                              |              | 巴黎     |                           |               |
|      |||||
| MPP               | 香港    | 阿姆斯特丹 | 華盛頓特區（美國東部）| 聖保羅     |
|                              | 首爾        | 法蘭克福 | 達拉斯（美國南部）         |               | 
|                              | 新加坡    | 倫敦    | 蒙特利爾                  |               | 
|                              | 雪梨       | 米蘭     | 克雷塔羅                 |               | 
|                              | 東京        | 奧斯陸      | 多倫多                   |               | 
|                              |              | 巴黎     |                           |               |
{: caption="表 1. 支援 Db2 Warehouse on Cloud 服務方案的資料中心" caption-side="top"}

*NA = 目前無法使用

## 入門方案限制
{: #ep_restrictions}

強烈建議您使用企業層級服務方案，而不要使用入門服務方案來處理任務攸關或效能敏感的工作負載。
{: important}

以下是 {{site.data.keyword.dashdbshort_notm}} 入門方案限制的表格：

|種類|項目|限制| 
|----------|------|-------------|
|資源|儲存空間|每位使用者 20 GB 的儲存空間。只有在使用少於 1 GB 的儲存空間時，方案才免費。|
|  |連線|每位使用者 50 個連線。此限制可能動態調整，以維護實例的系統完整性。|
|  |效能|效能可能會因為多方承租戶系統上其他使用者執行的工作負載而波動|
|  |  |
|特性及函數|聯合|不支援|
|  |Oracle 相容性|不支援|
|  |使用者定義延伸 (UDF) |不支援|
|  |使用者管理|使用者未被提供管理權限|
|  |列和欄存取控制 (RCAC) |不支援|
|  | IBM InfoSphere Data Replication 以便用於載入資料|不支援|
|  |  |
|網路環境| IBM Cloud Integrated Analytics |不支援|
|  | IBM Cloud Dedicated |不支援|
|  |  |
|安全規範| 1996 年醫療保險轉移和責任法 (HIPAA)|不支援。請參閱您的服務說明。|
|  | 歐盟一般資料保護規範 (GDPR) |無適用的特定限制|
|  |  |
|帳戶管理|重新啟動|無重新啟動需求|
{: caption="表 1. {{site.data.keyword.dashdbshort_notm}} 入門方案限制" caption-side="top"}
