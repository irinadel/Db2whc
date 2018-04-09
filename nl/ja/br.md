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

# バックアップとリストア
{: #br}

全 {{site.data.keyword.dashdbshort_notm}} データベースの暗号化バックアップは、1 日に 1 回行われます。Flex Performance プランでは、最近 7 日間の毎日のバックアップ・スナップショットが保持されます。SMP プランおよび MPP プランでは、最近 2 日間の毎日のバックアップが保持されます。
{: shortdesc}

Flex Performance プランでは、最も都合の良い時間にバックアップを実行するようにスケジュールを設定できます。また、いつでも、選択した保存バックアップ・スナップショットからデータベースをリストアできます。リストア期間中、システムはダウンします。リストア操作が完了したことを通知する E メールが送信されます。

SMP プランおよび MPP プランでは、保持されたバックアップは、災害またはシステムの損失が発生した場合に、システム回復の目的に限って IBM により使用されます。データベースをバックアップからリストアする要求は、サポートされていません。データをエクスポートするには、IBM Data Studio などの DB2 ツールを使用するか、**db2 export** コマンドを使用します。 
