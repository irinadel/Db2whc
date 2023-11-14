---

copyright:
  years: 2014, 2023
lastupdated: "2023-10-11"

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

A snapshot backup of the database is taken daily by IBM. You can also choose to take additional on-demand backups as required. Management of all backups and configuration of the daily backup schedule is built into the web console. While the backup is in progress, all writes will be suspended, and all reads that do not depend on the queued writes will continue.You can use the web console to restore from a snapshot backup if needed. While the restore is in progress, the system is unavailable. 

The recovery point objective (RPO) for snapshot backups is 24 hours. The recovery time objective (RTO) when restoring from a snapshot backup is approximately 1 hour.


<!--| Plan              | Backup frequency | Number of retained backups | Backup retention period   | Self service |
|-------------------|------------------|----------------------------|---------------------------|--------------|
| MPP               | 1 / day          | 2                          | 2 days; FIFO* rollover   | No           |
| Flex              | 1 / day          | Up to 7                    | 7 days; FIFO* rollover   | Yes          |
| Flex Performance  | 1 / day          | Up to 7                    | 7 days; FIFO* rollover   | Yes          |
{: caption="Table 1. Backup frequency and retention" caption-side="top"} -->

## IBM Cloud
{: #ibm_cloud_br}

Up to the the last 7 snapshots (whether taken by IBM or the clients) are retained by default. Snapshot backups are encrypted and stored in block storage local to the {{site.data.keyword.dashdbshort_notm}} system. Snapshot backups are free of charge. For information about disaster recovery (DR) backups that are not stored locally, see [Disaster Recovery](https://cloud.ibm.com/docs/Db2whc?topic=Db2whc-dr).

## Amazon Web Services
{: #aws_br}

For all instances on AWS, snapshot backups are encrypted and stored in Amazon Web Services S3. S3 keeps copies of each snapshot backup across 3 availability zones (AZs) in each region by default, which means that there are 3 copies of each snapshot backup in total.

In the previous generation of plans (all instances deployed before July 2023), the last 7 backups (whether taken by IBM or by the client) are retained by default. These first seven backups are free of charge. Additional backups can be retained at an additional cost.

In the current generation of plans (all instances deployed in or after July 2023 that support native object storage) backups (whether taken by IBM or by the client) are retained for 7 days by default. You are charged for all backups. You can reduce the retention period to one day, which means that only the last daily backup is retained. To meet the business continuity and disaster recovery requirements for the offering, and to meet compliance standards, a minimum backup retention of one day is required. With this generation of plans, the backup process backs up data on both block and object storage. The backup in this case includes snapshots of block storage and AWS S3 backup of object storage data.


| Cloud provider                            | Backup frequency | Number of retained backups              | Retention period         |
|-------------------------------------------|------------------|-----------------------------------------|--------------------------|
| IBM Cloud                                 | 1 / day          | Up to 7                                 | 7 days; FIFO* rollover   |
| Amazon Web Services (previous generation) | 1 / day          | Up to 7 by default; Can be increased    | 7 days; FIFO* rollover   |
| Amazon Web Services (current generation)  | 1 / day          | 7 by default; can be increased or decreased by configuring retention period | 7 days default; can be increased or decreased; FIFO rollover 
{: caption="Table 1. Snapshot backup frequency and retention period" caption-side="top"}

*First in, first out

## Logical schema backup and restore

This feature provides the ability to do full, cumulative incremental, or delta incremental backup of a Db2 schema followed by full restore of the schema or table(s) within the schema. Logical schema backup is a flexible and lightweight way to backup and restore table level data. 






<!--## SMP and MPP plans
{: #smp_mpp}

The last 2 daily backups are retained.

The retained backups are used exclusively by IBM for only system recovery purposes if there is a disaster or system loss. A request to restore your database from a backup is not supported. You can export your data by using Db2 tools such as IBM Data Studio or by using the **db2 export** command. -->

<!-- ## Flex and Flex Performance plans
{: #flex}

Up to the last 7 daily backup snapshots are retained. The number of retained snapshots to a maximum of 7 depends on the size of each snapshot (equal to the amount of data that is changed between snapshots after the first) and the amount of storage space for retained backups.

From the {{site.data.keyword.dashdbshort_notm}} console, you can schedule your backups to run when it's most convenient and you can restore your database from any of your retained backup snapshots at any time that you choose. The system goes down during the restore period. An email is sent to notify you that the restore operation was completed.

![View of the web console backup and restore page](images/br.png)
-->
