---

copyright:
  years: 2014, 2018
lastupdated: "2018-03-15"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# High availability (HA): Flex Performance plan
{: #ha_flex}

If an unexpected node failure does occur, your Flex Performance MPP cluster is brought back to full capacity after a short downtime due to using the IBM Container Service (based on Kubernetes). Nodes from a pool are used to move the failed node entities. 
{: shortdesc}

## Compute HA
{: #compute_ha}

Any node failure is immediately detected by the container service. The containers and pods that were running in the failed node are scheduled to a new node from a pool of nodes. The system is back to 100% normal operation after a short downtime.

## Storage HA
{: #storage_ha}

Your storage is configured with a dual-parity RAID6 implementation that provides protection against double disk failures in the same RAID group for high performance and highly available storage for your system.

## Network HA
{: #net_ha}

Network connections are made highly available by provisioning your service with a redundant network interface card (NIC). 

If the container service detects a network issue, pods and containers can automatically restart after a short downtime.
