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

# Backup and restore
{: #br}

An encrypted backup on the full {{site.data.keyword.dashdbshort_notm}} database is done once per day.
{: shortdesc}

| Plan              | Backup frequency | Number of retained backups | Backup retention period   | Self service |
|-------------------|------------------|----------------------------|---------------------------|--------------|
| MPP               | 1 / day          | 2                          | 2 days; FIFO* roll over   | No           |
| Flex              | 1 / day          | up to 7                    | 7 days; FIFO* roll over   | Yes          |
| Flex Performance  | 1 / day          | up to 7                    | 7 days; FIFO* roll over   | Yes          |
{: caption="Table 1. Backup frequency and retention" caption-side="top"}

*First in, first out

## SMP and MPP plans
{: #smp_mpp}

The last 2 daily backups are retained.

The retained backups are used exclusively by IBM for only system recovery purposes in the event of a disaster or system loss. A request to restore your database from a backup is not supported. You can export your data using Db2 tools such as IBM Data Studio or by using the **db2 export** command. 

## Flex and Flex Performance plans
{: #flex}

Up to the last 7 daily backup snapshots are retained. The number of retained snapshots to a maximum of 7 depends on the size of each snapshot (equal to the amount of data changed between snapshots after the first) and the amount of storage space for retained backups.

From the {{site.data.keyword.dashdbshort_notm}} console, you can schedule your backups to run when it's most convenient and you can restore your database from any of your retained backup snapshots at any time that you choose. The system goes down during the restore period. An email will be sent to notify you that the restore operation was completed.

![View of the web console backup and restore page](images/br.png)

