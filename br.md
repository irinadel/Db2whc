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

# Backup and restore
{: #br}

An encrypted backup on the full {{site.data.keyword.dashdbshort_notm}} database is done once per day. For the Flex Performance plan, the last 7 daily backup snapshots are retained. For SMP and MPP plans, the last 2 daily backups are retained.
{: shortdesc}

In the Flex Performance plan, you can schedule your backups to run when it's most convenient and you can restore your database from any of your retained backup snapshots at any time that you choose. The system goes down during the restore period. An email will be sent to notify you that the restore operation was completed.

In the case of the SMP and MPP plans, the retained backups are used exclusively by IBM for only system recovery purposes in the event of a disaster or system loss. A request to restore your database from a backup is not supported. You can export your data using Db2 tools such as IBM Data Studio or by using the **db2 export** command. 
