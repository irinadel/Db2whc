---

copyright:
  years: 2014, 2023
lastupdated: "2023-12-11"

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

A snapshot backup of the database is taken daily. Management and configuration of daily snapshot backups are built into the web console. 

You can use the web console to restore from a snapshot backup if needed. While the restore is in progress, all writes in the system are queued, and all reads that don’t depend on the queued writes will continue. 

<!--| Plan              | Backup frequency | Number of retained backups | Backup retention period   | Self service |
|-------------------|------------------|----------------------------|---------------------------|--------------|
| MPP               | 1 / day          | 2                          | 2 days; FIFO* rollover   | No           |
| Flex              | 1 / day          | Up to 7                    | 7 days; FIFO* rollover   | Yes          |
| Flex Performance  | 1 / day          | Up to 7                    | 7 days; FIFO* rollover   | Yes          |
{: caption="Table 1. Backup frequency and retention" caption-side="top"} -->

## IBM Cloud
{: #ibm_cloud_br}

The last 7 daily snapshots are retained by default. Snapshot backups are encrypted and stored in block storage local to the Db2 Warehouse on Cloud system. Snapshot backups are free of charge.

## Amazon Web Services
{: #aws_br}

The last 7 daily snapshots are retained by default. When deployed on Amazon Web Services, you can use the web console to configure a longer retention period for snapshot backups if desired. 

Potentially unlimited snapshots can be retained. Snapshot backups are encrypted and stored in Amazon Web services S3. S3 keeps copies of each snapshot backup across 3 availability zones (AZs) in each region by default, so there are 3 copies of each snapshot backup in total. 

With the previous generation of plans, the first 7 snapshot backups on Amazon Web Services are free of charge. You will be charged each month for the capacity required for any additional snapshot backups.

With the current generation of plans, you are charged for all backups. The backup process backs up data on both block and object storage. The backup in this case includes snapshots of block storage and AWS S3 backup of object storage data.

| Cloud provider                            | Backup frequency | Number of retained backups              | Retention period         |
|-------------------------------------------|------------------|-----------------------------------------|--------------------------|
| IBM Cloud                                 | 1 / day          | Up to 7                                 | 7 days; FIFO* rollover   |
| Amazon Web Services (previous generation) | 1 / day          | Up to 7 by default; Can be increased    | 7 days; FIFO* rollover   |
| Amazon Web Services (current generation)  | 1 / day          | 7 by default; can be increased or decreased by configuring retention period | 7 days default; can be increased or decreased; FIFO rollover 
{: caption="Table 1. Snapshot backup frequency and retention period" caption-side="top"}

*First in, first out

## Logical schema backup and restore

This feature provides the ability to do full, cumulative incremental, or delta incremental backup of a Db2 schema followed by full restore of the schema or table(s) within the schema. Logical schema backup is a flexible and lightweight way to backup and restore table level data. For more information about this feature, see [Schema-level and table-level backup and restore](https://www.ibm.com/docs/en/db2/11.5?topic=recovery-schema-level-table-level-backup-restore).

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
