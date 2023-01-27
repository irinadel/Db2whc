---

copyright:
  years: 2014, 2023
lastupdated: "2023-01-23"

keywords:

subcollection: Db2whc

---

# Scaling

{: #scale}

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

You can configure your {{site.data.keyword.dashdblong}} instance to autoscale, or you can independently scale storage and compute, by using the {{site.data.keyword.dashdbshort_notm}} console. Click **Administration** and then click the Scaling tab on the **Compute and storage** page. Click the appropriate **Edit** link to change the scaling settings manually or to configure autoscaling.
{: shortdesc}

![View of the web console Scaling tab](images/scaling.png){: caption="Figure 1. A screenshot of the Scaling tab" caption-side="bottom"}

You can scale your instance immediately or schedule a scaling operation to happen later. You can also scale your instance programmatically by using the [REST API](https://cloud.ibm.com/apidocs/db2-warehouse-on-cloud){: external}.

<!--![View of the web console Scaling tab in edit mode](images/scale_instance.png)-->

On-demand scaling is charged on an hourly basis.

Storage scaling occurs online. Only storage expansion is supported; decreasing storage is not permitted. During compute scaling, all uncommitted transactions are rolled back. RAM is allocated proportionally with a fixed ratio as the number of compute cores is changed.

## Downtime

{: #scaling_downtime}

How much downtime is associated with increasing or decreasing compute resources?

Approximately 45 minutes. The downtime will vary depending on the amount of crash recovery processing that might be required. The best practice is to gracefully end workloads prior to a scaling operation, or to schedule the scaling operation during a low period of activity.
