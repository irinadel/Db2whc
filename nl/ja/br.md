---

copyright:
  years: 2014, 2019
lastupdated: "2019-05-21"

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

# バックアップとリストア
{: #br}

{{site.data.keyword.dashdbshort_notm}} データベース全体の暗号化バックアップは、1 日 1 回行われます
{: shortdesc}

| プラン              | バックアップ頻度 | 保存されるバックアップ数 | バックアップ保存期間   | セルフサービス |
|-------------------|------------------|----------------------------|---------------------------|--------------|
| MPP               | 1 / 日          | 2                          | 2 日間。FIFO* 循環方式   | いいえ           |
| Flex              | 1 / 日          | 最大 7                    | 7 日間。FIFO* 循環方式   | はい          |
| Flex Performance  | 1 / 日          | 最大 7                    | 7 日間。FIFO* 循環方式   | はい          |
{: caption="表 1. バックアップ頻度と保存" caption-side="top"}

*先入れ先出し法

## SMP および MPP のプラン
{: #smp_mpp}

過去 2 日間の日次バックアップが保持されます。

保持されるバックアップは、災害またはシステムの損失が発生した場合に、システム復旧の目的に限って IBM のみが使用します。 データベースをバックアップからリストアする要求は、サポートされていません。 データをエクスポートするには、IBM Data Studio などの Db2 ツールを使用するか、**db2 export** コマンドを使用します。 

## Flex プランおよび Flex Performance プラン
{: #flex}

最近 7 日間の日次バックアップ・スナップショットが保持されます。保持されたスナップショットの数 (最大 7) は、各スナップショットのサイズ (最初のスナップショットの後にスナップショット間で変更されたデータの量と等しい) と、保持されたバックアップ用のストレージ・スペースの量によって異なります。

{{site.data.keyword.dashdbshort_notm}} コンソールから、最も都合の良い時間にバックアップを実行するようにスケジュールを設定できます。また、保持している任意のバックアップ・スナップショットからいつでもデータベースをリストアできます。 リストア期間中、システムはダウンします。 リストア操作が完了したことを通知する E メールが送信されます。

![Web コンソールの「バックアップとリストア」ページの表示](images/br.png)

