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

# High availability (HA): MPP plan
{: #ha_smp_mpp}

The {{site.data.keyword.dashdblong}} MPP plan cluster is provisioned with high availability.  
{: shortdesc}

When a node goes down for an MPP plan, the HA component restarts your database partitions in the remaining healthy nodes. A short downtime occurs during this phase. 

After the node is added back to the cluster, the database engine must be restarted to run at full capacity. 

